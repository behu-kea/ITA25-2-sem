

## Functions & lambda functions



## Learning goals

- Exceptions
- Nullability
- Functions
  - Lambda Functions
  - Higher Order-functions
  - Trailing lambda
  




## Overview

- Hvorfor det her semester er mega fedt!
- [https://behu.gitbook.io/ita24-2.-semester/ai-retningslinjer](https://behu.gitbook.io/ita24-2.-semester/ai-retningslinjer)
- [https://behu-kea.github.io/favicon-timer/](https://behu-kea.github.io/favicon-timer/)
- Alt kode jeg skriver smider jeg herind: [https://github.com/behu-kea/ita24-2sem-code](https://github.com/behu-kea/ita24-2sem-code)
- benjamin koder
  - Higher order function. Greeting
  - Løs samme opgaver som igår med map
  - Nullability



## Preparation

- [Learn Kotlin for Android: Lambda Expressions (Lesson 24)](https://www.youtube.com/watch?v=yx4CY_OUZok)
- [Learn Kotlin for Android: User Input (Lesson 6)](https://www.youtube.com/watch?v=XkBYH9vLs50)
- [043 Kotlin Programming Language Fundamentals - Trailing Lambda](https://www.youtube.com/watch?v=dRLTWKlz7QY)



<!--

## Peer instruction



### Question 1 - 1 min

What will the following code output?

```kotlin
fun main() {
    val greet: (String) -> String = { name -> "Hello, $name!" }
    println(greet("Kotlin"))
}
```

1. Hello, $name!
2. Hello, undefined!
3. Hello Kotlin!
4. EMPTY string
5. Syntax error



### Question 2 - 1 min

What is the output of the following code?

```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4)
    val doubled = numbers.map { it * 2 }
    println(doubled)
}
```

1. [3, 5, 6, 9]
2. [4, 8, 12, 16]
3. [1, 2, 3, 4]
4. None of the above

-->



## Topics



### Function

Remember the return types!

```kotlin
fun secondLargest(list: MutableList<Int>): Int {
    list.sort();

    return list.get(list.size - 2);
}

println(secondLargest(prices))
```



### Lambda function

```kotlin
val max2 = {a:Int, b:Int ->
     if(a > b) {
         a // This is implicitly returned
     } else {
         b // This is implicitly returned
     }
}
println(max2(33,4)) // 33

val hundredLarger = {a:Int -> a + 100 }
println(hundredLarger(10)) // 110
```

The last expression is automatically returned! We can control what is returned with this keyword `return@FUNCTION_NAME_TO_RETURN_TO` 

```kotlin
val max2 = {a:Int, b:Int ->
     if(a > b) {
         return@max2 a // This is implicitly returned
     } else {
         return@max2 a // This is implicitly returned
     }
}
println(max2(33,4)) // 33

val hundredLarger = {a:Int -> a + 100 }
println(hundredLarger(10)) // 110
```



### Lambda types

Lambda types are written like this:

```kotlin
val max2: (Int, Int) -> Int = {a:Int, b:Int ->
     if(a > b) {
         a // This is implicitly returned
     } else {
         b // This is implicitly returned
     }
}
println(max2(33,4)) // 33

val hundredLarger = {a:Int -> a + 100 }
println(hundredLarger(10)) // 110
```



### Higher order functions

A higher order function is a function that takes another function as a parameter. In the following example `runner` is a higher order function because its parameter is a function

```kotlin
fun main (){
    val happyPrinter = {toPrint: String ->
        println("$toPrint :)");
    }

    val sadPrinter = {toPrint: String ->
        println("$toPrint :(");
    }

    fun runner(printer: (String) -> Unit) {
        printer("hej");
    }

    runner(sadPrinter);
}
```

We can also pass in normal functions, but the syntax is a bit different:

```kotlin
fun main (){
    fun weirdPrinter(toPrint: String) {
        println("$toPrint $¢‰‰$‰");
    }

    fun runner(printer: (String) -> Unit) {
        printer("hej");
    }

    runner(::weirdPrinter);
}
```



<!--

### Trailing lambda

This you will see all the time later on!

If we have a higher order function where the last parameter is a function then we can call that function like so:

```kotlin
fun main (){
    fun runner(printer: (String) -> Unit) {
        printer("hej");
    }
		
  	// We give the runner function a lambda function directly here!
  	runner {toPrint ->
        println("$toPrint benjamin")
    }
}
```



Later we will see it in android in the following way:

```kotlin
Button {
	println("Click Me")
}
```

Here we call the `Button` higher order function that takes a function as its last parameter. 

-->

### Exceptions

Handle errors using `try`, `catch`, and `finally` blocks.

```kotlin
try {
    val result = divideNumbers(10, 0)
} catch (e: ArithmeticException) {
    println("Cannot divide by zero.")
} finally {
    println("Operation attempted.")
}
```



### Nullability

By default, variables cannot be `null`:

```kotlin
var name: String = "Alice"  // Non-nullable
name = null  // Compilation error
```



If a variable **can** be `null`, you must declare it with a **nullable type** using `?`:

```kotlin
var name: String? = "Alice"  // Nullable
name = null  // Allowed
```



To avoid `NullPointerException`, you can use **safe calls (`?.`)** when accessing properties or methods of a nullable variable:

```kotlin
val length: Int? = name?.length  // Returns length or null if name is null
```



## Exercises

<!--

### Opgave 0 - 10 min

Hvordan kan vi næste gang lave en opgave der gør at i som studerende skal snakke sammen om noget kode der bliver genereret af ChatGPT? 

-->

### Opgave 1 - Level 1

Write variables to represent a rectangle:

- Height of 8.5
- Width of 5.5

Create a function that computes the area and the perimeter of the rectangle and print the results



### Opgave 2 - level 2

Write a Kotlin function that takes two integers and then prints 

- the sum
- the difference
- the product
- the average
- the distance (the difference between integer, can only be positive)
- the maximum (the larger of the two integers)
- the minimum (smaller of the two integers)

Here is an example:

```
Input 1st integer: 25
Input 2nd integer: 5
Expected Output:
Sum of two integers: 30
Difference of two integers: 20
Product of two integers: 125
Average of two integers: 15.00
Distance of two integers: 20
Max integer: 25
Min integer: 5
```

The two inputs should come from user input



### Opgave 3 - level 2

Write a function that uses the `filter` function to filter all numbers of the list below greater than 10

```kotlin
val prices = mutableListOf(3, 6, 87, 99, 100, 101, -6)
```



### Opgave 4 - level 2

Write a function that takes an array of strings and returns an array with each strings length - if the strings has a length above 5 otherwise return 0 on the index.

- Hint: Use the [map](https://kotlinlang.org/docs/collection-transformations.html) function.

```kotlin
val inputStrings = listOf("apple", "banana", "kiwi", "strawberry", "pear")
val result = transformStringsLength(inputStrings)
println(result) // Output: [0, 6, 0, 10, 0]
```



### Opgave 5 - level 2

Write a function that takes a list of degrees in fahrenheit and returns and array with each degree in celcius.
- Hint: Use the [map](https://kotlinlang.org/docs/collection-transformations.html) function.



### Opgave 6 - level 2

Define a function called `greetPerson`.

- It should take two parameters:
  1. A `String` representing the person's name.
  2. A function (`(String) -> String`) that generates the greeting message.
- The function should print the generated greeting.

1. Test the `greetPerson` function by:
   - Passing a lambda function that adds "Hello" before the name.
   - Passing a lambda function that adds "Welcome, dear" before the name.



### Opgave 7 - Teachers students

Duration: 30 min

In the following exercise one group will randomly be selected to be teachers and the other group will be students

In groups of two people prepare a small 5 minute lecture. The lecture should explain the topic of **lambda functions in Kotlin** any way you like. That might be with a small slideshow or it might be with code, thats up to you. 

- As teachers present the 5 minute lecture
- As students ask good interesting questions



### Opgave 8 - level 3

Write a dice function that [generates](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.random/-random/) and returns a random number between 1-6

- Write another function that uses the dice function to roll an amount of times decided by the user
  - The functions returns the dice rolls as a list
- Write a function that takes the dice rolls as a parameter and returns the average
- Write a function that takes the dice rolls as a paramater and returns the mean
- Write a function that takes the dice rolls as a parameter and returns how many instances of 6 was rolled



When testing your functions it could be beneficial to instantiate a test-list with values you know.



### Opgave 7 - level 3

From: [Advent of code](https://adventofcode.com/2023/day/1)

The newly-improved calibration document consists of lines of text; each line originally contained a specific *calibration value* that the Elves now need to recover. On each line, the calibration value can be found by combining the *first digit* and the *last digit* (in that order) to form a single *two-digit number*.

For example:

```
1abc2
pqr3stu8vwx
a1b2c3d4e5f
treb7uchet
```

In this example, the calibration values of these four lines are `12`, `38`, `15`, and `77`. Adding these together produces `*142*`.

Consider your entire calibration document. *What is the sum of all of the calibration values?*



- Create a file with the [data](https://adventofcode.com/2023/day/1/input) as input
- Find a way to read the file - I would suggest [readLines 2.4](https://www.baeldung.com/kotlin/read-file)
  - The correct answer is 55002