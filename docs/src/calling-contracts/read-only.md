# 只读调用

<!-- This section should explain read-only calls  -->
<!-- read_only:example:start -->

有时候，您想调用一个不会改变区块链状态的合约方法。例如，一个仅从存储中读取值并返回的方法。

在这种情况下，没有必要生成一个实际的区块链事务；您只想快速读取一个值。

您可以使用 SDK 来实现这一点。而不是使用 `.call()` 调用方法，而是使用 `.simulate()`：

<!-- read_only:example:end -->

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:simulate}}
```

<!-- This section should explain what happens if you try a read-only call on a method that changes state  -->
<!-- simulate:example:start -->

请注意，如果您在一个改变区块链状态的方法上使用 `.simulate()`，它将无法正常工作；它只会进行 `dry-run`。

目前，您需要知道一个合约方法是否改变状态，并相应地使用 `.call()` 或 `.simulate()`。

<!-- simulate:example:end -->
