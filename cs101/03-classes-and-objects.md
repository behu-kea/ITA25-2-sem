# Classes and objects



## Learning goals

- Classes
  - Attributes
  - Getter, setter
  - Constructor
  - Encapsulation
- Objects
- This
- Behavior vs state
- toString



<!--

## In class considerations

- Det var lidt meget med også feedback på opgaver. 
- Mike sagde at videoerne var ret svære
- Getter og setter blev lidt messy. Måske ikke undervise det næste gang. 
- This var også sådan lidt semi. Behøves vi undervise det?

-->



## Overview

- Peer instruction
- Model Smartphone
  - Getter setter
    - Var, val
    - Price cannot be less than 0
    - priceInEuros attribute
  - Constructor
  - Data vs behaviour
  - toString
  - Briefly mention `this`!
- Classes are blueprints




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

Think about what should go into the constructor and what should be set as attributes

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
    - Setter: price cannot be negative (clamp to 0)
- Function:
  - `applyDiscount(percent: Int)` where 10 means 10%

Create a `Product` and print it. Then apply the discount, then print it again. 



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