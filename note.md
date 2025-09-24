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

- 逻辑运算优先级
! > && > ||
- 短路运算
```
// || 有真则真，左边为true 右边停止计算
int i = 1
bool result = true || ++i    //i == 1
// && 有假则假，左边为false 右边停止计算
result = false && ++i    //i == 1
```

#### 位运算符
将数值转换为二进制，进行位运算
位与&   位或|   异或^   位取反~   左移<<   右移>>
~先补全所有0再取反，包括符号位
左移几位 右侧加几个0
右移几位 右侧去掉几个数
```
a = 5;   //101
b = a << 1;   //1010
c = a << 2;   //10100
d = a >> 1;   //10
e = a >> 2;   //1
```

#### 三目运算符
`string str = true ? "真" : "假"`

do while 循环至少循环一次实例

### C#基础
#### 枚举
**枚举多配合switch使用**
枚举一般声明在namespace语句块
也可以声明在class、struct语句块
注意：枚举不能在函数语句块中声明
```
using System;

public class EnumTest
{
    enum Day { Sun, Mon, Tue, Wed, Thu, Fri, Sat };

    static void Main()
    {
        **Day today = Day.Sat;**   // 枚举
        int x = (int)Day.Sun;   //枚举转int
        string str = today.ToString();   //枚举转String   "Sat"
        //string转枚举
        //Parse 第一个参数：要转为哪个枚举类型， 第二个参数：需要转换的字符串
        //转换后是通用类型，需要使用括号强转为我们想要的枚举类型
        string str1 = "Sat"
        today = (Day)Enum.Parse(typeof(Day), str1)
        Console.WriteLine("Sun = {0}", x);   //Sun = 0
    }
}
```

#### 数组
数组是一个存储相同类型元素的固定大小的顺序集合。
数组的声明：
double[] balance = { 2340.0, 4523.69, 3421.0};
balance.Length   //3
balance[2]   //3421.0
balance[2] = 3421.8
声明 遍历 增删改查
**Array 类的属性**
二维数组
行优先存储
```
int [,] a = new int [3,4] {
 {0, 1, 2, 3} ,   /*  初始化索引号为 0 的行 */
 {4, 5, 6, 7} ,   /*  初始化索引号为 1 的行 */
 {8, 9, 10, 11}   /*  初始化索引号为 2 的行 */
};
```
array.GetLength(0)   //行
array.GetLength(1)   //列
#### 列表
#### 字典
