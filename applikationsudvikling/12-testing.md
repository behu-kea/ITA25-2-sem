# Testing



## Overview

- Min Strøm aflevering på søndag
- Præsentation på torsdag



### Eksamen

Minimum for at bestå:

- Klasser og objekter
- Big O & Datastrukturer
- Lambda funktioner, trailing lambda
- Composables
- Recomposition & state
- Git 



### Næste niveau

- Navigation
- Algoritmer
- 



https://katalog.kea.dk/course/4111201/2024-2025



## Preparation

- [https://developer.android.com/jetpack/compose/testing](https://developer.android.com/jetpack/compose/testing) (se video læs om Semantics, Setup og Testing APIs)
- [Writing Our First Unit Tests - Testing on Android - Part 3](https://youtu.be/W0ag98EDhGc?si=3lCv9r2_EFXq3tAL)



Testing er en del af kvalitetssikringen af jeres app.

Three types of tests:

1. Unit tests - single units. Fx function `getSum` 
2. Integration tests - How two components work together. Interaction betwen components
3. UI tests/end-to-end - Whole interaction. Log in, then click a button etc



TDD - Test driven development. Write tests first. Then start developing code. Could maybe be huge in the age of AI



### Testing folders

`androidtest` vs `test` folder

`androidtest` - Everything that runs on the emulator or need some android context

`test` - Everything else. Fx testing a `getSum` function does not need android



## Unit test

In a unit test we test that sum function works as expected. In the following example we have two tests: 

1. One where we check that an addition works
2. One where we check a sum function we have created

```kotlin
fun getSum(list: List<Int>): Int {
    return list.sum()
}

class ExampleUnitTest {
    @Test
    fun `Addition works`() {
        assertEquals(4, 2 + 2);
    }

    @Test
    fun `Sum function works`() {
        val list = listOf(1, 2, 3);
        val sum = getSum(list);
        assertEquals(6, sum);
    }
}
```

For each test we add the `@Test` annotation followed by a function with the thing we want to test. To test something we use the `assertEquals` function. The first argument is what we expected, the next is the actual result. With this line: `assertEquals(6, sum);` we say that we expect the value of the `sum` variable to be 6



### `@Before` and `@After`

If we want some code to run before each test is run

```kotlin
@Before
fun setup() {
	// do something here
}
```



After is usually meant to destroy objects or close database connections

```kotlin
@After
fun teardown() {
	// do something here
}
```



## UI tests

These are teste that test the ui more than the functionality. That means we write code that clicks buttons, writes text in input fields and check if the right elements are on the page



To create a UI test we must first create a rule that we can use to interact with our app

```kotlin
@get: Rule
val rule = createComposeRule()
```

you could say that `rule` is kind of like `document` in javascript. With the `document` we can get elements, click and set text in input fields. 



### Create a test

To create a test write the `@Test` annotation before a function. This function will now be part of your tests. 

First we have to specify what content we are testing. We can test the full application, but we can also just test a `@Composable`. 

```kotlin
rule.setContent { AppNavigation(notesViewModel); }
```

`AppNavigation(notesViewModel)` is a `Composable`



#### Getting a node

When we have defined the content we need to start selecting some elements. In javascript we did this with `document.querySelector` . Using a `rule` we do that with `rule.onNodeWithText("Add new note")`. Here we get a node that has the text `Add new note`. 



We can also select a node anothe way like this:

```kotlin
rule.onNode(
	hasText("Add new note")
	and
	hasClickAction()
)
```



We can also use tags like this

```kotlin
Button(
    onClick = { /* Do something */ },
    modifier = Modifier.testTag("myButtonTag")
) {
    Text("Click Me")
}
```



```kotlin
val buttonTag = composeTestRule.onNodeWithTag("myButtonTag")
```



#### Create some action

When we have a node, we can create an action on that note, fx click it, write text in the node etc.

Here we click a node

```kotlin
rule.onNodeWithText("Add new note")
	.performClick()
```



Here we write some text in a node

```kotlin
rule.onNodeWithText("Title")
	.performTextInput("olol")
```



#### Check stuff

Now we can check if some node was created with our action:

```kotlin
rule.onNodeWithText("olol")
	.assertExists()
```



#### Full example

Here is an example of a test that tests that creating a new node works as expected

```kotlin
@Test
fun addNote() {
    rule.setContent { AppNavigation(notesViewModel); }

    rule.onNodeWithText("Add new note")
        .performClick()

    rule.onNodeWithText("Title")
        .performTextInput("olol")

    rule.onNodeWithText("Content")
        .performTextInput("olol1")

    rule.onNodeWithText("Save note")
        .performClick()
  	
  	// Wait until compose is done changing screen
  	rule.waitForIdle()

    rule.onNodeWithText("olol")
        .assertExists()
}
```



Read more about UI testing in compose here: [https://developer.android.com/jetpack/compose/testing](https://developer.android.com/jetpack/compose/testing)



## Exercises

I skal lave nogle tests på en app i har lavet i kurset. Det oplagte ville være Min Strøm appen. 

Hvis i ikke er kommet så langt med Min Strøm, kan i bruge Note appen i har lavet.  

Ellers kan i finde Note appen med alle features [her](https://github.com/behu-kea/ita-23-2-sem-code/tree/for-testing-lecture/noteapp). I skal lige have firebase tilkoblet. Det kan i læse om under firebase gangen.



### Manual Exploratory Testing

I skal finde bugs og fejl i jeres applikation igennem manuel eksplorativ testing, ligesom Stefanos fra Framna snakkede om

- Test every feature you just developed thoroughly

- Think out-of-the box and test edge cases
  - What if the network is slow
  - What if the request fails
  - What if the result is empty
  - What if the app is paused and opened again
  - What if the app is killed and opened again
  - What if you get logged out (401)



### Unit tests

Lav nogle Unit tests for den app i har valgt.



### UI tests

Lav nogle UI tests for den app i har valgt.



### Fortsæt Min Strøm appen



<!--

## Notes app

For the notes app we were working on last time, lets write some tests for that app. The repo can be found [here](https://github.com/behu-kea/ita-23-2-sem-code/tree/for-testing-lecture/noteapp) with all features implemented. We will be focusing on UI tests



### UI tests

You have to write some ui tests that test the following:

- Clicking on a note in the overview will take you to the right note
- When creating a new note that note will show up in the overview
- When searching for a note the correct notes will be shown in the overview
- Deleting a note will delete it from the overview



-->



<!--

```
class UiTester {
    @get: Rule
    val rule = createComposeRule()

    val notesViewModel: NotesViewModel = NotesViewModel()

    @Test
    fun addNote() {
        rule.setContent { AppNavigation(notesViewModel); }

        rule.onNodeWithText("Add new note")
            .performClick()

        rule.onNodeWithText("Title")
            .performTextInput("olol")

        rule.onNodeWithText("Content")
            .performTextInput("olol1")

        rule.onNodeWithText("Save note")
            .performClick()

				rule.waitForIdle()

        rule.onAllNodesWithText("olol")
            .get(0).assertExists()
    }
}
```

-->





I need to create a signup page for my site using Supabase.

I need these fields:

- Email
- School
- Education
- Name
