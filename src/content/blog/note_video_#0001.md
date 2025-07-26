---
title: 记多语言项目如何运作
description: 记多语言项目如何运作
pubDate: July 26 2025
categories:
 - Note
tags:
 - Note
---


```markdown
# 为什么有些项目会使用多种编程语言
（哔哩哔哩视频笔记）

> 刷到一个视频，主题是：  
> “一个**多语言项目**（区别于简单的前后端分离）是如何协同工作的？”

---

## 最终编译为机器码的语言

- 常见代表：C、C++、Go、Rust  
- 特点：源代码经编译器直接生成机器码，由操作系统加载执行。

> 理解这些语言如何协作，必须深入“编译”这一过程。  
> 视频以 **GCC** 为例进行讲解。

---

### 常见误区：GCC ≠ “只编译 C 的编译器”

- 早期：GNU C Compiler  
- 现在：GNU **Compiler Collection**，支持 C、C++、Fortran、Ada、Go、D、Obj-C 等众多语言。

---

## GCC 编译一个 `.c` 文件的真实流程

通常我们只敲：

```bash
gcc code.c -o code
```

看似一步，实则内部包含多个独立阶段：

1. **Pre-Processor（预处理）**  
   - 将 `#include`、`#define` 等指令展开  
   - 把引用的头文件内容插入源文件

   ```c
   #include <iostream>
   using namespace std;
   ```

2. **Compiler（编译器前端）**  
   - 将预处理后的 `.i` 文件翻译成汇编 `.s`

3. **Assembler（汇编器）**  
   - 把汇编 `.s` 转成机器码 `.o`（目标文件）

4. **Linker（链接器）**  
   - 合并所有 `.o` 与库文件，生成最终可执行文件 `.exe` / `a.out`

> 这些阶段彼此独立，可单独执行；GCC 只是把它们串联起来，提供一条“流水线”。
```