# Hand-in 1

**Preface: **These exercises are solved easily by large language models such as ChatGPT. It is highly advised **against usage** of LLM's for the purpose of **generating code** to solve these exercises and would count as **fraud**. It would furthermore defeat the purpose as the following exercises are made to sharpen logical thinking & shape algorithmic understanding.

- Functions
- Control Flow
- Lambda Functions



### 1.

A person is elligible to vote if his/her age is greater than or equal to 18. Define a method to find out if he/she is elligible to vote. Let the user input their age. Get inspiration in the terminal output below:

```kotlin
Please enter your age
6
You are not eligible to vote
```



### 2.

Define two functions to print the maximum and the minimum number respectively among three numbers

```kotlin
val max : Int = getMax(1,18,8);

val min : Int = getMin(1,18,-8);

println(max); //18
println(min); //-8
```



### 3. 

Write a Kotlin function named `calculateAverage` that takes in a list of numbers and returns their average.



### 4.

Write a method that returns if a user has input a valid CPR number.

A valid CPR number has:

- 10 Digits.
- The first 2 digits are not above 31.
- The middle 2 digits are not above 12.

The method returns true if the CPR number is valid, false if it is not.



### 5.

Write a program that prints the numbers from 1 to 100. But for multiples of three print “Fizz” instead of the number and for the multiples of five print “Buzz”. For numbers which are multiples of both three and five print “FizzBuzz”.



### 6.

Write a program that takes your full name as input and displays the abbreviations of the first and middle names except the last name which is displayed as it is.

For example, if your name is `Robert Brett Roser`, then the output should be `R.B. Roser`. Or `Benjamin Dalsgaard Hughes` will be `B.D. Hughes`



### 7.

Write a program that takes a numerical grade (0-100) as input and prints out the corresponding american letter grade. Implement a function `calculateGrade` that takes an integer parameter representing the grade and returns a string representing the letter grade according to the following scale:

- 90-100: "A"
- 80-89: "B"
- 70-79: "C"
- 60-69: "D"
- Below 60: "F"



### 8. 

Write a Kotlin function named `filterWordsByLength` that takes in a list of strings and a minimum length, and returns a list containing only the words that have a length greater than or equal to the specified minimum length.

- Use filter function and lambda expressions



### Advanced (Optional)

### ISBN validation

The ISBN-10 format is 9 digits (0 to 9) plus one check character (either a digit or an X only). In the case the check character is an X, this represents the value '10'. These may be communicated with or without hyphens, and can be checked for their validity by the following formula:

```plain
(x1 * 10 + x2 * 9 + x3 * 8 + x4 * 7 + x5 * 6 + x6 * 5 + x7 * 4 + x8 * 3 + x9 * 2 + x10 * 1) mod 11 == 0
```

If the result is 0, then it is a valid ISBN-10, otherwise it is invalid.

### Example

Let's take the ISBN-10 `3-598-21508-8`. We plug it in to the formula, and get:

```plain
(3 * 10 + 5 * 9 + 9 * 8 + 8 * 7 + 2 * 6 + 1 * 5 + 5 * 4 + 0 * 3 + 8 * 2 + 8 * 1) mod 11 == 0

```

Given a string the program should check if the provided string is a valid ISBN-10. Putting this into place requires some thinking about preprocessing/parsing of the string prior to calculating the check digit for the ISBN.

The program should be able to verify ISBN-10 both with and without separating dashes.
