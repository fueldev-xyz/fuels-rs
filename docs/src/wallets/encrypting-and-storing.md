# 加密和存储钱包

## 创建钱包并将加密的 JSON 钱包存储到磁盘上

您还可以使用[JSON 钱包](https://cryptobook.nakov.com/symmetric-key-ciphers/ethereum-wallet-encryption)来管理一个钱包，该钱包被安全加密并存储在磁盘上。这样可以更轻松地管理多个钱包，特别是用于测试目的。

您可以创建一个随机钱包，并在同一时间加密和存储它。然后，稍后，如果您知道主密码，可以恢复钱包：

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:create_and_restore_json_wallet}}
```

## 使用助记词或私钥创建的钱包加密和存储

如果您已经使用助记词短语或私钥创建了钱包，您也可以将其加密并保存到磁盘上：

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:create_and_store_mnemonic_wallet}}
```
