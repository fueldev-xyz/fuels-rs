# 签名

一旦您使用先前讨论的方法之一将钱包实例化为解锁状态，您就可以使用`wallet.sign`来签署消息。以下是如何签署和恢复消息的完整示例。

```rust,ignore
{{#include ../../../packages/fuels-accounts/src/account.rs:sign_message}}
```

## 将`Signers`添加到交易构建器

输入中的每个已签名资源都需要具有指向有效见证的见证索引。更改输入中的见证索引将更改交易 ID。这意味着我们需要在最终签署交易之前设置所有见证索引。以前，用户需要确保见证人索引和见证人顺序是正确的。为了自动化这个过程，SDK 将跟踪交易构建器中的签名者，并自动解决最终交易。这是通过存储签名者直到最终交易构建完成来完成的。

以下是如何创建交易构建器并向其添加签名者的完整示例。

> 注意：当您向交易构建器添加`Signer`时，签名者将存储在其中，并且直到您调用`build()`才会解析交易！

```rust,ignore
{{#include ../../../packages/fuels-accounts/src/account.rs:sign_tb}}
```

## 对已构建的交易进行签名

如果您有一个已构建的交易，并且想要添加签名，您可以使用`sign_with`方法。

```rust,ignore
{{#include ../../../e2e/tests/contracts.rs:tx_sign_with}}
```
