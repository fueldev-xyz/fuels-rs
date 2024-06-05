# 估算合约调用成本

通过 `ContractCallHandler` 和 `MultiContractCallHandler` 提供的函数 `estimate_transaction_cost(tolerance: Option<f64>, block_horizon: Option<u32>)`，您可以获得特定调用的成本估算。返回类型 `TransactionCost` 是一个包含相关信息的结构体，用于估算：

```rust,ignore
{{#include ../../../packages/fuels-accounts/src/provider.rs:transaction_cost}}
```

下面是显示如何从单个和多个调用事务获取估计事务成本的示例。

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:contract_call_cost_estimation}}
```

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:multi_call_cost_estimation}}
```

事务成本估算可用于设置实际调用的燃料限制，或向用户显示估算成本。

> **注意**：脚本也具有相同的估算接口。
