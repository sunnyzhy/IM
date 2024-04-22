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
