# Protocol Buffers

Protocol Buffers 的特性：

1. 语言无关：Protobuf不依赖于特定的编程语言，这意味着您可以使用一个简单的语言无关接口描述语言（IDL）定义数据结构，然后生成适用于各种编程语言的代码来处理这些结构。

2. 数据结构定义：Protobuf使用结构化模式定义语言来定义要序列化的数据的结构。这个模式被编写在一个.proto文件中，它定义了数据结构的字段、类型和可选元数据。

3. 紧凑的二进制格式：Protobuf将结构化数据序列化为二进制格式，这种格式比传统的基于文本的格式（如XML或JSON）更紧凑和高效。较小的大小减少了带宽和存储需求，使其非常适用于网络通信或存储大量数据。

4. 高效的编码和解码：Protobuf使用高效的编码和解码机制，可以快速地对数据进行序列化和反序列化。二进制格式经过了优化，以提高速度，生成的代码提供了方便的API来处理序列化的数据。

5. 版本控制和向后兼容性：Protobuf支持版本控制和向后兼容性。可以随着时间的推移演进数据模式，通过修改模式来适应新的需求，同时保持与旧版本数据的兼容性。

Protobuf具有许多其他功能和优点，例如可扩展性、跨平台支持和代码生成。它被广泛应用于各种领域，包括分布式系统、网络通信、数据存储和交换等。

## 示例 protobuf 文件

编辑 test.proto：

```proto
syntax = "proto3";  // proto3 必须加此注解

package com.example.demo.model;  // 包名
option optimize_for = LITE_RUNTIME;             //optimize_for是文件级别的选项，Protocol Buffer定义三种优化级别SPEED/CODE_SIZE/LITE_RUNTIME
//缺省情况下是SPEED。 
//SPEED: 表示生成的代码运行效率高，但是由此生成的代码编译后会占用更多的空间。
//CODE_SIZE: 和SPEED恰恰相反，代码运行效率较低，但是由此生成的代码编译后会占用更少的空间，通常用于资源有限的平台，如Mobile。
//LITE_RUNTIME: 生成的代码执行效率高，同时生成代码编译后的所占用的空间也是非常少。     这是以牺牲Protocol Buffer提供反射功能为代价的

// 定义联系人message
message PeopleInfo {
  string name = 1;  // 姓名
  int32 age = 2;    // 年龄  
}
```