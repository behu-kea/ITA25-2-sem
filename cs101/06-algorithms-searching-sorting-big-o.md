# Searching, sorting and Big O

De næste to gange skal i selv planlægge og gennemføre jeres læring. Det er blandt andet for at styrke det her punkt fra studieordningen: " identificere egne læringsbehov".



I skal selv vurdere hvordan i mest effektivt lærer punkterne herunder. Jeg er der til at facilitere og hjælpe jer videre. 



**I skal arbejde i jeres studiegrupper. Hvis i ikke kommer skal i give jeres studiegruppe besked!**



## Emnerne i skal lære:

Fra studieordningen der er lidt fluffy:

**Viden**

- Viden om **algoritmer**, datastrukturer og gængse programmeringsparadigmer



**Færdigheder**

- anvende relevante programmeringssprog til udvikling af software ved **anvendelse af algoritmer**, abstraktioner og mønstre. 
- **vurdere praksisnære og teoretiske problemstillinger inden for algoritmer**, datastrukturer og gængse programmeringsparadigmer samt begrunde og vælge relevante løsningsmodeller 



Fra fagaftalen som er en konkretisering af Studieordningen. Det er **konkret** det her i skal lære. 

- Derudover introduceres algoritmer og datastrukturer: Abstrakte datastrukturer, Set, Map, List, hashing, sortering, filtrering og iterativ samt binær søgning. 
- Identificere forskelle på basale sortering- og søgealgoritmer, deres tidskompleksitet og vurdere sammenhæng med vækstbetingelser (Big O)



Altså:

- Big O
- Sortering af lister
- Søgning i lister
  - Iterativ søgning
  - Binær søgning



Eksamensspørgsmål i kan forvente af få:

Big O

- Forklar begrebet Big O notation, og hvorfor det er vigtigt i algoritmeanalyse
- Hvordan defineres O(1), O(n), O(log n), O(n²), og hvornår støder vi på dem i praksis?
- Giv et eksempel på en algoritme med O(log n) kompleksitet, og forklar hvorfor den har denne kompleksitet.
- Hvordan kan vi bruge Big O notation til at forudsige, hvordan en algoritme skalerer med stigende inputstørrelse?
- Kan du finde noget kode du har skrevet og vurdere Big O tidskompleksiteten for koden?



Sortering

- Nævn nogle almindelige sorteringsalgoritmer. Beskriv deres tidskompleksitet, hvordan de virker og hvornår man ville bruge dem. Her er nogle sorteringsalgoritmer
  - Bubble sort
  - Selection sort
  - Insertion sort
  - Merge sort
  - Quick sort




Søgning

- Hvordan fungerer lineær søgning (iterativ søgning), og hvad er dens tidskompleksitet?
- Hvornår er lineær søgning den bedste metode at bruge?
- Hvordan fungerer binær søgning, og hvorfor er den hurtigere end lineær søgning på sorterede lister?
- Hvilke forudsætninger skal være opfyldt for at kunne bruge binær søgning?
- Hvad er tidskompleksiteten for binær søgning, og hvordan udledes den?



Vis at man kan snakke med ChatGPT om det her. 

- https://chatgpt.com/c/67a48729-3b1c-8008-83ca-dedfaa092c96
- https://chatgpt.com/c/67a489bb-4e04-8008-b44c-44a4326642d9
- https://chatgpt.com/c/67a21569-cb70-8008-b263-2406ab7a3daa
- https://chatgpt.com/c/67a1feaf-9810-8008-861e-0020880baaf6
- https://chatgpt.com/c/67a1fac2-1b6c-8008-89df-8c617f7ee952



*Check out [https://visualgo.net/](https://visualgo.net/)*



## Preparation

- [Big O in 2 Minutes](https://www.youtube.com/watch?v=4TUgqm2gJkE)
- [Algorithms Explained for Beginners - How I Wish I Was Taught](https://www.youtube.com/watch?v=JJkWemM03Lg)
- [Top 7 Algorithms for Coding Interviews Explained **SIMPLY**](https://www.youtube.com/watch?v=kp3fCihUXEg)



## Feedback på aflevering

- Jeg er igang med at lave en eksamenssimulator. Vil nogle af jer interviewes 15-30 min om hvordan sådan en simulator kunne være en hjælp for jer?
  
- Smart måde at lave if else på: 
  
  ```kotlin
  class Employee(val firstname: String, val lastname: String, salary: Double) {
      var salary: Double = salary
          set(value) {
              field = if (value < 0) 0.0 else value // Prevents negative salary
          }
      init {
          if (salary < 0.0) this.salary = 0.0
      }
  
  }
  ```
  
- Funktions navngivninger:
  ```kotlin
  open fun checkSize() {
      println("YO! THIS COMPUTER IS $size!!! COOL")
  }
  ```

  ```kotlin
  fun countCameras() {
      println("There are $cameraCount cameras. ")
  }
  ```

- Tænk over typer
  ```kotlin
  class Shoe(name: String, price: Int, quantity: Int): Product(name, price, quantity) {
  ```

- Tænk over encapsulation, `private`, `public`, `internal`

- Tænk over typer: `private val radius: Double`

- Fedt med `ENMU`: `enum class DeviceState { OFF, ON } //Class til`

- I har meget `var` og meget `Double`

- Fedt med type: `val currentYear: Int = Year.now().value`

- OPtimering her:
  ```kotlin
  val ageOfModel: Int = currentYear - yearOfRelease
      if (ageOfModel == 1) {
          println("The current age of the $model is: $ageOfModel year")
      } else
          println("The current age of the $model is: $ageOfModel years")
  }
  ```

- ```kotlin
  val ageOfModel = currentYear - yearOfRelease
  println("The current age of the $model is: $ageOfModel year${if (ageOfModel == 1) "" else "s"}")
  ```

- ```kotlin
   fun displayRaise() {
      println("Yearly salary with a ten percent raise for ${this} is: \$$yearlySalaryTenPercentRaise in total")
  }
  ```

  Måske `printRaise`

- Det her behøves man ikke:

  ```kotlin
  
  class Laptop(model: String, serialNumber: Long, yearOfRelease: Int, var bluetoothStatus: Boolean): Computer(model, serialNumber, yearOfRelease) {
      override fun displayAgeOfModel() {
          super.displayAgeOfModel()
      }
  
      override fun displayDetails() {
          super.displayDetails()
      }
  
      fun isBluetoothOn() {
          println("Is Bluetooth on: $bluetoothStatus")
      }
  }
  ```

  

## Grupper

I skal arbejde i jeres studiegrupper



## Plan for idag - læringsfasen



### Overblik - 30 min

*Hvad skal vi overhovedet lære og hvad skal vi ikke lære?*

Først skal i finde ud af hvilke emner i vil fokusere på? Hvad vil i specifikt lære. For hvert punkt lav nogle underpunkter der specificerer hvad i vil lære og hvad i ikke vil lære. Er der noget af det her i allerede har styr på?



Find ud af hvordan i tester at i har den viden der skal til. Skal i kunne løse opgaver, svare på spørgsmål, gennemføre en quiz, vurdere forskellig situationer? Kan i allerede nu lave de ting i skal kunne når i er færdige? Måske kan i finde noget online eller spørge [chatten](https://chatgpt.com/share/675ac19d-69d0-8008-ae59-76f577ce63f0)

Ud af det her skal i lave en læringsplan:

- Hvad vil i lære idag?
- Hvad skal i lære imorgen?
- Er der hjemmearbejde?
- Er der forberedelse til imorgen?



### På klassen - Hvad skal de forskellige grupper lære og hvordan tester i? - 10 min



### Udførsel - indtil 11:15

- Hvordan lærer vi i vores gruppe stoffet bedst? 

- Hvordan vil i opnå den viden/de kompetencer der skal til? 

- Kan vi indgå med en anden gruppe, der lærer et emne og præsenterer det? 

- Hvordan laver vi materialet? Skal vi finde noget der allerede er lavet? NIFR har lavet materiale (slides og opgaver) Måske i kan bruge det?

- Skal vi have hjemmearbejde i gruppen? 
- Skal der være forberedelse til imorgen?



### Pause 10 - 10:15



### Refleksion i gruppen - 11:15 - 11:30

- Hvad lærte i af det? 
- Hvad fungerede godt?
- Hvad fungerede mindre godt?
- Hvad skal i lave imorgen?
  - Har i givet hinanden hjemmearbejde?
  - Skal i forberede noget til imorgen?



### Fælles på klassen - 11:30 - 11:45

- Hvilken refleksion havde i i grupperne?
- Hvad skal i lave imorgen? 
- Hvad skal i lave til imorgen?



## Læringsrubriks

Her er en liste over forskellige læringsteknikker i har prøvet før og deres pros/cons. I kan jo lave jeres egne eller finde andre online hvis i tænker det kunne være interessant. 



### Peer instruction

**Fordele** 

- Skaber viden på tværs af en gruppe
- Er social
- Ens viden bliver sat i kontekst med en andens viden
- Hurtig klaret
- Tester basal viden



**Ulempe**

- Tester ikke dybdegående viden, færdigheder eller kompetencer
- Tester paratviden
- Kan være svær at lave spørgsmål der hverken er for nemme eller svære



### Præsentation af et emne, fx Teachers/students

**Fordele**

- Skaber viden på tværs af grupper
- Skaber dybere viden, da man skal præsentere for andre
- Er god til at træne gruppearbejde



**Ulemper**

- Hvis man ikke er nok inde i stoffet er det svært at lave en præsentation
- Studerende kan blive præsenteret for viden der er forkert



### Tavle undervisning

**Fordele**

- Emner kan bliver forklaret pædagogisk og på de studerendes niveau
- Emner kan kontekstualiseres



**Ulemper**

- One size fits all, man kan spilde tid, da nogle studerende måske allerede kan emnet man underviser
- Underviser har typisk lært stoffet for lang tid siden og kan have svært ved at se det svære i stoffet. 
- Der skal være en "ekspert" der kan køre undervisningen



### Live kodning

**Fordele**

- Studerende bliver vist hvordan man kan programmerer et emne
- Man ser syntaksen, fejlene, genvejene når en underviser livekoder



**Ulemper**

- Underviser har typisk meget erfaring og kan hurtigt lave opgaverne, uden alle de frustrerende trin en studerende skal igennem
- Kan overse ting der er nemt for underviseren, men svært for de studerende



### Løs en opgave med programmering

**Fordele**

- Den studerende udvikler sine kompetencer. Ikke kun sin viden
- Den studerende skal både vide og kunne for at løse opgave
- Tester både syntax og problemløsnings kompetencer
- Effektiv til at lære



**Ulemper**

- Studerende kan løse opgaver med ChatGPT og derved undgå selve læringen
- Kan føre til frustrationer
- Hvis opgaven ikke er godt stillet kan der være forvirring omkring hvad den studerende skal
- Det kan være svært at ramme det rigtige niveau mellem nemt og svært
- Kan blive afkoblet fra virkeligheden



### Pair Programming

**Fordele**

- Man kan blive inspireret til hvordan man skal skrive kode
- Der bliver dannet viden og kompetencer på tværs af folk i en gruppe



**Ulemper**

- Man skal sikre sig at niveauet mellem de to udviklere er nogenlunde det samme
- Man skal sikre sig at alle får tid ved keyboardet
- Den dygtige studerende kan komme til at overtage programmeringen og derved kan den svage undgå læringen



### Giv feedback på kode

**Fordele**

- Den studerende bliver inspireret af at se andres kode.
- Refleksionen ift andres kode kan blive overført til egen kode. "Husk at starte med `const` som variable" - Hmm mon jeg egentlig selv gør det
- Forskning viser at det er en effektiv måde at lære på



**Ulemper**

- Man kan føle at man ikke har kompetencerne til at give feedback
- Hvad skal man fokusere på når man giver feedback? Her kan en Feedback rubrik være hjælpsom



### Case

**Fordele**

- Man arbejder på ting som man også laver i virkeligheden
- Man kan virkelig udvikle sine kompetencer her



**Ulemper**

- Det kan være svært og tidskrævende at finde en god case
- Det kan være svært at finde en balance mellem at arbejde på relevante kompetencer og samtidig løse et rigtigt problem



### ChatGPT

Fordele

- Kan være et super brugbart værktøj til læring
- Kan lave individualiseret læring der er tilpasset den studerende



Ulemper

- Kan være svær at bruge hvis man ikke har brugt LLM'er før
- Kan hallucinere, så den studerende lærer ting der er forkerte
- Kan løse den studerendes opgaver. Den studerende kan få en falsk fornemmelse af at de har nogle kompetencer de faktisk ikke har
