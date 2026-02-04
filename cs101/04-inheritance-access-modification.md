# Inheritance and access modifiers



## Learning goals

- Access Modifiers
- Inheritance
  - Override
- 4 pillars



## Overview

- Talk about 4 pillars of OOP. With code examples
  -  Survival MMO https://github.com/behu-kea/ita24-2sem-code/blob/main/inheritance/app/src/main/java/com/example/inheritance/main.kt
    -  They all have private energy
  
    -  Survivor base class
       -  name, health
    
       -  fight()
    
    -  TheLeader
       -  bravery
    
       -  motivateTeam()
    
       -  is secretelyTerrified
    
    -  TheGuyWhoAlwaysDiesFirst
       -  tripchance
       -  sayLastWords() <- Lad os spørge chatGPT
    
  -  **Abstraction** - Abstraction means abstracting away certain details. `hitApi('www.kealanparr.com', HTTPMethod.Get)`This function we dont need to know how it is implemented because we know how to work with it. Abstraction = exposing *what* an object can do, while hiding *how* it does it.
  -  **Encapsulation** - The action of enclosing something in or as if in a capsule. Removing access to parts of your code and making things private is exactly what **Encapsulation** is all about
  -  **Inheritance** - Inheritance is a fundamental concept in object-oriented programming  where a new class (subclass) can inherit properties and behaviors from  an existing class (superclass). This allows for code reusability and promotes organization
  -  **Polymorphism** - The condition of occurring in several different forms. More concretely an object will behave differently based on the context it is called from
  
- Videoproduktion skal være færdig kl 10:45
  
- Vi ser nogle af videoerne i fællesrummet fra 10:45 - 11:00 🍿
  
- Fra 11-11:30 arbejde på case
  
- 11:30 - 11:45 diskutere case på klassen
  
- Snakke om på mandag. Selvlæring



## Preparation

- [Fundamental Concepts of Object Oriented Programming](https://www.youtube.com/watch?v=m_MQYyJpIjg)
- [Learn Kotlin for Android: Inheritance (Lesson 17)](https://www.youtube.com/watch?v=33DNMPOFvuA)
- [Encapsulation](https://www.youtube.com/watch?v=85vDxSagygU)



## Peer instruction

<!--

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



### Question 2

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

-->



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



### Opgave 1

I skal forestille jer at arbejde på en formidlingskanal om softwareudvikling. Denne kanal skal lave en video der handler om 4 pillars of OOP. I skal producere denne video. Hvilken platform i vil producere til er op til jer. 

Målgruppen er unge i alderen 18-25 der har udviklet software før. 

Hvordan i laver videoen er helt op til jer

I har til kl 10:45

I kan (men behøves ikke) bruge opgaverne nedenfor til at lære koncepterne bedre. 



### Opgaver 1 - THE HEIST - Access modifiers

```kotlin
// ============================================
// EXERCISE 1: THE HEIST - Access Modifiers
// ============================================
// You're coding a bank vault system for a heist movie simulator.
// The vault has: 
// - A secret combination (only the Vault should know)
// - An alarm system (subclasses like SuperVault need access)
// - A public interface to attempt opening it
// 
// Task: A hacker is trying to break in. They can call tryOpen() with codes,
// but they shouldn't be able to directly read the combination or disable the alarm.
// Add access modifiers to make this secure!

class Vault {
    val secretCombination = "1234"
    var alarmEnabled = true
    var attempts = 0
    
    fun tryOpen(code: String): String {
        attempts++
        if (code == secretCombination && !alarmEnabled) {
            return "💰 VAULT OPENED! You got the money!"
        } else if (attempts >= 3) {
            return "🚨 ALARM TRIGGERED! Police are coming!"
        }
        return "❌ Wrong code. ${3 - attempts} attempts remaining."
    }
}

class HackerAttempt {
    fun breakIn() {
        val vault = Vault()
        
        val secretCode = vault.secretCombination;
      	vault.alarmEnabled = false;
        println(vault.tryOpen(secretCode));
    }
}
```



### Opgave 2 - level 2

Write a class called `Animal`. An `animal` has 3 properties:

- `name`
- `nrOfLegs`
- `isMammal`

Animal has a method: `makeSound()` that prints the sound of the animal

- Create 2 animal classes that extends the Animal class and overrides
  the method to produce their unique sound.
- Create a list, add 5 animals to the list and print every animals sound.
- Override the `toString` method such that if an animal object is printed, it will return a string in the following format: [name=`name`, nrOfLegs=`nrOfLegs`, isMammal=`isMammal`]



### Opgave 3 - level 2

Create a hierarchy of food items in a restaurant menu. Implement a base class called `FoodItem` with properties `name`, `description`, and `price`. 

- Derive three classes `Dessert`, `Appetizer` and `MainCourse` from `FoodItem`. Implement the properties: 
  - `servingSize` for `Appetizer` 
  - `spicinessLevel` for `MainCourse`
  - `isVegan` for `dessert`

- Additionally, implement the method `cook()` for all classes, which print out a message indicating what kind of fooditem is currently being cooked



### Opgave 4 - level 3

Create a class `Person`. A person has a cpr number and name

- A person has a private function that calculates the age of the person by their CPR number
- A person has a field: `age`
  - The field is public and uses the private function to return a result
  - The setter is private, as no one from outside should be able to use the function
- The setter for the CPR number should check if the CPR number is valid before setting it



### Case

Genereret af Claude Code

```kotlin
// ============================================
// MIN STRØM - ELECTRICITY OPTIMIZER APP
// ============================================
// This code was written by a junior developer who just learned Kotlin.
// It WORKS... but the company can't maintain or expand it.
// 
// YOUR MISSION:
// 1. READ the code and understand what it does
// 2. DISCUSS in groups: What are the problems?
// 3. IDENTIFY which OOP principles are violated
// 4. REFACTOR the code using the 4 pillars of OOP
//
// The app helps users decide WHEN to run appliances based on:
// - Current electricity price (kr/kWh)
// - CO2 emissions (green energy vs fossil fuel)
// - User's priority (save money vs save environment)
// ============================================

fun main() {
    // Current electricity data from the grid
    val currentPrice = 2.5 // kr per kWh
    val currentCO2 = 150.0 // grams CO2 per kWh
    
    // ====== WASHING MACHINE ======
    val washerName = "Miele Washing Machine"
    val washerPowerKW = 2.0
    val washerDurationHours = 1.5
    val washerEnergyUse = washerPowerKW * washerDurationHours // 3 kWh
    val washerCost = washerEnergyUse * currentPrice
    val washerCO2 = washerEnergyUse * currentCO2
    val washerIsRunning = false
    var washerCurrentCycleMinutes = 0
    
    println("$washerName:")
    println("  Energy use: $washerEnergyUse kWh")
    println("  Cost now: ${washerCost} kr")
    println("  CO2 emissions: ${washerCO2}g")
    
    if (currentPrice < 1.5 && currentCO2 < 100) {
        println("  ✅ BEST TIME TO RUN - Cheap and green!")
    } else if (currentPrice < 2.0) {
        println("  ⚠️ OK TIME - Reasonable price")
    } else {
        println("  ❌ WAIT - Too expensive and dirty energy")
    }
    println()
    
    // ====== DISHWASHER ======
    val dishwasherName = "Bosch Dishwasher"
    val dishwasherPowerKW = 1.5
    val dishwasherDurationHours = 2.0
    val dishwasherEnergyUse = dishwasherPowerKW * dishwasherDurationHours
    val dishwasherCost = dishwasherEnergyUse * currentPrice
    val dishwasherCO2 = dishwasherEnergyUse * currentCO2
    val dishwasherIsRunning = true
    var dishwasherCurrentCycleMinutes = 45
    
    println("$dishwasherName:")
    println("  Energy use: $dishwasherEnergyUse kWh")
    println("  Cost now: ${dishwasherCost} kr")
    println("  CO2 emissions: ${dishwasherCO2}g")
    
    if (dishwasherIsRunning) {
        println("  🔄 RUNNING - $dishwasherCurrentCycleMinutes minutes remaining")
    } else {
        if (currentPrice < 1.5 && currentCO2 < 100) {
            println("  ✅ BEST TIME TO RUN - Cheap and green!")
        } else if (currentPrice < 2.0) {
            println("  ⚠️ OK TIME - Reasonable price")
        } else {
            println("  ❌ WAIT - Too expensive and dirty energy")
        }
    }
    println()
    
    // ====== ELECTRIC OVEN ======
    val ovenName = "Samsung Electric Oven"
    val ovenPowerKW = 3.5
    val ovenDurationHours = 0.75
    val ovenEnergyUse = ovenPowerKW * ovenDurationHours
    val ovenCost = ovenEnergyUse * currentPrice
    val ovenCO2 = ovenEnergyUse * currentCO2
    val ovenIsRunning = false
    var ovenCurrentCycleMinutes = 0
    val ovenCurrentTemp = 0 // degrees celsius
    val ovenTargetTemp = 200
    
    println("$ovenName:")
    println("  Energy use: $ovenEnergyUse kWh")
    println("  Cost now: ${ovenCost} kr")
    println("  CO2 emissions: ${ovenCO2}g")
    
    if (currentPrice < 1.5 && currentCO2 < 100) {
        println("  ✅ BEST TIME TO BAKE - Cheap and green!")
    } else if (currentPrice < 2.0) {
        println("  ⚠️ OK TIME - Reasonable price")
    } else {
        println("  ❌ WAIT - Too expensive and dirty energy")
    }
    println()
    
    // ====== ELECTRIC CAR CHARGER ======
    val chargerName = "Tesla Wall Charger"
    val chargerPowerKW = 11.0
    val chargerDurationHours = 4.0
    val chargerEnergyUse = chargerPowerKW * chargerDurationHours // 44 kWh
    val chargerCost = chargerEnergyUse * currentPrice
    val chargerCO2 = chargerEnergyUse * currentCO2
    val chargerIsRunning = true
    var chargerCurrentCycleMinutes = 180
    val chargerBatteryPercent = 45
    val chargerTargetBatteryPercent = 80
    
    println("$chargerName:")
    println("  Energy use: $chargerEnergyUse kWh")
    println("  Cost now: ${chargerCost} kr")
    println("  CO2 emissions: ${chargerCO2}g")
    println("  Battery: $chargerBatteryPercent% → $chargerTargetBatteryPercent%")
    
    if (chargerIsRunning) {
        println("  🔄 CHARGING - $chargerCurrentCycleMinutes minutes remaining")
    } else {
        if (currentPrice < 1.5 && currentCO2 < 100) {
            println("  ✅ BEST TIME TO CHARGE - Cheap and green!")
        } else if (currentPrice < 2.0) {
            println("  ⚠️ OK TIME - Reasonable price")
        } else {
            println("  ❌ WAIT - Too expensive and dirty energy")
        }
    }
    println()
    
    // ====== HEAT PUMP ======
    val heatpumpName = "Nibe Heat Pump"
    val heatpumpPowerKW = 2.5
    val heatpumpDurationHours = 8.0 // runs all night
    val heatpumpEnergyUse = heatpumpPowerKW * heatpumpDurationHours
    val heatpumpCost = heatpumpEnergyUse * currentPrice
    val heatpumpCO2 = heatpumpEnergyUse * currentCO2
    val heatpumpIsRunning = true
    var heatpumpCurrentCycleMinutes = 480
    val heatpumpCurrentRoomTemp = 18.5
    val heatpumpTargetRoomTemp = 21.0
    
    println("$heatpumpName:")
    println("  Energy use: $heatpumpEnergyUse kWh")
    println("  Cost now: ${heatpumpCost} kr")
    println("  CO2 emissions: ${heatpumpCO2}g")
    println("  Temperature: ${heatpumpCurrentRoomTemp}°C → ${heatpumpTargetRoomTemp}°C")
    
    if (currentPrice < 1.5 && currentCO2 < 100) {
        println("  ✅ BEST TIME - Cheap and green!")
    } else if (currentPrice < 2.0) {
        println("  ⚠️ OK TIME - Reasonable price")
    } else {
        println("  ❌ EXPENSIVE - Consider lowering target temp")
    }
    println()
    
    // ====== TOTAL COSTS ======
    val totalCostNow = washerCost + dishwasherCost + ovenCost + chargerCost + heatpumpCost
    val totalCO2Now = washerCO2 + dishwasherCO2 + ovenCO2 + chargerCO2 + heatpumpCO2
    
    println("📊 TOTAL IF ALL RUN NOW:")
    println("  Cost: ${totalCostNow} kr")
    println("  CO2: ${totalCO2Now}g")
    
    // What if we wait for night time when prices drop?
    val nightPrice = 0.8 // kr per kWh
    val nightCO2 = 80.0 // more wind power at night
    
    val totalEnergyUse = washerEnergyUse + dishwasherEnergyUse + ovenEnergyUse + 
                         chargerEnergyUse + heatpumpEnergyUse
    val totalCostAtNight = totalEnergyUse * nightPrice
    val totalCO2AtNight = totalEnergyUse * nightCO2
    
    val savings = totalCostNow - totalCostAtNight
    val co2Savings = totalCO2Now - totalCO2AtNight
    
    println()
    println("💡 IF YOU WAIT UNTIL NIGHT (01:00-05:00):")
    println("  Cost: ${totalCostAtNight} kr")
    println("  CO2: ${totalCO2AtNight}g")
    println("  💰 You save: ${savings} kr")
    println("  🌱 You save: ${co2Savings}g CO2")
}

// ============================================
// DISCUSSION QUESTIONS:
// ============================================
// 1. What happens if the company wants to add 10 more appliance types?
//    (Air conditioner, pool pump, sauna, electric heater, etc.)
//
// 2. The calculation logic for "should I run this?" is copy-pasted 5 times.
//    What's the problem with that?
//
// 3. All the data is public (no var/val protection). Could users
//    accidentally break something? What about malicious code?
//
// 4. Some appliances have special properties (oven has temperature,
//    car charger has battery %). How would you organize this?
//
// 5. The company wants to add a "start()" and "stop()" method for all
//    appliances. How much code would you need to write now?
//
// 6. What if users want to customize the price thresholds (1.5 kr, 2.0 kr)?
//    Right now they're hardcoded everywhere!
//
```



