# Recap og klar til test

Idag skal i arbejde i studiegrupper



## Overview

- 10 min - Først sæt en streg ved det emne i har svært ved i [det her dokument](https://studkea-my.sharepoint.com/:w:/g/personal/behu_kea_dk/ERh-tU3hKjZOk5d9c6SAVT8Bcf8CYCZC4gXsWNtHE2blrg?e=xeaZL8) (I skal være logget ind)
- 30-45 min - Rapid fire: Jeg går igennem de emner der er flest streger ved.
  - I stiller spørgsmål imens
- 45 min - Arbejde i breakout grupper. Får tildelt emne i skal arbejde med. 
- Pause
- 10 min Fælles på klassen. Nogle grupper præsenterer hvad de har lært, tips og gotchas
- 45 min - Arbejde i breakout grupper. Får tildelt nyt emne.
- Fælles på klassen
- Mulighed for sidste recap fra mig af



Prøv den her. Den stiller 10 spørgsmål og giver en karakter 👉 [CS101 tester (GPT)](https://chatgpt.com/g/g-67a48f9af29081918f433883aae70884-cs101-tester)





## Handin feedback:

- Ansvar:
  ```kotlin
  class RedditPost (val title: String, val author: String) {
      var voteBalance: Int = 1
  
      companion object { // Forklar dette !!!
          val postList = mutableListOf<RedditPost>() // Fælles liste for alle instanser
  
          fun sortByUpvotes() {
              postList.sortBy {it.voteBalance}
              println("The post have been sorted by ascending!")
              postList.forEach { println("Author: ${it.author} - Title: ${it.title} - Vote Balance: ${it.voteBalance}") } // For hver post i listen skal den print
          }
          
  ```

- Navngivning: `frontPage.rmPost(0)`

- Access modifiers

- `val articles = ArrayList<Article>()`Hvorfor arraylist. det skal give mening. Vi kan stadig sige articles er en liste

- Skide godt. Man kunne også overveje at smide en fejl
  ```kotlin
   fun removeProduct(productName: String) {
          val product = products.find { it.getName() == productName }
          if (product != null) {
              products.remove(product)
          } else {
              println("Product not found: $productName")
          }
      }
  ```

- Tænk over datastrukturer:
  ```kotlin
  class Inventory {
      private val products = mutableMapOf<String, Int>()
  ```

- Der er mange der har problemer med GitHub stadig

- `var ingredients: String,` lugter af liste

- Fail fast:
  ```kotlin
  fun deleteRedditPostByIndex (indexToRemove: Int): Boolean {
          if (indexToRemove in 0 until listOfRedditPosts.size) {
  
              listOfRedditPosts.removeAt(indexToRemove) // remove post at index
  
              println("Removed post at index: $indexToRemove")
              listOfRedditPosts.forEach{println(it)} // print object on its own line
              return true
          } else {
              println("Invalid index, not in scope of listOfRedditPosts size")
              println("Printing original list")
              listOfRedditPosts.forEach{println(it)} // print object on its own line
              return false
          }
      }
  ```

  
