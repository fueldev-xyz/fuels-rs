# 检查余额和硬币

<!-- 此部分应解释如何获取钱包的余额 -->
<!-- balance:example:start -->

在 Fuel 网络中，每个 UTXO 对应于一个唯一的 _硬币_，而该 _硬币_ 有一个相应的 _金额_（就像一张美元钞票有 10 美元或 5 美元面值一样）。因此，当您想要查询给定资产 ID 的余额时，您要查询每个未使用的硬币中的金额之和。这个查询非常容易通过钱包来完成：

<!-- balance:example:end -->

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:get_asset_balance}}
```

<!-- 此部分应解释如何获取钱包的所有余额 -->
<!-- balances:example:start -->

如果您想要查询所有余额（即获取该钱包中每个资产 ID 的余额），您可以使用 `get_balances` 方法：

<!-- balances:example:end -->

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:get_balances}}
```

<!-- 此部分应解释 `get_balances` 的返回类型 -->
<!-- balances_return:example:start -->

返回类型是一个 `HashMap`，其中键是 _资产 ID_ 的十六进制字符串，值是相应的余额。例如，我们可以获取基础资产的余额：

<!-- balances_return:example:end -->

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:get_balance_hashmap}}
```
