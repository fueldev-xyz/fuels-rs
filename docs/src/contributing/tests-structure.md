# `fuels-rs` 中的集成测试结构

`fuels-rs` 的集成测试涵盖了 SDK 的几乎所有方面，并随着功能的增加而不断增长。为了使测试和相关的 `Sway` 项目更易于管理，它们被分成了几个类别。每个类别都包含一个用于测试的 `.rs` 文件，以及如果需要的话，一个用于 `Sway` 项目的单独目录。

当前的结构如下。

```shell
  .
  ├─  bindings/
  ├─  contracts/
  ├─  logs/
  ├─  predicates/
  ├─  storage/
  ├─  types/
  ├─  bindings.rs
  ├─  contracts.rs
  ├─  from_token.rs
  ├─  logs.rs
  ├─  predicates.rs
  ├─  providers.rs
  ├─  scripts.rs
  ├─  storage.rs
  ├─  types.rs
  └─  wallets.rs
```

即使测试组织是主观的，在添加新类别之前，请考虑以下准则：

- 当在 `Fuels Rust SDK` 书中创建新章节时，请添加新类别，例如 `Types`
- 如果有超过 3 个测试和超过 100 行代码，并且它们形成了一个测试组，请添加新类别，例如 `storage.rs`

否则，我们建议将集成测试放在上述现有类别中。
