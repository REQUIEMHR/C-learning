# C#Learning

## 1. C#程序结构
一个c#程序由以下部分组成：
- 命名空间声明
- 一个类
- 类体
- 主函数

```c#
using System; //引入system命名空间

namespace c.biancheng.net  //namespace 声明一个命名空间
{
    class Program   //class定义一个类
    {
        static void Main(string[] args)
        {
            // 第一个C#程序
            Console.WriteLine("Hello World!");
            Console.ReadKey();
        }
    }
}
```

## 2. C#基本语法

- `using`关键字：引入命名空间。一个程序可以包含多个using语句。
- `class`关键字：定义一个类。
- 成员变量：变量是类的属性，用于存储数据。
- 成员函数：函数是类的行为，用于定义类的功能。
- 实例化一个类：类 ExecuteRectangle 是一个包含 Main() 方法和实例化 Rectangle 类的类。
- 标识符：标识符是用来识别类、变量、函数等的一个字符序列。
- 关键字：关键字是C#编译器预定义的保留字，不能用作标识符。

```C#
using System;
using System.Collections.Generic;
using System.Text;

namespace c.biancheng.net
{
    class Rectangle //基本语法
    {
        // 成员变量
        double length;
        double width;

        // 成员函数
        public void Acceptdetails()
        {
            length = 4.5;
            width = 3.5;
        }

        public double GetArea()
        {
            return length * width;
        }

        public void Display()
        {
            Console.WriteLine("Length:{0}", length);
            Console.WriteLine("Width:{0}", width);
            Console.WriteLine("Area: {0}", GetArea());
        }
    }
    class ExecuteRectangle
    {
        static void Main(string[] args)
        {
            Rectangle r = new Rectangle();
            r.Acceptdetails();
            r.Display();
            Console.ReadLine();
        }
    }
}
```

### 顶级语句
顶级语句是一种新的编程范式，它允许开发者在文件的顶层直接编写语句，而不需要将它们封装在方法或类中。  
顶级语句支持所有常见的 C# 语法，包括声明变量、定义方法、处理异常等。
```C#
using System;
using System.Linq;

// 顶级语句中的变量声明
int number = 42;
string message = "The answer to life, the universe, and everything is";

// 输出变量
Console.WriteLine($"{message} {number}.");

// 定义和调用方法
int Add(int a, int b) => a + b;
Console.WriteLine($"Sum of 1 and 2 is {Add(1, 2)}.");

// 使用 LINQ
var numbers = new[] { 1, 2, 3, 4, 5 };
var evens = numbers.Where(n => n % 2 == 0).ToArray();
Console.WriteLine("Even numbers: " + string.Join(", ", evens));

// 异常处理
try
{
    int zero = 0;
    int result = number / zero;
}
catch (DivideByZeroException ex)
{
    Console.WriteLine("Error: " + ex.Message);
}
```
PS: 
- 文件限制：顶级语句只能在一个源文件中使用。
- 程序入口：如果使用顶级语句，则该文件会隐式地包含 Main 方法，并且该文件将成为程序的入口点。
- 作用域限制：顶级语句中的代码共享一个全局作用域，这意味着可以在顶级语句中定义的变量和方法可以在整个文件中访问。

## C#数据类型
- 值类型
- 引用类型
- 指针类型

### 值类型
值类型直接包含数据。它们存储在栈中。当声明一个值类型变量时，系统会在栈上为该变量分配内存。

| 值类型 | 描述 | 范围 | 默认值 |
| --- | --- | --- | --- |
|bool |布尔值 |true 或 false |false |
|byte |8 位无符号整数 |0 到 255 |0 |
|char |16 位 Unicode 字符 |U+0000 到 U+ffff |'\0' |
|decimal |128 位精确的十进制值，28-29 有效位数 |-7.9 x 10^28 到 7.9 x 10^28 |0.0M |
|double |64 位双精度浮点型 |±5.0 × 10^-324 到 ±1.7 × 10^308 |0.0D |
|float |32 位单精度浮点型 |±1.5 × 10^-45 到 ±3.4 × 10^38 |0.0F |
|int |32 位有符号整数 |-2,147,483,648 到 2,147,483,647 |0 |
|long |64 位有符号整数 |-9,223,372,036,854,775,808 到 9,223,372,036,854,775,807 |0L |
|sbyte |8 位有符号整数 |-128 到 127 |0 |
|short |16 位有符号整数 |-32,768 到 32,767 |0 |
|uint |32 位无符号整数 |0 到 4,294,967,295 |0 |
|ulong |64 位无符号整数 |0 到 18,446,744,073,709,551,615 |0 |
|ushort |16 位无符号整数 |0 到 65,535 |0 |

### 引用类型
引用类型不包含存储在变量中的实际数据，但它们包含对变量的引用。它们存储在堆中。当声明一个引用类型变量时，系统会在栈上为该变量分配内存，并在堆上为实际数据分配内存。
内置的引用类型有：`object`、`dynamic` 和 `string`。

#### object 类型
object 是所有数据类型的基类。它是一个通用的引用数据类型，可以存储任何类型的对象。object 类型可以被赋值为任何类型的值，也可以被转换为任何其他类型。

```c#
object obj = 100; // 将整数赋值给 object 类型的变量
int num = (int)obj; // 将 object 类型的变量转换为整数
```

#### dynamic 类型
dynamic 类型允许在编译时绕过类型检查，从而在运行时确定对象的实际类型。dynamic 类型可以存储任何类型的对象，并且可以在运行时进行类型转换。

```c#
dynamic obj = "Hello, World!"; // 将字符串赋值给 dynamic 类型的变量
int length = obj.Length; // 在运行时确定对象的实际类型，并获取字符串的长度
```

#### string 类型
string 类型表示字符串数据。它允许您给变量分配任何字符串值。字符串（String）类型是 System.String 类的别名。它是从对象（Object）类型派生的。字符串（String）类型的值可以通过两种形式进行分配：引号和 @引号。  
@ 字符串中可以任意换行，换行符及缩进空格都计算在字符串长度之内。  
```c#
string str = "Hello, World!"; // 创建一个字符串
@"runoob.com";
string str = @"C:\Windows"; //C# string 字符串的前面可以加 @（称作"逐字字符串"）将转义字符（\）当作普通字符对待
string str = "C:\\Windows"; //和上一句等价
```
引用类型不包含存储在变量中的实际数据，但它们包含对变量的引用。它们存储在堆中。当声明一个引用类型变量时，系统会在栈上为该变量分配内存，并在堆上为实际数据分配内存。
内置的引用类型有：`object`、`dynamic` 和 `string`。

#### object 类型
object 是所有数据类型的基类。它是一个通用的引用数据类型，可以存储任何类型的对象。object 类型可以被赋值为任何类型的值，也可以被转换为任何其他类型。

```c#
object obj = 100; // 将整数赋值给 object 类型的变量
int num = (int)obj; // 将 object 类型的变量转换为整数
```

#### dynamic 类型
dynamic 类型允许在编译时绕过类型检查，从而在运行时确定对象的实际类型。dynamic 类型可以存储任何类型的对象，并且可以在运行时进行类型转换。

```c#
dynamic obj = "Hello, World!"; // 将字符串赋值给 dynamic 类型的变量
int length = obj.Length; // 在运行时确定对象的实际类型，并获取字符串的长度
```

#### string 类型
string 类型表示字符串数据。它允许您给变量分配任何字符串值。字符串（String）类型是 System.String 类的别名。它是从对象（Object）类型派生的。字符串（String）类型的值可以通过两种形式进行分配：引号和 @引号。  
@ 字符串中可以任意换行，换行符及缩进空格都计算在字符串长度之内。  
```c#
string str = "Hello, World!"; // 创建一个字符串
@"runoob.com";
string str = @"C:\Windows"; //C# string 字符串的前面可以加 @（称作"逐字字符串"）将转义字符（\）当作普通字符对待
string str = "C:\\Windows"; //和上一句等价
```

### 指针类型
指针类型变量存储另一个变量的地址。指针类型变量声明时以*号开头。指针类型必须初始化，并且只能指向与其兼容的类型的变量。


## C#类型转换
类型转换有两种形式：隐式转换和显式转换。  
隐式转换是编译器自动进行的，不需要程序员进行干预。显式转换需要程序员使用强制转换运算符进行转换。

### 隐式转换
隐式转换发生在两种类型兼容的情况下，编译器会自动将一种类型转换为另一种类型。例如，将较小的整数类型转换为较大的整数类型，或将浮点数转换为整数类型。

```c#
int num1 = 10;
double num2 = num1; // 隐式转换：int 转换为 double
```

### 显式转换
显式转换需要程序员使用强制转换运算符进行转换。显式转换发生在两种类型不兼容的情况下，程序员需要手动进行转换。

```c#
double num1 = 10.5;
int num2 = (int)num1; // 显式转换：double 转换为 int
```

### 类型转换方法

#### 使用`convert`类
Convert 类提供了一组静态方法，可以在各种基本数据类型之间进行转换。
```c#
int num1 = 10;
string str = Convert.ToString(num1); // 将整数转换为字符串
double num2 = Convert.ToDouble(str); // 将字符串转换为双精度浮点数
```

#### 使用`parse`方法
Parse 方法用于将字符串转换为指定的数值类型。Parse 方法返回一个指定类型的值，如果字符串无法转换为指定的数值类型，则会引发异常。
```c#
string str = "123";
int num = int.Parse(str); // 将字符串转换为整数
```

#### 使用`try-parse`方法
TryParse 方法用于将字符串转换为指定的数值类型。TryParse 方法返回一个布尔值，表示转换是否成功，并使用 out 参数返回转换后的值。如果字符串无法转换为指定的数值类型，则不会引发异常。
```c#
string str = "123";
int num;
bool success = int.TryParse(str, out num); // 将字符串转换为整数
if (success)
{
    Console.WriteLine("转换成功：" + num);
} else{
    Console.WriteLine("转换失败");
}
```

## C#变量
变量是用于存储和表示数据的标识符，在声明变量时，需要指定变量的类型和名称，并且选择性的分配一个初始值。每个变量都有一个特定的类型，类型决定了变量的内存大小和布局，范围内的值可以存储在内存中，可以对变量进行一系列操作。

|类型|举例|
|---|---|
|整数类型|int, long, short, byte, sbyte, uint, ulong, ushort|
|浮点类型|float, double, decimal|
|布尔类型|bool|
|字符类型|char|
|字符串类型|string|
|对象类型|object|
|动态类型|dynamic|
|空类型|null|

C# 允许定义其他值类型的变量，比如 enum，也允许定义引用类型变量，比如 class。

### 变量的定义
变量定义的语法：
`<data_type> <variable_list>;`

```c#
int i, j, k;            // 声明三个整数变量
double f, g;            // 声明两个双精度浮点数变量
```

### 变量的初始化
初始化一般形式：
`variable_name = value;`
也可以使用以下方式初始化变量：
`<data_type> <variable_name> = value;`

- 接受来自用户的值
```C#
int num;
num = Convert.ToInt32(Console.ReadLine());
```

## C#变量作用域
变量的作用域定义了变量的可见性和生命周期。通常由{ }定义的代码块决定。

- 局部变量：变量的作用域定义了变量的可见性和生命周期。
- 块级作用域：即使用大括号 {} 创建的任何块都可以定义变量的作用域。
- 方法参数作用域：方法的参数也有其自己的作用域，它们在整个方法中都是可见的。
- 全局变量：在类的成员级别定义的变量是成员变量，它们在整个类中可见，如果在命名空间级别定义，那么它们在整个命名空间中可见。
- 静态变量作用域：静态变量是在类级别上声明的，但它们的作用域也受限于其定义的类。
- 循环变量作用域：在 for 循环中声明的循环变量在循环体内可见。

## C#常量
- 整数常量：十进制、八进制、十六进制。
- 浮点常量：整数部分、小数点、小数部分和指数部分组成。 
- 字符常量：字符常量是括在单引号里。
- 字符串常量：字符串常量是括在双引号 "" 里，或者是括在 @"" 里。字符串常量包含的字符与字符常量相似，可以是：普通字符、转义序列和通用字符
- 定义常量：常量是使用 const 关键字来定义的。`const <data_type> <constant_name> = value;`

## C#运算符  
- 算数运算符

|运算符|描述|
|---|---|
|+|加法|
|-|减法|
|*|乘法|
|/|除法|
|%|取模|
|++|自增|
|--|自减|

`c = a++`先赋值后自增
`c = ++a`先自增后赋值

- 赋值运算符  

|运算符|描述|
|---|---|
|=|赋值|
|+=|加等于|
|-=|减等于|
|*=|乘等于|
|/=|除等于|
|%=|取模等于|
|&=|按位与等于|
|&#124;=|按位或等于|
|^=|按位异或等于|
|<<=|左移等于|

- 关系运算符

|运算符|描述|
|---|---|
|==|等于|
|!=|不等于|
|>|大于|
|<|小于|
|>=|大于等于|
|<=|小于等于|  

- 逻辑运算符

|运算符|描述|
|---|---|
|&&|逻辑与|
|||逻辑或|
|!|逻辑非|

- 位运算符

|运算符|描述|
|---|---|
|&|按位与|
|&#124;|按位或|
|^|按位异或|
|~|按位取反|
|<<|左移|
|>>|右移|

- 其他运算符

|运算符|描述|
|---|---|
|sizeof|返回数据类型的大小|
|typeof|返回 class 的类型|
|&|返回变量的地址|
|*|变量的指针|
|is|判断对象是否为某一类型|
|as|强制转换，即使转换失败也不会抛出异常|

## C#判断  

判断语句：

|语句|描述|
|---|---|
|if 语句|条件判断|
|if else语句|条件判断|
|嵌套 if 语句|嵌套条件判断|
|switch 语句|多条件判断|
|嵌套 switch 语句|嵌套多条件判断|
| C# NULL 条件运算符|条件判断|

条件运算符`?`，可用来代替`if…else`：`Exp1 ? Exp2 : Exp3;`  如果 Exp1 为真，则返回 Exp2，否则返回 Exp3。

## C#循环

循环语句：

|语句|描述|
|---|---|
|while 语句|当条件为真时，重复执行循环体|
|for 语句|重复执行循环体，直到满足条件|
|do...while 语句|重复执行循环体，直到满足条件|
|foreach 语句|遍历集合中的每个元素|
|break 语句|跳出循环|
|continue 语句|跳过当前循环，继续下一次循环|

- 无限循环
如果条件永远不为假，则循环将变成无限循环。for 循环在传统意义上可用于实现无限循环。由于构成循环的三个表达式中任何一个都不是必需的，您可以将某些条件表达式留空来构成一个无限循环。
当条件表达式不存在时，它被假设为真。您也可以设置一个初始值和增量表达式，但是一般情况下，程序员偏向于使用 for(;;) 结构来表示一个无限循环。

## C#封装
*封装*：把一个或多个项目封闭在一个物理或逻辑的包中。
抽象和封装是面向对象程序设计的相关特性。抽象允许相关信息可视化，封装则使开发者实现所需级别的抽象。
C# 封装根据具体的需要，设置使用者的访问权限，并通过*访问修饰符*来实现。

访问修饰符：
- public：所有对象都可以访问；
- private：对象本身在对象内部可以访问；
- protected：只有该类对象及其子类对象可以访问；常见于继承。
- internal：同一个程序集的对象可以访问；允许一个类将其成员变量和成员函数暴露给当前程序中的其他函数和对象。换句话说，带有`internal`访问修饰符的任何成员可以被定义在该成员所定义的应用程序内的任何类或方法访问。
- protected internal：访问限于当前程序集或派生自包含类的类。

## C#方法  
一个方法是把一些相关的语句组织在一起，用来执行一个任务语句块。

### C#方法定义

```c#
<Access Specifier> <Return Type> <Method Name>(Parameter List)
{
   // Method Body
}
```

- 访问修饰符<Access Specifier>：定义了访问类中成员的方式。C# 支持以下访问修饰符（访问修饰符的表）：public、private、protected、internal 和 protected internal。
- 返回类型<Return Type>：一个方法可以返回一个值。返回类型是方法返回的值的数据类型。如果方法不返回任何值，则返回类型为 void。
- 方法名称<Method Name>：是方法的标识符。方法名称和参数列表一起构成了方法签名。
- 参数列表<Parameter List>：参数列表是指方法的参数类型、顺序和数量。参数是可选的，也就是说，一个方法可能不包含参数。参数列表是指方法的参数类型、顺序和数量。参数是可选的，也就是说，一个方法可能不包含参数。
- 方法主体<Method Body>：包含了完成任务所需的指令集。

### C#调用

- 方法调用
两种方式：
使用方法名调用方法。
使用类的实例从另一个类中调用其他类的公有方法。

- 递归调用
一个方法可以自我调用。

### C#参数传递

|方式|描述|
|---|---|
|值参数|值参数在方法被调用时，将实参的值复制给形参，实参和形参使用的是两个不同内存中的值。在这种情况下，当形参的值发生改变时，不会影响实参的值。|
|引用参数|引用参数允许一个方法修改其参数的值，当方法被调用时，将实参的引用（地址）复制给形参。在这种情况下，当形参的值发生改变时，实参的值也会相应地改变。|
|输出参数|输出参数允许方法返回多个值。|

值参数：
```c#
public class NumberManipulator
{
    public void squareNum(int i)
    {
        i *= i;
        Console.WriteLine("方法内部值: {0}", i);
    }
}
```

引用参数：
```c#
public class NumberManipulator
{
    public void squareNum(ref int i)
    {
        i *= i;
        Console.WriteLine("方法内部值: {0}", i);
    }
}
```

输出参数：可以从函数中返回两个值。当需要从一个参数没有指定初始值的方法中返回值时，输出参数特别有用。
```c#
public class NumberManipulator
{
    public void squareNum(out int i)
    {
        i = 10;
        i *= i;
        Console.WriteLine("方法内部值: {0}", i);
    }
}
```

## C#可空类型（Nullable）

可空类型就是允许值类型（如 int、bool、DateTime）可以有一个没有值的状态（即 null）。
可空类型可以表示其基础值类型的正常范围内的值，再加上一个 null 值。
可空类型声明：
`<data_type>? <variable_name> = null;`

?：可空类型标识符，让值类型可以为NULL
??：空合并运算符，当变量为NULL时提供默认值

*NUll合并运算符(??)*:
空合并运算符（??）用于为 可空类型 或 引用类型 定义一个默认值。
当左侧的值为 null 时，?? 返回右侧的默认值。
基本语法：
`<value> ?? <default_value>`
如果 value 为 null，则该表达式返回 default_value，否则返回 value。

可空类型的常用属性和方法：  

|成员|说明|示例|
|---|---|---|
|.HasValue|判断变量是否有值。如果值为 null，则为 false，否则为 true。|`int? a = null; Console.WriteLine(a.HasValue);`|
|.Value|获取实际值。如果 HasValue 为 true，则返回 Value 属性的值，否则为 null。|`int? a = 10; Console.WriteLine(a.Value);`|
|.GetValueOrDefault()|获取值或默认值（默认 0）|`int? a = 10; Console.WriteLine(a.GetValueOrDefault());`|

实际应用场景：在处理数据库或外部数据时，可空类型尤其常用

## C#数组

数组是一个存储相同类型元素的固定大小的顺序集合。数组是用来存储数据的集合，通常认为数组是一个同一类型变量的集合。

声明数组：
`datatype[] arrayName;`

创建数组：
`arrayName = new datatype[arraySize];`

初始化数组：
`datatype[] arrayName = new datatype[] {value0, value1, ..., valueN};`
或
`datatype[] arrayName = {value0, value1, ..., valueN};`

访问数组元素：
`datetype value = arrayName[index];`

### 使用foreach循环

我们可以使用for循环来访问每个数组元素，也可以使用foreach语句来遍历数组。
foreach 语句用于遍历数组中的每个元素，不需要通过索引来访问数组元素。

```C#
using System;

namespace ArrayApplication
{
   class MyArray
   {
      static void Main(string[] args)
      {
         int []  n = new int[10]; /* n 是一个带有 10 个整数的数组 */


         /* 初始化数组 n 中的元素 */         
         for ( int i = 0; i < 10; i++ )
         {
            n[i] = i + 100;
         }

         /* 输出每个数组元素的值 */
         foreach (int j in n )
         {
            int i = j-100;
            Console.WriteLine("Element[{0}] = {1}", i, j);
         }
         Console.ReadKey();
      }
   }
}
```

### 数组细节

|概念|描述|
|---|---|
|多维数组|多维数组最简单的形式是二维数组。一个二维数组，在本质上，是一个一维数组的列表。|
|交错数组|交错数组是数组的数组。交错数组是一维数组。|
|传递数组给函数|C# 允许您将一个数组作为参数传递给函数。|
|参数数组|C# 提供了一种特殊类型的参数，叫做参数数组。参数数组使用数组来传递可变数量的参数。|
|Array类|C# 数组类是 System.Array 类的派生类。Array 类提供了各种用于数组的属性和方法。|


## C#字符串
字符串是用于存储一系列字符的。字符串的声明方式与其他基本数据类型相似，但是字符串被封装在 `System.String` 类中。

创建string对象：
- 通过给string变量指定一个字符串
- 通过使用string类构造函数
- 通过使用字符串串联运算符（+）
- 通过检索属性或调用一个返回字符串的方法
- 通过格式化方法来转换一个值或对象为它的字符串表示形式

```C#
using System;

namespace StringApplication
{
    class Program
    {
        static void Main(string[] args)
        {
           //字符串，字符串连接
            string fname, lname;
            fname = "Rowan";
            lname = "Atkinson";

            string fullname = fname + lname;
            Console.WriteLine("Full Name: {0}", fullname);

            //通过使用 string 构造函数
            char[] letters = { 'H', 'e', 'l', 'l','o' };
            string greetings = new string(letters);
            Console.WriteLine("Greetings: {0}", greetings);

            //方法返回字符串
            string[] sarray = { "Hello", "From", "Tutorials", "Point" };
            string message = String.Join(" ", sarray);
            Console.WriteLine("Message: {0}", message);

            //用于转化值的格式化方法
            DateTime waiting = new DateTime(2012, 10, 10, 17, 58, 1);
            string chat = String.Format("Message sent at {0:t} on {0:D}", 
            waiting);
            Console.WriteLine("Message: {0}", chat);
            Console.ReadKey() ;
        }
    }
}
```

### string类的属性

|属性|描述|
|---|---|
|Chars|获取此字符串的 Unicode 字符数组。|
|Length|获取当前 String 对象中的字符数，不包含末尾的空字符。|
|IsNullOrEmpty|指示指定的字符串是否为 null 或者是否为一个空的字符串。|

### string类的方法

|方法|描述|
|---|---|
|public static int Compare( string strA, string strB, bool ignoreCase )|比较两个指定的 string 对象，并返回一个表示它们在排列顺序中相对位置的整数。但是，如果布尔参数为真时，该方法不区分大小写。|
|public static string Concat( string str0, string str1 )|连接两个 string 对象。|
|public bool Contains( string value )|返回一个表示指定 string 对象是否出现在字符串中的值。|
|public static string Copy( string str )|创建一个与指定字符串具有相同值的新的 String 对象。|
|public void CopyTo( int sourceIndex, char[] destination, int destinationIndex, int count )|从 string 对象的指定位置开始复制指定数量的字符到 Unicode 字符数组中的指定位置。|
|public bool EndsWith( string value )|判断字符串实例是否以指定的字符串结尾。|
|public bool Equals( string value )|判断当前的 string 对象是否与指定的 string 对象具有相同的值。|
|public static string Format( string format, Object arg0 )|把指定字符串中一个或多个格式项替换为指定对象的字符串表示形式。|
|public int IndexOf( char value )|返回指定 Unicode 字符在当前字符串中第一次出现的索引，索引从 0 开始。|
|public int IndexOf( string value )|返回指定字符串在当前字符串中第一次出现的索引，索引从 0 开始。|
|public int IndexOf( char value, int startIndex )|返回指定 Unicode 字符从该字符串中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。|
|public int IndexOf( string value, int startIndex )|返回指定字符串从该字符串中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。|
|public int IndexOfAny( char[] anyOf )|返回某一个指定的 Unicode 字符数组中任意字符在当前字符串中第一次出现的索引，索引从 0 开始。|
|public int IndexOfAny( char[] anyOf, int startIndex )|返回某一个指定的 Unicode 字符数组中任意字符在当前字符串中从指定字符位置开始搜索第一次出现的索引，索引从 0 开始。|
|public static string Join( string separator, string[] value )|连接一个字符串数组中的所有元素，使用指定的分隔符分隔每个元素。|
|public static string Join( string separator, string[] value, int startIndex, int count )|连接一个字符串数组中的指定位置开始的指定元素，使用指定的分隔符分隔每个元素。|
|public int LastIndexOf( char value )|返回指定 Unicode 字符在当前字符串中最后一次出现的索引位置，索引从 0 开始。|
|public int LastIndexOf( string value )|返回指定字符串在当前字符串中最后一次出现的索引位置，索引从 0 开始。|
|public string Remove( int startIndex, int count )|移除当前实例中的子字符串。|
|public string Remove( int startIndex, int count )|移除当前实例中的子字符串。|
|public string Replace( char oldChar, char newChar )|把当前字符串中，所有指定的 Unicode 字符替换为新指定的 Unicode 字符，并返回替换后的字符串。|
|public string Replace( string oldValue, string newValue )|把当前字符串中，所有指定的字符串替换为新指定的字符串，并返回替换后的字符串。|
|public string[] Split( params char[] separator )|返回一个字符串数组，包含当前的 string 对象中的子字符串，子字符串是使用指定的 Unicode 字符数组中的元素进行分隔的。|
|public string[] Split( char[] separator, int count )|返回一个字符串数组，包含当前的 string 对象中的子字符串，子字符串是使用指定的 Unicode 字符数组中的元素进行分隔的。|
|public bool StartsWith( string value )|判断字符串实例是否以指定的字符串开始。|
|public char[] ToCharArray()|返回一个带有当前 string 对象中所有字符的 Unicode 字符数组。|
|public char[] ToCharArray( int startIndex, int length )|返回一个带有当前 string 对象中所有字符的 Unicode 字符数组，从指定的索引开始，直到指定的长度为止。|
|public string ToLower()|把字符串转换为小写并返回。|
|public string ToUpper()|把字符串转换为大写并返回。|
|public string Trim()|移除当前 String 对象中的所有前导空白字符和后置空白字符。|

## C# 结构体

结构体是一种值类型，用于组织和存储相关数据，这样使得一个单一变量可以存储各种数据类型的相关数据。

### 定义结构体

为了定义一个结构体，您必须使用`struct`语句。
`struct`语句为程序定义了一个带有多个成员的新的数据类型。

```C#
struct Books
{
   public string title;
   public string author;
   public string subject;
   public int book_id;
};  
```

### C#结构体特点

- 结构可带有方法、字段、索引、属性、运算符方法和事件，适用于表示轻量级数据的情况，如坐标、范围、日期、时间等。
- 与类不同，结构不能继承其他的结构或类。
- 结构不能作为其他结构或类的基础结构。
- 结构可实现一个或多个接口。
- 结构成员不能指定为 abstract、virtual 或 protected。
- 当您使用 New 操作符创建一个结构对象时，会调用适当的构造函数来创建结构。与类不同，结构可以不使用 New 操作符即可被实例化。
- 如果不使用 New 操作符，只有在所有的字段都被初始化之后，字段才被赋值，对象才被使用。
- 结构变量通常分配在栈上，这使得它们的创建和销毁速度更快。但是，如果将结构用作类的字段，且这个类是引用类型，那么结构将存储在堆上。
- 结构默认情况下是可变的，这意味着你可以修改它们的字段。但是，如果结构定义为只读，那么它的字段将是不可变的。

### 结构体VS类

类和结构在设计和使用时有不同的考虑因素，类适合表示复杂的对象和行为，支持继承和多态性，而结构则更适合表示轻量级数据和值类型，以提高性能并避免引用的管理开销。
不同点：
*值类型 VS 引用类型*
- *结构是值类型*：结构是值类型，它们在栈上分配内存，而不是在堆上。当将结构实例传递给方法或赋值给另一个变量时，将复制整个结构的内容。
- *类是引用类型*：类是引用类型，它们在堆上分配内存。当将类实例传递给方法或赋值给另一个变量时，实际上是传递引用（内存地址）而不是整个对象的副本。

*继承和多态性*
- *结构不能继承*：结构不能继承其他结构或类。它们不能作为其他结构或类的基类。
- *类可以继承*：支持继承和多态性。可以派生新类来扩展现有类的功能。

*赋值行为*
- 类型为类的变量在赋值时存储的引用，因此两个变量指向同一个对象。
- 结构变量在赋值时会复制整个结构，因此每个变量都有自己独立的副本。
  
*传递方式*
- 类型为类的对象在方法调用时通过引用传递，这意味着在方法中对对象所做的更改会影响到原始对象。
- 结构对象通常通过值传递，这意味着传递的是结构的副本，而不是原始结构对象本身。因此，在方法中对结构所做的更改不会影响到原始对象。

*可空性*
- 结构体是值类型，不能直接设置为NULL：因为null是引用类型的默认值，而不是类型的默认值。如果你需要表示结构体变量的缺失或无效状态，可以使用 Nullable<T> 或称为 T? 的可空类型。
- 类默认可为NULL

*性能和内存分配*
- 结构通常更轻量：由于结构是值类型且在栈上分配内存，它们通常比类更轻量，适用简单数据表示。
- 类可能有更多开销：由于类是引用类型，可能涉及更多的内存开销和管理。

## 枚举
枚举是一组命名整型常量。枚举类型是使用`enum`关键字声明的。C#枚举是值类型，枚举包含自己的值，且不能继承或传递继承。

- 声明enum类型：
```C#
enum <enum_name>
{ 
    enumeration list 
};

//举例
enum Days { Sun, Mon, tue, Wed, thu, Fri, Sat };
```

## C#类

定义一个类时，相当于定义了一个数据类型的蓝图。这并没有定义任何数据，但它定义了类的名称意味着什么，也就是说，类的对象由什么组成以及在这个对象上可执行什么操作。

### 类的定义：
以关键字`class`开头，后跟类的名称。类的主体被大括号括起来。类的字段、属性、方法和事件都在类的主体内定义。

```C#
<access specifier> class  class_name 
{
    // member variables
    <access specifier> <data type> variableN;
    // member methods
    <access specifier> <return type> methodN(parameter_list) 
    {
        // method body 
    }
}
```

- 访问标识符 <access specifier> 指定了对类及其成员的访问规则。如果没有指定，则使用默认的访问标识符。类的默认访问标识符是 internal，成员的默认访问标识符是 private。
- 数据类型 <data type> 指定了变量的类型，返回类型 <return type> 指定了返回的方法返回的数据类型。
- 如果要访问类的成员，你要使用点（.）运算符。

### 成员函数和封装

类的成员函数是一个在类定义中有它的定义或原型的函数，就像其他变量一样。作为类的一个成员，它能在类的任何对象上操作，且能访问该对象的类的所有成员。

成员变量是对象的属性（从设计角度），且它们保持私有来实现封装。这些变量只能使用公共成员函数来访问。

### 类的构造函数

类的*构造函数*是类的一个特殊的成员函数，当创建类的新对象时执行。

构造函数的名称与类的名称完全相同，它没有任何返回类型。

*默认构造函数*没有任何参数。如果需要一个带参数的构造函数可以有参数，这种构造函数叫做*参数化结构函数*。这个可以在创建对象的同时给对象赋初始值。

*析构函数* 是类的一个特殊的成员函数，当类的对象超出范围时执行。析构函数的名称是在类的名称前加上一个波浪形（~）作为前缀，它不返回值，也不带任何参数。析构函数不能继承或重载。

### C#类静态成员

我们可以使用`static`关键字在类中创建静态成员。当我们声明一个成员为静态时，意味着无论创建多少对象，该成员只有一个副本（只有一个该成员的实例）。静态变量用于定义常量，因为它们的值可以通过直接调用类而不需要创建类的实例来获取。静态变量可在成员函数或类的定义外部进行初始化，也可以在类的定义内部初始化静态变量。


## C#继承

继承允许我们根据一个类来定义另一个类，这使得创建和维护应用程序变得更容易，同时也有利于重用代码和节省开发时间。
当创建一个类时，不需要完全重新编写新的数据成员和成员函数，只需要设计一个新的类，继承了已有的类的成员即可。
这个已有的类被称为的**基类**，这个新的类被称为**派生类**。

### 基类和派生类

派生类继承基类的成员变量和成员函数。派生类也可以添加它自己的成员变量和成员函数。

一个类可以继承自另一个类，被称为基类（父类）和派生类（子类）。

C# 不支持类的多重继承，但支持接口的多重继承，一个类可以实现多个接口。

一个类可以继承多个接口，但只能继承自一个类。

```C#
<访问修饰符> class <基类>
{
 ...
}
class <派生类> : <基类>
{
 ...
}

class BaseClass
{
    public void SomeMethod()
    {
        // Method implementation
    }
}

class DerivedClass : BaseClass
{
    public void AnotherMethod()
    {
        // Accessing base class method
        base.SomeMethod();
        
        // Method implementation
    }
}
```