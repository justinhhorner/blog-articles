## Introduction to Variables and Data Types

In the last article, we created a variable speed with a default value assigned from our Player class. We also added the `SerializeField` attribute to allow for adjustments in the inspector. However, I didn’t cover much on the topic of variables; it was just enough to get our player moving faster across the screen.

This article is a short break from the game we’re building to discuss variables in more depth.

## It’s All Data

As programmers, everything we do is some form of data manipulation. No matter how many abstractions are below the code you’ve written, at the end of those abstractions will ultimately be a translation to machine code, which is the only code computers understand. If you’ve ever heard the phrase, “It’s all 1s and 0s”, they are referring to machine language.

Don’t worry, we’re not going to cover machine or assembly language (assembly being one level above machine language). I bring this up because it’s important to understand that every instruction we write, every variable, and even the graphics you see in applications and video games are all examples of data.

## Data Types

Variables in C# have a data type that indicates the type of values that can be stored. The C# compiler guarantees that the values we attempt to store in variables are of the correct type, which is why we call C# a type-safe language.

### Type Categories
There are two categories of types in C#, value types and reference types.

A value type variable can only contain an instance of the type. For example, an int is a value type and can only be set to an integer value; it cannot contain a reference to another int.
```csharp
int a = 15;
int b = a;
```
In this example, we assign a value of 15 to variable `a`. We then assign the variable `b` to `a`. This may seem like we've created a connection between the two variables, but remember int is a value type; it cannot store a reference to another instance, so the value 15 is copied as the value for variable `b`.

On the other hand, reference type variables contain a reference to an instance of the type. Classes are reference types. Here's another simple example where we have a class called Item that has a name property.

```csharp
public class Item
{
    public string Name { get; set; }

    public Item(string name)
    {
        Name = name;
    }
}
```

Let's create two object instances of `Item` with names `itemA` and `itemB`. We'll then assign `itemA` to `itemB`, update the name property on `itemA`, and you'll see that the value is updated for both objects because they reference the same object instance.

```csharp
Item itemA = new Item("A");
Item itemB = new Item("B");

itemB = itemA;

itemA.Name = "C";
Debug.Log(itemA.Equals(b)); // Returns true
Debug.Log($"A={itemA.Name} B={itemB.Name}"); // Prints "A=C B=C"
```

As we continue through the series, we'll be working with value and reference types, and how they differ will become more clear. 

### Common Types
C# provides several [built-in primitive types](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/built-in-types), but we’ll cover the most commonly used.

### String

Strings are a series of sequential characters that are used to represent text. For example, you could use a string to display a player’s name, NPC dialog, etc. We also use string representations in the user interface, like getting a string representation of a numerical score value to display.

```csharp
string stringValue = "XYZ";
```

### Byte

A byte can store values that range from 0 to 255. This data type is what we call `unsigned` because it does not allow for negative numbers.

```csharp
byte byteValue = 24;
```

### Int

An int (integer) can store values in the range of -2,147,483,648 to 2,147,483,647. In scenarios where you don’t need negative numbers and would like a higher maximum range, you can use the UInt32 type, which can store values from 0 to 4,294,967,295.

```csharp
int intValue = 3;
```

### Float

A float (floating-point number) represents real numbers with the precision of ~6-9 digits. You may want to use this data type for storing speed or health, for example. We add the `f` suffix here to tell the compiler that we are being intentional in assigning a float value instead of a `double` value, which we’ll cover next.

```csharp
float floatValue = 50.52f;
```

### Double

Like float, the double type represents real numbers but with double the precision, allowing for ~15-17 digits.

```csharp
double doubleValue = 35.25978;
```

## Type Inference

When reading C# code, you may see the use of the `var` keyword instead of the specific data type like you’ve seen in the examples above, so I want to cover what we call type inference. The use of this feature is a personal/team preference. 

Type inference is a feature where the compiler will infer the type base on the result of an expression. For example, here’s a variable declared using var and assigned a string literal value.

```csharp
var stringValue = "This is a string literal";
```

Because we set the value to a string, the compiler knows that our variable is of type string without us having to specify the data type ourselves. 

Again, some people like this approach because it makes it easier for them to read, while others prefer to be explicit about the data type. The choice is yours!

## Summary

That’s all we need to cover about variables right now. We’ll cover more about variables and data types as the series continues. Stay tuned.

Take care.  
Stay awesome.