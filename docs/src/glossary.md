# 术语表

## 合约

<!-- 此部分应定义合约 -->
<!-- rs_contract:example:start -->

在 SDK 中，合约是表示与 Fuel 网络上特定智能合约的连接的抽象。此合约实例可以像常规的 Rust 对象一样使用，具有附加到其上的方法，这些方法反映了其智能合约等效物中的方法。

<!-- rs_contract:example:end -->

## 提供者

<!-- 此部分应定义提供者 -->
<!-- rs_provider:example:start -->

提供者是提供对 Fuel 节点连接的抽象的结构。它提供对节点的只读访问。您可以直接使用此提供者或通过钱包使用它。

<!-- rs_provider:example:end -->

## 钱包和签名者

<!-- 此部分应定义钱包和签名者 -->
<!-- rs_wallet_signer:example:start -->

`Wallet` 是一个具有直接或间接访问私钥的结构。您可以使用 `Wallet` 对消息和交易进行签名，以授权网络从您的帐户中扣款来执行操作。在 SDK 中，术语钱包和签名者通常可以互换使用，但从技术上讲，`Signer` 只是一个 Rust 特征，用于启用对交易和消息的签名；`Wallet` 实现了 `Signer` 特征。

<!-- rs_wallet_signer:example:end -->
