# Classes and objects



## Learning goals

- Classes
  - Attributes
  - Getter, setter
  - Constructor
  - Encapsulation
  - Objects
  - This
  - toString
- Behavior vs state



<!--

## In class considerations

- Det var lidt meget med også feedback på opgaver. 
- This var også sådan lidt semi. Behøves vi undervise det?

-->



## Overview

- I må gerne svare på spørgeskema omkring mineksamen

- Federe lokaler gruppe

- Imorgen første online klasse

- Vi har landet det næste projekt og jeg tror i vil synes det er fedt
  - [https://heart2heart.website/](https://heart2heart.website/)
  - [https://www.instagram.com/reel/DT0T9F3DFKW/](https://www.instagram.com/reel/DT0T9F3DFKW/)
  - [https://www.instagram.com/heart2heart_dk/reel/DUBMYGtDEiv/](https://www.instagram.com/heart2heart_dk/reel/DUBMYGtDEiv/)
  
- Feedback from handin

  - Godt klaret generelt. Jeg kan virkelig se at i har løse opgaverne selv, det skal i have ros for. Jeg ser ingen spor af AI faktisk. 

  - Fejlhåndtering

    - ```kotlin
      val stringInput = readLine()!!
          if (stringInput.toInt() >= 18)
              println("You are ${stringInput.toInt()}, and eligible to vote")
          else println("You are ${stringInput.toInt()}, and NOT eligible to vote")
      ```

  - Fedt at bruge de indbyggede kotlin funktioner! `maxOf(a, b, c)`

  - Tænk over parametre

    - ```kotlin
      fun calculateAverage(): Double {
          val myList = listOf(7,4,9,13,15)
      ```

  - Navngivning `cprNumberChecker`

  - Funktionsansvar

    - ```kotlin
      fun checkIfElligibleForVoting () {
          print("Enter your age: ")
          val ageInput = readLine()!!  // https://www.youtube.com/watch?v=XkBYH9vLs50
          val ageInt = ageInput.toInt()
              if (ageInt >= 18) {
                  println("You are elligble to vote")
              } else {
                  println("You are not elligible to vote")
              }
      }
      ```

  - Calculate average. use Kotlin functions!

  - Very nice

    - ```kotlin
      val numbersDividedBy3 = element % 3 == 0
      val numbersDividedBy5 = element % 5 == 0
      
      if (numbersDividedBy3 && numbersDividedBy5) {
      ```

  - Lav en lambda her

    - ```kotlin
      fun filterWordsByLength(listOfStrings: List<String>, minimumStringLength: Int): List<String> {
          return listOfStrings.filter { it.length >= minimumStringLength }
      }
      ```

  - Hvilke paramtere `fun isCPRValid(): Boolean {`

  - Lækkert 🤌

    - ```kotlin
      fun getCPRCheckValidity(cprNr: String): Boolean {
          val birthDay = cprNr.substring(0, 2).toInt()
          val birthMonth = cprNr.substring(2, 4).toInt()
      
          if (cprNr.length != 10) return false
          return birthDay in 1..31 && birthMonth in 1..12
      }
      ```

    - ```kotlin
      fun calculateGrade(grade: Int): Char {
          return when (grade) {
              in 90..100 -> 'A'
              in 80..89 -> 'B'
              in 70..79 -> 'C'
              in 60..69 -> 'D'
              else -> 'F'
          }
      }
      ```

    - Hvis lambda:

      ```kotlin
      val calculateGrade: (Int) -> Char = {
              when (it) {
                  in 90..100 -> 'A'
                  in 80..89 -> 'B'
                  in 70..79 -> 'C'
                  in 60..69 -> 'D'
              else -> 'F'
          }
      }
      ```

- Model Smartphone
  - Først lav attributter (brand, price, batteryPercentage). Dernæst constructor
  - Primary Constructor
  - Data vs behaviour
    - `getDiscount` function
  
  - toString
  - Briefly mention `this`!
  
- Classes are blueprints

- Peer instruction



## Preparation

- [Kotlin Class and Object](https://www.youtube.com/watch?v=Sn-PL6fNIkk)
- [Kotlin Getters and Setters](https://www.youtube.com/watch?v=rlJHzsgUwos)
- [Kotlin Constructor - Primary, Secondary Constructor and Init Block](https://www.youtube.com/watch?v=d6Lu1Wzspao)



Optional

- [https://kotlinlang.org/docs/classes.html#class-members](https://kotlinlang.org/docs/classes.html#class-members)
- [https://kotlinlang.org/docs/properties.html](https://kotlinlang.org/docs/properties.html)
- [https://kotlinlang.org/docs/visibility-modifiers.html](https://kotlinlang.org/docs/visibility-modifiers.html)



## Peer instruction

<!--

### Question 1

```kotlin
class MyClass {
    var x = 5
}

fun main() {
 
    val myObj = MyClass()
    println(myObj.x)
}
```

What is the output of the above code when executed?

1. 5
2. 0
3. Null
4. Compiler error



### Question 2

```kotlin
class MyClass(var x: Int = 5) {
    init {
        x = 7
    }
}

fun main() {
    val myObj = MyClass(1)
    println(myObj.x)
}
```

What is the output of the above code when executed?

1. 5
2. 7
3. 1
4. Null
5. Compiler error

-->



## Classes

To create a new class use the `class` keyword. 

```kotlin
class Dog () {
  val age: Int = 10;
}
```

Here we create a `Dog` with an `age` attribute set to 10



### Objects

To actually create a `Dog` we can create an object of the `Dog` class

```kotlin
val fido: Dog = Dog();
println(fido.age);
```

We can now reach the `age` attribute because we set the attribute to `val`. If we wanted to change the `age` attribute we would have to make the attribute `var` 

```kotlin
class Dog () {
  var age: Int = 10;
}
```

```kotlin
val fido: Dog = Dog();
fido.age = 10;
println(fido.age); // 10
```

This way of setting attributes is a bit cumbersome. Lets learn about the constructor:



### Constructor

To get values into the class when an object is created we use the constructor:

```kotlin
class Dog (stamina: Int, isHappy: Boolean,home: String, energy: Int) {
}
```

This will create a `Dog` class with 4 attributes. 

This part `(stamina: Int, isHappy: Boolean,home: String, energy: Int)` is called the primary constructor. It is used to initialize the class with parameters.

We can now create a `Dog` with specific attributes set to it

```kotlin
val skippy: Dog = Dog(1, true, "ballerup", 100);
```

The attributes in the primary constructor cannot be read or changed as it is right now! That means you cannot do this:

```kotlin
println(skippy.stamina); 
// or this
skippy.stamina = 10;
```



We can also set default values in our primary constructor:

```kotlin
class Dog (val stamina: Int = 20, isHappy: Boolean,home: String, energy: Int) {
}
```



### Read properties

If you want fx `stamina` to be read use the `val` keyword

```kotlin
class Dog (val stamina: Int, isHappy: Boolean,home: String, energy: Int) {
}
```

Now we can do this

```kotlin
println(skippy.stamina); 
```



### Set properties

If you want `stamina` to be changed, use the `var` keyword. 



```kotlin
class Dog (var stamina: Int, isHappy: Boolean,home: String, energy: Int) {
}

fun main() {
    val skippy: Dog = Dog(1, true, "ballerup", 100);
    println(skippy.stamina); // 1
    skippy.stamina = 10;
    println(skippy.stamina); // 10
}
```



### Secondary constructor

We can create a secondary constructor that is called when an object is created. We that by using an `init` block

```kotlin
class Dog (var stamina: Int, isHappy: Boolean,home: String, energy: Int) {
    init {
        println("First initializer block that prints $stamina")
    }
}
```



### Getter & setter

We can create getters and setters for attributes with the following syntax:

```kotlin
class Rectangle (val height: Double, val width: Double ) {
    val area: Double
        get() = this.width * this.height

    var test = 0
        set(value) { field = 30};
}

fun main() {
	val rectangle = Rectangle(4.3, 7.0);
    println(rectangle.area);
    rectangle.test = 10;
    println(rectangle.test); // 30
}
```

Be wary that here `set(value) { field = 30};`  the `field` **has to be** **called** `field`. Which will get the current value of the attribute

If we need multiple lines in fx the getter we can write it like this:

```kotlin
class Rectangle (val height: Double, val width: Double ) {
    val area: Double
        get() {
            val area: Double = this.width * this.height;
            return area
        }

    var test = 0
        set(value) { field = 30};
}
```

The getter method is called when an attribute is set fx like this

```kotlin
rectangle.test = 10;
```

So even though is looks like we just assign `rectangle.test` the value of `10` actually we call the `set` method, which will then set the `test` attribute to `30`!



The same with the getter, when we say `rectangle.area` the `get` method is called and the result returned!



### `this`

`this` keyword is used to reference the created object within the class itself

```kotlin
fun bark() {
    if(this.energy > 10) {
        println("WOOF WOOF");
    } else {
        println("woof");
    }
}
```

```kotlin
val skippy: Dog = Dog(1, true, "ballerup", 100);
skippy.bark(); // WOOF WOOF
```

In this example the value of `this` is equal to the object `skippy`. That means that `this.energy` is equal to 100



## Exercises



### Pre-exercise

Using the code from your handed in assignment. Present the code for your study mate. Talk about the code technically. What is it doing and why did you do it that way?

Hvis i ikke har fået lavet opgaven, så få ChatGPT til at lave løsningen for en af opgaverne og snak om det.



### 📝 Exercise 1 - level 1

Create a `Cat` class. The class should have

- 4 attributes that you choose
- 1 method that you choose
- Create 2 instances of cats using the constructor!

Now call the method on the two cat objects. 



### 📝 Exercise 2 - level 1

Create the classes modelling the following objects. Add both some relevant attributes and some relevant methods

Think about what should go into the primary constructor and what should be set as attributes

Think about what is data and what is behavior

- Recipe
- A Tinder profile
- A musical instrument

Instantiate at least one object per class



### 📝 Exercise 3 - level 2

Create a `Product` class for an online shop.

Requirements:

- Properties:
  - `name: String`
  - `price: Double`
    - Price cannot be negative (look into `getter` and  `setter`!)
- Function:
  - `applyDiscount(percent: Int)` where 10 means 10%

Create a `Product` and print it. Then apply the discount, then print it again. 



### 📝 Exercise 3.1 - level 2 kl 11

1. Først kig koden igennem individuelt
2. Forklar hvad koden gør for din sidemakker
   1. Brug de korrekte tekniske termer. Prøv at hjælpe hinanden med at være præcise i jeres sprog!
3. Sammen skal i foreslå nogle ændringer til koden. 
   1. Hvor kan den forbedres?
   2. Kan i lide måden koden virker? 
   3. Hvad kan i ikke lide, etc. 
   4. Dan en mening om koden. Smag på koden, hvad kan den, hvad kan den ikke

4. Implementer de foreslåede ændringer
5. Lad os sammen snakke om koden

```kotlin
class User(name: String, age: Double) {
    var name = name
    var age = age

    fun updateName(newName: String) {
        name = newName.trim()
    }

    fun haveBirthday() {
        age = age + 1.0
        println("Birthday! User is now $age years old")
    }

    override fun toString(): String {
        return "User: $name ($age)"
    }
}

class Account(user: User, balance: Double) {
    var user = user
    var balance = balance

    fun deposit(amount: Double) {
        balance = balance + amount
    }

    fun withdraw(amount: Double): Boolean {
        if (amount <= balance) {
            balance = balance - amount
            return true
        }
        return false
    }

    fun monthlyFee() {
        balance = balance - 29.0
    }

    override fun toString(): String {
        return "Account of ${user.name} has balance $balance"
    }
}

fun main() {
    val user = User(" Alice ", 20)
    val account = Account(user, 100.0)

    user.updateName("Alice Johnson")

    account.deposit(50.0)
    account.withdraw(30.0)
    account.monthlyFee()

    user.haveBirthday()

    println(user)
    println(account)

    account.balance = -100.0
    println(account)
}
```



### 📝 Exercise 4 - level 3

Create a class `SocialMediaPost` 

- A  `SocialMediaPost`  has `text`, and `likes`. `likes` cannot be less than 0! And the `text` field cannot be an empty string
  - It should have a function for adding a like, removing a like and editing the text
- A `Feed`
  - A feed has a list of  `SocialMediaPost` 
  - It should be possible to add and remove  `SocialMediaPost`  from a `Feed`
  - It should be possible to display the `Feed` in the terminal. Complete with `likes` and `text`



### 📝 Exercise 5 - level 3

Create classes for a todolist app. 

- `TodoItem`
  - Has a name, can be checked out, and can be favorited
- `TodoList` is a list that holds `TodoItems`
  - `TodoItems` can be removed and added from the list
  - The `TodoList` should also be able to display the `TodoItems`

Create a menu where a user can

- Create a `TodoItem`
- Check out a `TodoItem`
- Remove a `TodoItem`