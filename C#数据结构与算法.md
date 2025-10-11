### 数据结构
数据结构是一种具有一定**逻辑关系**，在计算机中应用某种**存储结构**，并且封装了相应操作的**数据元素集合**。它包含三方面的内容，**逻辑关系**、**存储关系**及**操作**。  
数据结构研究的内容：就是如何按一定的逻辑结构，把数据组织起来，并选择适当的存储表示方法把逻辑结构组织好的数据存储到计算机的存储器里。  
**常见的数据结构**  
栈（Stack）：栈是一种特殊的线性表，它只能在一个表的一个固定端进行数据结点的插入和删除操作。  
队列（Queue）：队列和栈类似，也是一种特殊的线性表。和栈不同的是，队列只允许在表的一端进行插入操作，而在另一端进行删除操作。  
数组（Array）：数组是一种聚合数据类型，它是将具有相同类型的若干变量有序地组织在一起的集合。  
链表（Linked List）：链表是一种数据元素按照链式存储结构进行存储的数据结构，这种存储结构具有在物理上存在非连续的特点。  
树（Tree）：树是典型的非线性结构，它是包括，2 个结点的有穷集合 K。  
图（Graph）：图是另一种非线性数据结构。在图结构中，数据结点一般称为顶点，而边是顶点的有序偶对。  
堆（Heap）：堆是一种特殊的树形数据结构，一般讨论的堆都是二叉堆。  
散列表（Hash table）：散列表源自于散列函数(Hash function)，其思想是如果在结构中存在关键字和T相等的记录，那么必定在F(T)的存储位置可以找到该记录，这样就可以不用进行比较操作而直接取得所查记录。  

#### 线性表
**List<T>常用方法**

```
using System.Collections.Generic;

List<string> strList = new List<string>();
strList.Add("123");
strList.Add("456");
strList.Add("789");
Console.WriteLine(strList.Count);    //3
Console.WriteLine(strList[1]);   //"456"
strList.IndexOf("456");   //获取元素索引
strList.Insert("n789", 1);    //插入元素
strList.Remove("789");   //移除元素
strList.RemoveAt(2);   //索引移除元素
strList.Contains("789");   //是否包含元素 false
strList.Sort();   //排序
strList.Clear();   //清空元素
```

**线性表接口定义**
```
interface IListDS<T>
{
    int GetLength();
    void Clear();
    bool IsEmpty();
    void Add(T item);
    void Insert(T item, int index);
    T Delete(int index);
    T this[int index] {get;}
    T GetEle(int index);
    int Locate(T value);
}
```
#### 顺序表SeqList
顺序表是用地址连续的存储单元顺序存储线性表中的各个数据元素
优点：查找任何位置上的数据元素都非常方便
缺点：插入和删除时，需要通过移动数据元素来实现，影响运行效率
```
class SeqList<T> : IListDS<T>
{
    private T[] data;   //用来存储数据
    private int count = 0;   //表示存储了多少数据
    
    public SeqList(int size)   //size就是最大容量，该实现未提供最大[扩容方案]
    {
        data = new T[size];
    }
    public SeqList():this(10)   //默认构造函数 容量为10
    {
    
    }
    
    public int GetLength()
    {
        return count;
    }
    
    public void Clear()   //这里将count赋值为0，就无法取出数据，相当于清空；重新添加也会从0开始赋值、取出
    {
        count = 0;
    }
    
    public bool IsEmpty()
    {
        return count == 0;
    }
    
    public void Add(T item)
    {
        if ( count == data.Length)   //当前数组已经存满
        {
            ConsoleWriteLine("当前顺序表已存满，不允许再存入");
        }
        else
        {
            data[count] = item;
            count++;
        }
    }
    
    public void Insert(T item, int index)
    {
        if ( count == data.Length)   //当前数组已经存满
            {
                ConsoleWriteLine("当前顺序表已存满，不允许再存入");
            }
        else
        {
            for (int i = count - 1; i >= index; i--)   //从前往后遍历数据会被覆盖，需要从后往前遍历
            {
                data[i + 1] = data[i]
            }
            data[index] = item;
            count++;
        }
    }
    
    public T Delete(int index)
    {
        for (int i = index + 1; i < count; i++)
        {
            data[i - 1] = data[i]
        }
        count--;
        return data[index];
    }
    
    public T this[int index]
    {
        get { return GetEle(index); }
    }
    
    public T GetEle(int index)
    {
        if( index >= 0 && index <= count - 1)
        {
            return data[index];
        }
        else
        {
            ConsoleWriteLine("索引不存在");
            return default(T);   //返回默认值
        }
    }
    
    public int Locate(T value)   //获取索引
    {
        for (int i = 0; i < count; i++)
        {
            if (data[i].Equals(value) )
            {
                return i;
            }
        }
        return -1;   //不存在返回-1
    }
}
```


#### 链表 Linked Storage
链表是一组任意的存储单元来存储线性表中的数据元素（不要求逻辑上相邻的数据元素在物理存储位置是也相邻）
优点：进行插入和删除时不需要移动数据元素
缺点：失去了顺序表可以随机存取数据元素的优点

##### 单链表 Singly Linked List
node（data、next）

**单链表节点定义**
```
class Node<T>
{
    private T data;   //存储数据
    private Node<T> next;   //指针用来指向下一个元素
    
    public Node()   //无参构造函数，返回默认值
    {
        data = default(T);
        next = null;
    }
    public Node(T value)
    {
        data = value;
        next = null;
    }
    public Node(Node<T> next)
    {
        this.next = next;
    }
    public Node(T value, Node<T> next)
    {
        data = value;
        this.next = next;
    }
    
    public T Data
    {
        get { return data; }
        set { data = value; }
    }
    public Node<T> Next
    {
        get { return next; }
        set { next = value; }
    }
}
```

**单链表实现**
```
class LinkList<T> : IListDS<T>
{
    private Node<T> head;   //存储一个头节点
    
    public  LinkList()
    {
      head = null;
    }

    public int GetLength()
    {
        if(head == null) return 0;
        Node<T> temp = head;
        int count = 1;
        while(true)
        {
            if (temp.Next != null)
            {
            count++;
            temp = temp.Next;
            }
            else break;
        }
        return count;
    }
    
    public void Clear()
    {
        head = null;
    }
    
    public bool IsEmpty()
    {
        return head == null;
    }
    
    public void Add(T item)
    {
        Node<T> newNode = new Node<T>(item);   //创建新节点
        if ( head == null)   //头节点为空，那么新节点就是头节点
        {
            head = newNode;
        }
        else   //将新节点放到链表的尾部
        {
            Node<T> temp = head;
            while (true)
            {
                if(temp.Next != null)
                {
                    temp = temp.Next;
                }
                else
                {
                    break;
                }
            }
            temp.Next = newNode;
        }
    }
    
    public void Insert(T item, int index)
    {
        Node<T> newNode = new Node<T>(item);
        if ( index == 0)   //插入到头节点
        {
            newNode.Next = head;
            head = newNode;
        }
        else
        {
            Node<T> temp = head;
            for (int i = 0; i < index; i++)
            {
                temp = temp.Next;
            }
            newNode.Next = temp.Next;
            temp.Next = newNode;
        }
    }
    
    public T Delete(int index)
    {
        T data = default(T);
        if ( index == 0)   //删除头节点
        {
            data = head.Data;
            head = head.Next;
        }
        else
        {
            Node<T> temp = head;
            for (int i = 0; i < index; i++)
            {
                temp = temp.Next;
            }
            data = temp.Next.Data;
            temp.Next = temp.Next.Next;
        }
        return data;
    }
    
    public T this[int index]
    {
        get
        {
            Node<T> temp = head;
            for (int i = 0; i <= index; i++)
            {
                temp = temp.Next;
            }
            return temp.Data
        }
    }
    
    public T GetEle(int index)
    {
        return this[index];
    }
    
    public int Locate(T value)   //获取索引
    {
        Node<T> temp = head;
        if(temp == null) return -1;   //不存在返回-1
        else
        {
            int index = 0
            while(true)
            {
                if (temp.Data.Equals(value)) return index;
                else
                {
                    if(temp.Next != null) temp = temp.Next;
                    else break;
                }
            }
        }
        return -1;
    }
}
```


**双链表**




#### 栈



#### 队列



#### 数组



### 算法
算法可以理解为有基本运算及规定的运算顺序所构成的完整解题步骤。  
算法研究的目的是为了更有效的处理数据，提高数据运算效率。数据的运算是定义在数据的逻辑结构上，但运算的具体实现要在存储结构上进行。一般有以下几种常用运算：  

**算法的评价标准**  
运行时间、占用空间
其他：正确性、可读性、健壮性（特殊情况的处理，不易报错）

**常见算法**  
检索：检索就是在数据结构里查找满足一定条件的节点。一般是给定一个某字段的值，找具有该字段值的节点。  
插入：往数据结构中增加新的节点。  
删除：把指定的结点从数据结构中去掉。  
更新：改变指定节点的一个或多个字段的值。  
排序：把节点按某种指定的顺序重新排列。例如递增或递减。  
#### 插入排序



#### 选择排序



#### 快速排序


