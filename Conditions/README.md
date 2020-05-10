# Conditions
## Conditions with `if`
> For conditional control flow, Kotlin uses the if and when keywords. The syntax of if-blocks is the same as in C and Java. Similarly, the when keyword is similar to switch in these languages but more powerful, as you will learn.

### Equality and Comparison Operators
Note for Java developers: In Kotlin, you use `==` where you would use `equals` in Java and `===` where you would use Java’s `==`.

## Conditions with `when`
You can use `when` conditions to define different behaviors for a given set of distinct values. This is typically more concise than writing cascades of `if-else if` conditions. For instance, you can replace the `if` condition above with a `when` condition to save around 30% of the lines of code in this example:
```kotlin
when (planet) {
  "Jupiter" -> println("Radius of Jupiter is 69,911km")
  "Saturn"  -> println("Radius of Saturn is 58,232km")
  else      -> println("No data for planet $planet")
}
```
The code block on the right-hand side must be wrapped in curly braces unless it’s a single expression. Optionally, an `else`-block can be used to define a block of code to run if no other case matches.
This language construct is basically the same as `switch` from languages like C or Java. However, it’s more powerful since it supports more complex checks:
```kotlin
when(temperatureInKelvin) {
      700              -> println("This is Mercury’s max surface temperature")
      0, 1, 2          -> println("This i as cold as it can physically get")
      in 300..699      -> println("This temperature is possible on Mercury")
      !in 0..300       -> println("This is pretty hot")
      earthSurfaceTemp() -> println("This is earth’s average surface temperature")
      is Int             -> println("The given temperature is of type Int")
      else               -> {
        // Example of a multiline code block
        println("Default case")
      }
    }
```
As you can see, there are various ways to define the value(s) to compare against:
1. Fixed value (700)
2. Multiple fixed values (0, 1, 2)
3. Ranges (in 300..699)
4. Ranges with negation (“not in range”) (!in 0..300)
5. Function call (earthSurfaceTemp())
6. Type check (is Int)
7. Default case (else)

> Note: Kotlin adds a `break` to the end of each case implicitly so that you cannot introduce bugs due to a forgotten fallthrough case.

In fact, the `when` construct is even more powerful because it allows arbitrary conditions by leaving out the variable after the `when` keyword:
```kotlin
when {
      age >= 18 && !hasAccess -> println("Falsely rejected")
      age < 18 && hasAccess -> println("Falsely approved")
      else -> println("Correctly authorized")
    }
```
Here, you can see the `age` variable is not mentioned in the `when` block’s header as in `when (age)`. This way, you can use any boolean expressions on the left-hand sides of each `when` case, such as `age >= 18`.

Using `when` is definitely preferable when comparing against two or more distinct fixed values.

In many cases, a `when` condition will be a more concise and readable alternative to a regular `if` condition, especially whenever the right-hand sides are single expressions.
### Exercises
Complete the following code snippet to check whether…
1. The age variable is between 18 and 21 (both inclusive)
2. The username variable equals "admin" or "system"
3. The number variable is not equal to neither 17 nor 42
```kotlin
// Check age
when (age) {
    in 18..21 -> println("Age is between 18 and 21")
    else -> println("Age is not between 18 and 21")
}

// Check username
when (username) {
    "admin", "system" -> println("User has root access")
    else -> println("User has no admin rights")
}

// Check number
when {
    number != 17 && number != 42 -> println("The number is not 17 and not 42")
    else -> println("The number is either 17 or 42")
}
```

## Conditions as Expressions
In Kotlin, both `if` and `when` can be used as expressions instead of statements. An expression is a piece of code that has a value, e.g. `"Kotlin"`, `42 * 17`, or `readInput()`. In contrast, a statement is a piece of code with no value, such as `fun foo() { ... }` or `while (active) { ... }`. In many programming languages, `if` and `when/switch` are statements. But in Kotlin, they are expressions.
### Expressions with `if`
Recall this listing from the lesson on if statements:
```java
if (planet == "Jupiter") {
  println("Radius of Jupiter is 69,911km")
} else if (planet == "Saturn") {
  println("Radius of Saturn is 58,232km")
} else {
  println("No data for planet $planet")
}
```
If you think about it, it seems that the relevant data that changes here based on the condition is the radius. So let’s store that in a variable by using an `if` expression:
```kotlin
val radiusInKm = if (planet == "Jupiter") {
	// Run code here...
	69911  // Last line defines the return value of this block
} else if (planet == "Saturn") {
	// Run code here...
	58232
} else {
	// Run code here...
	-1
}
```
Here, the entire `if-elseif-else` block has a value. This value for each branch is decided by the **last line in each branch**. You may run arbitrary code in each condition block but ultimately, the last line defines the value.
### Ternary Conditional Operator in Kotlin
Kotlin has no separate language construct for a ternary conditional operator of the form `someCondition ? thenThis : elseThat`, which you may know from other languages. Instead, `if` expressions are used:
```kotlin
val category1 = if (age >= 18) "adult" else "child"
```
> Note that you don’t need curly braces around the condition blocks if they’re a single expression.
### Expressions with `when`
Naturally, when can be used as an expression in the same way:
```kotlin
val radiusInKm = when (planet) {
    "Jupiter" -> 69911
    "Saturn"  -> 58232
    else      -> -1
}
```
### Summary
- Expressions have a value. Statements do not.
- In Kotlin, if and when are expressions.
  - If you don’t use the value, they work exactly like conditional statements in other languages.
- Conditional expressions are useful to assign a value directly instead of splitting up declaration and initialization.