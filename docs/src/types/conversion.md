# 类型转换

以下是常见类型转换的示例：

- [原生类型之间的转换](#convert-between-native-types)
- [转换为 `Bytes32`](#convert-to-bytes32)
- [转换为 `Address`](#convert-to-address)
- [转换为 `ContractId`](#convert-to-contractid)
- [转换为 `Identity`](#convert-to-identity)
- [转换为 `AssetId`](#convert-to-assetid)
- [转换为 `Bech32`](#convert-to-bech32)
- [转换为 `str`](#convert-to-str)
- [转换为 `Bits256`](#convert-to-bits256)
- [转换为 `Bytes`](#convert-to-bytes)
- [转换为 `B512`](#convert-to-b512)
- [转换为 `EvmAddress`](#convert-to-evmaddress)

## 原生类型之间的转换

你可能需要在原生类型之间进行转换（`Bytes32`、`Address`、`ContractId` 和 `AssetId`）。因为这些类型都是 `[u8; 32]` 的包装器，所以转换只是简单地对其中一个进行解引用，并使用解引用后的值实例化另一个。以下是一个示例：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:type_conversion}}
```

## 转换为 `Bytes32`

将 `[u8; 32]` 数组转换为 `Bytes32`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:array_to_bytes32}}
```

将十六进制字符串转换为 `Bytes32`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:hex_string_to_bytes32}}
```

## 转换为 `Address`

将 `[u8; 32]` 数组转换为 `Address`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:array_to_address}}
```

将 `Bech32` 地址转换为 `Address`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:bech32_to_address}}
```

将钱包转换为 `Address`：

```rust,ignore
{{#include ../../../examples/wallets/src/lib.rs:wallet_to_address}}
```

将十六进制字符串转换为 `Address`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:hex_string_to_address}}
```

## 转换为 `ContractId`

将 `[u8; 32]` 数组转换为 `ContractId`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:array_to_contract_id}}
```

将十六进制字符串转换为 `ContractId`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:string_to_contract_id}}
```

将合约实例转换为 `ContractId`：

```rust,ignore
{{#include ../../../e2e/tests/logs.rs:instance_to_contract_id}}
```

## 转换为 `Identity`

将 `Address` 转换为 `Identity`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:address_to_identity}}
```

将 `ContractId` 转换为 `Identity`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:contract_id_to_identity}}
```

## 转换为 `AssetId`

将 `[u8; 32]` 数组转换为 `AssetId`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:array_to_asset_id}}
```

将十六进制字符串转换为 `AssetId`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:string_to_asset_id}}
```

## 转换为 `Bech32`

将 `[u8; 32]` 数组转换为 `Bech32` 地址：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:array_to_bech32}}
```

将 `Bytes32` 转换为 `Bech32` 地址：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:bytes32_to_bech32}}
```

将字符串转换为 `Bech32` 地址：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:str_to_bech32}}
```

将 `Address` 转换为 `Bech32` 地址：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:address_to_bech32}}
```

## 转换为 `str`

将 `ContractId` 转换为 `str`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:contract_id_to_str}}
```

将 `Address` 转换为 `str`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:address_to_str}}
```

将 `AssetId` 转换为 `str`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:asset_id_to_str}}
```

将 `Bytes32` 转换为 `str`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:bytes32_to_str}}
```

## 转换为 `Bits256`

将十六进制字符串转换为 `Bits256`：

```rust,ignore
{{#include ../../../packages/fuels-core/src/types/core/bits.rs:hex_str_to_bits256}}
```

将 `ContractId` 转换为 `Bits256`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:contract_id_to_bits256}}
```

将 `Address` 转换为 `Bits256`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:address_to_bits256}}
```

将 `AssetId` 转换为 `Bits256`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:asset_id_to_bits256}}
```

## 转换为 `Bytes`

将字符串转换为 `Bytes`：

```rust,ignore
{{#include ../../../packages/fuels-core/src/types/core/bytes.rs:hex_string_to_bytes32}}
```

## 转换为 `B512`

将两个十六进制字符串转换为 `B512`：

```rust,ignore
{{#include ../../../e2e/tests/types_contracts.rs:b512_example}}
```

## 转换为 `EvmAddress`

将 `Bits256` 地址转换为 `EvmAddress`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:b256_to_evm_address}}
```
