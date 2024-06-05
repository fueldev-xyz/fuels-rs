# 使用 abigen 生成绑定

在之前的部分中，您可能已经注意到了这个代码片段：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:abigen_example}}
```

<!-- 本部分应解释 abigen 的目的 -->
<!-- abigen:example:start -->

SDK 允许您将智能合约的 ABI 方法转换为 Rust 结构和方法，这些方法由 JSON 对象指定（您可以从 [Forc](https://github.com/FuelLabs/sway/tree/master/forc) 获取）。这些 Rust 结构和方法在编译时进行类型检查。
要调用您的合约、脚本或谓词，您首先需要为它们生成 Rust 绑定。

<!-- abigen:example:end -->

以下小节包含有关 `abigen!` 语法及其生成的代码的更多细节。
