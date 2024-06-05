# `setup_program_test!` 宏

在使用 `abigen!` 宏部署合约时，用户可以：

- 更改默认的配置参数
- 启动多个提供程序
- 创建多个钱包
- 创建特定资产等。

然而，通常情况下，我们希望能够快速设置一个测试，使用默认值并直接与合约或脚本实例进行交互。`setup_program_test!` 正好可以做到这一点。

---

用于减少集成测试中的样板代码。输入形式为 `COMMAND(ARG...)...`

`COMMAND` 可以是 `Wallets`、`Abigen`、`LoadScript` 或 `Deploy`。

`ARG` 可以是：

- 名称-值对（例如 `name="MyContract"`），或者
- 文字字面量（例如 `"some_str_literal"`、`true`、`5`，...）
- 子命令（例如 `Abigen(Contract(name="MyContract", project="some_project"))`）

可用的 `COMMAND` 包括：

## Wallets

示例：`Wallets("a_wallet", "another_wallet"...)`

描述：启动本地提供程序并生成钱包，名称取自提供的 `ARG`。

基数：0 或 1。

## Abigen

示例：

```rust,ignore
Abigen(
    Contract(
        name = "MyContract",
        project = "some_folder"
    ),
    Script(
        name = "MyScript",
        project = "some_folder"
    ),
    Predicate(
        name = "MyPredicate",
        project = "some_folder"
    ),
)
```

描述：以 `name` 为名生成程序绑定。`project` 应指向 `forc` 项目的根目录。必须以 `release` 模式编译项目（使用 `--release` 标志），`Abigen` 命令才能正常工作。

基数：0 或 N。

## Deploy

示例：`Deploy(name="instance_name", contract="MyContract", wallet="a_wallet")`

描述：使用 `wallet` 部署带有 salt 的 `contract`。将创建一个通过 `name` 访问的合约实例。由于使用了 salt，同一合约可以部署多次。需要 `Abigen` 命令存在，并且 `name` 等于 `contract`。`wallet` 可以是 `Wallets` 命令中的一个钱包，也可以是您自己先前生成的钱包的名称。

基数：0 或 N。

## `LoadScript`

示例：`LoadScript(name = "script_instance", script = "MyScript", wallet = "wallet")`

描述：使用 `wallet` 在 `name` 下创建 `script` 的脚本实例。

基数：0 或 N。

---

你在之前的部分中看到的设置代码会被简化为：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:deploy_contract_setup_macro_short}}
```

> **注意** 由于宏使用了 salt 部署合约，因此同一个合约可以部署多次。您还可以通过引用相同的钱包在同一提供程序上部署不同的合约。

```rust,ignore
{{#include ../../../e2e/tests/contracts.rs:contract_setup_macro_multi}}
```

在这个例子中，使用 `Wallets` 命令生成的 `wallet` 在同一个提供程序上部署了三个合约。第二个和第三个宏使用相同的合约，但由于使用了 salt 进行部署，它们具有不同的 ID。它们都可以通过使用它们的 ID 调用第一个合约。

此外，您还可以手动创建 `wallet` 变量，然后在宏中使用它。如果您想要创建自定义钱包或提供程序，但仍希望使用宏减少样板代码，这是一个有用的方法。下面是这种方法的示例。

```rust,ignore
{{#include ../../../e2e/tests/contracts.rs:contract_setup_macro_manual_wallet}}
```
