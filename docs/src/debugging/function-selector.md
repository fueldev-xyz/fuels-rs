# 函数选择器

每当您调用合约方法时，SDK 将根据 fuel 规范生成一个函数选择器，该选择器将被节点用于确定我们希望执行哪个方法。

如果出于任何原因，您希望自己生成函数选择器，可以这样做：

```rust,ignore
{{#include ../../../examples/debugging/src/lib.rs:example_fn_selector}}
```
