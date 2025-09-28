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

#### 访问修饰符
public 公共的，外边内部都可访问
private 私有的（默认），内部才能访问
protected 保护的，内部和子类可以访问
#### 结构体struct
```
using System;

struct Student
    // 变量
    1、结构体申明的变量不能直接初始化，只能在外边或函数中赋值
    public string name;
    public int age;

    // 结构声明
    1、没有返回值
    2、函数名必须与结构体相同
    3、必须有参数
    4、如果申明了构造函数 那么必须在其中对所有变量数据初始化
    public Student(string name, int age)
    {
        this.name = name;
        this.age = age;
    }
    // 函数方法
    public void Speak()
    {
        Console.WriteLine("my name is {0}", this.name)
    }
}
```
```
Student s1 = new Student("jack", 18);
s1.Speak();
```

#### 排序
冒泡排序
两两相邻、不停比较、不停交换、比较m轮
```
int[] arr = {8, 7, 1, 5, 4, 2, 6, 3, 9}
for (int m = 0; m < arr.Length; m++)
{
    bool isSort = false;
    for (int n = 0; n < arr.Length -1 - m; n++)
    {
        if (arr[n] > arr[n + 1])
        {
            isSort = true;
            int temp = arr[n];
            arr[n] = arr[n + 1];
            arr[n + 1] = temp;
        }
    }
    // 当一轮结束后,已排序完成，退出循环
    if( !isSort )
    {
        break;
    }
}
```

选择排序
新建中间商、依次比较、找出极值、放入目标位置、比较n轮
```
int[] arr = {8, 7, 1, 5, 4, 2, 6, 3, 9}
int index = 0;
for (int m = 0; m < arr.Length; m++)
{
    for (int n = 1; n < arr.Length - m ; n++)
    {
        if(arr[index] < arr[n])
        {
            index = n;
        }
    }
    if( index != arr.Length - 1 - m )
    {
        int temp = arr[index];
        arr[index] = arr[arr.Length - 1 - m];
        arr[arr.Length - 1 - m ] = temp;
    }
}
```

#### 类
**封装**
类一般声明在namespace语句块
同一语句块中类不能重名
```
class Person
{
    //成员变量
    //1、用来描述对象的特征
    //2、是否赋值根据需求来定

    public string name;
    public int age;

    //成员方法
    //1、用来描述对象的行为
    //2、成员方法不要加static关键字
    public void Speak()
    {
        Console.WriteLine("my name is {0}", name);
    }
}
```
```
Person p = new Person();
p.Speak();
```


构造函数（初始化）
1、没有返回值
2、函数名和类名必须相同
3、没有特殊需求时 一般都是public
4、构造函数可以被重载
```
class Person
{
    public string name;
    public int age;

    //构造函数
    //无参构造函数
    public Person():this("jack", 18)
    {
    }
    public Person(string name)
    {
        this.name = name;
    }
    //特殊写法
    public Person(int age):this(name)
    {
        this.age = age;
    }


}
```

析构函数（释放时）
在垃圾回收时，才会调用的函数
```
~Line() //析构函数
      {
         Console.WriteLine("对象已删除");
      }
```

垃圾回收机制GC（Garbage Collector）
回收过程：在遍历堆（Heap）上动态分配的所有对象，识别它们是否被引用
垃圾：没有被任何变量引用的内容，需要被回收和释放

注意：GC只负责堆（Heap）内存的垃圾回收
值类型在栈（Stack）中分配内存，有自己的生命周期，会自动分配和释放

垃圾回收算法
引用计数 Reference Counting
标记清除 Mark Sweep
标记整理 Mark Compact
复制集合 Copy Collection

原理：
0代内存   1代内存   2代内存
代：是垃圾回收机制中使用的一种算法（分代算法）
新分配的对象被配置的第0代内存中
0代内存满时，触发垃圾回收

回收过程
1、标记对象 从根（静态字段、方法参数）开始检查引用对象，标记后为可达对象，不可达对象被认为是垃圾
2、搬迁对象（移到1代内存）压缩栈（修改引用地址）

1代内存满后，0、1内存一起释放到2代内存
0、1内存（速度快），2代内存（内存大）
大对象（83kb以上）被认为是2代对象  目的是减少性能消耗，提高性能。不会对大对象进行搬迁。

手动内存回收
一般在游戏loading时
```
GC.Collect();
```

***

**成员属性**
基本概念
1、用于保护成员变量
2、为成员属性的获取和赋值添加逻辑处理
3、解决3P的局限性
 public-内外访问
 private-内部访问
 protected-内部和子类访问
 属性能让成员变量在外部（只能获取不能修改、只能修改不能获取）

 get、set添加访问修饰符
 1、默认为属性的访问权限
 2、需要低于属性的访问权限
 3、不能get、set同时都低于属性的访问权限
```
class Person
{
    private string name;

    //属性命名一般使用 帕斯卡命名法
    public string Name
    {
        private get   //可添加逻辑处理、加密处理
        {
            return name;
        }
        set   //可添加逻辑处理、加密处理
        // value 表示外部传入的值
        {
            name = value;
        }
    }
}
```
自动属性
作用：外部能得不能改
```
public float Height
{
    get;
    private set;
}
```

索引器
概念：索引器让对象可以像数组一样，通过索引访问其元素
索引器可以重载
```
class Person
{
    private string name;
    private Person[] friends;

    // 索引器
    // 访问修饰符 返回值 this[参数列表]
    public Person this[int index]
    {
        get
        {
            if(friends == null || friends.Length - 1 < index)   //索引超出范围返回null
                {
                    return null;
                }
            return friends[index];
        }
        set
        {
            friends[index] = value;
        }
    }
}
```
```
Person p = new Person();
p[0] = new Person();   //通过索引给p添加friends
```

**静态成员 static**
特点：
1、直接用 [类名.] 使用（成员变量需要new才能使用，static可以直接使用）
2、静态成员在程序开始运行时，就会分配内存空间（成员变量实例化时才会分配内存）
3、同生共死，直到程序结束才会被释放
4、静态函数中不能使用非静态成员（因为 非静态成员 还未分配内存空间）
```
class Test
{
    public int age = 18;
    public static float PI = 3.1415926535789f;
}

Test.PI;

Test t = new Test();
t.age;
```

常量和静态变量
相同点：
都可以通过 [类名.] 使用
不同点：
1、const必须初始化，不能修改   static没有这个规则
2、const只能修饰变量；static可以修饰很多
3、const一定是写在访问修饰符后面的；static没有这个要求
```
class Test
{
    public const float = 9.8f; // 必须初始化不能修改
    static public float PI = 3.1415926535789f;
}
```

静态类
特点：
1、只能包含静态成员
2、不能被实例化

作用：
1、将常用的静态成员写在静态类中 方便使用
2、静态类不能实例化，更能体现工具类的 唯一性
```
Console 就是一个静态类
```

静态构造函数
特点：
1、静态类和普通类都可以用
2、不能使用访问修饰符
3、不能有参数
4、只会自动调用一次

作用：
在静态构造函数中 **初始化**静态变量
```
class Test
{
    public int testInt = 200;
    static Test()
    {
        // 第一次使用Test类时，自动调用一次
    }
    public Test()
    {
        // 每次实例化Test类时调用
    }
}
```

**拓展方法**
概念：
为现有的[非静态类] [变量类型] 添加 新方法
作用：
1、提升程序拓展性
2、不需要再对象中重新写方法
3、不需要继承来添加方法
4、为别人封装的类型写额外的方法
特点：
1、一定是写在静态类中
2、一定是个静态函数
3、第一个参数为拓展目标
4、第一个参数用this修饰
注意：
拓展方法与原方法相同，调用会使用原方法


访问修饰符 static 返回值 函数名(this 拓展类名 参数名，参数类型 参数名 ...)
```
static class Tools
{
    // 为int拓展了一个成员方法
    // 成员方法 是需要 实例化对象后 才能使用的
    // value代表 使用该方法的 实例化对象
    public static void SpeakValue(this int value)
    {
        value++
    }
}
```
```
int i = 10;
i.SpeakValue();   // i == 11
```

**运算符重载 operator**
作用：
让自定义类和结构体，能够使用运算符进行运算

特点：
1、一定是公共的静态方法
2、返回值写在operator前
3、逻辑处理自定义

注意：
1、条件运算符需要成对实现
2、一个返回可以多个重载
3、不能使用ref和out

语法：public static 返回类型 operator 运算符（参数列表）
```
class Point
{
    public int x;
    public int y;

    public static Point operator +(Point p1, Point p2)
    {
        Point p = new Point();
        p.x = p1.x + p2.x;
        p.y = p1.y + p2.y;
        return p;
    }
}
```

可重载的运算符：
算术运算符
逻辑运算符 ！
位运算符
条件运算符（有>就要写<）

不可重载的运算符：
逻辑运算符 && ||
索引符 []
强转运算符 ()
特殊运算符
点.   三目运算符 ? :   赋值符号 =

**内部类和分部类(了解)**
内部类
概念：在一个类中申明一个类
特点：使用时要用包裹着点出自己
作用：亲密关系的表现
注意：访问修饰符作用很大

```
class Person
{
    public string name;
    public int age;
    public Body body;

    public class Body
    {
        
    }
{

}
}
```
```
Person p = new Person();
Person.Body body = new Person.Body();
```

分部类 partial
概念：把一个类分成几部分申明
作用：分部描述一个类，增加程序的拓展性
注意：
分部类可以写在多个脚本中
分部类的访问修饰符要一致
分部类中不能有重复成员

```
partial class Student
{
    public string name;
}
partial class Student
{
    public int age;
}
```

分部方法（了解）
概念：将方法的申明和实现分离
特点：
1、不能加访问修饰符 默认所有
2、只能在分部类中申明
3、返回值只能是void
4、可以有参数但不用 out关键字

```
partial class Student
{
    partial void Speak();   //申明函数
}
partial class Student
{
    partial void Speak()
    {
        //实现逻辑
    }
}
```

***

#### String
string 关键字是 System.String 类的别名

**字符串切割**
```
string str = "1, 2, 3, 4, 5, 6";
string[] strs = str.Split(",");   // [1, 2, 3, 4, 5, 6]
```

**字符获取**
```
//字符串的本质是一个char数组
string str = "123";
char c1 = str[0];   // "1"
//转为char数组
char[] chars = str.ToCharArray();
char c2 = chars[1];   // "2" 
```

**字符串拼接**
```
str = string.Format("{0}{1}", "1", 2)   // "12"
```

**获取字符位置**
IndexOf
```
string str = "123";
// 找到返回索引
int index1 = str.IndexOf("2");   // 1
// 为找到返回-1
int index2 = str.IndexOf("5");   // -1
```

LastIndexOf
```
string str = "123123";
// 找到返回索引
int index1 = str.LastIndexOf("23");   // 4
// 为找到返回-1
int index2 = str.LastIndexOf("56");   // -1
```

**移除字符**
```
string str = "123456";

// 移除索引2后的字符，包含索引2
string str1 = str.Remove(2);   //"12"

// 执行两个参数移除
// arg1:开始位置   arg2：字符个数
string str2 = str.Remove(2,2);   //"1256"
```

**字符串截取**
```
string str = "123456";

// 截取中指定位置开始之后的字符串，包含索引2，其他部分删除
string str1 = str.Substring(2);   //"3456"

// 执行两个参数移除
// arg1:开始位置   arg2：字符个数
string str2 = str.Substring(2);   //"34"
```

**替换字符**
```
string str = "12345634";

// arg1:oldValue   arg2：newValue
string str1 = str.Replace("34", "78");   //"12785678"
```

**大小写转换**
```
string str = "abCD";

// 转大写ToUpper
string str1 = str.ToUpper();   //"ABCD"

// 转小写ToLower
string str2 = str.ToLower();   //"abcd"
```

#### StringBuilder
string是特殊的引用，每次重新赋值或者拼接会分配新的内存空间，经常改变字符串非常浪费空间
使用StringBuilder修改字符串不会创建新的对象，提升 频繁修改字符串 的性能

```
// 需要引用Text命名空间
using Text

StringBuilder str = new StringBuilder("123123123");
```

**容量Capacity**
StringBuilder容量满时会自动扩容
```
using Text
// 自定义容量
StringBuilder str = new StringBuilder("123123123", 16);

str.Capacity;   // 16->32->64
str.Length;   // 9
```

**增删改查**
不能使用+拼接，不能使用==判断是否相等
```
StringBuilder str = new StringBuilder("123");

//增
str.Append("4");   //"1234"
str.AppendFormat({0}{1}, 5, "6");   //"123456"
//在索引0前插入0字符
str.Insert(0， "0");   //"0123456"

//删
// arg1:开始位置   arg2：字符个数
str.Remove(1, 2);   //"03456"
//清空
str.Clear();   //""

//查
str[1];   //"3"

//改
str[1] = 9;   //"09456"
//替换
str.Replace("45", "78");   //"09786"

//判断是否相等
str == "09786"   //报错

str.Equals("09786")   //使用Equals判断StringBuilder是否相等
```

#### 结构体和类的区别
数据类型                  值类型      引用类型
存储位置                  栈          堆
                         封装        封装、继承、多态
static、protected修饰    不能        可以
指定初始值                不能        可以
声明无参构造函数          不能        可以

结构体可以继承接口，因为接口是行为的抽象

**如何选择结构体和类**
1. 想要使用继承和多态时，直接淘汰结构体。如玩家、怪物等
2. 对象是数据集合时，优先考虑结构体。如位置、坐标等
3. 从值类型和引用类型赋值时的区别考虑，比如经常被赋值传递的对象，并且改变赋值对象，原对象不想跟着变化时，就用结构体。如坐标、向量、旋转等

#### 抽象类和接口的区别
相同点：
1. 都可以被继承
2. 都不能直接实例化
3. 都可以包含方法声明
4. 子类必须实现未实现的方法
5. 都遵循里氏替换原则

不同点：
1. 抽象类中可以有构造函数；接口不能
2. 抽象类只能被单一继承；接口能继承多个
3. 抽象类中可以有成员变量，接口不能
4. 抽象类中可以声明成员方法、虚方法、抽象方法、静态方法；接口只能声明没有实现的抽象方法
5. 抽象类方法可以使用访问修饰符；接口建议不写（默认public）

**如何选择抽象类和接口**
表示对象的用抽象类，表示行为拓展的用接口

例如：动物是一类事物，可以选择抽象类；飞翔是一个行为，可以选择接口


