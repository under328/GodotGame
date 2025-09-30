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

## C#进阶

### 数据结构

#### ArrayList-数组列表
Arraylist是C#为我们封装好的类
本质是一个object数组（优点什么都可以装，但存在装箱拆箱导致的内存消耗）

```
//需要引用命名空间System.Collections
using System.Collections;

ArrayList array = new ArrayList();

//增
array.Add(2);
array.Add("二");
//插入
array.Insert(1, "789")
//把另一个list容器的内容加在后面
array.AddRange(array2);

//删
//删除指定元素
array.Remove("二");   //删除第一个 "二"
//删除指定位置的元素
array.RemoveAt(2);   //删除索引为2的元素
//清空
array.Clear();

//查
array[0];
//查看元素是否存在
array.Contains("123");   //返回值为bool
//正向查元素位置
array.IndexOf("123");   //返回 第一个元素的索引
//反向查元素位置
array.LastIndexOf("123");   //返回 最后一个元素的索引

//改
array[0] = 999
```

**遍历**
//长度
array.Count
//容量
array.Capacity
```
forEach ( object item in array )
{

}
```

**装箱拆箱**
因为Arraylist本质上是一个自动扩容的object数组，所以存在装箱拆箱，存在内存消耗
int i = 1;
array[0] = i;   //装箱

i = (int)array[0];   //拆箱

#### Stack栈-先进后出
Stack是C#为我们封装好的类
本质是一个object数组，只是封装了特殊的存储规则

Stack是栈存储容器，栈是一种 **先进后出** 的数据结构
先存入的数据后获取，后存入的数据先获取

```
//需要引用命名空间System.Collections
using System.Collections;

Stack s = new Stack();

//增
// 压栈
s.Push("123");   //添加在最后一位
s.Push(2);

//取
object o = s.Pop();   //取出最后一个

//查
//只能查看栈顶的内容
object o = s.Peek();   //查看栈顶内容
//查看元素是否在栈中
s.Contains("123")   //返回bool

//改
//不能修改，只能清空
s.Clear();
```

**遍历**
//长度
s.Count

```
//forEach循环
forEach ( object item in s )
{
    //顺序从栈顶到栈底
}

//转换成object数组后for循环遍历
object[] array = s.ToArrat();

//循环弹栈
while(s.Count > 0)
{
    object o = s.Pop();
}
```

**装箱拆箱**
同Arraylist

#### Queuq队列-先进先出
Queuq是C#为我们封装好的类
本质是一个object数组，只是封装了特殊的存储规则

Queuq是一种 **先进先出** 的数据结构
先存入的数据先获取，后存入的数据后获取

```
//需要引用命名空间System.Collections
using System.Collections;

Queuq q = new Queuq();

//增
q.Enqueue("123");   //添加在最后一位
q.Enqueue(2);

//取
object o = q.Dequeue();   //取出队列第一位

//查
//查看队列头部元素
object o = q.Peek();
//查看元素是否在队列中
q.Contains("123")   //返回bool

//改
//不能修改，只能清空
q.Clear();
```

**遍历**
//长度
q.Count

```
//forEach循环
forEach ( object item in q )
{
    //顺序从第一个到最后一个
}

//转换成object数组后for循环遍历
object[] array = q.ToArrat();

//循环出列
while(q.Count > 0)
{
    object o = q.Dequeue();
}
```

**装箱拆箱**
同Arraylist

#### Hashtable哈希表
Hashtable（又称散列表） 是基于健的哈希代码组织起来的 **键值对**

```
//需要引用命名空间System.Collections
using System.Collections;

Hashtable h = new Hashtable();

//增
//不能出现相同的健
h.Add("健", "值");
h.Add(x, 1);

//删
//只能通过健来删除
h.Remove(x);
//清空
h.Clear();

//查
//通过健查看值
object o = h[x];   //找不到返回空
//查看 健 是否存在
h.Contains(x)  == h.ContainsKey(x);    //返回bool
//查看 值 是否存在
h.ContainsValue(1);

//改
//只能改健对应的值，不能改健
h[x] = 2;
```

**遍历**
//长度
h.Count

```
//forEach循环 健
forEach ( object item in h.Keys )
{
    h[item];
}
//forEach循环 值
forEach ( object item in h.Values )
{
    item;
}
//forEach循环 健值对
forEach ( DictionaryEntry item in h )
{
    item.Key;
    item.Value;
}

//迭代器遍历(了解)
IDictionaryEnumerator myEnumerator = h.GetEnumerator();
bool flag = myEnumerator.MoveNext();
while (flag)
{
    myEnumerator.Key;
    myEnumerator.Value;
    flag = myEnumerator.MoveNext();
}
```

**装箱拆箱**
同Arraylist







### 泛型相关
泛型
泛型约束
List列表
Dictionary字典

***

#### 顺序存储和链式存储
**数据结构**
数据结构是计算机存储、组织数据的规则
数据结构是指相互之间存在一种或多种特定关系的数据元素集合
例如：自定义一个类，也可以称为一种数据结构-自己定义的数据组合规则
常用的数据结构：数组、栈、队列、链表、树、图、堆、散列表...

**线性表**
线性表是一种数据结构，是由n个具有相同特性数据元素组成的有限序列
例如：数组、ArrayList、Stack、Queue、链表...

**顺序存储**
顺序存储是用一组**地址连续的存储单元**依次存储线性表的各种元素
例如：数组、ArrayList、List、Stack、Queue

**链式存储**
链式存储是用一组**任意的存储单元**存储线性表中的各种元素（通过链来连接数据，不需要扩容不会产生额外垃圾）
例如：单向链表、双向链表、循环链表

```
//单向链表节点
class LinkedNode<T>
{
    //数据的值
    public T value;
    //下一个元素（钩子）
    public LinkedNode<T> nextNode;

    //构造函数
    public LinkedNode(T value)
    {
        this.value = value;
    }
}
//单向链表类 （管理节点、添加、删除等逻辑）
class LinkedList<T>
{
    //定义头节点
    public LinkedNode<T> head;
    //定义尾部节点
    public LinkedNode<T> last;

    //添加
    public void Add(T value)
    {
        LinkedNode<T> node = new LinkedNode(T value);
        if(head == null)
        {
            head = node;
            last = node;
        }
        else
        {
            last.nextNode = node;
            last = node;
        }
    }

    //删除
public void Remove(T value)
{
    if(head == null)
    {
        return;
    }
    else if (head.value.Equals(value))
    {
        head = head.nextNode;
        //如果只有一个节点，尾也要清空
        if(head == null)
        {
            last = null;
        }
        return; 
    }
    //定义一个临时node，和链表所有元素进行比较
    LinkedNode<T> node = head;
while(node.nextNode != null)
{
    if(node.nextNode.value.Equals(value)
    {
        //让自己上一个节点 指向 自己的下一个节点（相当于删除自己）
        node.nextNode = node.nextNode.nextNode;
        break;
    }
}
}

}
```
```
//通过new生成的数据，存储位置不确定
LinkedNode<int> node1 = new LinkedNode<int>(1);
LinkedNode<int> node2 = new LinkedNode<int>(2);
node1.nextNode = node2;
node2.nextNode = new LinkedNode<int>(3);

//使用Add、Remove
LinkedLink<int> link = new LinkedLink<int>();
link.Add(1);
link.Add(2);
link.Add(3);
Link.Remove(2);

//循环链表
LinkedNode<int> node = Link.head;
while(node != null)
{
    Console.WriteLine(node);
    node = node.nextNode;
}
```

**顺序存储和链式存储优缺点**
链式存储计算上优于顺序存储：
增加、删除时不需要扩容或移动到新容器
顺序存储计算上优于链式存储：
查找、修改时数组可以直接通过下标得到元素，链表需要遍历

#### Linkedlist链表
Linkedlist是一个C#为我们封装好的类
本质是一个**可变类型的泛型双向链表**

Value 值
Previous 上一个节点
Next 下一个节点

```
//需要引用命名空间System.Collections.Generic
using System.Collections.Generic;

Linkedlist<int> link = new Linkedlist<int>();

//增
//尾部添加
link.AddLast(1);
link.AddLast(2);
//头部添加
link.AddFirst(0);   //0 -> 1 -> 2
//节点后添加
link.AddAfter(node, 10);
//节点前添加
link.AddBefore(node, 5);

//删
//移除头节点
link.RemoveFirst();
//移除尾节点
link.RemoveLast();
//移除指定节点
link.Remove(1);
//清空
link.Clear();

//查
//头节点
LinkedlistNode<int> first = link.First;
//尾节点
LinkedlistNode<int> last = link.Last;
//找到指定值的节点
LinkedlistNode<int> node = link.Find(2);
//判断是否存在
link.Contains(1);

//改
//先得到节点，再通过value来改
LinkedlistNode<int> node = link.Find(2);
node.value = 2;
```

**遍历**
```
//forEach循环
forEach ( int item in link )
{
    item;   //取出的不是节点，直接是值
}

//通过节点遍历
//从头到尾
LinkedlistNode<int> node = link.First;
while(newHead != null)
{
    Console.WriteLine(node.value);
    node = node.Next;
}

//从尾到头
LinkedlistNode<int> node = link.Last;
while(newHead != null)
{
    Console.WriteLine(node.value);
    node = node.Previous;
}
```

#### 泛型栈和队列
需要引用命名空间System.Collections.Generic
和Stack和Queue一样

```
Stack<int> s = new Stack<int>();
Queue<int> q = new Queue<int>();
```

### 委托事件
#### 委托delegate
概念
委托是函数的容器，可以理解为表示函数的变量类型
用来 存储、传递函数
委托本质是一个类，用来定义函数的类型（返回值和参数的类型）
不同的 函数必须对应和各自"格式"一致的委托
例如：作为类的成员、函数的参数
```
//无参无返回值
delegate void MyFun1();
//有参有返回值
delegate int MyFun2(int i);
```
```
static void Fun()
{

}
//专门用来装载函数的容器
MyFun1 f1 = new MyFun1(Fun);
MyFun1 f2 = Fun;   //简写
//使用被装载的函数
f1.Invoke();
f2();   //简写

//有参
MyFun2 f3 = Fun;
f3(5);
```

```
//
class Test
{
    public MyFun fun;
    public MyFun2 fun2;

    public void TestFun(MyFun fun, MyFun2 fun2)
    {
        //先处理一些其他逻辑，处理完后 再执行传入的函数
        Console.WriteLine("123");
        int i = 1 + 2 + 3
        i += 2
        //fun();
        //fun2(i);
        this.fun = fun;
        this.fun2 = fun2;
    }
}
```

**多播委托**
委托变量可以存储多个函数

```
MyFun f = Fun1;
f += Fun2;   // 使用 += -= 添加、删除函数
f -= Fun2;
f = null;   //清空
f();   //先执行Fun1再执行Fun2
```

**系统定义好的委托**

Action   无返回值
Func     有返回值


//无参无返回值的委托
```
Action a = Fun1;
a += Fun2;
a();
```
//有参无返回值的委托
```
Action<int, string> a = Fun1
a(10, "10");
```

//泛型委托
//无参有返回值
```
static string Fun3()
{
    return "";
}

//返回值类型为string
Func<string> funcString = Fun3;

//有参有返回值--arg1~16 -> 参数；last arg -> 返回值
Func<string, int> funcString = Fun4;   //参数为string，返回值为int
```

#### 事件event
概念
事件是基于委托的存在，是委托的安全包裹
事件是一种特殊的变量类型，只能作为成员存在于类、接口以及结构体中
事件不能在**类外部** **赋值、调用**

作用
1. 防止外部随意置空委托
2. 防止外部随意调用委托
3. 事件相当于对委托进行了一次封装 让其更加安全
```
class Test
{
    //委托成员变量 用于储存函数
    public Action myFun;
    //事件成员变量 用于储存函数
    public event Action myEvent;

    public Test()
    {
        //事件的使用和委托一模一样(内部)
        myFun = TestFun;
        myEvent = TestFun;
        myEvent += TestFun1;
        myEvent -= TestFun1;
        //myEvent = null;
        myEvent();
    }
    
    public void TestFun()
    {
    
    }
}

//事件不能在外部赋值、调用（外部）
Test t = new Test();
t.myEvent = TestFun;   //报错
t.myEvent += TestFun;   //可以 += 、 -+   不能 =
t.myEvent -= TestFun;

t.myEvent();   //调用报错
//只能在类内部封装一个自定义函数来调用
t.DoEvent();
```

#### 匿名函数delegate
概念
没有名字的函数，匿名函数主要是配合委托和事件使用的

作用
函数中传递参数
委托或事件赋值
主要是委托传递和存储时使用

```
//无参无返回值
Action a = delegate()
{
};
a();

//有参
Action<int, string> a = delegate(int i , string s)
{
};
a(10, "10");

//有返回值
Func<string> a = delegate()
{
    return "100";
};
string s = a();
```
```
//一般情况下会作为函数参数传递 或者 作为函数返回值

class Test
{
    public Action action;

    //参数传递
    public void Dosomething(int i, Action fun)
    {
        Console.WriteLine(i);
        fun();
    }

    //返回值
    public Action GetFun()
    {
        return delegate()   //不需要先声明一个函数，再做为返回值返回
        {
            Console.WriteLine("返回的匿名函数");
        };
    }
}
```

```
 //参数传递
Test t = new Test();
t.Dosomething(100, delegate()   //不需要先声明一个函数，再做为参数传递
{
    Console.WriteLine("参数传递的匿名函数");
});

//返回值
Action ac = t.GetFun();
ac();
//一步到位直接调用返回的委托函数
t.GetFun()()
```

**匿名函数的缺点**
添加到委托或事件容器中后 不记录 无法单独移除，只能清空。


#### Lambad表达式
概念
可以将lambad表达式 理解为匿名函数的简写

```
//无参无返回值
Action a = () =>
{
};
a();

//有参
Action<int, string> a = (int i , s) =>   //参数类型可省略
{
};
a(10, "10");

//有返回值
Func<string> a = () =>
{
    return "100";
};
string s = a();
```

**闭包**
内层的函数可以引用包含在它外层的函数变量，即使外层函数的执行已经终止

注意
该变量提供的值并非变量创建时的值，而是在父函数范围内的最终值

```
class Test
{
    public event Action action;

    public Test()
    {
        int value = 10;
        value = 20;
    
        action = ()
        {
            Console.WriteLine(value);   //由于函数使用了外部变量形成了闭包；value不会被释放
        };
        value = 30;   //value为最终值
    }
}
```

### 多线程
[操作系统]  -->  n个[进程]  -->  n个[线程]

#### 进程
进程Process 是计算机中程序关于某数据集合上的一次运动活动
是系统进行资源分配和调度的基本单位，是操作系统结构的基础
例如：打开一个应用程序就是在操作系统上开启了一个进程
进程之间可以相互独立运行互不干扰；也可以相互访问、操作

#### 线程
操作系统能够进行运算调度的最小单位
它被包含在进程之中，是进程中的实际运作单位
一条线程指的是进程中一个单一顺序的控制流，一个进程中可以并发多个线程
我们目前写的程序 都在主线程中

简单理解
线程就是代码从上往下运行的一条"管道"

#### 多线程
可以通过代码 开启新的线程
可以同时运行代码的多条"管道"

线程类 Thread
```
//需要引入System.Threading才能使用
using System.Threading;

//1、声明一个新的线程
//注意：线程执行的代码，需要封装到一个函数中
Thread t = new Thread(NewThreadLogic);

static void NewThreadLogic()
{
    //新线程逻辑
}

//2、启动线程
t.Start();

//3、设置为后台线程
//当前台线程结束的时候，整个程序就结束了，即使还有后台线程正在运行
//后台线程不会防止应用程序的进程被终止掉
//如果不设置后台线程 可能导致进程无法正常关闭（例如：前台线程中写了死循环）
t.IsBackground = true;   //一般都设置为后台线程

//4、关闭释放线程
//如果开启的线程不是死循环 不用刻意去关闭它
//死循环中添加bool标准
bool isRunning = true;
while (isRunning)
{

}
//通过Abort关闭，.Net core版本中无法使用
t.Abort();

//5、线程休眠
//单位：毫秒；在哪个线程执行就休眠哪个线程
Thread.Sleep(1000)
```

#### *线程之间共享数据
//多个线程使用的内存是共享的，都属于该应用程序（进程）
//所以要注意 当多线程 同时操作同一片内存区域时可能会出问题（多个线程同时操作同一个内存数据）
//可以通过加锁的形式避免问题

//lock
//当我们在多个线程中想要访问同样的内容 进行逻辑处理时
//为了避免逻辑顺序执行的差错

```
lock(obj)   // 参数需要是引用数据类型
{
    //线程1的逻辑代码
}

lock(obj)
{
    //线程2的逻辑代码
}

```

#### 多线程的意义
可以用多线程专门处理一些复杂耗时的逻辑
例如：寻路、网络通信等等



### 反射和特性
#### 反射
**程序集**
程序集是经由编译器编译得到的 供进一步编译执行的那个中间产物
在WINDOWS系统中，它一般表现为后缀为 [.dll](库文件) 或者 [.exe](可执行文件) 的格式

作用：我们写的一个代码集合，最终会被编译为一个程序集供人使用
例如：[.dll](库文件) 或者 [.exe](可执行文件)
dll文件（库文件），可以看做一种代码仓库，它提供给使用者一些可以直接拿来用的变量、函数或类

**元数据**
元数据就是用来描述数据的数据

例如：程序中的类；类中的函数、变量等信息 就是程序中的元数据

**反射的概念**
程序正在运行时，可以查看其他程序集或自身的元数据
一个运行的**程序查看本身或其他程序元数据的行为**就叫做**反射**

**反射的作用**
因为反射可以在程序编译后获取信息，所以提高了程序的拓展性和灵活性
1. 程序运行时得到所有元数据，包括元数据的特性
2. 程序运行时，实例化对象，操作对象
3. 程序运行时创建新对象，用新对象执行任务

##### Type
Type（类的信息类）是反射功能的基础；是访问元数据的主要方式
作用
使用 Type 的成员获取有关类型（构造函数、方法、字段、属性和类的事件）声明的信息

获取Type
```
//1. 在object中的GetType() 可以获取对象的Type
int i = 10;
Type t = i.GetType();   //System.Int32;t中包含int类型的方法

//2. 通过typeof关键字 传入类名 也可以得到对象的Type
Type t = typeof(int);   //常用

//3. 通过类的名字 也可以获取类型（类名必须包含命名空间 不然找不到）
Type t = Type.GetType("System.Int32");   //不同程序集之间 常用
```

**得到类的程序集信息**
```
t.Assembly
```

```
using System.Reflection;

Type t = typeof(Test);

//得到所有公共成员
MemberInfo[] infos = t.GetMembers();

//得到所有构造函数
ConstructorInfo[] ctors = t.GetConstructors();
//得到一个构造函数，并执行
//需要用Type数组表示参数类型
//无参
ConstructorInfo info = t.GetConstructor(new Type[0]);  //Type[0]无参构造
Test obj = info.Invoke(null) as Test;   //无参构造 没有参数 传入null
obj.i;   //10
//有参
ConstructorInfo info = t.GetConstructor(new Type[] { typeof(int) });  //Type[] { typeof(int), typeof(string) }   参数1为int类型,参数2为string类型
Test obj = info.Invoke( new Type[] {2, "111"} ) as Test;
obj.i;   //2

//得到所有成员变量
FieldInfo[] fieldInfos = t.GetFields();
//得到指定名称的成员变量
FieldInfo infoI = t.GetField("i");
//通过反射获取和设置对象的值
Test test = new Test();   //程序集内部
test.i = 10;   
infoI.GetValue(test);   //不同程序集之间
infoI.SetValue(test, 100);

//得到所有成员方法
Type strType = typeof(string);
MethodInfo[] methods = strType.GetMethods();
//得到单个成员方法
MethodInfo method = strType.GetMethod("Substring", new Type[] { typeof(int), typeof(int) });
//调用方法
//注意：如果是静态方法 Invoke中的第一个参数传null即可
string str = "Hello World";
//arg1：执行方法的对象   arg2：
object result = subStr.Invoke( str, new object[] {2, 3} );
```

**其他**
枚举--GetEnumName
事件--GetEvent
接口--GetInterface
属性--GetProperty

##### Activator
用于快速实例化对象的类
作用
将Type对象快捷实例化为对象

```
Type t = typeof(Test);
//无参构造
Test testObj = Activator.GreateInstance(t) as Test;

//有参构造
Test testObj = Activator.GreateInstance(t, 100) as Test;
```

##### Assembly
程序集类
主要用来加载其它程序集（dll、exe）

```
//同一文件下的其它程序集
Assembly a = Assembly.Load("程序集名称");

//不在同一文件下的其它程序集
Assembly b = Assembly.LoadFrom("包含程序集清单的文件名称或路径");
Assembly c = Assembly.LoadFile("要加载的文件的完全限定路径");

//使用其它程序集的方法
Type[] types = b.GetTypes();
Type type = b.GetType("文件名.类名");

object obj = Activator.GreateInstance(type, 100);  //实例化
MethodInfo methods = obj.GetMethod("move");   //获取方法
move.Invoke(obj, null);   //调用方法
```

#### 特性
特性是一种允许我们向程序集添加元数据的语言结构
它们用于保存程序结构信息的某种特殊类型的类







### 其他
#### 预处理器指令#
**编译器**
编译器是一种编译程序，用于将源语言程序（C#、C、C++、Java等） 编译为 目标语言程序（二进制数表示的伪机器代码程序）

**预处理器指令**
预处理器指令 指导编译器 在实际编译开始之前对信息进行预处理
预处理指令不是语句，所以不以分号 ";" 结束
目前我们经常用到的 折叠代码块，就是预处理指令

**常见的预处理器指令**

#define
定义一个符号，类似一个没有值的变量
#undef
取消define定义的符号，让其失效

作用：配合 if指令使用 或配合特性（写在脚本文件最前面）
```
#define Unity4
#define Unity5
#undef Unity4

#define IOS
#define Android

using System;
//
```

#if
#else
#elif
#endif

作用：用于告诉编译器进行编译代码的流程控制（与if语句规则一致，一般配合#define定义的字符使用）
```
#if Unity5   //如果发现有Unity5这个符号，那么其中的代码会被编译
    Console.WriteLine("版本为Unity5");
#elif Unity4  && IOS
    Console.WriteLine("版本为Unity4");
#endif   //必须以#endif结束
```

#warning
#error
告诉编译器 是报警告还是报错误
一般配合if使用
```
#if Unity5
    #warning 这个版本不合法
#endif
```





List排序

斜变逆变

迭代器

特殊语法

排序进阶

