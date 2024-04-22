# ProtoBuf 的用法 - java

## 编辑 protobuf 文件

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

## 生成 java 文件

```bash
# protoc --java_out=./ ./test.proto
```

会在当前目录下生成子目录 ```com/example/demo/model/Test.java```

## 新建 springboot 工程

添加依赖项：

```xml
<dependency>
    <groupId>com.google.protobuf</groupId>
    <artifactId>protobuf-java</artifactId>
    <version>4.26.1</version>
</dependency>
<dependency>
    <groupId>com.googlecode.protobuf-java-format</groupId>
    <artifactId>protobuf-java-format</artifactId>
    <version>1.4</version>
</dependency>
```

**注：protobuf-java 的版本与 protoc 的版本保持一致。**

示例代码：

```java
Test.PeopleInfo.Builder builder = Test.PeopleInfo.newBuilder();
builder.setAge(10);
builder.setName("aa");
Test.PeopleInfo build = builder.build();

// 序列化与反序列化
byte[] byteArray = build.toByteArray();
Test.PeopleInfo info = Test.PeopleInfo.parseFrom(byteArray);
System.out.println(info);

// 把对象转为json字符串
// 不能直接使用 jackson，需要使用第三方工具
JsonFormat objectMapper = new JsonFormat();
String s = objectMapper.printToString(info);
System.out.println(s);
```
