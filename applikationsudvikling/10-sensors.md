# Working with sensors

Idag skal i selv researche et emne. Det er for at gøre jeg klar til at blive rigtige webudviklere. Det kan godt være lidt angstprovokerende, men husk at jeg er her til at hjælpe jer i processen! 



## Overview

- Snakke eksamen lav en mineksamen



<!--

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



https://katalog.kea.dk/course/4111201/2024-2025

-->



## Sådan researcher jeg

1. Big picture gerne med noget youtube eller ChatGPT
   1. Får overblikket
   2. Hvad kan teknologien?
   3. Hvilke forskellige dele findes der?
   4. Måske tidlig kig på lidt syntax
   5. ChatGPT explain like i am five. Explain in a pedagogical easy to understand way. Use metaphors i already
2. Dykker nærmere ned i teknologien
   1. Hvordan virker de forskellige dele
   2. Bruger den viden jeg allerede har. Kan jeg relatere det til noget jeg ved nu? Minder det om noget jeg har lært før? Fx via ChatGPT. Er `Spacer` komponenten ligesom `<br>` i html?
   3. Forskellige vinkler. Se 3 forskellige youtube videoer, læse en medium artikel, spørge ChatGPT. Nærmer den viden sig hinanden? Er de enige om det hele?
3. Koge det jeg skal lære ned til det mindste kode jeg kan skrive og få det på GitHub. Dokumenter den kode. 
4. Tag noter mens jeg researcher (de noter kan i se i de fleste af mine gange)



## Forbinde android telefon til Android Studio

1. Gå til `Settings` -> `About Phone`
2. Tryk 7 gange på der hvor der står `Build number`
3. Go to developer settings by pressing `System -> Developer options -> Enable USD debugging`
4. Press `Allow`

Now in Android Studio Select the phone and press play. That's it! 



## Class overview

08:30 - 10:00 - Investigate your topic

10:00 - 10:15 - Break

10:15 - 10:45 - Presentations

10:45 - 11:30 - Exercises

11:30 - 11:45 - Recap



### Investigate your topic

The first 1.5 hours you have to investigate one of the technologies below. Here are some of the things you have to consider:

1. How does the technology work in a non technical way? What is it doing? Why is it smart? When should i use it?
2. How do i implement the technology in Android Studio using kotlin? Create a small prototype and push the code to GitHub
3. Make a 5-10 minute presentation focusing on your topic
4. Create a fun exercise that a group can spend about 45 minutes on
   1. Remember to make the first steps of the exercise super easy!



Here are the topics:

1. Accelerometer
2. Position (latitude and longitude)
3. Notification
4. Camera - Level 3



<!--

### Camera

https://www.youtube.com/watch?v=GRHQcl496P4

https://github.com/behu-kea/ita-23-2-sem-code/tree/for-testing-lecture/workingwithsensors/app/src/main/java/com/example/working_with_sensors

Tjek her. Især husk gradle!



**Kotlin compose ui**

Add this to the `AndroidManifest.xml` file.

This gives access to the camera

```xml
<uses-feature
    android:name="android.hardware.camera"
    android:required="false" />

<uses-permission android:name="android.permission.CAMERA" />
```



### Accelerometer

https://github.com/ricknout/compose-sensors



### Location

**Gradle**

```
implementation("com.google.android.gms:play-services-location:21.1.0")
implementation("com.google.accompanist:accompanist-permissions:0.35.0-alpha")
```



**Manifest.xml**

```kotlin
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```



```kotlin
package com.example.working_with_sensors

import android.Manifest
import android.annotation.SuppressLint
import android.content.Context
import android.content.pm.PackageManager
import android.hardware.Sensor
import android.hardware.SensorManager
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.rememberLauncherForActivityResult
import androidx.activity.compose.setContent
import androidx.activity.result.contract.ActivityResultContracts
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.material3.Button
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Surface
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.runtime.LaunchedEffect
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.viewinterop.AndroidView
import androidx.core.app.ActivityCompat
import androidx.core.content.ContextCompat
import com.example.working_with_sensors.ui.theme.WorkingwithsensorsTheme
import com.google.accompanist.permissions.ExperimentalPermissionsApi
import com.google.accompanist.permissions.rememberMultiplePermissionsState
import com.google.android.gms.location.LocationServices
import com.google.android.gms.location.Priority
import com.google.android.gms.tasks.CancellationTokenSource
import com.mutualmobile.composesensors.rememberAccelerometerSensorState

class MainActivity : ComponentActivity() {

// Optional: You could also write: rememberAccelerometerSensorState(sensorDelay = SensorDelay.Fastest) for fetching sensor data faster



    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        setContent {
            WorkingwithsensorsTheme {
                // A surface container using the 'background' color from the theme
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    //Accellerameter()
                    LocationScreen()
                }
            }
        }
    }
}

@Composable
fun Accellerameter() {
    val accelerometerState = rememberAccelerometerSensorState()
    Text(
        text = "Force X: ${accelerometerState.xForce}" +
                "\nForce Y: ${accelerometerState.yForce}" +
                "\nForce Z: ${accelerometerState.zForce}" +
                "\nIs Available?: ${accelerometerState.isAvailable}"
    )
}


@Composable
fun LocationScreen() {
    val context = LocalContext.current
    var location by remember { mutableStateOf("Your location") }

    // Create a permission launcher
    val requestPermissionLauncher =
        rememberLauncherForActivityResult(
            contract = ActivityResultContracts.RequestPermission(),
            onResult = { isGranted: Boolean ->
                if (isGranted) {
                    // Permission granted, update the location
                    getCurrentLocation(context) { lat, long ->
                        location = "Latitude: $lat, Longitude: $long"
                    }
                }
            })

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Button(
            onClick = {
                if (hasLocationPermission(context)) {
                    // Permission already granted, update the location
                    getCurrentLocation(context) { lat, long ->
                        location = "Latitude: $lat, Longitude: $long"
                    }
                } else {
                    // Request location permission
                    requestPermissionLauncher.launch(android.Manifest.permission.ACCESS_FINE_LOCATION)
                }
            }
        ) {
            Text(text = "Allow")
        }
        Spacer(modifier = Modifier.height(16.dp))
        Text(text = location)
    }
}

private fun hasLocationPermission(context: Context): Boolean {
    return ContextCompat.checkSelfPermission(
        context,
        android.Manifest.permission.ACCESS_FINE_LOCATION
    ) == PackageManager.PERMISSION_GRANTED
}

private fun getCurrentLocation(context: Context, callback: (Double, Double) -> Unit) {
    val fusedLocationClient = LocationServices.getFusedLocationProviderClient(context)
    if (ActivityCompat.checkSelfPermission(
            context,
            Manifest.permission.ACCESS_FINE_LOCATION
        ) != PackageManager.PERMISSION_GRANTED && ActivityCompat.checkSelfPermission(
            context,
            Manifest.permission.ACCESS_COARSE_LOCATION
        ) != PackageManager.PERMISSION_GRANTED
    ) {
        // TODO: Consider calling
        //    ActivityCompat#requestPermissions
        // here to request the missing permissions, and then overriding
        //   public void onRequestPermissionsResult(int requestCode, String[] permissions,
        //                                          int[] grantResults)
        // to handle the case where the user grants the permission. See the documentation
        // for ActivityCompat#requestPermissions for more details.
        return
    }
    fusedLocationClient.lastLocation
        .addOnSuccessListener { location ->
            if (location != null) {
                val lat = location.latitude
                val long = location.longitude
                callback(lat, long)
            }
        }
        .addOnFailureListener { exception ->
            // Handle location retrieval failure
            exception.printStackTrace()
        }
}
```

-->













