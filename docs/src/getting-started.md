# 入门指南

## 安装指南

请访问 Fuel 的 [安装指南](https://docs.fueldev.xyz/guides/installation) 来安装 Fuel 工具链二进制文件和先决条件。

`forc` 是 Rust 的 `cargo` 的 Sway 等效工具。 `fuel-core` 是 Fuel 完整节点的实现。

您可以使用 Fuel Rust SDK 的两种主要方式：

1. 使用 `forc` 创建一个新的 Sway 项目并运行测试
2. 创建一个独立项目并导入 `fuels-rs` crate

## 使用 Forc 创建一个新项目

您可以使用以下命令创建一个新的 Sway 项目：

```shell
forc new <Project name>
```

或者您可以在现有文件夹中初始化一个项目：

```shell
forc init
```

### 在 Sway 项目中添加 Rust 集成测试

现在我们有了一个新项目，我们可以使用 `cargo generate` 模板添加一个 Rust 集成测试。
如果尚未安装 `cargo generate`，您可以使用以下命令安装它：

<!-- 此部分应包含安装 cargo generate 的命令 -->
<!-- cargo_gen_install:example:start -->

```shell
cargo install cargo-generate
```

<!-- cargo_gen_install:example:end -->

> **注意** 您可以通过访问其 [存储库](https://github.com/cargo-generate/cargo-generate) 了解有关 cargo generate 的更多信息。

让我们使用以下命令生成默认的测试框架：

<!-- 此部分应包含用于生成测试框架的 cargo generate 命令 -->
<!-- cargo_gen:example:start -->

```shell
cargo generate --init fuellabs/sway templates/sway-test-rs --name <Project name> --force
```

<!-- cargo_gen:example:end -->

<!-- 此部分应解释 `--force` 标志 -->
<!-- force_flag:example:start -->

`--force` 强制您的 `--name` 输入保留您在模板中的 `{{project-name}}` 占位符的所需大小写。否则，`cargo-generate` 会自动将其转换为 kebab-case。使用 `--force`，这意味着 `my_fuel_project` 和 `my-fuel-project` 都是有效的项目名称，具体取决于您的需求。

<!-- force_flag:example:end -->

在运行测试之前，我们需要使用以下命令构建 Sway 项目：

```shell
forc build
```

然后，我们可以使用以下命令运行测试：

<!-- 此部分应包含运行测试的命令 -->
<!-- run_test:example:start -->

```shell
cargo test
```

<!-- run_test:example:end -->

> **注意** 如果您需要捕获测试的输出，请使用以下命令之一：

<!-- 此部分应包含不捕获输出的测试命令 -->
<!-- run_test_nocap:example:start -->

```shell
cargo test -- --nocapture
```

<!-- run_test_nocap:example:end -->

## 导入 Fuel Rust SDK

在您的 `Cargo.toml` 中添加以下依赖项：

```toml
fuels = "0.63.0"
```

> **注意** 我们使用版本 `0.63.0` 的 SDK，在撰写本文时为最新版本。

然后，在您将使用 SDK 的 Rust 文件中：

```rust,ignore
use fuels::prelude::*;
```

## Fuel Rust SDK 源代码

体验 SDK 的另一种方式是查看源代码。 `e2e/tests/` 文件夹中充满了涵盖 SDK 几乎所有方面的集成测试。

> **注意** 在运行测试之前，我们需要构建所有 Sway 测试项目。文件 `packages/fuels/Forc.toml` 包含一个 `[workspace]`，其成员是所有集成测试的路径。
> 要构建这些测试，请运行以下命令：

```shell
forc build --release --path packages/fuels
```

> `forc` 也可用于清理和格式化测试项目。查看 `help` 输出以获取更多信息。

构建项目后，我们可以使用以下命令运行测试

```shell
cargo test
```

如果您需要所有目标和所有功能，则可以运行

```shell
cargo test --all-targets --all-features
```

> **注意** 如果您需要捕获测试的输出，您可以运行

```shell
cargo test -- --nocapture
```

## 更深入的 Fuel 和 Sway 知识

阅读 [Sway 书籍](https://docs.fueldev.xyz/docs/sway/) 获取有关 Sway 的更深入知识，Sway 是 Fuel 虚拟机的官方智能合约语言。
