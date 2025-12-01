# Kotlin learning

[https://kotlinlang.org/docs/home.html](https://kotlinlang.org/docs/home.html)

`val` is like const

`var` is like let



## Loops

Can be done like this

```kotlin
for (i in 0..5) {
    println(i) // 0,1,2,3,4,5   --> upto 5
}
```



## Collections

Array is a part of collections. 

```kotlin
// static number of elements
var names = ListOf("asd", "asd2");
names.add("asdss"); // Error!

// Now it can be changed
var names2 = MutableListOf("asd", "asd2");
names.add("asdss"); 
```



## Classes

`val` property is read only

`var` property is read and write



Can create custom getters like this:



```kotlin
val area: Int // property type is optional since it can be inferred from the getter's return type
	get() = this.width * this.height
```



Or like this

```kotlin
val area get() = this.width * this.height
```



Or custom setters like this

```kotlin
var test = 0
  set(value) { field = 30};
```

Called when the property is set like fx `rectangle.test = 10;`



### Visibility modifiers

```kotlin
open class Outer {
    private val a = 1
    protected open val b = 2
    internal open val c = 3
    val d = 4  // public by default

    protected class Nested {
        public val e: Int = 5
    }
}
```





## What i dont understand



### Nullable

val b: Int = 10000
println(b == b) // Prints 'true'
val boxedB: Int? = b
val anotherBoxedB: Int? = b
println(boxedB == anotherBoxedB) // Prints 'true'



### Unsigned integer types



### Sequences



### MutableList

```kotlin
 MutableList<Person> = mutableListOf()
```

```kotlin
val test = mutableMapOf<String, Int>();
test.put("price1", 10);
```





### Class constructors fully

Something with a primary and a secondary



### Lambda







## This is cool

```kotlin
when (x) {
    in 1..10 -> print("x is in the range")
    in validNumbers -> print("x is valid")
    !in 10..20 -> print("x is outside the range")
    else -> print("none of the above")
}
```





### 
