# 从助记词短语创建钱包

助记词短语是一组经过加密生成的单词序列，用于派生私钥。例如：`"oblige salon price punch saddle immune slogan rare snap desert retire surprise"`；这将生成地址`"0xdf9d0e6c6c5f5da6e82e5e1a77974af6642bdb450a10c43f0c6910a212600185"`。

除此之外，我们还支持[分层确定性钱包](https://www.ledger.com/academy/crypto/what-are-hierarchical-deterministic-hd-wallets)和[派生路径](https://thebitcoinmanual.com/articles/btc-derivation-path/)。您可能从某个地方认识到字符串`"m/44'/60'/0'/0/0"`；这是一个派生路径。简单来说，这是从单个根钱包派生许多钱包的方法。

SDK 为您提供了两种从助记词短语实例化钱包的方法：一种是带有派生路径的方法（`Wallet::new_from_mnemonic_phrase_with_path`），另一种是使用默认派生路径的方法，以防您不想或不需要配置派生路径（`Wallet::new_from_mnemonic_phrase`）。

以下是如何使用助记词短语和派生路径创建钱包的示例：

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:create_wallet_from_mnemonic}}
```
