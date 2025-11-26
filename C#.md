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
引用类型不包含数据，而是包含对数据的引用。它们存储在堆中。当声明一个引用类型变量时，系统会在栈上为该变量分配内存，并在堆上为实际数据分配内存。

### 指针类型
指针类型变量存储另一个变量的地址。指针类型变量声明时以*号开头。指针类型必须初始化，并且只能指向与其兼容的类型的变量。

