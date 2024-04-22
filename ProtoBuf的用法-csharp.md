# ProtoBuf 的用法 - csharp

## 编辑 protobuf 文件

使用 README.md 里的 test.proto。

## 生成 csharp 文件

```bash
# protoc --csharp_out=./ ./test.proto
```

会在当前目录下生成 ```Test.cs```

## 新建 csharp 工程

添加引用：

使用 NuGet 安装 ```Google.Protobuf```。

**注：protobuf 的版本与 安装的 protoc 的版本保持一致。**

示例代码：

```csharp
{
    PeopleInfo info = new PeopleInfo();
    info.Age = 10;
    info.Name = "aa";

    // 序列化
    byte[] byteArray = new byte[info.CalculateSize()];
    using (CodedOutputStream outputStream = new CodedOutputStream(byteArray))
    {
        info.WriteTo(outputStream);
    }

    // 反序列化1
    PeopleInfo info1 = PeopleInfo.Parser.ParseFrom(byteArray);
    Console.WriteLine(info1);

    // 反序列化2
    PeopleInfo info2 = ParseFrom<PeopleInfo>(byteArray);
    Console.WriteLine(info2);
}

public T ParseFrom<T>(byte[] byteArray) where T : IMessage, new()
{
    T t = new T();
    using (CodedInputStream inputStream = new CodedInputStream(byteArray))
    {
        t.MergeFrom(inputStream);
    }
    return t;
}
```
