# 谓词

在 Sway 中，谓词是返回布尔值且没有任何副作用（它们是纯粹的）的程序。谓词地址可以拥有资产。谓词地址是从编译后的字节码生成的，与比特币中使用的 `P2SH` 地址相同。用户可以像发送给任何其他地址一样无缝地将资产发送到谓词地址。要花费谓词资金，用户必须提供谓词的原始 `byte code` 和 `谓词数据`。在执行 `byte code` 时将使用 `谓词数据`，如果谓词成功验证，则可以转移资金。

## 实例化谓词

让我们考虑以下谓词示例：

```rust,ignore
{{#include ../../../e2e/sway/predicates/basic_predicate/src/main.sw}}
```

我们将看到一个完整的示例，使用 SDK 从谓词中发送和接收资金。

首先，我们设置钱包和一个节点实例。调用 `abigen!` 宏将为我们生成谓词中指定的所有类型，以及两个自定义结构体：

- 一个编码器，带有一个 `encode_data` 函数，可以方便地为我们编码主函数的所有参数。
- 一个可配置结构，其中包含设置谓词中提到的所有可配置项的方法

> 注意：`abigen!` 宏将向谓词的 `name` 字段附加 `Encoder` 和 `Configurables`。例如，`name="MyPredicate"` 将导致两个名为 `MyPredicateEncoder` 和 `MyPredicateConfigurables` 的结构体。

```rust,ignore
{{#include ../../../examples/predicates/src/lib.rs:predicate_data_setup}}
```

一旦我们使用 `forc build` 编译了我们的谓词，我们就可以通过 `Predicate::load_from` 创建一个 `Predicate` 实例。然后可以将 `encode_data` 的结果设置到加载的谓词上。

```rust,ignore
{{#include ../../../examples/predicates/src/lib.rs:with_predicate_data}}
```

接下来，使用第一个钱包在此谓词中锁定一些资产：

```rust,ignore
{{#include ../../../examples/predicates/src/lib.rs:predicate_data_lock_amount}}
```

然后，我们可以通过 [Account](../accounts.md) 特性转移由谓词拥有的资产：

```rust,ignore
{{#include ../../../examples/predicates/src/lib.rs:predicate_data_unlock}}
```

## 可配置常量

与合约和脚本一样，您可以在 `predicates` 中定义可配置常量，在谓词执行期间可以更改。以下是定义常量的示例。

```rust,ignore
{{#include ../../../e2e/sway/predicates/predicate_configurables/src/main.sw:predicate_configurables}}
```

每个可配置常量在 SDK 中都会获得一个专用的 `with` 方法。例如，常量 `U8` 将获得名为 `with_U8` 的方法，该方法接受 sway 中定义的相同类型。下面是一个示例，其中我们链接了几个 `with` 方法，并使用新的常量更新了谓词。

```rust,ignore
{{#include ../../../e2e/tests/predicates.rs:predicate_configurables}}
```
