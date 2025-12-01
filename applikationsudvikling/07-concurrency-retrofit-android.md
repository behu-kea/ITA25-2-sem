# Async with coroutines & retrofit



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



## Opgaver

<!--

### Opgave 1 - Procrastination App

Brug starterkoden nedenfor og implementer følgende i koden:

1. **Blocking Delay:** Implementer en function ved brug af `runBlocking`, som venter 5 sekunder, før den viser en reminder.
2. **Non-Blocking Delay:** Implementer en function ved brug af `lifecycleScope.launch` and `delay()`, som venter 5 sekunder, før den viser en reminder.
3. **User Input:** Gør sådan at en bruger kan skrive, hvor lang tid der skal ventes, før en reminder skal vises.
4. (Optional) Få appen til at tjekke om en task er blevet skrevet ned før den procrastinater. Er der ikke skrevet nogen task, så skal der vises en besked i 3 sekunder, som fortæller at denne ikke kan procrastinate uden en task er blevet skrevet ned.

Kopier denne starterkode ind i jeres `MainActivity.kt`:

```kotlin
package com.example.coroutines_exercise // Udskift med jeres egen package path
  
import android.os.Bundle  
import androidx.activity.ComponentActivity  
import androidx.activity.compose.setContent  
import androidx.activity.enableEdgeToEdge  
import androidx.compose.foundation.layout.Arrangement  
import androidx.compose.foundation.layout.fillMaxSize  
import androidx.compose.foundation.layout.padding  
import androidx.compose.material3.Scaffold  
import androidx.compose.material3.Text  
import androidx.compose.runtime.Composable  
import androidx.compose.ui.Modifier  
import androidx.compose.ui.tooling.preview.Preview  
import com.example.coroutines_exercise.ui.theme.CoroutinesexerciseTheme  
import androidx.compose.foundation.layout.Column  
import androidx.compose.material3.Button  
import androidx.compose.material3.MaterialTheme  
import androidx.compose.material3.Surface  
import androidx.compose.material3.TextField  
import androidx.compose.runtime.getValue  
import androidx.compose.runtime.mutableStateOf  
import androidx.compose.runtime.remember  
import androidx.compose.runtime.setValue  
import androidx.compose.ui.Alignment  
import androidx.compose.ui.unit.dp  
import androidx.lifecycle.ViewModel  
import androidx.lifecycle.viewmodel.compose.viewModel  
import kotlin.random.Random  
  
class MainActivity : ComponentActivity() {  
    override fun onCreate(savedInstanceState: Bundle?) {  
        super.onCreate(savedInstanceState)  
        enableEdgeToEdge()  
        setContent {  
            CoroutinesexerciseTheme {  
                ProcrastinationScreen()  
            }  
        }    }  
}  
  
@Composable  
fun ProcrastinationScreen() {  
    val viewModel: ProcrastinationViewModel = viewModel()  
  
    Column(  
        modifier = Modifier  
            .fillMaxSize()  
            .padding(16.dp)  
            .padding(bottom = 100.dp),  
        horizontalAlignment = Alignment.CenterHorizontally,  
        verticalArrangement = Arrangement.Center  
    ) {  
        TextField(  
            value = viewModel.task,  
            onValueChange = {  
                viewModel.updateTask(it)
            },  
            label = { Text("Task that needs to be done") },  
            modifier = Modifier.padding(bottom = 16.dp)  
        )  
  
        Button(onClick = {  
            viewModel.showMessage()  
        }) {  
            Text("Procrastinate!")  
        }  
  
        // Reminder  
        if (viewModel.message.isNotEmpty()) {  
            Text(  
                text = viewModel.message,  
                modifier = Modifier.padding(top = 16.dp)  
            )  
        }  
    }  
}  
  
class ProcrastinationViewModel : ViewModel() {  
    private var _message by mutableStateOf("")  
    val message: String get() = _message  
  
    private var _task by mutableStateOf("")  
    val task: String get() = _task  
  
    fun updateTask(newTask: String) {  
        _task = newTask  
    }  
  
    fun showMessage() {  
        _message = getRandomMessage()  
    }  
  
    private fun getRandomMessage(): String {  
        val messageOptions = listOf(  
            "Hey! Remember that '[Task]' you were supposed to be doing? Yeah, time's up (sort of). Maybe just...one more cat video?",  
            "Procrastination successful! You've successfully avoided '[Task]' for a few moments. High five! Now, maybe consider actually doing it?",  
            "The universe has spoken. It says: '[Task]'. Just kidding... mostly. But seriously, maybe?",  
            "Congratulations! You've unlocked the 'Few Moments Procrastination Achievement' for '[Task]'. What's next? Level 2?",  
            "Psst... it's been a few moments. '[Task]' is still waiting for you. Don't make it sad." )  
        val randomIndex = Random.nextInt(messageOptions.size)  
        return messageOptions[randomIndex].replace("[Task]", _task)  
    }  
}  

@Preview(showBackground = true)  
@Composable  
fun ProcrastinationScreenPreview() {  
    ProcrastinationScreen()  
}
```

-->



### Opgave 1 - Timer app

1. Kig koden igennem og forstå den
2. Lav en timer der venter 5 sekunder før den viser konfetti. Funktionaliteten skal laves inde i `ConfettiViewModel.kt`
   1. Gør det først via blocking behavior. Altså hvor UI ikke kan bruges imens vi venter 
   2. Derefter vent i 5 sekunder vha coroutines. 
3. Gør sådan at en bruger kan skrive hvor lang tid der skal ventes før Konfetti skal vises efter der bliver trykket på knappen



[Her er starterkoden](https://github.com/behu-kea/konfetti-android) til opgaven



### Opgave 2 - Arbejd videre på din GenAI app

Arbejd videre med din GenAI app. Fokuser på repository pattern og suspend funktioner



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