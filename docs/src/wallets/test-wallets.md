# 设置测试钱包

在测试合约时，通常需要创建一个或多个测试钱包。以下是如何执行的。

## 设置多个测试钱包

<!-- This section should explain setting up multiple test wallets -->
<!-- test_wallets:example:start -->

如果您需要多个测试钱包，可以使用 `launch_custom_provider_and_get_wallets` 方法进行设置。

<!-- test_wallets:example:end -->

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:multiple_wallets_helper}}
```

<!-- This section should explain how to customize test wallets -->
<!-- custom_test_wallets:example:start -->

您可以通过 `WalletsConfig` 自定义测试钱包。

<!-- custom_test_wallets:example:end -->

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:setup_5_wallets}}
```

<!-- This section should explain that test wallets are deterministic -->
<!-- deterministic:example:start -->

> **注意** 使用 `launch_provider_and_get_wallet` 或 `launch_custom_provider_and_get_wallets` 生成的钱包将具有确定性地址。

<!-- deterministic:example:end -->

## 使用多个随机资产设置测试钱包

您可以创建包含多个资产（包括用于支付 gas 的基本资产）的测试钱包。

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:multiple_assets_wallet}}
```

- coins: `Vec<(UtxoId, Coin)>` 具有 `num_assets` \* `coins_per_assets` 个币（UTXO）
- asset_ids: `Vec<AssetId>` 包含 `num_assets` 随机生成的 `AssetId`（始终包括基本资产）

## 使用多个自定义资产设置测试钱包

您还可以创建具有特定 `AssetId`、币金额和币数量的资产。

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:custom_assets_wallet}}
```

这也可以直接通过 `WalletsConfig` 实现。

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:custom_assets_wallet_short}}
```

> **注意** 在这种情况下，您需要手动添加基本资产和相应的币数量和币金额

## 设置资产

Fuel 区块链持有许多不同的资产；您可以使用其独特的 `AssetId` 创建您的资产，也可以为测试目的创建随机资产。

您只能使用一个资产来支付交易费用和 gas：基本资产，其 `AssetId` 为 `0x000...0`，32 字节的零值。

对于测试目的，您可以配置资产的币和金额。您可以使用 `setup_multiple_assets_coins`：

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:multiple_assets_coins}}
```

> **注意** 如果设置多个资产，其中一个资产将始终是基本资产。

如果您只想使用基本资产创建币，则可以使用：

```rust,ignore
{{#include ../../../examples/providers/src/lib.rs:setup_single_asset}}
```

> **注意** 选择大量的币和资产对 `setup_multiple_assets_coins` 或 `setup_single_asset_coins` 可能导致这些方法的运行时显着增加。这将在将来得到改进，但目前，我们建议同时使用最多 **1_000_000** 个币，或 **1000** 个币和资产。
