# 账户

`ViewOnlyAccount` trait 提供了一个通用接口来查询余额。

`Account` trait 除了上述功能之外，还提供了一个通用接口来检索可花费的资源或转移资产。在执行 SDK 中导致交易的操作时，通常需要提供一个账户，该账户将用于分配交易所需的资源，包括交易费用。

这两个 trait 都由以下类型实现：

- [钱包](./wallets/index.md)
- [Predicate](./predicates/index.md)

## 转移资产

一个账户实现了以下方法来转移资产：

- `transfer`
- `force_transfer_to_contract`
- `withdraw_to_base_layer`

以下示例是针对 `Wallet` 账户的。`Predicate` 账户的工作方式类似，但在尝试花费其拥有的资源之前，您可能需要设置其断言数据。

使用 `wallet.transfer` 您可以启动一个交易，将资产从您的账户转移到目标地址。

```rust,ignore
{{#include ../../examples/wallets/src/lib.rs:wallet_transfer}}
```

您可以通过 `wallet.force_transfer_to_contract` 将资产转移到合约。

```rust,ignore
{{#include ../../examples/wallets/src/lib.rs:wallet_contract_transfer}}
```

要将资产转移到基础层链，您可以使用 `wallet.withdraw_to_base_layer`。

```rust,ignore
{{#include ../../examples/wallets/src/lib.rs:wallet_withdraw_to_base}}
```

上面的示例从字符串创建了一个 `Address` 并将其转换为 `Bech32Address`。接下来，它通过提供地址、要转移的金额和交易策略来调用 `wallet.withdraw_to_base_layer`。最后，为了验证转移是否成功，使用 `provider.get_message_proof` 检索相关的消息证明，并验证金额和接收方。
