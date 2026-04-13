# Async with coroutines & retrofit - Online



## Learning goals

- Handling asynchronous code in Kotlin and Compose UI
- `runBlocking`
- Coroutines
  - `suspend`
  - Different ways of launching coroutines
    - `lifecycleScope`
    - `globalScope`
    - `viewModelScope`
    - `CoroutineScope`



## Preparation

- [WHY: Co-Routines](https://youtu.be/ne6CD1ZhAI0?si=0WWltvIn1skCfkV9)
- [WHAT: Co-Routines](https://youtu.be/ShNhJ3wMpvQ?si=cXQfE2A6wYuoxt2v)
- [HOW: Co-Routines](https://youtu.be/kvfpuzSwVZ8?si=6khS1C1za8mts_a3)

(Optional) Documentation
[https://developer.android.com/kotlin/coroutines](https://developer.android.com/kotlin/coroutines)



## Overview

- Concurrency slides
- Show example
- Opgaver
- Students teachers



## Topics



### Coroutines

#### What is it?

Coroutines is Kotlins way of handle asynchronous code. Coroutines simplify complex asynchronous programming by making the code look like normal sequential code while avoiding callback hell.

Coroutine functions can be paused and resumed when needed.



#### Installation

```
implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.3.9")
```

Remember to install viewmodel: [https://behu.gitbook.io/ita24-2.-semester/applikationsudvikling/04-architecture-mvvm#installation](https://behu.gitbook.io/ita24-2.-semester/applikationsudvikling/04-architecture-mvvm#installation)



#### Usage

Coroutines are managed in different scopes. The scopes manage the coroutines. Fx what should happen if the coroutine should be cancelled. What happens with the coroutine if the user closes the app and so on.

- `viewModelScope` - Best for Running coroutines in a `ViewModel`. The coroutine gets automatically cancelled when the viewModel is cleared
- `lifecycleScope` - Running coroutines in `Activity` or `Fragment`. Automatically cancels coroutines when the activity and fragment is destroyed
- `coroutineScope` - Best for custom coroutine scopes that you manage yourself.  Use when you need a custom scope for non-UI related tasks
- `GlobalScope` - This scope should generally be avoided. But is for long-running background work. Coroutine does not get cancelled



#### Dispatchers

 `Dispatchers` control which thread a coroutine runs on.

- `Dispatchers.Default` → CPU-intensive tasks
- `Dispatchers.IO` → Network, database, file I/O
- `Dispatchers.Main` → UI-related work
- `Dispatchers.Unconfined` → Runs in the current thread



Here is an example:

```kotlin
lifecycleScope.launch(Dispatchers.IO) {

}
```



### Creating a delay in kotlin

To create a delay use the `delay` suspend function

You can try and add in inside the `setContent` of `MainActivity`

```kotlin
lifecycleScope.launch {
    Log.d("timer", "Logged before delay call")
    // wait one second
    delay(5000)
    Log.d("timer", "Logged after 5 seconds")
}
```



## Opgaver



### Opgave 1 - Timer app

[Her er starterkoden](https://github.com/behu-kea/konfetti-android) til opgaven



1. Kig koden igennem og forstå den
2. Lav en timer der venter 5 sekunder før den viser konfetti. Funktionaliteten skal laves inde i `ConfettiViewModel.kt`
   1. Gør det først via blocking behavior. Altså hvor UI ikke kan bruges imens vi venter 
   2. Derefter vent i 5 sekunder vha coroutines. 
3. Gør sådan at en bruger kan skrive hvor lang tid der skal ventes før Konfetti skal vises efter der bliver trykket på knappen



### Opgave 2 -  GenAI app

Arbejd videre på jeres Generativ AI app



<!--

Solution

```
package com.example.confetti_timer

import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.lifecycle.ViewModel
import androidx.lifecycle.viewModelScope
import androidx.lifecycle.viewmodel.compose.viewModel
import kotlinx.coroutines.coroutineScope
import kotlinx.coroutines.delay
import kotlinx.coroutines.launch
import kotlinx.coroutines.runBlocking

class ConfettiViewModel: ViewModel() {
    var confettiKey by mutableStateOf(0)
    var timeToWait by mutableStateOf(0)

    fun onButtonClicked() {
//        runBlocking {
//            delay(timeToWait.toLong() * 1000)
//            // Trigger the confetti by incrementing the key
//            confettiKey++
//        }
//
//        viewModelScope.launch {
//            delay(timeToWait.toLong() * 1000) // Non-blocking delay
//            confettiKey++
//        }
    }

    fun onTimeChanged(newTime: String) {
        if(newTime.isNotEmpty()) timeToWait = newTime.toInt()
    }
}
```



Mainactivity

```

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        lifecycleScope.launch(Dispatchers.IO) {

        }

        setContent {
            val confettiViewModel = viewModel<ConfettiViewModel>()

            ConfettitimerTheme {
                ConfettiApp(
                    confettiViewModel.confettiKey,
                    confettiViewModel.timeToWait,
                    confettiViewModel::onButtonClicked,
                    confettiViewModel::onTimeChanged,

                    )
            }
        }
    }
}

@Composable
fun ConfettiApp(confettiKey: Int, timeToWait: Int, onButtonClicked: () -> Unit, onTimeChanged: (String) -> Unit) {
    Box(
        modifier = Modifier.fillMaxSize(),
        contentAlignment = Alignment.Center
    ) {
        Column {
            // Our Button to trigger confetti
            Button(
                onClick = onButtonClicked
            ) {
                Text("Spray Confetti!")
            }

            TextField(onValueChange = onTimeChanged, value = timeToWait.toString())
        }


        // Force re-initialization of KonfettiView whenever confettiKey changes
        key(confettiKey) {
            if(confettiKey!=0) {
                KonfettiView(
                    modifier = Modifier.fillMaxSize(),
                    parties = listOf(
                        Party(
                            speed = 0f,
                            maxSpeed = 30f,
                            damping = 0.9f,
                            spread = 360,
                            colors = listOf(0xfce18a, 0xff726d, 0xf4306d, 0xb48def),
                            position = Position.Relative(0.5, 0.3),
                            emitter = Emitter(duration = 100, TimeUnit.MILLISECONDS).max(100),
                        )
                    )
                )
            }
        }
    }
}
```

-->