# Recap og klar til test

I dag skal i arbejde i studiegrupper



## Overview

Husk at vi bytter stil imorgen!



Test Feedback

- 18 opgaver i gennemsnit klarede i jer igennem

| Part 5 | 8/68    | 11.8% |
| ------ | ------- | ----- |
| Part 4 | 46/136  | 33.8% |
| Part 3 | 53/136  | 39.0% |
| Part 2 | 231/374 | 61.8% |
| Part 1 | 362/476 | 76.1% |

- I har klaret class opgaverne ret fint. God brug af lambda funktioner i filter!

- Helt overordnet brug de funktioner der er tilgængelige i Kotlin. Lav noget research. Sum, average, max, 

- Fedt her:
  ```kotlin
  fun secondLargest(list: List<Int>): Int {
      // Your code here
      return list.sortedDescending()[1]
  }
  ```

- Fedt:
  ```kotlin
  fun findMax(numbers: List<Int>): Int? {
      // Your code here
      return numbers.maxOrNull()
  }
  ```

- Yes
  ```kotlin
  // Create a function that filters out negative numbers from a list.
  fun filterNegativeNumbers(numbers: List<Int>): List<Int> {
      // Your code here
      return numbers.filter { it > 0 }
  }
  ```

- Lugter af when
  ```kotlin
  fun checkNumber(number: Int): String {
      // Your code here
      return if (number > 0) {
          "Positive"
      } else if (number < 0) {
          "Negative"
      } else {
          "Zero"
      }
  }
  ```

- Brug `.average()`
  ```kotlin
  fun averageGrade(): Double {
      return (grades.sum() / grades.size).toDouble()
  }
  ```

- Kan optimeres
  ```kotlin
  fun isEven(number: Int): Boolean {
      if (number % 2 == 0) {
  
          return true
  
      } else return false
  }
  ```
  
- Hvad tænker i om det her?

  ```kotlin
  fun averageGrade(): Double {
      return if (grades.isEmpty()){
          0.0
      } else {
          grades.average()
      }
  }
  ```

- Brug `filter`
  ```kotlin
  fun filterOddNumbers(numbers: List<Int>): List<Int> {
      var oddNumbers = mutableListOf<Int>()
  
      for (number in numbers) {
          if (number % 2 != 0) {
              oddNumbers.add(number)
          }
      }
      return oddNumbers
  }
  ```

- Cadeau for at skrive at man har brugt chat. Kæmpe thumbs up! Det kræver mod og det har den studerende udvist. Vær dog obs på om man også forstår det kode. Kan man forklare hvad der sker
  ```kotlin
  fun charFrequency(str: String): Map<Char, Int> {
      return str
          .filter { it.isLetter() }
          .map { it.lowercaseChar() }
          .groupingBy { it }
          .eachCount() // har fået en del hjælp af chat her
  }
  ```



## Idag

- 10 min - Først sæt en streg ved det emne i har svært ved i [det her dokument](https://ek.itslearning.com/ContentArea/ContentArea.aspx?LocationID=7574&LocationType=1&TextURL=%2fLearningToolElement%2fViewLearningToolElement.aspx%3fLearningToolElementId%3d1493793) (I skal være logget ind)
- 30-45 min - Rapid fire: Jeg går igennem de emner der er flest streger ved.
  - I stiller spørgsmål imens
- 45 min - Arbejde i breakout grupper. Vælger emne i har sværest ved i gruppen
- Pause
- 10 min Fælles på klassen. Nogle grupper præsenterer hvad de har lært, tips og gotchas
- 45 min - Arbejde i breakout grupper. Får tildelt nyt emne.
- Fælles på klassen
- Mulighed for sidste recap fra mig af



Prøv den her. Den stiller 10 spørgsmål og giver en karakter 👉 [CS101 tester (GPT)](https://chatgpt.com/g/g-67a48f9af29081918f433883aae70884-cs101-tester)

