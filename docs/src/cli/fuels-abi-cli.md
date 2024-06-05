# `fuels-abi-cli`

一个简单的 CLI 程序，用于编码 Sway 函数调用和解码其输出。编码和解码的 ABI 在[这里](https://specs.fuel.network/master/abi/index.html)指定。

## 用法

```plaintext
sway-abi-cli 0.1.0
FuelVM ABI 编码器

USAGE:
    sway-abi-cli <SUBCOMMAND>

FLAGS:
    -h, --help 打印帮助信息
    -V, --version 打印版本信息

SUBCOMMANDS:
    codegen 输出 Rust 类型文件
    decode 解码 ABI 调用结果
    encode 编码 ABI 调用
    help 打印此消息或给定子命令的帮助信息
```

## 示例

你可以选择只编码给定的参数，或者更进一步，使用完整的 JSON ABI 文件，并对 JSON 文件中定义的某个函数调用的整个输入进行编码。

### 仅编码参数

```console
$ cargo run -- encode params -v bool true
0000000000000001
```

```console
$ cargo run -- encode params -v bool true -v u32 42 -v u32 100
0000000000000001000000000000002a0000000000000064
```

请注意，对于每个要编码的参数，你必须传递一个`-v`标志，后跟类型，然后是值：`-v <type_1> <value_1> -v <type_2> <value_2> -v <type_n> <value_n>`

### 编码函数调用

`example/simple.json`:

```json
[
  {
    "type": "function",
    "inputs": [
      {
        "name": "arg",
        "type": "u32"
      }
    ],
    "name": "takes_u32_returns_bool",
    "outputs": [
      {
        "name": "",
        "type": "bool"
      }
    ]
  }
]
```

```console
$ cargo run -- encode function examples/simple.json takes_u32_returns_bool -p 4
000000006355e6ee0000000000000004
```

`example/array.json`

```json
[
  {
    "type": "function",
    "inputs": [
      {
        "name": "arg",
        "type": "u16[3]"
      }
    ],
    "name": "takes_array",
    "outputs": [
      {
        "name": "",
        "type": "u16[2]"
      }
    ]
  }
]
```

```console
$ cargo run -- encode function examples/array.json takes_array -p '[1,2]'
00000000f0b8786400000000000000010000000000000002
```

请注意，输出的第一个字（8 个字节）保留用于函数选择器，其最后 4 个字节只是函数签名的 256 哈希值。

嵌套结构体的示例：

```json
[
  {
    "type": "contract",
    "inputs": [
      {
        "name": "MyNestedStruct",
        "type": "struct",
        "components": [
          {
            "name": "x",
            "type": "u16"
          },
          {
            "name": "y",
            "type": "struct",
            "components": [
              {
                "name": "a",
                "type": "bool"
              },
              {
                "name": "b",
                "type": "u8[2]"
              }
            ]
          }
        ]
      }
    ],
    "name": "takes_nested_struct",
    "outputs": []
  }
]
```

```console
$ cargo run -- encode function examples/nested_struct.json takes_nested_struct -p '(10, (true, [1,2]))'
00000000e8a04d9c000000000000000a000000000000000100000000000000010000000000000002
```

### 仅解码参数

类似于仅编码参数：

```console
$ cargo run -- decode params -t bool -t u32 -t u32 0000000000000001000000000000002a0000000000000064
Bool(true)
U32(42)
U32(100)
```

### 解码函数输出

```console
$ cargo run -- decode function examples/simple.json takes_u32_returns_bool 0000000000000001
Bool(true)
```
