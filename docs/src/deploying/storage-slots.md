# 覆盖存储槽

如果您的合约中使用了存储槽，Sway 编译器将生成默认的存储值，并以 JSON 文件（例如 `my_contract-storage_slots.json`）的形式提供。当您加载合约二进制文件时，这些值将自动加载。如果您希望覆盖某些默认值，则需要手动提供相应的存储槽：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:storage_slots_override}}
```

如果由于某种原因您没有存储槽文件（例如上述示例中的 `my_contract-storage_slots.json`），或者您不希望加载任何默认值，则可以禁用自动加载存储槽：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:storage_slots_disable_autoload}}
```
