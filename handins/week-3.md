# Hand-in 3

**Preface: **These exercises are solved easily by large language models such as ChatGPT. It is highly advised **against usage** of LLM's for the purpose of **generating code** to solve these exercises and would count as **fraud**. It would furthermore defeat the purpose as the following exercises are made to sharpen logical thinking & shape algorithmic understanding.

- Collections



### **1.**

Write a class: *Article*

- An article has an author and a title

Create 5 articles, add them into an ArrayList and print them by overriding the *.toString()* method



<!--

### 2.

Create an interface called `FastFood` (with appropriate methods) and create a `Sandwich` class, a `Pizza` class and a class you decide that implements the `FastFood` interface.

Add some different `Fastfood` objects to an array. Now iterate through that array and use some of the methods you have created above. 



### 3.

Create a class that implements the following interface. Now create two objects using the class created

```java
interface Vehicle {
    changeGear(int a);
    speedUp(int a);
    applyBrakes(int a);
}
```

-->



### 2.

Write a class: *RedditPost*

- A Redditpost has :
  - A date of which is has been posted
  - An author
  - A balance of upvotes / downvotes
  - A Title

When a new instance of RedditPost is instantiated:

- The current date will be generated.
- The balance of upvotes and downvotes starts at 1.
- The title and author has to be provided by the constructor.



Ensure all attributes are private, but accesible by getters & setters.

Implement functionality such that redditposts can be sorted by upvotes/downvotes



### 3

Write a class: *RedditFrontPage*

The RedditFrontPage has:

- A List of all RedditPosts
- A method in RedditFrontPage deletes a RedditPost from the list, by its index number



### 4.

Write a program that takes a list of words as input and prints the frequency of each word.

- Hint: Use a MutableMap

```kotlin
val words = listOf("apple", "banana", "apple", "orange", "banana", "apple", "orange", "banana", "apple","banana", "apple", "orange", "banana","banana", "apple", "orange", "apple", "orange", "banana")
```



### 5.

Create a product inventory system where each product has a name and a quantity. Implement functions to add products, remove products, and display the current inventory.
