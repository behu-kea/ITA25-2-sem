# Working with sensors

Idag skal i selv researche et emne. Det er for at gøre jeg klar til at blive rigtige webudviklere. Det kan godt være lidt angstprovokerende, men husk at jeg er her til at hjælpe jer i processen! 



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

https://github.com/mutualmobile/ComposeSensors



**Androidmanifest.xml**

```xml
<uses-permission android:name="android.permission.VIBRATE" />
```



**Gradle**

```
implementation("com.mutualmobile:composesensors:1.1.2")
```



**Code**

```kotlin
val accelerometerState = rememberAccelerometerSensorState()
Text(
    text = "Force X: ${accelerometerState.xForce}" +
    "\nForce Y: ${accelerometerState.yForce}" +
    "\nForce Z: ${accelerometerState.zForce}" +
    "\nIs Available?: ${accelerometerState.isAvailable}"
)
```

They have lots of different sensors, like Light, Step Detector and Ambient Temperature



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





<!--

**Java android**

For code examples go to: [https://github.com/behu-kea/sensors-android-java](https://github.com/behu-kea/sensors-android-java)

## How sensors work:

In `onCreate` you create a new SensorManager:

```java
sensorManager = (SensorManager) getSystemService(SENSOR_SERVICE);
```



I `onResume` lave en accelerometer vha. SensorManager: 

```java
Sensor accelerometer = sensorManager.getDefaultSensor(Sensor.TYPE_ACCELEROMETER);
```



Tjek om der er en accellerometer og derefter registrer listeneren:

```java
if (accelerometer != null) {
            sensorManager.registerListener(this, accelerometer,
                    SensorManager.SENSOR_DELAY_NORMAL, SensorManager.SENSOR_DELAY_UI);
        }
```



Implementer `SensorEventListener` interfacet og nu får du data fra sensor ved at implementere onSensorChanged metoden



```java
@Override
public void onSensorChanged(SensorEvent event) {
    if (event.sensor.getType() == Sensor.TYPE_ACCELEROMETER) {
        float[] values = event.values;
      	sout(values);
        //textView1.setText("x: "+values[0]+"\ny: "+values[1]+"\nz: "+values[2]);
    } 
}
```



## How location works

First in the `AndroidManifest.xml` file make sure that permissions are asked for:

```xml
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.INTERNET" />
```

Now it works quite like the other sensor:

Create a `LocationManager` like this

```java
locationManager = (LocationManager) getSystemService(Context.LOCATION_SERVICE);
```



Now start location updates using this code 

```java
locationManager.requestLocationUpdates(LocationManager.GPS_PROVIDER, 0L, (float) 0, (LocationListener) this);
```



Implement the `LocationListener` interface. Now in the `onLocationChanged` method get the latitude and longitude

```java
@Override
public void onLocationChanged(Location location) {
    textView1 = (TextView) findViewById(R.id.textView1);
    textView1.setText("Latitude:" + location.getLatitude() + ", Longitude:" + location.getLongitude());
}
```



## How camera works

First create a button and an `ImageView` in the `activity_main.xml`

In `onCreate` get the `ImageView`.



When button to take image with is clicked create a new `cameraIntent` and start the activity

```java
Intent cameraIntent = new Intent(android.provider.MediaStore.ACTION_IMAGE_CAPTURE);
startActivityForResult(cameraIntent, CAMERA_REQUEST);
```

Now when the camera comes back with an image taken the `onActivityResult` gets called. We can now get the data from the image and put into the `ImageView`



```java
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (requestCode == CAMERA_REQUEST) {
        Bitmap photo = (Bitmap) data.getExtras().get("data");
        imageView.setImageBitmap(photo);
    }
}
```

`CAMERA_REQUEST` is just a number that identifies that intent. It could have been literally any number. 



## Ressources



### Sensors

- https://www.youtube.com/watch?v=reDLrzGyAfk&list=PL_CeQH2n4d4FJnPGpcNL8Byk96TGyoNDj
- https://developer.android.com/guide/topics/sensors/sensors_position
- https://developer.android.com/guide/topics/sensors/sensors_motion
- https://developer.android.com/guide/topics/sensors



### Location

Husk at give lokationsadgang til appen!

- https://javapapers.com/android/get-current-location-in-android/



### Camera

- 



-->









