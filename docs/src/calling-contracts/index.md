# 调用合约

一旦您部署了您的合约，就像在前面的部分中看到的那样，您可能希望：

1. 调用合约方法；
2. 配置调用参数和交易策略；
3. 在合约调用中转发货币和燃料；
4. 读取和解释返回的值和日志。

下面是一个示例。假设您的 Sway 合约有两个名为 `initialize_counter(u64)` 和 `increment_counter(u64)` 的 ABI 方法。一旦您部署了该合约，您可以像这样调用这些方法：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:use_deployed_contract}}
```

上面的示例使用了所有默认配置，并执行了一个简单的合约调用。

此外，如果出于任何原因您需要将提交与值检索分开，您可以像下面这样操作：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:submit_response_contract}}
```

接下来，我们将看到如何进一步配置合约调用中的许多不同参数。
