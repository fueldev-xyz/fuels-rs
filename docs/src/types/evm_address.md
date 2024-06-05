# `EvmAddress`

在 Rust SDK 中，以太坊虚拟机（EVM）地址可以用 `EvmAddress` 类型表示。其定义与 Sway 标准库中具有相同名称的类型匹配，并在与合约交互时相应地进行转换：

```rust,ignore
{{#include ../../../packages/fuels-core/src/types/core/bits.rs:evm_address}}
```

以下是一个示例：

```rust,ignore
{{#include ../../../e2e/tests/types_contracts.rs:evm_address_arg}}
```

> **注意：** 当从 `Bits256` 创建 `EvmAddress` 时，前 12 字节将被清除，因为 EVM 地址只有 20 字节长。
