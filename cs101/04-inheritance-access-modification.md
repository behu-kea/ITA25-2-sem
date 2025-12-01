# Inheritance and access modifiers



## Learning goals

- Access Modifiers
- Inheritance
  - Override
- 4 pillars



<!--

## In class considerations

- Exercises missed encapsulation

-->



## Overview

- Talk about 4 pillars of OOP. With code examples
  -  Survival MMO
    -  Survivor - name. fightZombies
  
    -  TheLeader - name, bravery, motivateTeam(), is secretelyTerrified

    -  TheMedic - numberOfMedKits, healSurvivor()
  
    -  TheGuyWhoAlwaysDiesFirst, tripchance, sayLastWords() <- Lad os spørge chatGPT
  
  -  **Abstraction** - Abstraction means abstracting away certain details. `hitApi('www.kealanparr.com', HTTPMethod.Get)`This function we dont need to know how it is implemented because we know how to work with it
  -  **Encapsulation** - The action of enclosing something in or as if in a capsule. Removing access to parts of your code and making things private is exactly what **Encapsulation** is all about 
  -  **Inheritance** - Inheritance is a fundamental concept in object-oriented programming  where a new class (subclass) can inherit properties and behaviors from  an existing class (superclass). This allows for code reusability and promotes organization
  -  **Polymorphism** - The condition of occurring in several different forms. More concretely an object will behave differently based on the context it is called from



- Snakke om på mandag. Selvlæring



## Preparation

- [Fundamental Concepts of Object Oriented Programming](https://www.youtube.com/watch?v=m_MQYyJpIjg)
- [Learn Kotlin for Android: Inheritance (Lesson 17)](https://www.youtube.com/watch?v=33DNMPOFvuA)





## Peer instruction

### Question 1

```kotlin
open class Base {
    open fun showMessage() {
        println("Base Message")
    }
}

class Derived : Base() {
    override fun showMessage() {
        println("Derived Message")
    }
}

fun main() {
    val obj: Base = Derived()
    obj.showMessage()
}

```

1. `Base Message`
2. `Derived Message`
3. Compilation error due to improper override
4. Runtime exception
5. None of the above



### Question 3

What will the following code print?

```kotlin
class User {
    var name: String = "Guest"
        set(value) {
            field = value.uppercase()
        }
}

fun main() {
    val user = User()
    user.name = "john"
    println(user.name)
}
```

1. `Guest`
2. `john`
3. `JOHN`
4. Compilation error due to invalid setter
5. None of the above





## Topics

*The following is generated from ChatGPT: [https://chatgpt.com/share/675aa097-4168-8008-88a4-d9d7746102f2](https://chatgpt.com/share/675aa097-4168-8008-88a4-d9d7746102f2)*



### Inheritance

Inheritance allows one class to inherit the properties and methods of another class. Use the `:` symbol to indicate inheritance.

```kotlin
open class Animal(val name: String) {
    fun eat() {
        println("$name is eating")
    }
}

class Dog(name: String) : Animal(name) {
    fun bark() {
        println("$name is barking")
    }
}
```

Here, `Dog` inherits from the `Animal` class, meaning it has access to the `eat` method in addition to its own `bark` method.

```kotlin
val fido = Dog("Fido")
fido.eat()  // Fido is eating
fido.bark() // Fido is barking
```



### Access Modifiers

Access modifiers control the visibility of class members. In Kotlin, these include:

- `public` (default): Accessible everywhere.
- `private`: Accessible only within the same class.
- `protected`: Accessible within the class and its subclasses.
- `internal`: Accessible within the same module.



```kotlin
open class Animal {
    protected fun sleep() {
        println("Sleeping...")
    }
}

class Dog : Animal() {
    fun takeNap() {
        sleep() // Accessible because `sleep` is protected
    }
}

fun main() {
    val dog = Dog()
    dog.takeNap() // Sleeping...
    // dog.sleep() // Error: Cannot access 'sleep': it is protected
}
```



### Inheritance - Override

To override a method in the parent class, use the `override` keyword in the subclass.

```kotlin
open class Animal {
    open fun makeSound() {
        println("Some generic sound")
    }
}

class Dog : Animal() {
    override fun makeSound() {
        println("Bark")
    }
}

fun main() {
    val animal: Animal = Dog()
    animal.makeSound() // Bark
}
```

The `open` keyword is required to make a method in the parent class overridable.

The overridden method must have the same signature as the method in the parent class.



### `super` Keyword

To call the parent class method inside an overridden method, use `super`.

```kotlin
open class Animal {
    open fun makeSound() {
        println("Some generic sound")
    }
}

class Dog : Animal() {
    override fun makeSound() {
        super.makeSound()
        println("Bark")
    }
}
```

This calls the parent class method and then adds the subclass-specific functionality.



### 4 Pillars of Object-Oriented Programming

#### Encapsulation

Encapsulation involves bundling data (attributes) and behavior (methods) into a single unit (class) and restricting access to them.



```kotlin
class Account(private var balance: Int) {
    fun deposit(amount: Int) {
        balance += amount
    }

    fun getBalance(): Int {
        return balance
    }
}

val account = Account(100)
account.deposit(50)
println(account.getBalance()) // 150
// account.balance // Error: Cannot access 'balance'
```



#### Abstraction

Abstraction hides implementation details and exposes only the necessary parts of an object.

```kotlin
abstract class Animal {
    abstract fun makeSound()
}

class Dog : Animal() {
    override fun makeSound() {
        println("Bark")
    }
}

val dog = Dog()
dog.makeSound() // Bark
```



#### Inheritance

Inheritance enables code reuse by allowing one class to inherit the properties and methods of another. (See examples above.)



#### Polymorphism

Polymorphism allows objects to be treated as instances of their parent class, enabling flexibility and reuse.

```kotlin
open class Animal {
    open fun makeSound() {
        println("Some generic sound")
    }
}

class Dog : Animal() {
    override fun makeSound() {
        println("Bark")
    }
}

class Cat : Animal() {
    override fun makeSound() {
        println("Meow")
    }
}

fun main() {
    val animals: List<Animal> = listOf(Dog(), Cat())
    for (animal in animals) {
        animal.makeSound()
    }
    // Output:
    // Bark
    // Meow
}
```



## Opgaver



### Opgave 1 - level 2

Write a class called `Animal`. An `animal` has 3 properties:

- `name`
- `nrOfLegs`
- `isMammal`

Animal has a method: `makeSound()` that prints the sound of the animal.

- Create 2 animal classes that extends the Animal class and overrides
  the method to produce their unique sound.
- Create a list, add 5 animals to the list and print every animals sound.
- Override the `toString` method such that if an animal object is printed, it will return a string in the following format: [name=`name`, nrOfLegs=`nrOfLegs`, isMammal=`isMammal`]



### Opgave 2 - level 2

Create a hierarchy of food items in a restaurant menu. Implement a base class called `FoodItem` with properties `name`, `description`, and `price`. 

- Derive two classes `Dessert`, `Appetizer` and `MainCourse` from `FoodItem`. Implement the properties: 
  - `servingSize` for `Appetizer` 
  - `spicinessLevel` for `MainCourse`
  - `isVegan` for `dessert`

- Additionally, implement the method `cook()` for all classes, which print out a message indicating what kind of fooditem is currently being cooked.



### Opgave 3 - level 2

Create a Kotlin class called `BankAccount` with the following properties:

1. `accountNumber`: The account number of the bank account.
2. `balance`: The current balance of the bank account.

- Implement custom getter and setter methods for the `balance` property. The setter should ensure that the balance is always non-negative. If a negative value is attempted to be set, it should be adjusted to 0.



### Opgave 4 - level 2

Create a class named `Student` to represent student information.  Include properties such as `name`, `birthdate`, and `grade`. 

- Implement a custom setter for the `grade` property to ensure that the grade is within a valid range (e.g., 0 to 100).
- Additionally, implement a custom getter for the `age` property to calculate the student's age based on their birthdate, which is passed as a parameter during object construction.



### Opgave 6 - level 3

Create a class `Person`. A person has a cpr number and name

- A person has a private function that calculates the age of the person by their CPR number
- A person has a field: age.
  - The field is public and uses the private function to return a result.
  - The setter is private, as no one from outside should be able to use the function
- The setter for the CPR number should check if the CPR number is valid before setting it. 
