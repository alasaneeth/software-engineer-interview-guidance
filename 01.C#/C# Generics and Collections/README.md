# C# Generics and Collections — Interview Questions Guide

## Section 1 — Basic C# Generics

### Q1. What are Generics in C#?

Generics allow you to create classes, methods, interfaces, and delegates with a placeholder for the data type, enabling type safety and code reuse.

```csharp
List<int> numbers = new List<int>();
```

**Advantages:**
- Type safety
- Code reuse
- Better performance
- Compile-time checking

### Q2. Why do we use Generics?

**Before Generics:**

```csharp
ArrayList list = new ArrayList();
list.Add(10);
list.Add("Hello");
```

**Problems:**
- No type safety
- Runtime errors
- Boxing/Unboxing

**With Generics:**

```csharp
List<int> list = new List<int>();
list.Add(10);
```

**Benefits:**
- Strong typing
- Better performance
- IntelliSense support

### Q3. What problems do Generics solve?

- Eliminates casting
- Eliminates boxing/unboxing
- Improves performance
- Improves code readability
- Provides compile-time validation

### Q4. Difference between Generic and Non-Generic Collections?

| Generic | Non-Generic |
|---|---|
| Type Safe | Not Type Safe |
| No Boxing | Boxing Required |
| Compile-time checking | Runtime checking |
| Faster | Slower |
| Namespace: `System.Collections.Generic` | Namespace: `System.Collections` |

### Q5. What is type safety?

Only one data type can be stored.

```csharp
List<int> list = new List<int>();
list.Add(10);
list.Add("Hello"); // Compile Error
```

# C# Generics – Section 2: Generic Classes

This guide covers the fundamentals of **Generic Classes** in C#, including creating generic classes, type parameters, multiple type parameters, nested generics, and inheritance.

---

# Q6. How do you create a Generic class?

A **Generic Class** allows you to define a class that works with different data types without rewriting code.

## Syntax

```csharp
public class Box<T>
{
    public T Value { get; set; }
}
```

### Explanation

- `T` is a placeholder for a data type.
- The actual type is specified when creating an object.
- The compiler replaces `T` with the specified type.

---

## Usage

```csharp
Box<int> numberBox = new Box<int>();
numberBox.Value = 100;

Box<string> textBox = new Box<string>();
textBox.Value = "Hello";

Console.WriteLine(numberBox.Value);
Console.WriteLine(textBox.Value);
```

### Output

```
100
Hello
```

---

## Advantages

- Reusable code
- Compile-time type safety
- No casting required
- Better performance than using `object`

---

# Q7. What does `T` represent?

`T` is called a **Type Parameter**.

It acts as a placeholder that will be replaced with the actual data type when the generic class or method is used.

Example:

```csharp
public class Box<T>
{
    public T Value { get; set; }
}
```

When creating an object:

```csharp
Box<int> b1 = new Box<int>();
```

The compiler treats it as:

```csharp
public class Box
{
    public int Value { get; set; }
}
```

---

## Common Generic Type Names

| Type Parameter | Meaning |
|---------------|---------|
| T | Generic Type |
| TKey | Dictionary Key |
| TValue | Dictionary Value |
| TResult | Return Type |
| TInput | Input Type |
| TOutput | Output Type |

Example:

```csharp
Dictionary<int, string>
```

- `TKey = int`
- `TValue = string`

---

# Q8. Can a Generic class have multiple type parameters?

**Yes.**

A generic class can have two or more type parameters.

## Syntax

```csharp
class Pair<TKey, TValue>
{
    public TKey Key;
    public TValue Value;
}
```

---

## Example

```csharp
Pair<int, string> student = new Pair<int, string>();

student.Key = 101;
student.Value = "John";

Console.WriteLine(student.Key);
Console.WriteLine(student.Value);
```

### Output

```
101
John
```

---

## Another Example

```csharp
Pair<string, double> product = new Pair<string, double>();

product.Key = "Laptop";
product.Value = 1250.50;

Console.WriteLine(product.Key);
Console.WriteLine(product.Value);
```

### Output

```
Laptop
1250.5
```

---

## Benefits

- Store related values with different types.
- Used in collections like `Dictionary<TKey, TValue>`.
- Improves code readability and reusability.

---

# Q9. Can Generics be nested?

**Yes.**

A generic type can contain another generic type.

Example:

```csharp
Dictionary<int, List<string>>
```

Here:

- Outer Generic → `Dictionary`
- Inner Generic → `List`

---

## Example

```csharp
Dictionary<int, List<string>> students =
    new Dictionary<int, List<string>>();

students.Add(1, new List<string>
{
    "Math",
    "Science",
    "English"
});

foreach (string subject in students[1])
{
    Console.WriteLine(subject);
}
```

### Output

```
Math
Science
English
```

---

## Another Example

```csharp
List<List<int>> matrix = new List<List<int>>
{
    new List<int>{1,2,3},
    new List<int>{4,5,6}
};

foreach(var row in matrix)
{
    foreach(var value in row)
    {
        Console.Write(value + " ");
    }

    Console.WriteLine();
}
```

### Output

```
1 2 3
4 5 6
```

---

## Why use Nested Generics?

Commonly used for:

- Dictionaries
- Trees
- Graphs
- JSON objects
- Database result sets
- Hierarchical data

---

# Q10. Can Generic classes inherit from another Generic class?

**Yes.**

A generic class can inherit from another generic class.

---

## Syntax

```csharp
class Base<T>
{
}

class Child<T> : Base<T>
{
}
```

---

## Example

```csharp
class Base<T>
{
    public T Data;
}

class Child<T> : Base<T>
{
    public void Display()
    {
        Console.WriteLine(Data);
    }
}
```

Usage:

```csharp
Child<int> obj = new Child<int>();

obj.Data = 500;
obj.Display();
```

### Output

```
500
```

---

## Example with Different Type Parameters

```csharp
class Person<T>
{
    public T Id;
}

class Employee<T> : Person<T>
{
    public string Name;
}
```

Usage:

```csharp
Employee<int> emp = new Employee<int>();

emp.Id = 1001;
emp.Name = "David";

Console.WriteLine(emp.Id);
Console.WriteLine(emp.Name);
```

### Output

```
1001
David
```

---

# Advantages of Generic Inheritance

- Promotes code reuse
- Supports polymorphism
- Preserves type safety
- Reduces code duplication
- Easy to extend functionality

---

# Quick Revision

## Generic Class

```csharp
class Box<T>
{
    public T Value;
}
```

---

## Multiple Type Parameters

```csharp
class Pair<TKey, TValue>
{
    public TKey Key;
    public TValue Value;
}
```

---

## Nested Generics

```csharp
Dictionary<int, List<string>>
```

---

## Generic Inheritance

```csharp
class Base<T>
{
}

class Child<T> : Base<T>
{
}
```

---

# Interview Tips

### ✔ What is a Generic Class?

A class that can work with different data types using type parameters.

---

### ✔ What does `T` represent?

A placeholder for a data type that is specified when the class or method is used.

---

### ✔ Can a Generic class have multiple type parameters?

Yes. Example:

```csharp
Pair<TKey, TValue>
```

---

### ✔ Can Generics be nested?

Yes.

Example:

```csharp
Dictionary<int, List<string>>
```

---

### ✔ Can a Generic class inherit from another Generic class?

Yes.

Example:

```csharp
class Child<T> : Base<T>
{
}
```

---

# Key Takeaways

- Generic classes provide reusable, type-safe code.
- `T` represents a generic type parameter.
- Multiple type parameters (`TKey`, `TValue`, etc.) are supported.
- Generics can be nested to represent complex data structures.
- Generic classes can inherit from other generic classes while maintaining type safety.