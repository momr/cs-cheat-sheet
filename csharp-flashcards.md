# C# Flash Cards

## Basic Syntax

What is the basic structure of a C# program?
?
```csharp
using System;

namespace MyNamespace
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello, World!");
        }
    }
}
```

---

How do you write a single-line comment in C#?
?
```csharp
// This is a single-line comment
```

---

How do you write a multi-line comment in C#?
?
```csharp
/* This is a
   multi-line comment */
```

## Data Types

What are the main value types in C#?
?
- bool
- byte, sbyte
- char
- decimal
- double
- float
- int, uint
- long, ulong
- short, ushort

---

What are the main reference types in C#?
?
- string
- object
- dynamic

---

How do you declare a nullable type in C#?
?
```csharp
int? nullableNumber = null;
```

## Variables and Constants

How do you declare and initialize a variable in C#?
?
```csharp
int number = 10;
string name = "John";
```

---

How do you declare a constant in C#?
?
```csharp
const double PI = 3.14159;
```

---

How do you use type inference in C#?
?
```csharp
var age = 25;
```

## Operators

What are the arithmetic operators in C#?
?
+, -, *, /, %

---

What are the comparison operators in C#?
?
==, !=, <, >, <=, >=

---

What are the logical operators in C#?
?
&&, ||, !

---

What is the null-coalescing operator in C#?
?
??

---

What is the null-conditional operator in C#?
?
?.

## Control Structures

How do you write an if-else statement in C#?
?
```csharp
if (condition)
{
    // code
}
else if (anotherCondition)
{
    // code
}
else
{
    // code
}
```

---

How do you write a switch statement in C#?
?
```csharp
switch (variable)
{
    case value1:
        // code
        break;
    case value2:
        // code
        break;
    default:
        // code
        break;
}
```

---

How do you write a for loop in C#?
?
```csharp
for (int i = 0; i < 10; i++)
{
    // code
}
```

---

How do you write a foreach loop in C#?
?
```csharp
foreach (var item in collection)
{
    // code
}
```

## Methods

How do you declare a method with optional parameters in C#?
?
```csharp
public static void Greet(string name, string greeting = "Hello")
{
    Console.WriteLine($"{greeting}, {name}!");
}
```

---

How do you declare a method with out parameters in C#?
?
```csharp
public static bool TryParse(string input, out int result)
{
    return int.TryParse(input, out result);
}
```

---

How do you write an expression-bodied method in C#?
?
```csharp
public static int Multiply(int a, int b) => a * b;
```

## Arrays and Collections

How do you declare and initialize an array in C#?
?
```csharp
int[] numbers = new int[5];
string[] names = { "John", "Jane", "Alice" };
```

---

How do you declare and initialize a List in C#?
?
```csharp
List<string> fruits = new List<string> { "Apple", "Banana", "Orange" };
```

---

How do you declare and initialize a Dictionary in C#?
?
```csharp
Dictionary<string, int> ages = new Dictionary<string, int>
{
    { "John", 25 },
    { "Jane", 30 }
};
```

## Classes and Objects

How do you declare a class with properties in C#?
?
```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```

---

How do you create an object from a class in C#?
?
```csharp
Person person = new Person();
// or
var person = new Person();
```

---

How do you write a constructor in C#?
?
```csharp
public class Person
{
    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
}
```

## Inheritance and Polymorphism

How do you declare a class that inherits from another class in C#?
?
```csharp
public class Dog : Animal
{
    // Dog-specific members
}
```

---

How do you override a method in a derived class in C#?
?
```csharp
public override void MakeSound()
{
    Console.WriteLine("The dog barks");
}
```

## Interfaces

How do you declare an interface in C#?
?
```csharp
public interface IShape
{
    double CalculateArea();
}
```

---

How do you implement an interface in a class in C#?
?
```csharp
public class Circle : IShape
{
    public double Radius { get; set; }

    public double CalculateArea()
    {
        return Math.PI * Radius * Radius;
    }
}
```

## Lambda Expressions

How do you write a lambda expression with no parameters in C#?
?
```csharp
Action sayHello = () => Console.WriteLine("Hello!");
```

---

How do you write a lambda expression with parameters in C#?
?
```csharp
Func<int, int, int> add = (x, y) => x + y;
```

## LINQ

How do you write a LINQ query using query syntax in C#?
?
```csharp
var query = from num in numbers
            where num % 2 == 0
            orderby num
            select num;
```

---

How do you write a LINQ query using method syntax in C#?
?
```csharp
var result = numbers.Where(n => n % 2 == 0)
                    .OrderBy(n => n)
                    .Select(n => n);
```

## Asynchronous Programming

How do you declare an asynchronous method in C#?
?
```csharp
public async Task<string> FetchDataAsync()
{
    // Asynchronous code
}
```

---

How do you await an asynchronous operation in C#?
?
```csharp
string data = await FetchDataAsync();
```

## Exception Handling

How do you write a try-catch block in C#?
?
```csharp
try
{
    // Code that may throw an exception
}
catch (Exception ex)
{
    // Handle the exception
}
finally
{
    // Code that always executes
}
```

---

How do you throw an exception in C#?
?
```csharp
throw new ArgumentException("Invalid argument", nameof(parameter));
```

