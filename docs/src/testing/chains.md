# 增加区块高度

你可以使用 `produce_blocks` 来帮助实现任意的区块高度；当你想进行任何关于交易成熟度的测试时，这非常有用。

> **注意**：为了使 `produce_blocks` API 生效，必须在运行节点的配置中将 `manual_blocks_enabled` 设置为 `true`。参见下面的示例。

```rust,ignore
{{#include ../../../e2e/tests/providers.rs:use_produce_blocks_to_increase_block_height}}
```

你还可以将自定义的区块时间作为第二个可选参数。下面是一个示例：

```rust,ignore
{{#include ../../../e2e/tests/providers.rs:use_produce_blocks_custom_time}}
```
