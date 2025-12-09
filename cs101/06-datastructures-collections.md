# Collections framework, ADT, Datastrukturer & `ENUM`



## Overview

- Go through slides



<!--

## Afterclass consideration

- Slidsene var okay, men mangler noget implementation

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



### Opgave 1 - del 1 - I studiegruppen - 20 min

For hver meeting skal i vælge en datastruktur og skrive kort hvorfor i har valgt den i har



📝 **Meeting 1 — The Bakery Order Queue**

A bakery wants a system to manage **orders that come in throughout the day**.
 They mainly need to:

- Always serve **the first order that came in**
- Occasionally inspect the next 1–2 orders
- New orders come in frequently
- They rarely need to jump to order *#50*, *#100*, etc.



📝 **Meeting 2 — VIP Guest List for a Music Festival**

A festival needs to maintain a **VIP guest list** where:

- **No duplicate names** are allowed
- Order **does not matter**
- They need to quickly check whether a name is on the list



📝 **Meeting 3 — Tracking User Preferences in an App**

An app stores settings like:

```
theme = "dark"
fontSize = 16
notifications = true
language = "en"
```

Requirements:

- Each preference has a **unique key**
- They need to quickly find a preference by key
- Order does **not** matter



📝 **Meeting 4 — Recently Viewed Products on a Webshop**

The webshop needs to show a customer’s **recently viewed products** in the exact order viewed.

Requirements:

- No duplicates
- Must preserve order
- Fast membership checks ("have they seen this product before?")



📝 **Meeting 5 — Playlist System for a Music App**

Users should be able to:

- Add songs to the playlist
- Jump to any song by index
- Occasionally insert songs in the **middle**
- Order matters
- Duplicates are allowed



📝 **Meeting 6 — Inventory System for a Warehouse**

The warehouse stores items like this:

- Each item has a **unique ID**
- They must keep insertion order (for audit purposes)
- They also need **fast lookup by ID**



📝 **Meeting 7 — Undo/Redo History for a Text Editor**

The text editor stores actions:

- You must always remove the **newest** action first ("undo")
- You only need linear access and occasional iteration
- Insertions/deletions at the head must be fast



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
  - Subjects: List
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
