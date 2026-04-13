# Data from the internet - Retrofit



## Learning goals

- `interface`
- Retrofit
  - Sending http requests with Retro
    - Get, post, put, update, delete
  - Getting data into models



## Preparation

- [Learn Kotlin for Android: Interfaces (Lesson 20)](https://www.youtube.com/watch?v=RctW18zpgec)
- https://developer.android.com/codelabs/basic-android-kotlin-compose-getting-data-internet#5
  - 4, 5, 6, 7, 8
- [The Ultimate Retrofit Crash Course](https://youtu.be/t6Sql3WMAnk?si=RAlDRMktVSe3PAdD) - *optional*



## Overview

- [https://www.youtube.com/@Fireship](https://www.youtube.com/@Fireship)
- Go through slides
- Opgaver
- Kl 10:00 teacher students



## Topics



### Interface

An interface works a lot like a contract or a set of rules. In an interface we define attributes and functions a class should have to implement that specific interface. 

Lets get concrete:

This Interface defines what it is like to be a `Product`. That means that classes implementing this interface **has to have** 

- An attribute called `name` which is a `String`
- An attribute called `price` which is an `Int`
- An attribute called `name` which is an `Int`
- An function called `printProductDetails` 

```kotlin
interface Product {
    val name: String;
    val price: Int;
  	val id: Int;
    fun printProductDetails();
}
```

Here is how an `interface` gets implemented by a class

```kotlin
class Television(
    override val name: String,
    override val price: Int,
    override val id: Int
) : Product {
    override fun printProductDetails() {
        TODO("Not yet implemented")
    }
}
```

Let's initialise a television

```kotlin
val samsungTelevision: Television = Television("Samsung TV", 8000, 123456789);
```

We use the `override` keyword because we are overwriting a property from the interface we are implementing

We can even add functionality inside of the interface:

```kotlin
interface Computer{
    val name: String;
    val price: Int;
    val location: Map<String, Double>;

    fun printLocation() {
        println("${this.name} is an amazing television");
    };
}
```

Now we dont need to override the `printLocation` method because it has been defined

A class can inherit from only one class but can implement mutiple interfaces







### Getting internet to work

Reference: [https://github.com/nicklasdean/catfacts-app](https://github.com/nicklasdean/catfacts-app)

**Important**

- Insert the following into your `AndroidManifest.xml`
  - Found in the manifests folder

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

- Insert before the <application tag

```xml
// Like this

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">
    <uses-permission android:name="android.permission.INTERNET" />

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"                             
...
```



### Install retrofit2

Add this to the module gradle file under dependencies

```
// Retrofit
implementation("com.squareup.retrofit2:retrofit:2.9.0")
// Retrofit with Scalar Converter
implementation ("com.squareup.retrofit2:converter-gson:2.9.0")
```



### Retrofit HTTP Client

Retrofit is a popular HTTP client library in Kotlin that simplifies sending HTTP requests and processing API responses. It uses annotations to define the HTTP operations and converts JSON to Kotlin objects automatically.



#### API Interface

The API interface in Retrofit defines the endpoints of your API. It acts as a contract that specifies the HTTP operations your app can perform. Annotations like `@GET`, `@POST`, etc., specify the type of HTTP request.



**Example:**

```kotlin
interface CatFactsApi {
    @GET("/fact")
    suspend fun getFact(): CatFact
}
```

**Explanation:**

- `@GET("/fact")`: This defines an HTTP GET request to the `/fact` endpoint.
- `suspend fun getFact()`: A suspend function is used for coroutine-based asynchronous requests.
- The return type, `CatFact`, is a Kotlin data class that represents the response.



#### Model / Data Transfer Object (DTO)

The model, also known as a Data Transfer Object (DTO), represents the structure of the data received from or sent to the API. Retrofit automatically maps JSON responses to these data classes using libraries like Gson or Moshi.

**Example:**

```kotlin
data class CatFact(
    @SerializedName("fact")
    val fact: String,

    @SerializedName("length")
    val length: Int
)
```

**Explanation:**

- `@SerializedName`: Maps the JSON key to the property in the Kotlin class.
- `fact`: A `String` that holds the cat fact text.
- `length`: An `Int` representing the length of the cat fact.



#### Retrofit Instance

The Retrofit instance is the central part of the library. It defines the base URL and configures how API requests and responses are handled, including JSON conversion.

**Example:**

```kotlin
class RetrofitInstance {
    private val baseURL = "https://catfact.ninja/"

    private val retrofitClient = Retrofit.Builder()
        .baseUrl(baseURL)
        .addConverterFactory(GsonConverterFactory.create())
        .build()

    val apiService = retrofitClient.create(CatFactsApi::class.java)
}
```

**Explanation:**

- `Retrofit.Builder()`: Creates a new Retrofit instance.
- `.baseUrl(baseURL)`: Sets the base URL for the API.
- `.addConverterFactory(GsonConverterFactory.create())`: Specifies Gson for JSON serialization and deserialization.
- `retrofitClient.create(CatFactsApi::class.java)`: Creates an implementation of the `CatFactsApi` interface.



### Getting the results

```kotlin
class MainActivity : ComponentActivity() {
    @SuppressLint("CoroutineCreationDuringComposition")
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()

        val retroFitInstance = RetrofitInstance()

        setContent {
            var posts: List<Post> by remember { mutableStateOf(listOf()) }
						
          	// Kalde asynkron kode
            lifecycleScope.launch {
              	// This is another example than the cats example
                posts = retroFitInstance.apiService.getAllPosts()
            }
          
            LazyColumn {
                items(posts) { post ->
                    Text(post.title)
                    Text(post.body)
                }
            }
        }
    }
}
```



## Opgaver



### Opgave 1 - level 1

Create two classes `Mobile` and `RaspberryPi` that implements this interface:

```java
public interface Computer {
    val name: String;
    val price: Int;
  
  	fun printNameAndPrice();
}
```

Create two `Mobile` and two `RaspberryPi` objects



### Opgaver 2 - Få trænet dine Retrofit skills 🏋️‍♀️ i grupper

Reference project: [https://github.com/nicklasdean/retrofit-basic](https://github.com/nicklasdean/retrofit-basic)

Vi starter med nogle opgaver der skal træne jeres Retro færdigheder og få sendt nogle requests afsted. vi skal arbejde med det her api: [https://jsonplaceholder.typicode.com](https://jsonplaceholder.typicode.com)



#### Get requests

1. Log alle posts ud vha  [https://jsonplaceholder.typicode.com/posts](https://jsonplaceholder.typicode.com/posts)
2. Log en specifik post ud vha [https://jsonplaceholder.typicode.com/posts/1](https://jsonplaceholder.typicode.com/posts/1)



#### Post request

Opret en ny bruger.

*Brugeren bliver ikke rent faktisk oprettet, api'et simulerer det bare*



#### Put/patch request

Opdater en bruger



#### Delete request

Slet en bruger



### kl 14:15 Teacher students

I skal præsentere hvordan man henter data via Retrofit



### Opgave 3 - Generativ AI app

Start arbejdet på en Generativ AI app. I kan køre en model lokalt, eller bruge mistral, openai, etc

[https://behu.gitbook.io/ita25-1-sem/webteknologi/17-lets-build-a-generative-ai-tool#getting-started](https://behu.gitbook.io/ita25-1-sem/webteknologi/17-lets-build-a-generative-ai-tool#getting-started)

- Open AI api dokumentation: [https://developers.openai.com/api/reference/resources/responses/methods/create](https://developers.openai.com/api/reference/resources/responses/methods/create)



