# 多合约调用

使用 `MultiContractCallHandler`，您可以在单个事务中执行多个合约调用。为此，首先准备您要捆绑的所有合约调用：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:multi_call_prepare}}
```

您还可以为每个合约调用设置调用参数、变量输出或外部合约，只要您不使用 `call()` 或 `simulate()` 执行它。

接下来，将准备好的调用提供给您的 `MultiContractCallHandler`，并可选择配置事务策略：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:multi_call_build}}
```

> **注意：** 在单独的合约调用上配置的任何事务策略都会被忽略，而是使用提供给 `MultiContractCallHandler` 的参数。

此外，如果由于任何原因需要将提交与值检索分开，可以按如下方式执行：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:submit_response_multicontract}}
```

## 输出值

要获取捆绑调用的输出值，您需要在将 `call()` 或 `simulate()` 的结果保存到变量时提供显式类型注释：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:multi_call_values}}
```

您还可以通过将类型注释移到调用的方法上与 `FuelCallResponse` 进行交互：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:multi_contract_call_response}}
```

> **注意：** `MultiContractCallHandler` 仅支持返回堆类型的一个合约调用。由于堆类型的处理方式，此合约调用需要位于最后位置，即最后使用 `add_call` 添加。这是一个暂时的限制，我们希望尽快解除。与此同时，如果有多个处理堆类型的调用，请将它们拆分成多个常规单个调用。
