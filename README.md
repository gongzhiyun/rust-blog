# 图解 Rust (Illustrated Rust) 🦀

> **用视觉语言拆解 Rust 的深度特性，让底层原理一眼可见。**

本仓库是一个专注于 **Rust 核心特性与底层原理** 的图解博客。通过精心设计的 SVG 架构图与逻辑图，配合硬核的技术解析，帮助开发者跨越 Rust 的学习曲线。

欢迎大家围观与转发！🦀

---

## 📚 文章目录 (Roadmap)

按照 Rust 的典型学习路径排列：

1.  **[所有权 (Ownership)](./articles/Ownership.md)** - 极简内存安全指南
2.  **[结构体 (Struct)](./articles/Struct.md)** - 内存布局与对齐
3.  **[字符串 (String)](./articles/String.md)** - 彻底搞懂 String 与 &str
4.  **[特征 (Trait)](./articles/Trait.md)** - 接口抽象的底层实现
5.  **[生命周期 (Lifetime)](./articles/Lifetime.md)** - 引用安全的时空边界
6.  **[高级特征 (Trait Advanced)](./articles/Trait_Advanced.md)** - 泛型与关联类型深度解析
7.  **[智能指针 Box](./articles/Box.md)** - 堆内存分配与尺寸适配的艺术
8.  **[引用计数 Rc](./articles/Rc.md)** - 单线程共享所有权
9.  **[原子引用计数 Arc](./articles/Arc.md)** - 多线程共享所有权
10. **[迭代器 (Iterator)](./articles/Iterator.md)** - 零成本抽象的艺术

---

## ✨ 特色

- **视觉化学习**：拒绝纯文字堆砌，每一篇核心文章都包含多张深度解析图（SVG 格式，清晰且支持缩放）。
- **底层视角**：不仅教你怎么用，更告诉你内存里发生了什么、编译器做了哪些优化。
- **零成本抽象**：深度剖析 Rust 如何在保持高阶抽象的同时，实现极致的运行效率。

---

## 🖼️ 核心图解示例

在 [Box.md](./articles/Box.md) 中，通过直观的对比展示了 `Box` 如何将栈上的固定尺寸指针映射到堆上的动态数据：

<div align="center">
  <img src="./articles/imgs/box_layout.svg" alt="Box 内存布局图解" width="800" />
</div>


---

## 🤝 关注与支持

如果你喜欢这些内容，欢迎关注我的公众号 **“楠风的小宇宙”**。

本公众号坚持 **“图解一切知识点”** 的原创理念，专注于通过高质量的可视化表达，拆解 Rust 以及操作系统等底层核心技术。

<div align="center">
  <img src="./articles/imgs/公众号.jpg" alt="楠风的小宇宙公众号二维码" width="250" />
  <br/>
  <sub><b>扫描二维码，关注公众号 “楠风的小宇宙” —— 洞察底层，图解架构</b></sub>
</div>

---

## 📄 开源协议

本项目采用 [MIT License](LICENSE) 开源。
