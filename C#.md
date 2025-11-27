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

