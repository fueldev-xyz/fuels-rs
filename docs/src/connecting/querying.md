# 查询区块链

一旦您设置了提供程序，就可以与 Fuel 区块链进行交互。以下是您可以使用提供程序执行的一些操作示例；有关 API 的更详细概述，请查阅[官方提供程序 API 文档](https://docs.rs/fuels/latest/fuels/accounts/provider/struct.Provider.html)。

- [设置](#设置)
- [从地址获取所有币](#从地址获取所有币)
- [获取地址拥有的可花费资源](#获取地址拥有的可花费资源)
- [从地址获取余额](#从地址获取余额)

## 设置

您可能需要首先设置一个测试区块链。如果您连接到外部区块链，则可以跳过此步骤。

```rust,ignore
{{#include ../../../examples/providers/src/lib.rs:setup_test_blockchain}}
```

## 从地址获取所有币

此方法返回钱包中所有未使用的币（特定资产 ID 的）。

```rust,ignore
{{#include ../../../examples/providers/src/lib.rs:get_coins}}
```

## 获取地址拥有的可花费资源

以下示例显示了如何获取地址拥有的资源。首先，您创建一个 `ResourceFilter`，其中指定了目标地址、资产 ID 和金额。您还可以定义在检索资源时应排除的 UTXO ID 和消息 ID：

```rust,ignore
{{#include ../../../packages/fuels-accounts/src/provider.rs:resource_filter}}
```

该示例使用了资产 ID 和排除列表的默认值。这分别解析为基本资产 ID 和空向量用于 ID 列表：

```rust,ignore
{{#include ../../../examples/providers/src/lib.rs:get_spendable_resources}}
```

## 从地址获取余额

获取地址的所有资产的可花费余额。这与获取币不同，因为我们只返回数字（每个资产 ID 的 UTXOs 币金额之和），而不是 UTXOs 币本身。

```rust,ignore
{{#include ../../../examples/providers/src/lib.rs:get_balances}}
```
