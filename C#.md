# C#Learning

## 1. C#程序结构
一个c#程序由以下部分组成：
- 命名空间声明
- 一个类
- 类体
- 主函数

```csharp
using System;
namespace HelloWorldApplication
{
    class HelloWorld
    {
        static void Main(string[] args)
        {
            /* 我的第一个 C# 程序 */
            Console.WriteLine("Hello World!");
            Console.ReadKey();
        }
    }
}
```