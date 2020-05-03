# Variables and Data Types
## Read-Only vs Mutable Variables
```kotlin
var age = 23 // can be reassigned
val name = "XiaoqiZhang" // can not be reassigned
```

- var lets you declare mutable variables.
- val lets you declare read-only variables.
- Good practice is to prefer val over var whenever possible to reduce mutability and therefore facilitate understanding of the program’s state and data flow.

## Basic Data Types
Kotlin is a statically typed language, meaning that the data type of every expression is known at compile time.
### Integers
```kotlin
// the largest allowed for the corresponding data type
val byte: Byte = 127
val short: Short = 32767
val int: Int = 2147483647
val long: Long = 9223372036854775807
```
### Floating Point Numbers
```kotlin
val float: Float = 3.4028235e38f
val double: Double = 1.7976931348623157e308
```
### Text
```kotlin
val character: Char = '#'
val text: String = "Learning"
val multiline: String = 
"""
hello
hi
bye
"""
```
### Boolean
```kotlin
val yes: Boolean = true
val no: Boolean = false
```
### Type Mapping to Java
|Kotlin Type|Type in Java Bytecode|
|--|--|
|Byte|	byte|
|Short|	short|
|Int|	int|
|Long	|long|
|Float|	float|
|Double	|double|
|Char	|char|
|Boolean|	boolean|
> The mapping is quite trivial, but note that this mapping only works because Kotlin’s types cannot be null by default, just like Java’s primitive types cannot hold null. Kotlin’s approach to null safety is explained in detail later in [Nullable Types](https://github.com/hishark/Kotlin-Crash-Course/tree/master/Variables%20and%20Data%20Types#nullable-types).

### Exercise
```kotlin
val favoriteMovie: String = "begin again"
val rating: Double = 5.0
```
## Kotlin's Type inferences
> Type inference is a compiler feature that allows you to omit types in your code when the compiler can infer it for you.
### Type Inference for Literals
```kotlin
val string = "Educative"
val int = 27
val long = 42L
val double = 2.71828
val float = 1.23f
val bool = true
```
### Type Inference for Objects
> Naturally, type inference doesn’t only work with literal values on the right-hand side. The compiler can infer types of object just as easily:

```kotlin
import java.util.*
import java.time.*
import java.io.*

val stringBuffer = StringBuffer("PREFIX")
val localDate = LocalDate.now()
val file = File("foo.txt")
```
> Tip: You may still choose to add explicit types for clarity or to use a more abstract type than what would be inferred. It is good practice to program against abstract interfaces where it makes sense.

### More Type Inference
Apart from simple variable types, Kotlin’s compiler can infer types in lambda expressions, function return types, generic type parameters, and so forth – given sufficient context.

## Nullable Types
After this lesson, you'll be able to recognize and use nullable types, and know how to work with nullables effectively by using Kotlin's special operators to safely access potentially null data.

Kotlin’s type system differentiates between nullable and non-nullable types.

Kotlin’s basic data types, such as Int, can map safely to Java’s primitive types, such as int, in the bytecode. Both can never be null.
```kotlin
// Compile-time error: cannot assign null to non-nullable type
val input: String = null
```
### Declaring Nullable Types
The nullable counterpart of some type `A` is denoted as `A?`. For example, `String?` denotes a nullable string and `Int?` denotes a nullable integer.
```kotlin
val str: String? = null
val int: Int? = null
```
### Using Nullable Objects
Kotlin is focused on safety. Therefore, you cannot simply access any members on a nullable object as this might cause a null pointer exception:
```kotlin
val input: String? = null
// Compile-time error: unsafe call on nullable object
val output = input.toUpperCase() 
```
#### Safe Call Operator
To access members of a nullable object in Kotlin, you use the safe call operator by appending a `?` to the object:
```kotlin
val input: String? = null
val output = input?.toUpperCase()  // Works and returns null
```
#### Elvis Operator
In Kotlin, this is done using `?:`, the so-called Elvis operator:
```kotlin
val name: String? = null

val chatName = name ?: "Anonymous"  // Elvis operator
val displayName = chatName.toUpperCase()
```

You can read the Elvis operator as “or else”. Here, chatName is equal to name or else "Anonymous".
> Fun fact: The name “Elvis operator” stems from the fact that it looks like an elvis emoji ?:-O

It’s worth mentioning that this operator is not just for setting default values. Anything you put on its right-hand side is executed if the accessed value is null, so another typical case is throwing an exception:
```kotlin
val input: String? = null

val userInput = input ?: throw IllegalArgumentException("Input must not be null.")
```
#### Unsafe Call Operator
The last way to access a member on a nullable object (and literally the last one you should typically use) is the unsafe call operator `!!`.

With it, you’re telling the compiler that the object you’re trying to access cannot be null at this particular place in your code.

Using this operator is one of the few ways to get a null pointer exception in Kotlin. Think of it as an assertion and only use it if necessary. Usually, you can avoid this by refactoring your code to avoid nullability in the first place or by using the safe operators, as explained above.
### Effective Nullability Handling
Of course, it takes more effort to always think about the “null case”, but Kotlin facilitates this with:
- Operators such as ? and ?:
- Various standard library functions such as String?.isNullOrEmpty()

### Quiz
Given a variable `age: Int?`, what’s the type of the expression `age ?: 0`?
- ✅ Int

### Exercise
> In the following, you’re given variables x, y, z of type Double? (in hidden code that is prepended to your code). Calculate and print the sum x + y + z. If a number is null, it should be ignored for the sum.
>
> Hint: you can print to the console using println.

```kotlin
val nonNullableX = x ? 0.0
val nonNullableY = y ? 0.0
val nonNullableZ = z ? 0.0
val sum = nonNullableX + nonNullableY + nonNullableZ

println("Sum of $x, $y, $z = $sum")
```
### Summary
Here are the key takeaways from this lesson:
- Kotlin’s type system uses explicit nullable types.
    - By default, types are non-nullable (e.g. Person).
    - Each type has a nullable counterpart (e.g. Person?).
- The safe call operator `?` is used to safely access members of nullable types.
- The Elvis operator `?:` is used to handle null values conveniently (e.g. to define useful default values).
- The unsafe call operator `!!` acts like a non-null assertion and should be used judiciously.