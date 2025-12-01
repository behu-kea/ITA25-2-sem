# Navigation



<!--

## After class considerations

- 

-->



## Learning goals

- Compose navigation
- `Navhost`
- `NavController`
- Backstack



## Overview

- Vise løsningen på todo items: [https://github.com/behu-kea/note-app-mvvm/tree/solution/app/src/main/java/com/example/note_app_mvvm](https://github.com/behu-kea/note-app-mvvm/tree/solution/app/src/main/java/com/example/note_app_mvvm)
- Diskussion om forberedelse
- Small guided meditation through Medito
  - Quick intro to benefits from meditating
  - [https://meditofoundation.org/meditations/beginner-meditation-course](https://meditofoundation.org/meditations/beginner-meditation-course)
- Work on case. Recreate the navigation of the Medito App
- Tænk over hvilken GenAI app i vil lave til næste gang. Vi kommer til at have 2 gange til det



![Meditation benefits](assets/CleanShot-2024-03-14-at-07.27.03.png)



## Preparation

- Today you have prepare for yourself. How you do that is up to you. But you have to be able to go from one screen to another using Jetpack compose navigation
  - In the start of the class i would like to know how you prepared. Youtube? ChatGPT? Articles?



## Navigation

### Installation

Add this to your `build.gradle.kts` file under `dependencies`

```kotlin
val nav_version = "2.8.9"
implementation("androidx.navigation:navigation-compose:$nav_version")
```



### 2 parts

Navigation consists of 3 parts: 

1. `navhost` - Where the navigation will be displayed
2. `navController` - controls the navigation. Fx when goin from one page to another
3. `composable` - shows the different composable that can be navigated to



### `Navhost`

An empty container that displays the composables that are navigated to. Kind of like `index.html` shows different routes in react.

A NavHost is a Composable that displays other composable destinations, based on a given route. 

As you navigate between composables, the content of the `NavHost` is automatically [recomposed](https://developer.android.com/jetpack/compose/mental-model#recomposition).



### `NavController`

An object that manages app navigation within a `NavHost`. The `NavController` orchestrates the swapping of destination content in the `NavHost` as users move throughout your app.



### BackStack

[https://developer.android.com/guide/navigation/backstack](https://developer.android.com/guide/navigation/backstack)

The back stack consists of a stack of navigation screens. Every time you navigate to a new screen, the with fx `navController.navigate("screen1")` the stack new screen is added to the back stack. When the back button is pressed, the latest screen on the backstack is removed (or [poped](https://www.youtube.com/watch?v=o724TbnN4Mk) to be more precise)



### `popBackStack`

We can pop the back stack ourselves by calling `navController.popBackStack()`. This will be like pressing the back button

We can also pop back to a specific route `navController.popBackStack("screen1", false)`. Everything above that route will pop. The second argument specifies if the route itself should also be poped. 



### Sending data from on screen to another

Sending data (arguments) to another route is a bit tricky. Here is how it works:



### First setup the route

First we need to tell Compose that the route can take an argument, we do that in the route by adding the `sendArgumentsHere/{name}`. This is very much like in NodeJS/Express. We now need to tell Compose navigation that the route `sendArgumentsHere` can take some arguments. We do that with the `arguments = listOf(navArgument("name") { type = NavType.StringType })`. Here we tell Compose navigation that it can take one parameter that has a String as a type. 

Now to get the actual argument we write this:

```kotlin
val name = backStackEntry.arguments?.getString("name") ?: return@composable
SendArgumentsHere(name)
```

The first line gets the name argument from the backStack if the name argument is passed. Then we call the `SendArgumentsHere` Composable function with that argument



### Add the argument to the Composable

The Composable function need to take the name argument

```kotlin
@Composable
fun SendArgumentsHere(name: String) {
    Text(text = name)
}
```



### Navigate to the route with a specific name

This is the easy part:

```kotlin
navController.navigate("sendArgumentsHere/Benjamin");
```

Here we send the string `"Benjamin"` to the `SendArgumentsHere` composable function



## Code examples



### Simple navigation between two composables

```kotlin
package com.example.navigation

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.Column

import androidx.compose.material3.Button
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.unit.sp
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import androidx.navigation.compose.rememberNavController

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        setContent {
            val navController = rememberNavController()
            Column {
                Text(
                    text = "Navigation App Example",
                    fontSize = 45.sp
                )
                
                NavHost(navController = navController, startDestination = "home-screen") {
                    composable("home-screen") {
                        HomeScreen("benjamin",
                            onScreen2ButtonClick = {
                                navController.navigate("screen-2")
                            })
                    }
                    composable("screen-2") {
                        Screen2(onBackButtonClick = {
                          	// This will go back to the home-screen
                            navController.popBackStack()
                        })
                    }
                }
            }
        }
    }
}

@Composable
fun HomeScreen(name: String, onScreen2ButtonClick: () -> Unit) {
    Column {
        Text(
            text = "Screen 1",
            fontSize = 32.sp
        )
        Text(
            text = "Hello $name!"
        )
        Button(onClick = onScreen2ButtonClick) {
            Text("Go to Screen 2")
        }
    }
}

@Composable
fun Screen2(onBackButtonClick: () -> Unit) {
    Column {
        Text(
            text = "Screen 2!",
            fontSize = 32.sp
        )
        Button(onClick = onBackButtonClick) {
            Text("Back")
        }
    }
}
```



### Sending arguments from one screen to another

```kotlin
package com.example.navigation

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.Column
import androidx.compose.material3.Button
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.unit.sp
import androidx.navigation.NavType
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import androidx.navigation.compose.rememberNavController
import androidx.navigation.navArgument

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        setContent {
            val navController = rememberNavController()
            Column {
                Text(
                    text = "Navigation App Example",
                    fontSize = 45.sp
                )
                NavHost(navController = navController, startDestination = "home-screen") {
                    composable("home-screen") {
                        HomeScreen("benjamin",
                            onArgumentsButtonClick = {
                                val stringToSend = "Benjamin"
                                // this is how the "url" will look: sendArgumentsHere/Benjamin
                                navController.navigate("sendArgumentsHere/${stringToSend}")
                            })
                    }
                    composable("sendArgumentsHere/{name}", arguments = listOf(navArgument("name") { type = NavType.StringType })) { backStackEntry ->
                        val name = backStackEntry.arguments?.getString("name") ?: return@composable
                        SendArgumentsHere(name)
                    }
                }
            }
        }
    }
}

@Composable
fun HomeScreen(name: String, onArgumentsButtonClick: () -> Unit) {
    Column {
        Text(
            text = "Screen 1",
            fontSize = 32.sp
        )
        Text(
            text = "Hello $name!"
        )
        Button(onClick = onArgumentsButtonClick) {
            Text("To arguments screen")
        }
    }
}

@Composable
fun SendArgumentsHere(name: String) {
    Text(text = "This is from the arguments: $name")
}
```



## 📝 Discuss preparation in class - 10 min

How is navigation done in Compose UI?



## 📝 Case - Recreate the Medito app

In this case you will recreate the navigation of the Medito App. Todays focus should be on the navigation part and not the design of the app. The design can be very crude and that is fine

For the case you can download the Medito app ([Link here](https://meditofoundation.org/medito-app)) or follow the screenshots below. 

Medito Foundation is a nonprofit dedicated to improving mental wellbeing and helping people cope better with depression, stress, anxiety, and  any other negative states of mind. They have created a free app that gives you tons of really good meditations to try out. 



### 1 - Dashboard - Level 1

First create a `Composable` that shows the dashboard. Dont focus on design, but more the content.



![Medito welcome screen](assets/Screenshot_20240122-133014.png)

### 2 - Downloads - Level 2

From the Dashboard clicking on `Downloads` should take you to this view. Again dont spend too much time on design, but more on creating a `Donwloads` `Composable` that is activated when clicking on `Downloads`

![Downloads](assets/downloads.png)

### 3 - Explore - Level 2

Clicking on `Explore` Will take you to this view. There is a back button, a `TextField` and a list of `Meditations`

Make the back button work and make the items in the list clickable. 

You can simplify this by not using a `List` of meditations, but just have individual `Composable`'s on top of each other!

![Explore screen](assets/Screenshot_20240122-133116.png)

### 4 - Meditation group - Level 2/Level 3

Clicking on one of the Meditations from above will take you to one of these views. 

**Level 2** - Here you navigate to a `Composable`  fx. called `BodyScan`. You can then make individual composables for each item in the list above (or as many as see fit)

**Level 3** - Make a `Composable` that is more general that can receive the clicked item. Maybe you call it `MeditationOverview`. That composable needs a title, image, description and list of meditations. Now to send these attributes as an object is not best practice, neither is sending an image: [https://stackoverflow.com/questions/67121433/how-to-pass-object-in-navigation-in-jetpack-compose](https://stackoverflow.com/questions/67121433/how-to-pass-object-in-navigation-in-jetpack-compose) More official details [here](https://stackoverflow.com/a/69060224/2263329). 

So how can we fix this problem?

<!-- Therefore instead when you click on a topic above, you only send the id of the topic. Then you have another `List` or `Map` that keeps track of the topics list `List<Topics>` -->



![Screenshot_20240122-133122](assets/Screenshot_20240122-133122.png)



### 5 - Finish the app navigation

Clicking a meditation will take you to the meditation composable.

![Screenshot_20240122-133128](assets/Screenshot_20240122-133128.png)



Clicking play will take you to the player

![Screenshot_20240122-133137](assets/Screenshot_20240122-133137-6107403.png)

