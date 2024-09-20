# C# Cheat Sheet

## Table of Contents
- [C# Cheat Sheet](#c-cheat-sheet)
  - [Table of Contents](#table-of-contents)
  - [Basic Syntax](#basic-syntax)
  - [Data Types](#data-types)
  - [Variables and Constants](#variables-and-constants)
  - [Operators](#operators)
  - [Control Structures](#control-structures)
  - [Methods](#methods)
  - [Arrays and Collections](#arrays-and-collections)
  - [Classes and Objects](#classes-and-objects)
  - [Inheritance and Polymorphism](#inheritance-and-polymorphism)
  - [Interfaces and Abstract Classes](#interfaces-and-abstract-classes)
  - [Properties and Indexers](#properties-and-indexers)
  - [Delegates and Events](#delegates-and-events)
  - [Lambda Expressions](#lambda-expressions)
  - [LINQ](#linq)
  - [Asynchronous Programming](#asynchronous-programming)
  - [Exception Handling](#exception-handling)
  - [File I/O](#file-io)
  - [Generics](#generics)
  - [Attributes](#attributes)
  - [Reflection](#reflection)
  - [Nullable Types](#nullable-types)
  - [Tuples](#tuples)
  - [Pattern Matching](#pattern-matching)
  - [Records](#records)
  - [Span and Memory](#span-and-memory)
  - [Ranges and Indices](#ranges-and-indices)
  - [Switch Expressions](#switch-expressions)
  - [Default Interface Methods](#default-interface-methods)
  - [Init-only Setters](#init-only-setters)
  - [Top-level Statements](#top-level-statements)
  - [Global Using Directives](#global-using-directives)
  - [File-scoped Namespaces](#file-scoped-namespaces)
  - [Required Members](#required-members)
  - [Static Abstract Members in Interfaces](#static-abstract-members-in-interfaces)
  - [Extended Property Patterns](#extended-property-patterns)
  - [List Patterns](#list-patterns)
  - [Raw String Literals](#raw-string-literals)

## Basic Syntax

```csharp
// Single-line comment
/* Multi-line
   comment */

using System;  // Import namespace

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

## Data Types

```csharp
// Value Types
bool    // True or False
byte    // 8-bit unsigned integer
sbyte   // 8-bit signed integer
char    // 16-bit Unicode character
decimal // 128-bit precise decimal
double  // 64-bit double-precision float
float   // 32-bit single-precision float
int     // 32-bit signed integer
uint    // 32-bit unsigned integer
long    // 64-bit signed integer
ulong   // 64-bit unsigned integer
short   // 16-bit signed integer
ushort  // 16-bit unsigned integer

// Reference Types
string  // String of characters
object  // Base type of all other types
dynamic // Type is resolved at runtime
```

## Variables and Constants

```csharp
// Variable declaration and initialization
int number = 10;
string name = "John";

// Implicitly typed local variable
var age = 25;

// Constant
const double PI = 3.14159;

// Nullable type
int? nullableNumber = null;
```

## Operators

```csharp
// Arithmetic operators
+, -, *, /, %

// Comparison operators
==, !=, <, >, <=, >=

// Logical operators
&&, ||, !

// Bitwise operators
&, |, ^, ~, <<, >>

// Assignment operators
=, +=, -=, *=, /=, %=, &=, |=, ^=, <<=, >>=

// Null-coalescing operator
??

// Null-conditional operator
?.

// Ternary operator
condition ? trueExpression : falseExpression
```

## Control Structures

```csharp
// If statement
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

// Switch statement
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

// For loop
for (int i = 0; i < 10; i++)
{
    // code
}

// While loop
while (condition)
{
    // code
}

// Do-while loop
do
{
    // code
} while (condition);

// Foreach loop
foreach (var item in collection)
{
    // code
}
```

## Methods

```csharp
// Method declaration
public static int Add(int a, int b)
{
    return a + b;
}

// Method with optional parameters
public static void Greet(string name, string greeting = "Hello")
{
    Console.WriteLine($"{greeting}, {name}!");
}

// Method with out parameter
public static bool TryParse(string input, out int result)
{
    return int.TryParse(input, out result);
}

// Method with ref parameter
public static void Swap(ref int a, ref int b)
{
    int temp = a;
    a = b;
    b = temp;
}

// Expression-bodied method
public static int Multiply(int a, int b) => a * b;
```

## Arrays and Collections

```csharp
// Array declaration and initialization
int[] numbers = new int[5];
string[] names = { "John", "Jane", "Alice" };

// Multidimensional array
int[,] matrix = new int[3, 3];

// Jagged array
int[][] jaggedArray = new int[3][];
jaggedArray[0] = new int[4];
jaggedArray[1] = new int[3];
jaggedArray[2] = new int[5];

// List
List<string> fruits = new List<string> { "Apple", "Banana", "Orange" };

// Dictionary
Dictionary<string, int> ages = new Dictionary<string, int>
{
    { "John", 25 },
    { "Jane", 30 }
};

// HashSet
HashSet<int> uniqueNumbers = new HashSet<int> { 1, 2, 3, 4, 5 };

// Queue
Queue<string> queue = new Queue<string>();
queue.Enqueue("First");
queue.Enqueue("Second");

// Stack
Stack<int> stack = new Stack<int>();
stack.Push(1);
stack.Push(2);
```

## Classes and Objects

```csharp
public class Person
{
    // Fields
    private string name;
    private int age;

    // Constructor
    public Person(string name, int age)
    {
        this.name = name;
        this.age = age;
    }

    // Properties
    public string Name
    {
        get { return name; }
        set { name = value; }
    }

    public int Age
    {
        get { return age; }
        set { age = value; }
    }

    // Methods
    public void Introduce()
    {
        Console.WriteLine($"Hi, I'm {name} and I'm {age} years old.");
    }
}

// Creating an object
Person person = new Person("John", 25);
person.Introduce();
```

## Inheritance and Polymorphism

```csharp
public class Animal
{
    public virtual void MakeSound()
    {
        Console.WriteLine("The animal makes a sound");
    }
}

public class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("The dog barks");
    }
}

public class Cat : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("The cat meows");
    }
}

// Using polymorphism
Animal myDog = new Dog();
Animal myCat = new Cat();
myDog.MakeSound();  // Output: The dog barks
myCat.MakeSound();  // Output: The cat meows
```

## Interfaces and Abstract Classes

```csharp
// Interface
public interface IShape
{
    double CalculateArea();
}

// Abstract class
public abstract class Shape
{
    public abstract double CalculateArea();
    
    public void DisplayArea()
    {
        Console.WriteLine($"The area is: {CalculateArea()}");
    }
}

// Concrete class implementing interface
public class Circle : IShape
{
    public double Radius { get; set; }

    public double CalculateArea()
    {
        return Math.PI * Radius * Radius;
    }
}

// Concrete class inheriting from abstract class
public class Rectangle : Shape
{
    public double Width { get; set; }
    public double Height { get; set; }

    public override double CalculateArea()
    {
        return Width * Height;
    }
}
```

## Properties and Indexers

```csharp
public class Temperature
{
    private double celsius;

    // Auto-implemented property
    public string Scale { get; set; }

    // Full property
    public double Celsius
    {
        get { return celsius; }
        set { celsius = value; }
    }

    // Property with expression-bodied members
    public double Fahrenheit
    {
        get => celsius * 9 / 5 + 32;
        set => celsius = (value - 32) * 5 / 9;
    }

    // Indexer
    public double this[int index]
    {
        get
        {
            if (index == 0) return Celsius;
            if (index == 1) return Fahrenheit;
            throw new IndexOutOfRangeException();
        }
    }
}
```

## Delegates and Events

```csharp
// Delegate declaration
public delegate void MessageHandler(string message);

// Event declaration
public event MessageHandler MessageReceived;

// Method that matches delegate signature
public void DisplayMessage(string message)
{
    Console.WriteLine(message);
}

// Using delegate and event
MessageHandler handler = DisplayMessage;
handler("Hello via delegate!");

MessageReceived += DisplayMessage;
MessageReceived?.Invoke("Hello via event!");
```

## Lambda Expressions

```csharp
// Lambda expression with no parameters
Action sayHello = () => Console.WriteLine("Hello!");

// Lambda expression with parameters
Func<int, int, int> add = (x, y) => x + y;

// Lambda expression with multiple statements
Func<int, int> factorial = n =>
{
    int result = 1;
    for (int i = 1; i <= n; i++)
    {
        result *= i;
    }
    return result;
};
```

## LINQ

```csharp
// LINQ query syntax
var query = from num in numbers
            where num % 2 == 0
            orderby num
            select num;

// LINQ method syntax
var result = numbers.Where(n => n % 2 == 0)
                    .OrderBy(n => n)
                    .Select(n => n);

// Common LINQ operations
var firstEven = numbers.First(n => n % 2 == 0);
var anyGreaterThan10 = numbers.Any(n => n > 10);
var sumOfNumbers = numbers.Sum();
var groupedByFirstLetter = words.GroupBy(w => w[0]);
```

For a visual explanation of LINQ concepts, check out [LINQ Explained with Sketches](https://steven-giesel.com/blogPost/d65c5411-a69b-489f-b73f-18ce0ed8678d).

## Asynchronous Programming

```csharp
// Asynchronous method
public async Task<string> FetchDataAsync()
{
    using (var client = new HttpClient())
    {
        return await client.GetStringAsync("https://api.example.com/data");
    }
}

// Using async/await
public async Task ProcessDataAsync()
{
    string data = await FetchDataAsync();
    Console.WriteLine(data);
}

// Parallel processing
await Task.WhenAll(
    ProcessDataAsync(),
    AnotherAsyncMethod()
);
```

## Exception Handling

```csharp
try
{
    // Code that may throw an exception
    int result = 10 / 0;
}
catch (DivideByZeroException ex)
{
    Console.WriteLine("Divide by zero error: " + ex.Message);
}
catch (Exception ex)
{
    Console.WriteLine("An error occurred: " + ex.Message);
}
finally
{
    Console.WriteLine("This code always executes");
}

// Throwing an exception
throw new ArgumentException("Invalid argument", nameof(someParameter));
```

## File I/O

```csharp
// Reading from a file
string content = File.ReadAllText("file.txt");

// Writing to a file
File.WriteAllText("file.txt", "Hello, World!");

// Reading lines from a file
string[] lines = File.ReadAllLines("file.txt");

// Appending to a file
File.AppendAllText("file.txt", "New line of text");

// Using StreamReader and StreamWriter
using (StreamReader reader = new StreamReader("input.txt"))
using (StreamWriter writer = new StreamWriter("output.txt"))
{
    string line;
    while ((line = reader.ReadLine()) != null)
    {
        writer.WriteLine(line.ToUpper());
    }
}
```

## Generics

```csharp
// Generic class
public class GenericList<T>
{
    private List<T> items = new List<T>();

    public void Add(T item)
    {
        items.Add(item);
    }

    public T GetAt(int index)
    {
        return items[index];
    }
}

// Generic method
public T Max<T>(T a, T b) where T : IComparable<T>
{
    return a.CompareTo(b) > 0 ? a : b;
}

// Using generics
GenericList<int> numbers = new GenericList<int>();
numbers.Add(10);
numbers.Add(20);

int maxNumber = Max(5, 10);
```

## Attributes

```csharp
// Custom attribute
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method)]
public class AuthorAttribute : Attribute
{
    public string Name { get; }
    public string Date { get; }

    public AuthorAttribute(string name, string date)
    {
        Name = name;
        Date = date;
    }
}

// Using custom attribute
[Author("John Doe", "2023-05-20")]
public class MyClass
{
    [Author("Jane Smith", "2023-05-21")]
    public void MyMethod() { }
}
```

## Reflection

```csharp
// Getting type information
Type type = typeof(MyClass);
MethodInfo[] methods = type.GetMethods();

// Creating an instance using reflection
object obj = Activator.CreateInstance(type);

// Invoking a method using reflection
MethodInfo method = type.GetMethod("MyMethod");
method.Invoke(obj, null);

// Getting and setting property values
PropertyInfo property = type.GetProperty("MyProperty");
object value = property.GetValue(obj);
property.SetValue(obj, newValue);
```

## Nullable Types

```csharp
// Nullable value type
int? nullableInt = null;

// Checking for null
if (nullableInt.HasValue)
{
    Console.WriteLine(nullableInt.Value);
}

// Null-coalescing operator
int result = nullableInt ?? 0;

// Null-conditional operator
string name = person?.Name;
```

## Tuples

```csharp
// Creating a tuple
(string Name, int Age) person = ("John", 30);

// Accessing tuple elements
Console.WriteLine($"{person.Name} is {person.Age} years old");

// Tuple as method return type
(int Min, int Max) FindMinMax(int[] numbers)
{
    return (numbers.Min(), numbers.Max());
}

// Deconstruction
var (min, max) = FindMinMax(new int[] { 1, 5, 3, 7, 2 });
```

## Pattern Matching

```csharp
// Type pattern
if (obj is string s)
{
    Console.WriteLine(s.Length);
}

// Switch expression
string GetSound(Animal animal) => animal switch
{
    Dog => "Woof",
    Cat => "Meow",
    _ => "Unknown"
};

// Property pattern
if (person is { Name: "John", Age: 30 })
{
    Console.WriteLine("Found John, age 30");
}

// Tuple pattern
static string Classify(int a, int b) => (a, b) switch
{
    (0, 0) => "Origin",
    (_, 0) => "X-axis",
    (0, _) => "Y-axis",
    var (x, y) when x == y => "Diagonal",
    _ => "Neither"
};

// Positional pattern
public class Point
{
    public int X { get; }
    public int Y { get; }
    public void Deconstruct(out int x, out int y) => (x, y) = (X, Y);
}

static string Classify(Point point) => point switch
{
    (0, 0) => "Origin",
    (_, 0) => "X-axis",
    (0, _) => "Y-axis",
    var (x, y) when x == y => "Diagonal",
    _ => "Neither"
};
```

## Records

```csharp
// Record declaration
public record Person(string FirstName, string LastName);

// Creating a record instance
var person = new Person("John", "Doe");

// Records have built-in value equality
var person2 = new Person("John", "Doe");
Console.WriteLine(person == person2);  // True

// Non-destructive mutation
var modifiedPerson = person with { FirstName = "Jane" };

// Inheritance in records
public record Employee(string FirstName, string LastName, int EmployeeId) 
    : Person(FirstName, LastName);

// Record structs (C# 10+)
public record struct Point(int X, int Y);
```

## Span and Memory

```csharp
// Using Span<T>
Span<int> numbers = stackalloc int[10];
for (int i = 0; i < numbers.Length; i++)
{
    numbers[i] = i;
}

// Slicing with Span<T>
Span<int> slice = numbers.Slice(2, 5);

// Using Memory<T>
Memory<char> memory = new char[20];
memory.Span.Fill('A');

// Passing Memory<T> to methods
void ProcessMemory(Memory<char> mem) { /* ... */ }
ProcessMemory(memory);
```

## Ranges and Indices

```csharp
// Using Index
Index last = ^1;
var lastElement = array[last];

// Using Range
int[] numbers = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
var slice = numbers[2..^2];  // { 2, 3, 4, 5, 6, 7 }

// Range in strings
string text = "Hello, World!";
string substring = text[7..];  // "World!"
```

## Switch Expressions

```csharp
// Traditional switch statement
string GetDayType(DayOfWeek day)
{
    switch (day)
    {
        case DayOfWeek.Saturday:
        case DayOfWeek.Sunday:
            return "Weekend";
        default:
            return "Weekday";
    }
}

// Switch expression
string GetDayType(DayOfWeek day) => day switch
{
    DayOfWeek.Saturday or DayOfWeek.Sunday => "Weekend",
    _ => "Weekday"
};
```

## Default Interface Methods

```csharp
public interface ILogger
{
    void Log(string message);

    // Default implementation
    void LogError(string message) => Log($"ERROR: {message}");
}

// Class implementing the interface doesn't need to implement LogError
public class ConsoleLogger : ILogger
{
    public void Log(string message) => Console.WriteLine(message);
}
```

## Init-only Setters

```csharp
public class Person
{
    public string FirstName { get; init; }
    public string LastName { get; init; }
}

var person = new Person { FirstName = "John", LastName = "Doe" };
// person.FirstName = "Jane";  // This would cause a compile-time error
```

## Top-level Statements

```csharp
// Program.cs
Console.WriteLine("Hello, World!");

// No need for explicit Main method or namespace
```

## Global Using Directives

```csharp
// In a central file, e.g., GlobalUsings.cs
global using System;
global using System.Collections.Generic;
global using System.Linq;

// These using directives will be available in all files in the project
```

## File-scoped Namespaces

```csharp
namespace MyNamespace;

// All types in this file are now part of MyNamespace
public class MyClass
{
    // ...
}
```

## Required Members

```csharp
public class Person
{
    public required string Name { get; set; }
    public required int Age { get; set; }
}

// Must set all required members
var person = new Person { Name = "John", Age = 30 };
```

## Static Abstract Members in Interfaces

```csharp
public interface IFactory<T>
{
    static abstract T Create();
}

public class ConcreteFactory : IFactory<ConcreteFactory>
{
    public static ConcreteFactory Create() => new();
}
```

## Extended Property Patterns

```csharp
public record Address(string Street, string City, string Country);
public record Person(string Name, Address Address);

var person = new Person("John", new Address("123 Main St", "New York", "USA"));

if (person is { Address: { City: "New York" } })
{
    Console.WriteLine("Person lives in New York");
}
```

## List Patterns

```csharp
int[] numbers = { 1, 2, 3, 4, 5 };

var result = numbers switch
{
    [1, 2, ..] => "Starts with 1, 2",
    [.., 4, 5] => "Ends with 4, 5",
    [1, .., 5] => "Starts with 1 and ends with 5",
    _ => "No match"
};
```

## Raw String Literals

```csharp
var json = """
{
    "name": "John Doe",
    "age": 30,
    "city": "New York"
}
""";

var query = @"""
    SELECT *
    FROM Users
    WHERE Name = "John"
""";
```

This concludes the comprehensive C# cheat sheet, covering a wide range of language features from basic syntax to advanced concepts and recent additions to the language. This cheat sheet should serve as a quick reference for C# developers of all levels.
