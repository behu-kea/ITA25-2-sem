# Architecture components & MVVM



## Learning goals

- Clean architecture
  - Seperation of concerns
  - Clear responsibilities
- MVVM architecture
  - Model
  - View
  - ViewModel
- Hoisting state



## Preparation

- [MVVM in 100 Seconds](https://youtu.be/-xTqfilaYow?si=KWIuays0YUOqO3Dn)
- [ViewModels & Configuration Changes - Android Basics 2023](https://youtu.be/9sqvBydNJSg?si=Zq2EveH-FIY-VzES)
- [State Hoisting with Jetpack Compose](https://www.youtube.com/watch?v=GT1VJweyNr0)
- [Guide to app architecture](https://developer.android.com/topic/architecture)
-  [Add a ViewModel](https://developer.android.com/codelabs/basic-android-kotlin-compose-viewmodel-and-state?continue=https%3A%2F%2Fdeveloper.android.com%2Fcourses%2Fpathways%2Fandroid-basics-compose-unit-4-pathway-1%23codelab-https%3A%2F%2Fdeveloper.android.com%2Fcodelabs%2Fbasic-android-kotlin-compose-viewmodel-and-state#0) - Optional



## Overview

- Jeg har lavet spørgsmål til eksamen
- Benjamin viser slides og går igennem
  - Clean architecture

  - MVVM
    - Hvad er de forskellige lag

  - State hoisting
    - Hvordan kommer vi fra en stateful komponent over til en der er stateless?
  - Nævn at der er flere måder at håndtere state på
    - `mutableStateOf`
    - `MutableStateFlow`
- Ane præsenterer noget omkring arkitektur



## Topics



### Viewmodels

### Installation

First install the relevant libraries:

To import the ViewModel library add this:

```toml
androidx-lifecycle-viewmodel-compose = { module = "androidx.lifecycle:lifecycle-viewmodel-compose", version = "2.6.2" }
```

To the `Gradle Scripts/libs.versions.toml` file under `[libraries]`



Now in the `build.gradle.kts (module)` add this:

```
implementation(libs.androidx.lifecycle.viewmodel.compose)
```

to the `dependencies {` part!



### Create a viewmodel class

To create a viewmodel class we extend the Viewmodel class as shown here:

```kotlin
class ButtonViewmodel: ViewModel() {
    var count by mutableStateOf(0)
    var buttonText by mutableStateOf("")

    fun onButtonClicked (){
        val randomInt = Random.nextInt(1, 100)
        if(randomInt <= 33) {
            buttonText = "$randomInt is a small number"
        } else if (randomInt <= 66) {
            buttonText = "$randomInt is a medium number"
        } else {
            buttonText = "$randomInt is a large number"
        }

        count++
    }
}
```



### Creating a viewmodel object

Initier dine viewmodels sådan her:

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        setContent {
          // Her laver vi et viewmodel som vi kalder vores App med som argument
            val notesViewModel = viewModel<NotesViewModel>();

            App(notesViewModel);
        }
    }
}
```




## How to save state ChatGPT talk

- [Should You Use Compose State or StateFlow in Your ViewModels?](https://www.youtube.com/watch?v=T8vApYJlW8o)
- [Should i use mutableStateOf, MutableStateFlow or MutableLiveData?](https://chatgpt.com/c/675ae6af-2de8-8008-a841-9b367fce5c80)



## Exercises

### Opgave 1 - Diskussion omkring forberedelse - 10 min

I studiegruppen diskuter følgende:

- Hvad er state hoisting og hvorfor gør vi det?
- Hvad er MVVM



### Opgave 2 - Todo list app arkitektur

Arbejd i studiegrupper!

Vi er hyret ind som IT-arkitekter ved firmaet Todoist. De har promtet sig til en app som de er begyndt at sælge. De oplever desværre bare mange problemer med deres app. 

- Det er svært for dem at tilføje features. 
- Når de skal teste deres app er det vildt besværligt, da de manuelt skal ind og genskabe de use cases der var problemer med.
- Desuden ligger det hele bare i en enkelt fil og det er svært for dem at finde rundt i den

Deres CEO (Michael) har hørt fra en af hans gamle studiekammerater på CBS at Clean Architecture er "The Shit". Studiekammeraten nævnte også noget med MV et eller andet, men det ved CEO'en ikke hvad er. 

Vi skal som it-arkitekter vejlede og hjælpe vores kunde til at komme ud af den knibe de er kommet i.



Appen ligger [her](https://github.com/behu-kea/note-app-mvvm) og der er desværre ikke noget dokumentation til den. 



### Opgaver

1. Finde ud af hvordan appen virker. Gå igennem koden og forstå koden grundigt. Det kan i måske få hjælp til at ChatGPT. I skal kunne forklare hvad der sker i appen!
2. Læg en plan for hvordan i vil restrukturere appen. Lav en kort præsentation til Michael, der viser hvad det er i har tænkt jeg at gøre for a fikse de problemer de har med deres app. Jeg udvælger to grupper der skal præsentere deres plan kl 10:15
3. Fork projektet og lav de ændringer der skal til for at appen følger Clean Architecture tankegangen
4. Kl 11:20 vælger jeg to grupper der skal præsentere deres ændringer
5. Michael sagde at hvis der var tid må i gerne tilføje to features:
   1. Man skal kunne slette et todo item
   2.  Man kan se antal elementer man har tilbage i listen (dem der ikke er krydset ud)




Michael sagde at Todoist bestyrelse var ret obs på at den ny genererede kode ikke var lavet af ChatGPT, da det jo var chatten der havde fået dem i det her rod til at begynde med



*I skal måske lave en `gradle.properties` fil, der skal ligge i roden af projektet. Den skal indeholde den her linje: `android.useAndroidX=true`*

