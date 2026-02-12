# Rust 视觉化深度解析 (Illustrated Rust) 🦀

> **用视觉语言拆解 Rust 的深度特性，让底层原理一眼可见。**

本仓库是一个专注于 **Rust 核心特性与底层原理** 的图解博客。通过精心设计的 SVG 架构图与逻辑图，配合硬核的技术解析，帮助开发者跨越 Rust 的学习曲线。

欢迎大家围观与转发！🦀

---

## 📚 文章目录 (Roadmap)

按照 Rust 的典型学习路径排列：

### 01 基础核心 (Basic Core)
- **[所有权 (Ownership)](./01-Basic/Ownership.md)** - 极简内存安全指南
- **[生命周期 (Lifetime)](./01-Basic/Lifetime.md)** - 引用安全的时空边界

### 02 数据结构 (Data Structures)
- **[结构体 (Struct)](./02-Data-Structures/Struct.md)** - 内存布局与对齐
- **[字符串 (String)](./02-Data-Structures/String.md)** - 彻底搞懂 String 与 &str
- **[向量 (Vec)](./02-Data-Structures/Vec.md)** - 动态数组的扩容机制
- **[双端队列 (VecDeque)](./02-Data-Structures/VecDeque.md)** - 跨越物理边界的环形缓冲区

### 03 智能指针 (Smart Pointers)
- **[智能指针 Box](./03-Smart-Pointers/Box.md)** - 堆内存分配与尺寸适配机制
- **[引用计数 Rc](./03-Smart-Pointers/Rc.md)** - 单线程共享所有权
- **[原子引用计数 Arc](./03-Smart-Pointers/Arc.md)** - 多线程共享所有权

### 04 泛型与特征 (Generics & Traits)
- **[特征 (Trait)](./04-Generics-Traits/Trait.md)** - 接口抽象的底层实现
- **[泛型 (Generics)](./04-Generics-Traits/Generics.md)** - 单态化与代码膨胀

### 05 迭代器 (Iterators)
- **[迭代器 (Iterator)](./05-Iterators/Iterator.md)** - 零成本抽象的实现原理
- **[Vec 迭代 (Iter)](./05-Iterators/Iter.md)** - 内存布局与转换机制

---

## ✨ 特色

- **视觉化学习**：拒绝纯文字堆砌，每一篇核心文章都包含多张深度解析图（SVG 格式，清晰且支持缩放）。
- **底层视角**：不仅教你怎么用，更告诉你内存里发生了什么、编译器做了哪些优化。
- **零成本抽象**：深度剖析 Rust 如何在保持高阶抽象的同时，实现极致的运行效率。

---

## 🖼️ 核心图解示例

在 [Box.md](./03-Smart-Pointers/Box.md) 中，通过直观的对比展示了 `Box` 如何将栈上的固定尺寸指针映射到堆上的动态数据：

<div align="center">
  <img src="./03-Smart-Pointers/imgs/box_layout.svg" alt="Box 内存布局图解" width="800" />
</div>


---

## 📄 开源协议

本项目采用 [MIT License](LICENSE) 开源。
