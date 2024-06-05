# 结构体和枚举

<!-- This section should explain how to get the custom types from a Sway program -->
<!-- custom_types:example:start -->

你在 Sway 代码中定义的结构体和枚举将由 SDK 的 `abigen!` 宏自动生成对应的类型。

<!-- custom_types:example:end -->

例如，如果你的 Sway 代码中有一个名为 `CounterConfig` 的结构体，如下所示：

```rust,ignore
struct CounterConfig {
  dummy: bool,
  initial_value: u64,
}
```

在使用了 `abigen!` 宏后，`CounterConfig` 将可以在你的 Rust 文件中访问！以下是一个示例：

```rust,ignore
{{#include ../../../e2e/tests/types_contracts.rs:struct_generation}}
```

你可以自由地在此范围内使用你的自定义类型（结构体或枚举）。这也意味着可以将自定义类型传递给函数，并从函数调用中接收

## 泛型

Fuel Rust SDK 支持泛型枚举和泛型结构体。如果你已经熟悉 Rust，那么这是你典型的 `struct MyStruct<T>` 类型的泛型支持。

例如，你的 Sway 合约可能如下所示：

```Rust
contract;

use std::hash::sha256;

struct SimpleGeneric<T> {
    single_generic_param: T,
}

abi MyContract {
  fn struct_w_generic(arg1: SimpleGeneric<u64>) -> SimpleGeneric<u64>;
}

impl MyContract for Contract {
    fn struct_w_generic(arg1: SimpleGeneric<u64>) -> SimpleGeneric<u64> {
        let expected = SimpleGeneric {
            single_generic_param: 123u64,
        };

        assert(arg1.single_generic_param == expected.single_generic_param);

        expected
    }
}
```

你的 Rust 代码将如下所示：

```rust,ignore
{{#include ../../../e2e/tests/types_contracts.rs:generic}}
```

### 未使用的泛型类型参数

Sway 支持在声明结构体/枚举时使用未使用的泛型类型参数：

```Rust
struct SomeStruct<T, K> {
  field: u64
}

enum SomeEnum<T, K> {
  One: u64
}

```

如果你在 Rust 中尝试相同的操作，你会收到关于必须使用或删除 `T` 和 `K` 的投诉。当为这些类型生成 Rust 绑定时，我们会使用 [`PhantomData`](https://doc.rust-lang.org/std/marker/struct.PhantomData.html#unused-type-parameters) 类型。上述示例的生成绑定将如下所示：

```Rust
struct SomeStruct<T, K> {
   pub field: u64,
   pub _unused_generic_0: PhantomData<T>
   pub _unused_generic_1: PhantomData<K>
}

enum SomeEnum<T, K> {
  One(u64),
  IgnoreMe(PhantomData<T>, PhantomData<K>)
}
```

为了减少对开发者体验的影响，你可以使用 `SomeStruct::new` 来初始化上述结构，而不需要处理 `PhantomData`：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:unused_generics_struct}}
```

如果你的结构没有任何字段，我们也会派生 `Default`。至于枚举，所有的 `PhantomData` 都放在了一个名为 `IgnoreMe` 的新变体中，你需要在匹配中忽略它们：

```rust,ignore
{{#include ../../../examples/types/src/lib.rs:unused_generics_enum}}
```
