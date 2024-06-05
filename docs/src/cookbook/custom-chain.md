# 自定义链

该示例演示了如何为底层链启动一个具有自定义共识参数的短暂 Fuel 节点。

首先，我们需要导入 `ConsensusParameters` 和 `ChainConfig`：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_chain_import}}
```

接下来，我们可以为共识参数定义一些值：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_chain_consensus}}
```

在启动节点之前，我们可能还想定义一些初始代币，并将它们分配给一个地址：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_chain_coins}}
```

最后，我们调用 `setup_test_provider()`，它会使用给定的配置启动一个节点，并返回与该节点关联的提供程序：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:custom_chain_provider}}
```
