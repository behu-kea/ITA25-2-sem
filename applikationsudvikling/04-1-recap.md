# Recap - arbejd på et projekt





## Overview

- Er der emner i vil have jeg skal recappe?
- Vise branches



## Opgaver



### State hoisting

```kotlin

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            Name()
        }
    }
}

@Composable
fun Name() {
    var name by remember { mutableStateOf("") }

    Column(
        modifier = Modifier.padding(16.dp).fillMaxWidth()
    ) {
        Row {
            TextField(
                value = name,
                onValueChange = { name = it }
            )

            Button(onClick = { name = "" }) {
                Text("Clear")
            }
        }
        
        Spacer(modifier = Modifier.height(16.dp))

        Text("Hello $name")
    }
}
```



#### 1. Hoist the state out

Take `name` and move it out of the `Name` component. That means adding it to the parameter

Try and call the function with the new argument in `setContent`



#### 2. Hoist the `onClick` function out

Add the `onClick` function as a parameter to the function

Call the function



#### 2. Hoist the `onValueChange` function out

Add the `onValueChange` function as a parameter to the function. 

**Be aware:** The lambda function should have a parameter that is a string (the new value written in the `TextField`)

Call the function with the new lambda function



### MVVM

Now lets seperate the code into a View and a ViewModel



#### View

Take the composable function called `Name` and put into its own seperate file.

That could be under a `package` called `components`



#### ViewModel

Now comes the tricky part 😱

Firstly in order to get access to viewmodels we it need to install it. Please follow this guide: https://behu.gitbook.io/ita25-2-sem/applikationsudvikling/04-architecture-mvvm#installation



Now we need to do two things:

#### 1. Create the viewModel class

Create a class called `NameViewModel`. That could be under a package called `viewModels`

The `NameViewModel` should inherit from the class `ViewModel`. If you forgot how to do that, go back to the inheritance class



Now move the state variable `name` into `NameViewModel`. Remember to remove `remember` part as we dont need it anymore (when our component is recomposed it does not affect the state variables in `NameViewModel`)



Create two functions in the `NameViewModel` class: `onClearPressed` and `onValueChanged`

The functionality of the functions should come from where the `Name` component gets called



#### 2. Create an object of that `NameViewModel` class

Create an object of the `NameViewModel` in the `MainActivity` under `setContent` like this:

`val nameViewModel = viewModel<NameViewModel>();`

Now the last thing is to reference the state and the functions using `nameViewModel`. Like fx `nameviewModel.name`





### I skal lave en fjollet app idag!

I jeres studiegrupper skal i lave en fjollet app. 



Kravene er at i skal arbejde med læringsmålene for de sidste tre gange. Det vil sige

- Composables
  - Text
  - Button
  - TextField
  - Layout
- State
  - mutableStateOf
  - MutableStateListOf
- MVVM
  - Der skal være en model (klasse)
  - En viewModel der indeholder business logik
  - Nogle views (composable funktioner)



**Kl 11:00 skal projektet være pushet til et github repo**

Nu skal en anden gruppe reviewed jeres kode!

1. Hvad kan forforbedres og hvad fungerer godt?
2. Er IT-Arkitekturen fornuftig? Hvad hvis der nu kommer 100.000 brugere?
3. Er koden nem at forstå?
4. Er der Clean Architecture?



<!--

## Vi skal vibekode idag!

[https://x.com/karpathy/status/1886192184808149383?lang=da](https://x.com/karpathy/status/1886192184808149383?lang=da)



### Fuld vibe aktiveret

I skal vibekode en ide i har i jeres gruppe. Der skal være fuld fokus på bare at smadre kode ud! Fuld Vibe aktiveret! Vibe så hårdt i kan. Ikke noget med at reviewed eller kigge kode igennem, bare smadder derudaf 🚀 Læg koden op på et github repo!



### Reviewe hinandens AI slop

Slop - "low-quality, high-volume, AI-generated text, images, and videos flooding social media and the internet, often created as clickbait to generate  revenue"



I skal nu reviewe en andens gruppes AI projekt 👇

1. Hvad gør koden og hvordan fungerer den? Kan i køre projektet? Hvis ikke skal i brokke jer højlydt til den anden gruppe. Så skal den anden gruppe sige at det virker på deres computer
2. Review koden. 
   1. Hvad kan forforbedres?
   2. Er IT-Arkitekturen fornuftig? Hvad hvis der nu kommer 100.000 brugere?
   3. Er koden nem at forstå?
   4. Er den godt dokumenteret?
   5. Er der skrevet tests?

-->





