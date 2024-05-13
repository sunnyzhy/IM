# ProtoBuf 的用法 - java

## 编辑 protobuf 文件

使用 README.md 里的 test.proto。

## 生成 java 文件

```bash
# protoc --java_out=./ ./test.proto
```

会在当前目录下生成 ```com/example/demo/model/Test.java```。

注意：

1. 生成的 ```.java``` 文件名是以 ```.proto``` 的文件名所命名的，且生成的 ```.java``` 文件名的首字母会自动转换为大写。
   - 比如 ```test.proto``` 和 ```Test.proto``` 所生成的 java 文件都是 ```Test.java```
2. 如果 ```.proto``` 的文件名与 message 名称一样，则：
   - 如果名称的大小写一致
      - 比如 ```Test.proto``` 和 ```message Test```，生成的 java 文件名就会自动附加 ```OuterClass```，也就是 ```TestOuterClass.java```
      - 比如 ```test.proto``` 和 ```message test```，生成的 java 文件就是 ```Test.java```，**因为生成的 ```.java``` 文件名的首字母会自动转换为大写**
   - 如果名称的大小写不一致
      - 比如 ```Test.proto``` 和 ```message test```，生成的 java 文件就是 ```Test.java```
      - 比如 ```test.proto``` 和 ```message Test```，生成的 java 文件名就会自动附加 ```OuterClass```，也就是 ```TestOuterClass.java```
3. 当使用 ```option java_outer_classname = "xxx";``` 自定义类名的时候，如果类名、 ```.proto``` 的文件名 和 ```message``` 名称，这三者的名称一样且大小写也一样的话，就会报错：```Cannot generate Java output because the file's outer class name, "xxx", matches the name of one of the types declared inside it.  Please either rename the type or use the java_outer_classname option to specify a different outer class name for the .proto file.```
   - 比如 ```Test.proto``` 、 ```message Test``` 和 ```option java_outer_classname = "Test";``` 生成的 java 文件时就会报上述错误
4. 综上所述，```.java``` 文件名的生成流程：
   1. 取 ```.proto``` 的文件名，如果名称的首字母是小写，就把首字母转换成大写
   2. 把转换后的名称与```message``` 名称作比较，如果名称和大小写都一样的话，生成的 java 文件名就会自动附加 ```OuterClass```。

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

**注：protobuf 的版本与安装的 protoc 的版本保持一致。**

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
