# 断言中的签名示例

这是一个更复杂的示例，其中断言接受三个签名并将它们与三个预定义的公钥匹配。`ec_recover_address` 函数用于从签名中恢复公钥。如果三个中提取的公钥中有两个与预定义的公钥匹配，则可以花费资金。请注意，签名顺序必须与预定义的公钥顺序相匹配。

```rust,ignore
{{#include ../../../e2e/sway/predicates/signatures/src/main.sw}}
```

让我们使用 SDK 与断言交互。首先，让我们创建三个具有特定密钥的钱包。它们的哈希公钥已硬编码在断言中。然后我们创建接收方钱包，我们将使用它来花费断言资金。

```rust,ignore
{{#include ../../../examples/predicates/src/lib.rs:predicate_wallets}}
```

接下来，让我们添加一些硬币，启动一个提供程序，并将其与钱包连接起来。

```rust,ignore
{{#include ../../../examples/predicates/src/lib.rs:predicate_coins}}
```

现在我们可以使用断言 abigen 为我们创建一个断言编码器实例。要现在花费锁定在断言中的资金，我们必须提供两个签名，其公钥与我们在断言中定义的公钥相匹配。在这个示例中，签名是从一个零数组生成的。

```rust,ignore
{{#include ../../../examples/predicates/src/lib.rs:predicate_load}}
```

接下来，我们将一些资产从一个钱包转移到创建的断言中。我们还确认资金确实已转移。

```rust,ignore
{{#include ../../../examples/predicates/src/lib.rs:predicate_receive}}
```

我们可以使用 [Account](../accounts.md) 特性中的 `transfer` 方法来转移资产。如果断言数据正确，则 `receiver` 钱包将获得资金，我们将验证金额是否正确。

```rust,ignore
{{#include ../../../examples/predicates/src/lib.rs:predicate_spend}}
```
