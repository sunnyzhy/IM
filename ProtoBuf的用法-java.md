# ProtoBuf 的用法 - java

## 编辑 protobuf 文件

使用 README.md 里的 test.proto。

## 生成 java 文件

```bash
# protoc --java_out=./ ./test.proto
```

会在当前目录下生成 ```com/example/demo/model/Test.java```

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

**注：protobuf-java 的版本与安装的 protoc 的版本保持一致。**

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
