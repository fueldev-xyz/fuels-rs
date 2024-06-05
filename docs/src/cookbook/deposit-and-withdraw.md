# 存款和提款

考虑以下合约：

```rust,ignore
{{#include ../../../e2e/sway/contracts/liquidity_pool/src/main.sw}}
```

顾名思义，它代表了一个简化的流动性池合约示例。`deposit()` 方法期望您提供任意数量的 `BASE_TOKEN`。作为结果，它会向调用地址铸造双倍数量的流动性资产。类似地，如果您调用 `withdraw()` 并提供流动性资产，它将把一半数量的 `BASE_TOKEN` 转移回调用地址，而不是从合约余额中扣除，而是从铸造中扣除。

与 Rust SDK 中与任何合约交互的第一步是调用 `abigen!` 宏以为合约方法生成类型安全的 Rust 绑定：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:liquidity_abigen}}
```

接下来，我们使用自定义定义的资产设置一个钱包。我们为我们的钱包提供了一些合约的 `BASE_TOKEN` 和默认资产（部署合约所需的资产）：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:liquidity_wallet}}
```

启动提供程序并创建钱包后，我们可以部署我们的合约并创建其方法的实例：

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:liquidity_deploy}}
```

准备工作完成后，我们最终可以通过合约实例调用 `deposit()` 来存入流动性池。由于我们必须向合约转移资产，我们创建适当的 `CallParameters` 并将它们链接到方法调用上。为了接收铸造的流动性池资产，我们必须将一个变量输出附加到我们的合约调用中。

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:liquidity_deposit}}
```

作为最后的演示，让我们使用我们所有的流动性资产余额从池中提款，并确认我们检索到了初始金额。为此，我们获取我们的流动性资产余额，并通过 `CallParameters` 将其提供给 `withdraw()` 调用。

```rust,ignore
{{#include ../../../examples/cookbook/src/lib.rs:liquidity_withdraw}}
```
