# 使用 abigen 生成绑定

<!-- 本部分应解释 abigen 的目的 -->
<!-- abigen:example:start -->

`abigen!` 是一个过程宏 -- 它会生成代码。它接受以下格式的输入：

```text
ProgramType(name="MyProgramType", abi="my_program-abi.json")...
```

其中：

- `ProgramType` 是 `Contract`、`Script` 或 `Predicate` 中的一种，

- `name` 是将分配给生成的绑定的名称，

- `abi` 是 JSON ABI 文件的路径或其实际内容。
<!-- abigen:example:end -->

---

因此，生成绑定两个合约和一个脚本的 `abigen!` 如下所示：

```rust,ignore
{{#include ../../../examples/macros/src/lib.rs:multiple_abigen_program_types}}
```

## 生成的代码是什么样的？

一个简单的概述：

```rust,ignore
pub mod abigen_bindings {
    pub mod contract_a_mod {
        struct SomeCustomStruct{/*...*/};
        // 其他合约中使用的自定义类型

        struct ContractA {/*...*/};
        impl ContractA {/*...*/};
        // ...
    }
    pub mod contract_b_mod {
        // ...
    }
    pub mod my_script_mod {
        // ...
    }
    pub mod my_predicate_mod{
        // ...
    }
    pub mod shared_types{
        // ...
    }
}

pub use contract_a_mod::{/*..*/};
pub use contract_b_mod::{/*..*/};
pub use my_predicate_mod::{/*..*/};
pub use shared_types::{/*..*/};
```

每个 `ProgramType` 都有自己的 `mod`，其名称基于 `abigen!` 中给定的 `name`。在相应的模块中，生成了程序使用的自定义类型以及用于进行实际调用的绑定。

如果 `abigen!` 检测到给定的程序共享类型，则会生成一个额外的名为 `shared_types` 的 `mod`。与其每个 `mod` 都重新生成类型相比，将类型提取到 `shared_types` 模块中仅生成一次，然后在所有使用它的程序绑定之间共享。每个 `mod` 都添加了重新导出，以便即使类型被视为共享，您仍然可以像每个 `mod` 都为自己生成类型一样访问它（例如 `my_contract_mod::SharedType`）。

如果其名称和定义匹配，则将类型视为共享。这可能是因为您使用了相同的库（自定义库或 `stdlib` 中的类型）或者因为您恰好定义了完全相同的类型。

最后，会插入 `pub use` 语句，以便您不必完全限定生成的类型。为了避免冲突，只有具有唯一名称的类型才会获得 `pub use` 语句。如果您发现 `rustc` 找不到您的类型，可能只是因为另一个生成的类型具有相同的名称。要解决此问题，只需通过 `abigen_bindings::whatever_contract_mod::TheType` 来修饰路径即可。

> **注意：**
> 强烈建议您在一个 `abigen!` 调用中生成所有绑定。以这种方式进行操作将允许类型共享，并避免在同一命名空间内多次调用 `abigen!` 时通常会出现的名称冲突。如果选择以其他方式进行操作，请记住上面介绍的生成的代码概览，并适当地将 `abigen!` 调用分隔到不同的模块中以解决冲突。

### 类型路径

通常，在合约、脚本或断言中使用库中的类型时，它们将直接生成在程序绑定的主 `mod` 下，即从库 `some_library` 导入的合约绑定中的类型将生成在 `abigen_bindings::my_contract_mod::SomeLibraryType` 下。

如果您的程序的不同库中恰好有两个同名的类型，则可能会导致问题。

如果类型没有重新导出，这种情况可能会发生。正如前面解释的那样，如果您的类型在一个 `abigen!` 调用中没有唯一的名称，则可能会发生这种情况。然后，您将需要完全限定对它的访问。

通过使用以下方式编译您的 Sway 项目，可以更改此行为以包括库路径：

```shell
forc build --json-abi-with-callpaths
```

现在，前面示例中的类型将生成在 `abigen_bindings::my_contract_mod::some_library::SomeLibraryType` 下。

如果您的类型没有重新导出，则这可能仅变得重要。这可能会发生，正如前面解释的，如果您的类型在一个 `abigen!` 调用中没有唯一的名称，则可能会发生。您将需要完全限定对它的访问。

将类型路径包含其中最终将成为默认设置，并且将删除该标志。

## 使用绑定

让我们看一个具有两个方法的合约的示例：`initialize_counter(arg: u64) -> u64` 和 `increment_counter(arg: u64) -> u64`，其 JSON ABI 如下：

```json,ignore
{{#include ../../../examples/rust_bindings/src/abi.json}}
```

通过执行以下操作：

```rust,ignore
{{#include ../../../examples/rust_bindings/src/lib.rs:use_abigen}}
```

或者：

```rust,ignore
{{#include ../../../examples/rust_bindings/src/lib.rs:abigen_with_string}}
```

您将生成如下所示的代码（为简洁起见进行了缩短）：

```rust,ignore
{{#include ../../../examples/rust_bindings/src/rust_bindings_formatted.rs}}
```

> **注意：** 这都是 **生成的** 代码。永远不需要编写其中的任何代码。生成的代码在不同版本之间可能会有所不同，这只是一个示例，以便让您了解它的样子。

然后，您可以使用它来调用已部署合约上的实际方法：

```rust,ignore
{{#include ../../../examples/contracts/src/lib.rs:use_deployed_contract}}
```
