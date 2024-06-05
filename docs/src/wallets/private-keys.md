# 从私钥创建钱包

您可以通过提供`Option<Provider>`来创建一个具有随机生成的私钥的新钱包。

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:create_random_wallet}}
```

或者，您可以从预定义的`SecretKey`创建一个钱包。

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:create_wallet_from_secret_key}}
```

> 注意：如果提供的是`None`而不是提供者，那么与钱包相关的任何交易都将导致错误，直到使用`set_provider()`链接提供者。可选参数使您能够在启动提供者之前定义创世币的所有者（钱包地址）。
