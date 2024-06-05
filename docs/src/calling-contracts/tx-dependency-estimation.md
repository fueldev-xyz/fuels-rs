# 交易依赖估算

之前，我们提到一个合约调用可能需要您手动指定外部合约、变量输出或输出消息。SDK 还可以尝试为您估算并设置这些依赖关系，但需要在后台运行多个模拟调用。

下面的示例使用一个调用外部合约的合约调用，然后将资产铸币到指定地址。如果不包含依赖项进行调用，将会导致回滚：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:dependency_estimation_fail}}
```

如前面章节所述，您可以使用 `.with_contracts()` 指定外部合约，并使用 `append_variable_outputs()` 添加输出变量来解决这个问题：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:dependency_estimation_manual}}
```

但这需要您知道外部合约的合约 ID 和所需的输出变量数量。或者，您可以通过链式调用 `.estimate_tx_dependencies()` 来自动估算并设置依赖关系。可选参数是模拟尝试的最大次数：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:dependency_estimation}}
```

最小尝试次数对应于所需的外部合约和输出变量数量，并默认为 10。

> **注意：** 当使用脚本调用或多合约时，`estimate_tx_dependencies()` 也可以使用。`estimate_tx_dependencies()` 目前不会解决外部合约日志所需的依赖关系。有关更多信息，请参阅[这里](./logs.md)。如果在耗尽所有模拟尝试后找不到解决方案，则将传播最后收到的错误。如果错误与事务依赖关系无关，则会发生相同的情况。
