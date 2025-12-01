# Collections framework, ADT, Datastrukturer & `ENUM`



## Overview

- Go through slides



<!--

## Afterclass consideration

- Messy gang
- Den første case var ikke specielt god. For svær. Den ligger heller ikke op til noget oplagt, men er ret svær. 
- Jeg ved ikke helt hvor meget de lærer af at snakke med hinanden om deres kode
- Slidsene var okay, men mangler noget implementation
- Jeg rodede lidt rundt i det idag

-->



## Learning goals

- Collections
- Ordering: Comparable / CompareTo
- Abstract Data Types (ADT):
  - List
  - Set
  - Map



## Preparation

- [Kotlin Collections](https://youtu.be/F8jj7e-_jFA?si=43_nhN_D7tYwtDUQ)
- [HashMap](https://youtu.be/vJvqYFKXo5E?si=kNQQlY7rDit8BK6h)
- [Comparable](https://www.baeldung.com/kotlin/comparable)



## Opgaver



### Pre-exercise

Using the code from your handed in assignment. Present the code for your study mate. Talk about the code technically. What is it doing and why did you do it that way?

Hvis i ikke har fået lavet opgaven, så få ChatGPT til at lave løsningen for en af opgaverne og snak om det.



### Opgave 1 - del 1 - I studiegruppen - 20 min

**Case 1: Sorted City Names for a Travel Agency**

**Scenario:** A travel agency wants to maintain a list of all cities they offer tours to. The system must:

- Ensure city names are stored in alphabetical order.
- Automatically place new cities in the correct order when added.



**Case 2: Managing a Playlist**

**Scenario:** A music streaming app needs to manage a user’s playlist. The playlist:

- Should allow duplicate songs (e.g., a user can add the same song multiple times).
- Must maintain the order of the songs as added.
- Needs efficient random access to any song.



**Case 3: Employee Directory**

**Scenario:** A company wants to store employee records where:

- Each employee has a unique ID (key) and associated details like name and department (value).
- Lookups by ID need to be fast.
- Order of entry is irrelevant.



### Opgave 1 - del 2 - 10 min

Gå sammen med en anden studiegruppe. I skal blive enige om hvilken datastruktur i vil bruge til opgaverne ovenfor

Vi tager en fælles snak på klassen om hvilken datastruktur i har valgt



### Opgave 2 - level 1

- Write a basic dictionary using a HashMap.
- The keys will represent words and the values will be descriptions of the words
- Now add some words to the dictionary with a description. 



### Opgave 3 - level 2

1. Create a class called `SpaceLog`
2. The spacelog should have a `private` HashMap named `spaceLogEntries` to store entries in an astronaut's log. [The key will be the date of the entry](https://www.baeldung.com/kotlin/current-date-time), and the value will be a description of the events that occurred on that date (String).
3. Implement the following functions for the space log:
   - `addLogEntry(date: LocalDate, entry: String)`: Adds a new entry to the log with the specified date and description.
   - `updateLogEntry(date: LocalDate, newEntry: String)`: Updates an existing log entry with a new description for the specified date.
   - `removeLogEntry(date: LocalDate)`: Removes an entry from the log for the specified date.
   - `viewLog()`: Displays all entries in the log, showing the date and corresponding description.
4. Create a main function to test the functionality of the `SpaceLog`:
   - Add several entries to the log using the `addLogEntry` function.
   - Update one of the entries using the `updateLogEntry` function.
   - Remove one of the entries using the `removeLogEntry` function.
   - Display the remaining entries using the `viewLog` function.



### Opgave 4 - level 2

To solve the following exercises you need to understand how to [read text files](https://www.baeldung.com/kotlin/read-file)

- We have users from 3 different platforms ([users-1, users-2, users-3](https://kea-fronter.itslearning.com/Folder/processfolder.aspx?FolderID=1360566)) Ligger på fronter
- We want to know:
  - What users are identical across all platforms
  - What users are only specific to each platform.



### Opgave 5 - Comparable

- Write a class `Student`
- A student has the following fields:
  - Name
  - Email
  - Age
  - Subjects : list
- Implement the comparable interface such that students can be sorted by age
  - Improve the solution such that if students are the same age, they are sorted by amount of subjects
  - I.E A student with the same age as another student is rated "higher" if the have more subjects

<!--

### Opgave 6 - level 2

1. Create a data class named `Book` with the following properties:
   - `title`: The title of the book.
   - `author`: The author of the book.
   - `isbn`: The ISBN (International Standard Book Number) of the book.
   - `price`: The price of the book.
2. Implement a class called `Bookstore` with the following methods:
   - `addBook(book: Book)`: Adds a book to the inventory.
   - `removeBook(isbn: String)`: Removes a book from the inventory based on its ISBN.
   - `searchBookByTitle(title: String): Book?`: Searches for a book in the inventory by its title and returns the book if found, otherwise returns null.
   - `displayInventory()`: Displays all books in the inventory.
3. Create a main function to test the functionality of the `Bookstore` class:
   - Instantiate a `Bookstore` object.
   - Add a few sample books to the inventory.
   - Test adding, removing, searching for, and displaying books in the inventory.

-->



### Opgave 6

We want to analyse [The republic by Plato.](https://kea-fronter.itslearning.com/LearningToolElement/ViewLearningToolElement.aspx?LearningToolElementId=1235821)

- How many times does each word occur?
  - Plato, PlAtO and plato should all count as the same word
- What are the top 10 words that are not in the top 10 of [conjuctions](https://www.grammar-monster.com/lists/list_of_conjunctions.htm)



### Opgave 7 - level 3

- Write a method called `smallWordFilter` that, given a non-`null` `String` (not list!) containing words separated by single spaces (`" "`), returns all the words in the original `String` that are 3 characters or shorter in the same order in which they appeared in the original `String`, as a `List<String>`.

- For example, given the input "Xyz is the very best cat" you would return the `List<String>` containing `{"Xyz", "is", "the", "cat"}`. We have skipped both "very" and "best" because they are longer than 3 characters.

From: https://www.learncs.online/practice/kotlin/small-word-filter-with-list/challen@illinois.edu?returnTo=lists

Hint: https://kotlinandroid.org/kotlin/kotlin-split-string/



### Opgave 8 - level 3

(This question was asked by microsoft for a coding interview)

Given a string and a pattern, find the starting indices of all occurrences of the pattern in the string. For example, given the string "abracadabra" and the pattern "abr", you should return `[0, 7]`.
