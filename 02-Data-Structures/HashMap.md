# 图解 Rust HashMap：高并发下的 Swiss Table

Rust 的 `HashMap` 是标准库中极其精妙的工程实现。它并非传统的拉链法（Chaining）哈希表，而是采用了 Google 的 **Swiss Table** 设计。这种设计通过 SIMD 指令加速查找，并将元数据（Control Bytes）与数据（Slots）分离，以最大化 CPU 缓存利用率。它在物理上是“一整块连续内存”，在逻辑上则是“分组探测的哈希桶”。

---

## 1. 物理本质：元数据与数据的分离

`HashMap` 的物理布局极具特色：它将所有 buckets 的状态（Control Bytes）集中存储在数组头部，而将真正的 Key-Value 数据存储在数组尾部（或紧随其后）。

![HashMap 物理布局](./imgs/hashmap_physical_layout.svg)

---

## 2. 逻辑算法：H1 与 H2 的分工

为了实现 SIMD 加速，Rust 将 64 位的 Hash 值拆分为两部分：**H1** 用于定位 Group，**H2** 用于组内匹配。

![HashMap 逻辑映射](./imgs/hashmap_logical_mapping.svg)

*   **H1 (Index)**：Hash 值的低 57 位（具体取决于 bucket 数量）。它决定了元素应该落在哪个 Group（每组 16 个 buckets）。
*   **H2 (Control Tag)**：Hash 值的高 7 位。它作为“指纹”存储在 Control Byte 中。
*   **SIMD Magic**：
    *   查找时，CPU 一次性加载 16 个 Control Bytes 到寄存器。
    *   使用 SIMD 指令（如 SSE2/AVX2）并行比较这 16 个字节与 H2。
    *   生成一个 bitmask，标记所有匹配的位置。

---

## 3. 核心行为：SIMD 探测流

查找（Lookup）或插入（Insert）的过程，本质上是一次“并行探测”。

![HashMap 插入流程](./imgs/hashmap_insert_flow.svg)

1.  **定位 Group**：使用 H1 计算出起始位置。
2.  **并行匹配**：加载 16 个 Control Bytes，与 H2 进行 SIMD 比较。
3.  **候选校验**：
    *   如果 bitmask 非零，说明有潜在匹配。
    *   遍历 bitmask 中的每一个 `1`，根据索引找到对应的 Slot。
    *   **Key Check**：比较 Slot 中的 Key 与目标 Key 是否真正相等（处理哈希冲突）。
4.  **线性探测 (Quadratic Probing)**：
    *   如果当前 Group 没找到且未遇到空位，则跳到下一个 Group 继续查找（Rust 使用二次探测或三角数步长来避免堆积）。

---

## 4. 设计哲学

Rust `HashMap` (Swiss Table) 的设计权衡了空间与时间，展现了现代 CPU 友好的编程思想：

*   **物理上 (Physical)**
    *   **缓存友好**：Control Bytes 紧凑排列，极大地提高了 CPU L1 Cache 命中率。
    *   **内存布局**：元数据与数据分离，扫描元数据时不会污染缓存行（不会加载无用的 Key/Value 数据）。
*   **逻辑上 (Logical)**
    *   **小表优化**：空表不分配内存（悬垂指针），只有插入元素时才分配。
    *   **DoS 防护**：默认使用 `SipHash` 算法（通过 `RandomState` 随机化），防止哈希洪水攻击。
*   **操作上 (Operational)**
    *   **SIMD 加速**：利用现代 CPU 指令集，将“逐个比较”变为“分组并行比较”。
    *   **零开销抽象**：尽管内部逻辑复杂，但对用户暴露的接口依然简单直观，且性能处于顶尖水平。

---

> **创作声明**：本文以“图解”为核心，所有技术图表均由作者原创设计。文章利用 AI 工具辅助进行文字润色与纠错，以确保技术表述的严谨性与准确性。
