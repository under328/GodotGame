#### 变量
- 折叠代码
```csharp
#region MyRegion
Console.WriteLine("折叠代码");
Console.WriteLine("折叠代码");
#endregion
```

- 变量类型
- 有符号 无符号 浮点数 特殊
f 7-8 有效位数
d 15-17 有效位数
char 字符类型 用来存储单个字符
char l = "李";
多个同类型变量声明
int a = 1, b = 2;
变量本质
sizeof
获取变量类型所占用的内存空间 byte
1 4 2 8
4 8 16
bool 1
char 2

变量命名规范
驼峰命名法（变量）myName
帕斯卡命名法（函数、类）MyName

常量 const
必须初始化、不能被修改
const int num = 18

转义字符
"\'"
\a警告音
\0空字符
@ 取消转义字符

隐式转换
 相同大类型之间的转换
**大范围装小范围**
double -> float -> 整型 -> char
decimal -> 整型 -> char
string、bool类型不能隐式转换

有符号变量不能隐式转换为无符号的
无符号的能隐式转换为有符号的（大范围转小范围）
decimal 不能使用隐式转换存储double和float
浮点数（包括decimal）可以装任何类型的整数
整数不能装浮点数
char隐式转换为数值类型会转换为ASCII码

显式转换
- 括号强转
```
int i = 10;
byte b = (byte)i; // 显式转换，需要使用强制类型转换符号
```
string、bool类型不能括号强转

- Parse法
  语法：变量类型.Parse("字符串")
  注意：字符串必须能够转换成对应类型，否则报错
  ```
  int num = int.parse("123")  //123
  int num = int.parse("123.456")  //报错
  ```

  - Convert法
  Convert会四舍五入

其他类型转string
1.ToString();
拼接打印

异常捕获
```
// 必备部分
try
{
}
catch（ExceptionName e）
{
// try报错后执行catch中的代码 来捕获异常
}
// 可选部分
finally
{
// 最后执行的代码，有没有出错都执行
}
```
