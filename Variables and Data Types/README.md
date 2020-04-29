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
> The mapping is quite trivial, but note that this mapping only works because Kotlin’s types cannot be null by default, just like Java’s primitive types cannot hold null. Kotlin’s approach to null safety is explained in detail later in the course.

## Kotlin's Type inferences

## Nullable Types
