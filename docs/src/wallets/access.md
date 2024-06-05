# 钱包访问

<!-- 此部分应解释不同类型钱包之间的区别 -->
<!-- wallet_types:example:start -->

我们可以通过 `Wallet` 实例执行的操作的类型取决于我们是否可以访问钱包的私钥。

为了区分那些知道它们的私钥和那些不知道的 `Wallet` 实例，我们分别使用 `WalletUnlocked` 和 `Wallet` 类型。

<!-- wallet_types:example:end -->

## 钱包状态

<!-- 此部分应解释解锁的钱包类型 -->
<!-- wallet_unlocked:example:start -->

`WalletUnlocked` 类型表示一个知道其私钥并且在内存中存储的钱包。为了执行涉及签名消息或交易的操作，钱包必须是 `WalletUnlocked` 类型。

<!-- wallet_unlocked:example:end -->

你可以在[这里](./signing.md)了解更多关于签名的内容。

<!-- 此部分应解释锁定的钱包类型 -->
<!-- wallet_locked:example:start -->

`Wallet` 类型表示一个私钥未知或未在内存中存储的钱包。相反，`Wallet` 只知道其公共地址。`Wallet` 不能用于签署交易，但它仍然可以执行一系列有用的操作，包括列出交易、资产、查询余额等等。

<!-- wallet_locked:example:end -->

注意，`WalletUnlocked` 类型提供了一个针对其内部 `Wallet` 类型的 `Deref` 实现。这意味着在 `Wallet` 类型上可用的所有方法也可以在 `WalletUnlocked` 类型上使用。换句话说，`WalletUnlocked` 可以被视为一个围绕 `Wallet` 的轻量包装，通过其私钥提供更大的访问权限。

## 状态转换

可以通过提供私钥来解锁 `Wallet` 实例：

```rust,ignore
let wallet_unlocked = wallet_locked.unlock(private_key);
```

可以使用 `lock` 方法锁定 `WalletUnlocked` 实例：

```rust,ignore
let wallet_locked = wallet_unlocked.lock();
```

大多数创建或生成新钱包的钱包构造函数都提供在 `WalletUnlocked` 类型上。在处理了新的私钥后，考虑使用 `lock` 方法锁定钱包，以减少内存中存储钱包私钥的范围。

## 设计准则

在设计接受钱包作为输入的 API 时，我们应该仔细考虑我们需要的访问类型。API 开发人员应该尽量减少对 `WalletUnlocked` 的使用，以确保私钥在内存中的存储时间尽可能短，从而减少下游库和应用程序中攻击和漏洞的表面积。
