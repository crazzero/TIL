# π ComposeState

μ΄λ² λ¬Έμλ [Android-Compose κ³΅μλ¬Έμ](https://developer.android.com/jetpack/compose/state) κΈ°λ°μΌλ‘ μμ±νμλ€.

## κ°μ

μνλ μκ°μ΄ μ§λ¨μ λ°λΌ λ³ν  μ μλ κ°μ΄λ€.  
μ΄λ λ§€μ° κ΄λ²μν μ μλ‘μ Room λ°μ΄ν°λ² μ΄μ€λΆν° ν΄λμ€μμ μλ λ³μκΉμ§ λͺ¨λ  ν­λͺ©μ΄ ν¬ν¨λλ€.

λͺ¨λ  Android μ±μμλ μ¬μ©μμκ² μνκ° νμλλλ°, λ€μμ Android μ± μνμ λͺ κ°μ§ μμμ΄λ€.

- λ€νΈμν¬ μ°κ²°μ μ€μ ν  μ μμ λ νμλλ μ€λ΅λ°
- λΈλ‘κ·Έ κ²μλ¬Ό λ° κ΄λ ¨ λκΈ
- μ¬μ©μκ° ν΄λ¦­νλ©΄ λ²νΌμμ μ¬μλλ ripple animations (λ¬Όκ²° μ λλ©μ΄μ)
- μ¬μ©μκ° μ΄λ―Έμ§ μμ κ·Έλ¦΄ μ μλ μ€ν°μ»€

Jetpack Composeλ₯Ό μ¬μ©νλ©΄ Android μ±μμ μνλ₯Ό μ μ₯νκ³  μ¬μ©νλ μμΉμ λ°©λ²μ λͺμμ μΌλ‘ λνλΌ μ μλλ°,  
μ΄ λ¬Έμμμλ State μ Composable κ°μ κ΄κ³μ κ΄ν΄ κ·Έλ¦¬κ³  λ³΄λ€ μμ¬μ΄ μν μ²λ¦¬λ₯Ό μν΄ Jetpack Composeμμ μ κ³΅λλ APIμ κ΄ν΄ μ§μ€μ μΌλ‘ μ€λͺνλ €κ³  νλ€.

## State and Composition (μν λ° μ»΄ν¬μ§μ)

Composeλ μ μΈμ μ΄λ―λ‘ Composeλ₯Ό μλ°μ΄νΈνλ μ μΌν λ°©λ²μ μ arguments(μΈμ)λ‘ λμΌν composable μ νΈμΆνλ κ²μ΄λ€.  
μ΄λ¬ν μΈμλ UI μ μνλ₯Ό νννλλ°, ν΄λΉ μνκ° μλ°μ΄νΈλ  λλ§λ€ recomposition(μ¬κ΅¬μ±) μ΄ μ€νλλ€.  
λ°λΌμ TextFieldμ κ°μ ν­λͺ©μ λͺλ Ήν XML κΈ°λ° λ·°μμμ²λΌ μλμΌλ‘ μλ°μ΄νΈλμ§ μκ³ , composable μ΄ μ μνμ λ°λΌ μλ°μ΄νΈλλ €λ©΄ μ μνλ₯Ό λͺμμ μΌλ‘ μλ €μ€μΌ νλ€.

``` kotlin
@Composable
fun HelloContent() {
   Column(modifier = Modifier.padding(16.dp)) {
       Text(
           text = "Hello!",
           modifier = Modifier.padding(bottom = 8.dp),
           style = MaterialTheme.typography.h5
       )
       OutlinedTextField(
           value = "",
           onValueChange = { },
           label = { Text("Name") }
       )
   }
}
```

μ μ½λλ₯Ό μ€ννλ©΄ μλ¬΄ μΌλ μΌμ΄λμ§ μλλ€.  
TextFieldκ° μμ²΄μ μΌλ‘ μλ°μ΄νΈλμ§ μκΈ° λλ¬Έμ΄κ³ , value λ§€κ°λ³μκ° λ³κ²½λ  λ μλ°μ΄νΈλλ€.  
μ΄λ Composeμμμ composition λ° recomposition μλ λ°©μ λλ¬Έμ΄λ€.

### ν΅μ¬μ©μ΄

> Composition(μ»΄ν¬μ§μ): Jetpack Composeκ° composable μ μ€νν  λ λΉλν UIμ κ΄ν μ€λͺ
> Initial Composition(μ΄κΈ° μ»΄ν¬μ§μ): μ²μ composable μ μ€ννμ¬ compositionμ λ§λ λ€.
> Recomposition(λ¦¬μ»΄ν¬μ§μ): λ°μ΄ν°κ° λ³κ²½λ  λ composition μ μλ°μ΄νΈνκΈ° μν΄ composable μ λ€μ μ€ννλ κ²μ λ§νλ€.

## State in composables(μ»΄ν¬μ λΈμ μν)

Composable ν¨μλ `remeber` composable μ μ¬μ©νμ¬ λ©λͺ¨λ¦¬μ λ¨μΌ κ°μ²΄λ₯Ό μ μ₯ν  μ μλ€.  
`remember` μ μν΄ κ³μ°λ κ°μ `Initial Composition` μ μ μ₯λκ³  μ μ₯λ κ°μ `Recomposition` μ€μ λ°νλλ€.  
`remember` λ λ³κ²½ κ°λ₯ν κ°μ²΄λΏλ§ μλλΌ λ³κ²½ν  μ μλ κ°μ²΄λ₯Ό μ μ₯νλλ°μλ μ¬μ©ν  μ μλ€.

### μ°Έκ³ 

> `remember` λ κ°μ²΄λ₯Ό composition μ μ μ₯νκ³ , `remember`λ₯Ό νΈμΆν composable μ΄ composition μμ μ­μ λλ©΄ κ·Έ κ°μ²΄ λν μμ΄λ²λ¦°λ€.  
> mutableStateOfλ κ΄μ°° κ°λ₯ν `MutableState<T>`λ₯Ό μμ±νκ³ , μ΄λ λ°νμ μ Composeμ ν΅ν©λλ κ΄μ°° κ°λ₯ μ νμ΄λ€.

``` kotlin
interface MutableState<T> : State<T> {
    override var value: T
}
```

`value`κ° λ³κ²½λλ©΄ `value`λ₯Ό μ½λ composable ν¨μμ recomposition μ΄ μμ½(schedulbe)λλ€.  
μλ₯Ό λ€μ΄, ExpandingCardμ κ²½μ° expandedκ° λ³κ²½λ  λλ§λ€ ExpandingCardκ° μ¬κ΅¬μ±λλ€.

Composable μμ MutableState κ°μ²΄λ₯Ό μ μΈνλ λ°λ μΈ κ°μ§ λ°©λ²μ΄ μλ€.

``` kotlin
val mutableState = remember { mutableStateOf(default) }
var value by remember { mutableStateOf(default) }
val (value, setValue) = remember { mutableStateOf(default) }
```

μ΄λ¬ν μ μΈμ λμΌν κ²μ΄λ©° μλ‘ λ€λ₯Έ μ©λμ μνλ₯Ό μ¬μ©νκΈ° μν΄ μ κ³΅λκ³ ,  
μμ± μ€μΈ composable μμ κ°μ₯ μ½κΈ° μ¬μ΄ μ½λλ₯Ό μμ±νλ μ μΈμ μ νν΄μΌ νλ€.
μ¬κΈ°μ, by μμ κ΅¬λ¬Έ(delegate syntax) μλ λ€μμ imports κ° νμνλ€.

``` kotlin
import androidx.compose.runtime.getValue
import androidx.compose.runtime.setValue
```

`remember` λ κ°μ λ€λ₯Έ composable μ λ§€κ°λ³μλ‘ μ¬μ©νκ±°λ λ‘μ§μΌλ‘ μ¬μ©νμ¬ νμν  composable μ λ³κ²½ν  μ μλ€.  
μλ₯Ό λ€μ΄ μ΄λ¦μ΄ λΉμ΄ μλ κ²½μ° μΈμ¬λ§μ νμνμ§ μμΌλ €λ©΄ if λ¬Έμ μνλ₯Ό μ¬μ©νλ©΄ λλ€.

``` kotlin
@Composable
fun HelloContent() {
   Column(modifier = Modifier.padding(16.dp)) {
       var name by remember { mutableStateOf("") }
       if (name.isNotEmpty()) {
           Text(
               text = "Hello, $name!",
               modifier = Modifier.padding(bottom = 8.dp),
               style = MaterialTheme.typography.h5
           )
       }
       OutlinedTextField(
           value = name,
           onValueChange = { name = it },
           label = { Text("Name") }
       )
   }
}
```

`remember` κ° recomposition κ³Όμ  μ μ²΄μμ μνλ₯Ό μ μ§νλ λ° λμμ λμ§λ§ composable μ λ°μμλ μνκ° μ μ§λμ§ μλλ€.  
μ΄ κ²½μ°μλ rememberSaveableμ μ¬μ©ν΄μΌ νλλ°, rememberSaveableμ Bundleμ μ μ₯ν  μ μλ λͺ¨λ  κ°μ μλμΌλ‘ μ μ₯νλ€.  
λ€λ₯Έ κ°λ€μ κ²½μ°μλ Custom Saver κ°μ²΄λ₯Ό μ λ¬ν  μ μλ€.

## Other supported types of state(μ§μλλ κΈ°ν μν μ ν)

Jetpack Compose μμλ `State`λ₯Ό λ³΄μ‘΄νκΈ° μν΄μ λ°λμ `MutableState<T>` λ₯Ό μ¬μ©ν  νμκ° μλ€.  
Jetpack Compose λ κ΄μ°° κ°λ₯ν λ€λ₯Έ μ νμ μ§μνλλ°, μ΄ λ Compose μμ κ΄μ°° κ°λ₯ν λ€λ₯Έ μ νμ μ½μΌλ €λ©΄ μνλ₯Ό `State<T>`λ‘ λ³νν΄μΌ νλ€.  
κ·ΈλμΌ μνκ° λ³ν  λ Jetpack Composeκ° μλμΌλ‘ μ¬κ΅¬μ±λλ€.

Composeμλ λ€μμ Android μ±μ μ¬μ©λλ κ΄μ°° κ°λ₯ν μΌλ° μ νμ λν΄ `State<T>` λ₯Ό λ§λ€ μ μλ ν¨μκ° κΈ°λ³Έμ μΌλ‘ λ΄μ₯λμ΄ μλ€.

- LiveData
- Flow
- RxJava2

μ±μ κ΄μ°° κ°λ₯ν μ»€μ€ν ν΄λμ€(observable custom class)λ₯Ό μ¬μ©νλ κ²½μ° κ΄μ°° κ°λ₯ν λ€λ₯Έ μ νμ μ½μ΄μ€κΈ° μν Composeμ© νμ₯ ν¨μ(Extension function)λ₯Ό λΉλν  μ μλ€.  
λͺ¨λ  λ³κ²½μ¬ν­μ μμ νλλ‘ Compose μ νμ©νλ λͺ¨λ  κ°μ²΄λ₯Ό `State<T>` λ‘ λ³ννκ³  composable μ ν΅ν΄ μ½μ΄μ¬ μ μλ€.

### μμ 
> Composeλ `State<T>` κ°μ²΄λ₯Ό μ½μ΄μ€λ©΄μ μλμΌλ‘ μ¬κ΅¬μ±λλ€.  
> Composeμμ `LiveData` κ°μ κ΄μ°° κ°λ₯ν λ λ€λ₯Έ μ νμ μ¬μ©ν  κ²½μ°, composable μμ `LiveData<T>.observeAsState()` κ°μ composable νμ₯ ν¨μ(Extension function)λ₯Ό μ¬μ©νμ¬ κ·Έ μ νμ  `State<T>` λ‘ λ³νν νμ μ½μ΄μ¬ μ μλ€.

### μ£Όμ
> Composeμμ `ArrayList<T>` λλ `mutableListOf()` κ°μ λ³κ²½ κ°λ₯ κ°μ²΄λ₯Ό μνλ‘ μ¬μ©νλ©΄ μ±μ μλͺ»λκ±°λ μ€λλ λ°μ΄ν°κ° νμλ  μ μλ€.  
> λ³κ²½ κ°λ₯ν κ°μ²΄ μ€ `ArrayList<T>` λλ λ³κ²½ κ°λ₯ν λ°μ΄ν° ν΄λμ€ κ°μ κ΄μ°° λΆκ°λ₯ν κ°μ²΄λ κ·Έ κ°μ²΄κ° λ³κ²½λ  λ composition μ νΈλ¦¬κ±°νλλ‘ Compose μμ κ΄μ°°ν  μ μλ€.  
> κ΄μ°° λΆκ°λ₯νλ©΄μ λ³κ²½ κ°λ₯ν κ°μ²΄λ₯Ό μ¬μ©νλ λμ  `State<List<T>>` λ° λ³κ²½ λΆκ°λ₯ν listOf() κ°μ κ΄μ°° κ°λ₯ λ°μ΄ν° νλλ₯Ό μ¬μ©νλ κ²μ΄ μ’λ€.

## Stateful and stateless(μ€νμ΄νΈνκ³Ό μ€νμ΄νΈλ¦¬μ€)

`remember` λ₯Ό μ¬μ©νμ¬ κ°μ²΄λ₯Ό μ μ₯νλ composable μ λ΄λΆ μνλ₯Ό μμ±νμ¬ composable μ μ€νμ΄νΈν(Stateful)λ‘ λ§λ λ€.  
HelloContentλ λ΄λΆμ μΌλ‘ name μνλ₯Ό λ³΄μ‘΄νκ³  μμ νλ―λ‘ μ€νμ΄νΈν(Stateful) μ»΄ν¬μ λΈμ ν μκ° λλ€.  
μ΄λ νΈμΆμ(caller)κ° μνλ₯Ό μ μ΄ν  νμκ° μκ³  μνλ₯Ό μ§μ  κ΄λ¦¬νμ§ μμλ μνλ₯Ό μ¬μ©ν  μ μλ κ²½μ°μ μ μ©νλ€.  
κ·Έλ¬λ λ΄λΆ μνλ₯Ό κ°λ μ»΄ν¬μ λΈμ μ¬μ¬μ© κ°λ₯μ±μ΄ μ κ³  νμ€νΈνκΈ°κ° λ μ΄λ €μ΄ κ²½ν₯μ΄ μλ€.

μ€νμ΄νΈλ¦¬μ€(Stateless) composable μ μνλ₯Ό κ°μ§ μλ μΉκ΅¬μ΄λ€. μ€νμ΄νΈλ¦¬μ€(Stateless)λ₯Ό λ¬μ±νλ ν κ°μ§ μ¬μ΄ λ°©λ²μ `State hoisting` μ μ¬μ©νλ κ²μ΄λ€.

μ¬μ¬μ© κ°λ₯ν composable μ κ°λ°ν  λλ λμΌν μ»΄ν¬μ λΈμ μ€νμ΄νΈν(Stateful) λ²μ κ³Ό μ€νμ΄νΈλ¦¬μ€(Stateless) λ²μ μ λͺ¨λ λΈμΆν΄μΌ νλ κ²½μ°κ° μλ€.  
μ€νμ΄νΈν(Stateful) λ²μ μ μνλ₯Ό μΌλμ λμ§ μλ νΈμΆμ(caller)μ νΈλ¦¬νλ©°, μ€νμ΄νΈλ¦¬μ€(Stateless) λ²μ μ μνλ₯Ό μ μ΄νκ±°λ λμ΄μ¬λ €μΌ νλ νΈμΆμ(caller)μ κ²½μ°μ νμνλ€.

## μν νΈμ΄μ€ν

Composeμμ state hoisting μ composable μ μ€νμ΄νΈλ¦¬μ€(Stateless)λ‘ λ§λ€κΈ° μν΄ state λ₯Ό composable μ νΈμΆμ(caller)λ‘ μ?κΈ°λ ν¨ν΄μ΄λ€.  
Composeμμ state hoisting μ μν μΌλ°μ  ν¨ν΄μ μν λ³μλ₯Ό λ€μ λ κ°μ λ§€κ°λ³μλ‘ λ°κΎΈλ κ²μ΄λ€.

- `value`: T: νμν  νμ¬ κ°
- `onValueChange`: (T) -> Unit: Tκ° μ μλ μ κ°μΈ κ²½μ° κ°μ λ³κ²½νλλ‘ μμ²­νλ μ΄λ²€νΈ

νμ§λ§ μ΄λ `onValueChange` λ‘λ§ μ νλμ§ μλλ€.  
μ»΄ν¬μ λΈμ λ νΉμ ν μ΄λ²€νΈκ° μ΄μΈλ¦¬λ κ²½μ°, μλ₯Ό λ€μ΄, ExpandingCardκ° onExpandμ onCollapseλ₯Ό μ μν  λμ κ°μ΄ λλ€λ₯Ό μ¬μ©νμ¬ κ·Έ μ΄λ²€νΈλ₯Ό μ μν  μ μλ€.

μ΄λ¬ν λ°©μμΌλ‘ λμ΄μ¬λ¦°(hoisting) μνμλ μ€μν μμ±μ΄ λͺ κ°μ§ μλ€.

- Single source of truth(λ¨μΌ μμ€ μ μ₯μ): μνλ₯Ό λ³΅μ νλ λμ  μ?κ²ΌκΈ° λλ¬Έμ μμ€ μ μ₯μκ° νλλ§ μλ€. λ²κ·Έ λ°©μ§μ λμμ΄ λλ€.
- Encapsulated(μΊ‘μνλ¨): μ€νμ΄νΈν(Stateful) composable λ§ μνλ₯Ό μμ ν  μ μλ€. μ² μ ν λ΄λΆμ  μμ±μ΄λ€.
- Shareable(κ³΅μ  κ°λ₯ν¨): νΈμ΄μ€νν μνλ₯Ό μ¬λ¬ composable κ³Ό κ³΅μ ν  μ μλ€. λ€λ₯Έ composableμμ nameμ μ¬μ©νλ €λ κ²½μ° νΈμ΄μ€νμ ν΅ν΄ κ·Έλ κ² ν  μ μλ€.
- Interceptable(κ°λ‘μ±κΈ° κ°λ₯ν¨): μ€νμ΄νΈλ¦¬μ€(Stateless) composableμ νΈμΆμ(caller)λ μνλ₯Ό λ³κ²½νκΈ° μ μ μ΄λ²€νΈλ₯Ό λ¬΄μν μ§ μμ ν μ§ κ²°μ ν  μ μλ€.
- Decoupled(λΆλ¦¬λ¨): μ€νμ΄νΈλ¦¬μ€(Stateless) ExpandingCardμ μνλ μ΄λμλ μ μ₯ν  μ μλ€. μλ₯Ό λ€μ΄ nameμ ViewModelλ‘ μ?κΈΈ μ μλ€.

μλμ μμ μμλ `HelloContent`μμ `name`κ³Ό `onValueChange`λ₯Ό μΆμΆν λ€μ,  
μ΄λ¬ν ν­λͺ©μ νΈλ¦¬ μλ¨μ κ±°μ³ `HelloContent`λ₯Ό νΈμΆνλ `HelloScreen` composable λ‘ μ?κΈ΄λ€.

``` kotlin
@Composable
fun HelloScreen() {
    var name by rememberSaveable { mutableStateOf("") }

    HelloContent(name = name, onNameChange = { name = it })
}

@Composable
fun HelloContent(name: String, onNameChange: (String) -> Unit) {
    Column(modifier = Modifier.padding(16.dp)) {
        Text(
            text = "Hello, $name",
            modifier = Modifier.padding(bottom = 8.dp),
            style = MaterialTheme.typography.h5
        )
        OutlinedTextField(
            value = name,
            onValueChange = onNameChange,
            label = { Text("Name") }
        )
    }
}
```

HelloContentμμ μνλ₯Ό λμ΄μ¬λ¦¬λ©΄(hoisting) λ μ½κ² composable μ μΆλ‘ νκ³  μ¬λ¬ μν©μμ μ¬μ¬μ©νλ©° νμ€νΈν  μ μλ€.  
HelloContentλ μνμ μ μ₯ λ°©μκ³Ό λμ»€νλ§(λΆλ¦¬)λλ€.  
λμ»€νλ§ λλ€λ κ²μ HelloScreenμ μμ νκ±°λ κ΅μ²΄ν  κ²½μ° HelloContentμ κ΅¬ν λ°©μμ λ³κ²½ν  νμκ° μλ€λ μλ―Έμ΄λ€.

![Image](./img/udf-hello-screen.png)

μνκ° λ΄λ €κ°κ³  μ΄λ²€νΈκ° μ¬λΌκ°λ ν¨ν΄μ *λ¨λ°©ν₯ λ°μ΄ν° νλ¦*μ΄λΌκ³  νλ€.  
μ΄ κ²½μ° μνλ HelloScreenμμ HelloContentλ‘ λ΄λ €κ°κ³  μ΄λ²€νΈλ HelloContentμμ HelloScreenμΌλ‘ μ¬λΌκ°λ€.  
λ¨λ°©ν₯ λ°μ΄ν° νλ¦μ λ°λ₯΄λ©΄ UIμ μνλ₯Ό νμνλ composable κ³Ό μνλ₯Ό μ μ₯νκ³  λ³κ²½νλ μ± λΆλΆμ μλ‘ λΆλ¦¬ν  μ μλ€.

### ν΅μ¬ μ¬ν­
> μνλ₯Ό λμ΄μ¬λ¦΄ λ μνμ μ΄λ μμΉλ₯Ό μ½κ² νμν  μ μλ μΈ κ°μ§ κ·μΉμ΄ μλ€.  
> 
> 1. μνλ μ μ΄λ κ·Έ μνλ₯Ό μ¬μ©νλ λͺ¨λ  μ»΄ν¬μ λΈμ κ°μ₯ λ?μ κ³΅ν΅ μμ μμλ‘ λμ΄μ¬λ €μΌ νλ€(μ½κΈ°).
> 2. μνλ μ΅μν λ³κ²½λ  μ μλ κ°μ₯ λμ μμ€μΌλ‘ λμ΄μ¬λ €μΌ νλ€(μ°κΈ°).
> 3. λμΌν μ΄λ²€νΈμ λν μλ΅μΌλ‘ λ μνκ° λ³κ²½λλ κ²½μ° λ μνλ₯Ό ν¨κ» λμ΄μ¬λ €μΌ νλ€.
> 
> μ΄λ¬ν κ·μΉμμ μκ΅¬νλ κ²λ³΄λ€ μνλ₯Ό λ λμ μμ€μΌλ‘ λμ΄μ¬λ¦΄ μ μλ€.  
> νμ§λ§ μνλ₯Ό λμ΄λ΄λ¦¬λ©΄ λ¨λ°©ν₯ λ°μ΄ν° νλ¦μ λ°λ₯΄κΈ°κ° μ΄λ ΅κ±°λ λΆκ°λ₯ν  μ μλ€.

## Restoring state in Compose(Compose μμ state λ³΅μ)

`remeberSaveable` μ μ¬μ©ν΄μ μ‘ν°λΉν° λλ νλ‘μΈμ€κ° μ¬μμ±λμ λ, UI μνλ₯Ό λ³΅μν  μ μλ€.  
`remeberSaveable` λ recomposition λ  λμ μνλ₯Ό μ μ§νλ€.  
λν΄μ, `rememberSaveable` μ μ‘ν°λΉν°μ νλ‘μΈμ€κ° μ¬μμ±λ  λ λν μνλ₯Ό μ μ§νλ€.

### μνλ₯Ό μ μ₯νλ λ°©λ²

`Bundle` μ μΆκ°λ λͺ¨λ  data νμλ€μ μλμ μΌλ‘ μ μ₯λλ€.  
λ§μ½ `Bundle`μ μΆκ°λκΈ° μ΄λ €μ΄ λ¬΄μΈκ°λ₯Ό μ μ₯νκΈ° μνλ€λ©΄, λ€μκ³Ό κ°μ μ΅μμ΄ μλ€.  

1. Parcelize
2. MapSaver
3. ListSaver

**1.Parcelize**

κ°μ²΄μ `@Parcelize` annotation μ μΆκ°νλ©΄ κ°μ₯ μ½κ² μνλ₯Ό μ μ₯ν  μ μλ€.  
μ΄λ₯Ό ν΅ν΄ κ°μ²΄λ parcelable μ΄ λκ³ , bundled λ  μ μλ€.  
μλ₯Ό λ€μ΄, μλ μ½λλ City λ°μ΄ν° νμμ parcelable λ‘ λ§λ€κ³  μ΄λ₯Ό μνμ μ μ₯μν¨λ€.

``` kotlin
@Parcelize
data class City(val name: String, val country: String) : Parcelable

@Composable
fun CityScreen() {
    var selectedCity = rememberSaveable {
        mutableStateOf(City("Madrid", "Spain"))
    }
}
```

**2.MapSaver**

κ°λ `@Parcelize` κ° μμ΄μΈλ¦¬λ κ²½μ°μλ, mapSaver λ₯Ό μ¬μ©ν΄μ κ°μ²΄λ₯Ό converting νλ custom λ£°μ λ§λ€μ΄μ μμ€νμΌλ‘ νμ¬κΈ bundle μ μ μ₯μν¬ μ μλλ‘ λ§λ€ μ μλ€.

``` kotlin
data class City(val name: String, val country: String)

val CitySaver = run {
    val nameKey = "Name"
    val countryKey = "Country"
    mapSaver(
        save = { mapOf(nameKey to it.name, countryKey to it.country) },
        restore = { City(it[nameKey] as String, it[countryKey] as String) }
    )
}

@Composable
fun CityScreen() {
    var selectedCity = rememberSaveable(stateSaver = CitySaver) {
        mutableStateOf(City("Madrid", "Spain"))
    }
}
```

**3.ListSaver**

map μΌλ‘ λ§λ€μ΄μ λ°λμ key λ₯Ό λ§λλκ² μ«λ€λ©΄, listSaver λ₯Ό μ¬μ©ν  μ μλ€.

``` kotlin
data class City(val name: String, val country: String)

val CitySaver = listSaver<City, Any>(
    save = { listOf(it.name, it.country) },
    restore = { City(it[0] as String, it[1] as String) }
)

@Composable
fun CityScreen() {
    var selectedCity = rememberSaveable(stateSaver = CitySaver) {
        mutableStateOf(City("Madrid", "Spain"))
    }
}
```

## Managing state in Compose(Compose μμ μν κ΄λ¦¬)

κ°λ¨ν μν νΈμ΄μ€νμ composable ν¨μ μμ²΄μμ κ΄λ¦¬ν  μ μλ€.  
κ·Έλ¬λ μΆμ ν  μνμ μμ΄ μ¦κ°νκ±°λ composable κΈ°λ₯μμ μνν  λ‘μ§μ΄ μκΈ°λ κ²½μ° λ‘μ§ λ° μνμ λν μ±μμ λ€λ₯Έ ν΄λμ€μΈ state holders μκ² μμνλ κ²μ΄ μ’λ€.

### μ£Όμ μ©μ΄
> State holders: composable μ λ‘μ§ λ° μνλ₯Ό κ΄λ¦¬ν©λλ€.
> λ€λ₯Έ κ³³μμλ state holders λ₯Ό *hoisted state objects*λΌκ³ λ λΆλ¦λλ€.

μ§κΈλΆν° Composeμμ λ€μν λ°©μμΌλ‘ μνλ₯Ό κ΄λ¦¬νλ λ°©λ²μ λν΄ μμλ³΄μ.  
Composable μ λ³΅μ‘μ±μ λ°λΌ λ€μκ³Ό κ°μ΄ μνκ΄λ¦¬λ₯Ό νλκ² μ’λ€.

- κ°λ¨ν UI μμ μν κ΄λ¦¬λ₯Ό μν composable.
- λ³΅μ‘ν UI μμ μν κ΄λ¦¬λ₯Ό μν state holders. State holders λ UI μμμ μνμ UI λ‘μ§μ μμ ν©λλ€.
- [Architecture Components ViewModels](https://developer.android.com/topic/libraries/architecture/viewmodel) λ λΉμ¦λμ€ λ‘μ§κ³Ό νλ©΄ λλ UI μνμ λν μ‘μΈμ€λ₯Ό μ κ³΅νλ νΉλ³ν μ νμ state holders μ΄λ€.

State holders λ νλ¨ μ± λ°μ κ°μ λ¨μΌ μμ ―μμ μ μ²΄ νλ©΄μ μ΄λ₯΄κΈ°κΉμ§ κ΄λ¦¬νλ ν΄λΉ UI μμμ λ²μμ λ°λΌ λ€μν ν¬κΈ°λ‘ μ κ³΅λλ€.  
State holders λ λ³΅ν© κ°λ₯νλ€. μ¦, μν λ³΄μ μλ νΉν μνλ₯Ό μ§κ³ν  λ λ€λ₯Έ state holders μ ν΅ν©λ  μ μλ€.

λ€μ λ€μ΄μ΄κ·Έλ¨μ Compose μν κ΄λ¦¬μ κ΄λ ¨λ entities κ°μ κ΄κ³μ λν μμ½μ λ³΄μ¬μ€λ€.  

- Composable μ λ³΅μ‘μ±μ λ°λΌ 0κ° μ΄μμ state holder(μΌλ° κ°μ²΄, ViewModel λλ λ λ€μΌ μ μμ)μ μ’μλ  μ μλ€.
- μΌλ° state holders λ λΉμ¦λμ€ λ‘μ§ λλ νλ©΄ μνμ λν μ κ·Όμ΄ νμν κ²½μ° ViewModelμ μμ‘΄ν  μ μλ€.
- ViewModelμ λΉμ¦λμ€ λλ λ°μ΄ν° κ³μΈ΅μ λ°λΌ λ€λ₯΄λ€.

![Image](./img/state-dependencies.svg)

### Types of state and logic(μνμ λ‘μ§μ μ ν)

Android μ±μμλ λ€μν μ νμ μνλ₯Ό κ³ λ €ν΄μΌ νλ€.

- **UI element state** λ UI μμμ νΈμ΄μ€νΈ μνμ΄λ€. μλ₯Ό λ€μ΄ ScaffoldStateλ Scaffold composable μνλ₯Ό μ²λ¦¬νλ€.
- **Screen or UI state** λ νλ©΄μ νμλμ΄μΌ νλ μνμ΄λ€. μλ₯Ό λ€μ΄ CartUiState ν΄λμ€μμλ μ₯λ°κ΅¬λ ν­λͺ©, μ¬μ©μμκ² νμν  λ©μμ§ λλ λ‘λ νλκ·Έλ₯Ό ν¬ν¨νλ€. μ΄ μνλ μ νλ¦¬μΌμ΄μ λ°μ΄ν°λ₯Ό ν¬ν¨νκΈ° λλ¬Έμ μΌλ°μ μΌλ‘ κ³μΈ΅μ λ€λ₯Έ κ³μΈ΅κ³Ό μ°κ²°λλ€.

λν λ€μν μ νμ λ‘μ§μ΄ μλ€.

- UI behavior logic or UI logic μ νλ©΄μ μν λ³κ²½ μ¬ν­μ νμνλ λ°©λ²κ³Ό κ΄λ ¨μ΄ μλ€. μλ₯Ό λ€μ΄ navigation logic μ λ€μμ νμν  νλ©΄μ κ²°μ νκ±°λ μ€λ΅λ° λλ ν μ€νΈλ₯Ό μ¬μ©ν  μ μλ νλ©΄μ μ¬μ©μ λ©μμ§λ₯Ό νμνλ λ°©λ²μ κ²°μ νλ UI λ‘μ§μ΄λ€. UI behavior logic μ ν­μ Composition μ μμ΄μΌ ν©λλ€.
- Business logic μ μν λ³κ²½μ μ²λ¦¬νλ κ²μ΄λ€. μλ₯Ό λ€μ΄ κ²°μ λ₯Ό νκ±°λ μ¬μ©μ κΈ°λ³Έ μ€μ μ μ μ₯νλ€. μ΄ λ‘μ§μ μΌλ°μ μΌλ‘ UI κ³μΈ΅μ΄ μλ λΉμ¦λμ€ λλ λ°μ΄ν° κ³μΈ΅μ λ°°μΉλλ€.

### Composables as source of truth

UI λ‘μ§κ³Ό UI μμ μνλ₯Ό composable μ λλ κ²μ μνμ λ‘μ§μ΄ λ¨μν κ²½μ° μ’μ μ κ·Ό λ°©μμ΄λ€.  
μλ₯Ό λ€μ΄ λ€μμ ScaffoldState λ° CoroutineScopeλ₯Ό μ²λ¦¬νλ MyApp composable μ΄λ€.

```kotlin
@Composable
fun MyApp() {
    MyTheme {
        val scaffoldState = rememberScaffoldState()
        val coroutineScope = rememberCoroutineScope()

        Scaffold(scaffoldState = scaffoldState) {
            MyContent(
                showSnackbar = { message ->
                    coroutineScope.launch {
                        scaffoldState.snackbarHostState.showSnackbar(message)
                    }
                }
            )
        }
    }
}
```

ScaffoldStateμλ λ³κ²½ κ°λ₯ν μμ±μ΄ ν¬ν¨λμ΄ μκΈ° λλ¬Έμ λͺ¨λ  μνΈ μμ©μ MyApp κ΅¬μ± κ°λ₯μμ λ°μν΄μΌ νλ€.  
κ·Έλ μ§ μκ³  λ€λ₯Έ composable μ μ λ¬νλ©΄ single source of truth principle μ μ€μνμ§ μκ³  λ²κ·Έ μΆμ μ λ μ΄λ ΅κ² λ§λλ μνλ‘ λ³κ²½λ μ μλ€.

### State holders as source of truth

Composable μ μ¬λ¬ UI μμμ μνλ₯Ό ν¬ν¨νλ λ³΅μ‘ν UI λ‘μ§μ΄ ν¬ν¨λ κ²½μ°, ν΄λΉ μ±μμ state holders μκ² μμν΄μΌ νλ€.  
μ΄λ κ² νλ©΄ μ΄ λ‘μ§μ κ²©λ¦¬λ μνμμ λ μ½κ² νμ€νΈν  μ μκ³  composable μ λ³΅μ‘μ±μ μ€μΌ μ μλ€.  
μ΄ μ κ·Ό λ°©μμ κ΄μ¬ λΆλ¦¬ μμΉμ μ νΈνκ³ , Composable μ UI μμ λ°©μΆμ λ΄λΉνκ³  state holder λ UI λ‘μ§κ³Ό UI μμμ μνλ₯Ό ν¬ν¨νλ€.

State holders λ compositionμμ μμ±λκ³  κΈ°μ΅λλ μΌλ° ν΄λμ€μ΄κ³ , λλ¬Έμ Composable μ μλͺ μ£ΌκΈ°λ₯Ό λ°λ₯΄κΈ° λλ¬Έμ Compose μ’μμ±μ μ¬μ©ν  μ μλ€.

Composables as the source of truth μΉμμ MyApp μ»΄ν¬μ λΈμ λν μ±μμ΄ μ»€μ§λ©΄ MyAppState μν νλλ₯Ό λ§λ€μ΄ λ³΅μ‘μ±μ κ΄λ¦¬ν  μ μλ€.

``` kotlin
// Plain class that manages App's UI logic and UI elements' state
class MyAppState(
    val scaffoldState: ScaffoldState,
    val navController: NavHostController,
    private val resources: Resources,
    /* ... */
) {
    val bottomBarTabs = /* State */

    // Logic to decide when to show the bottom bar
    val shouldShowBottomBar: Boolean
        @Composable get() = /* ... */

    // Navigation logic, which is a type of UI logic
    fun navigateToBottomBarRoute(route: String) { /* ... */ }

    // Show snackbar using Resources
    fun showSnackbar(message: String) { /* ... */ }
}

@Composable
fun rememberMyAppState(
    scaffoldState: ScaffoldState = rememberScaffoldState(),
    navController: NavHostController = rememberNavController(),
    resources: Resources = LocalContext.current.resources,
    /* ... */
) = remember(scaffoldState, navController, resources, /* ... */) {
    MyAppState(scaffoldState, navController, resources, /* ... */)
}
```

MyAppStateλ μ’μμ±μ μ¬μ©νλ―λ‘ μ»΄ν¬μ§μμμ MyAppStateμ μΈμ€ν΄μ€λ₯Ό κΈ°μ΅νλ λ©μλλ₯Ό μ κ³΅νλ κ²μ΄ μ’λ€. μ΄ κ²½μ°μλ RememberMyAppState ν¨μμ΄λ€.

μ΄μ  MyAppμ UI μμλ₯Ό λ΄λ³΄λ΄λ λ° μ€μ μ λκ³  μμΌλ©° λͺ¨λ  UI λΌλ¦¬ λ° UI μμμ μνλ₯Ό MyAppStateμ μμνλ€.

```
@Composable
fun MyApp() {
    MyTheme {
        val myAppState = rememberMyAppState()
        Scaffold(
            scaffoldState = myAppState.scaffoldState,
            bottomBar = {
                if (myAppState.shouldShowBottomBar) {
                    BottomBar(
                        tabs = myAppState.bottomBarTabs,
                        navigateToRoute = {
                            myAppState.navigateToBottomBarRoute(it)
                        }
                    )
                }
            }
        ) {
            NavHost(navController = myAppState.navController, "initial") { /* ... */ }
        }
    }
}
```

μμ κ°μ΄, composable μ μ±μμ λλ¦¬λ©΄ state holders κ° νμνλ€.=

### μ°Έκ³ 

> State holders κ° μ‘ν°λΉν° λλ νλ‘μΈμ€λ₯Ό λ€μ λ§λ  ν λ³΄μ‘΄νλ €λ μνλ₯Ό ν¬ν¨νλ κ²½μ°, `rememberSaveable`λ₯Ό μ¬μ©νκ³  μ΄μ λν custom Saverλ₯Ό λλ€.

### ViewModels as source of truth

μΌλ°μ μΈ state holders ν΄λμ€κ° UI λ‘μ§ λ° UI μμμ μνλ₯Ό λ΄λΉνλ κ²½μ° ViewModelμ λ€μμ λ΄λΉνλ νΉμν μ νμ state holders μ΄λ€.
- μΌλ°μ μΌλ‘ λΉμ¦λμ€ λ° λ°μ΄ν° κ³μΈ΅κ³Ό κ°μ κ³μΈ΅μ λ€λ₯Έ κ³μΈ΅μ λ°°μΉλλ μ νλ¦¬μΌμ΄μμ λΉμ¦λμ€ λ‘μ§μ λν μ‘μΈμ€λ₯Ό μ κ³΅νκ³ ,
- νλ©΄ λλ UI μνκ° λλ νΉμ  νλ©΄μ νμνκΈ° μν΄ μ νλ¦¬μΌμ΄μ λ°μ΄ν°λ₯Ό μ€λΉνλ€.

ViewModelμ configuration λ³κ²½ νμλ μ μ§λκΈ° λλ¬Έμ Composition λ³΄λ€ μλͺμ΄ λ κΈΈλ€.  
μ΄λ€μ Compose μ½νμΈ  νΈμ€νΈμ μλͺ μ£ΌκΈ°(μ¦, activities or fragments) λλ λμμ μλͺ μ£ΌκΈ° λλ navigation λΌμ΄λΈλ¬λ¦¬λ₯Ό μ¬μ©νλ κ²½μ° navigation-graphλ₯Ό λ°λ₯Ό μ μλ€.  
μλͺμ΄ λ κΈΈκΈ° λλ¬Έμ ViewModelμ compositionμ μλͺμ λ°μΈλ©λ μνμ λν μλͺμ΄ κΈ΄ μ°Έμ‘°λ₯Ό λ³΄μ νμ§ μμμΌ νλ€. νΉμ, κ·Έλ΄ κ²½μ° λ©λͺ¨λ¦¬ λμκ° λ°μν  μ μλ€.

λΉμ¦λμ€ λ‘μ§μ λν μ‘μΈμ€λ₯Ό μ κ³΅νκ³  UI μνμ λν μ λ³΄ μμ€κ° λκΈ° μν΄ ViewModelμ μ¬μ©νλ €λ©΄ νλ©΄ μμ€ composable μ μ¬μ©νλ κ²μ΄ μ’λ€.  
λ€μμ νλ©΄ μμ€ composable μμ μ¬μ©λλ ViewModelμ μμμ΄λ€.

``` kotlin
data class ExampleUiState(
    dataToDisplayOnScreen: List<Example> = emptyList(),
    userMessages: List<Message> = emptyList(),
    loading: Boolean = false
)

class ExampleViewModel(
    private val repository: MyRepository,
    private val savedState: SavedStateHandle
) : ViewModel() {

    var uiState by mutableStateOf<ExampleUiState>(...)
        private set

    // Business logic
    fun somethingRelatedToBusinessLogic() { ... }
}

@Composable
fun ExampleScreen(viewModel: ExampleViewModel = viewModel()) {

    val uiState = viewModel.uiState
    ...

    Button(onClick = { viewModel.somethingRelatedToBusinessLogic() }) {
        Text("Do something")
    }
}
```

> μ°Έκ³  : ViewModelsμ νλ‘μΈμ€ μ¬μμ± ν λ³΄μ‘΄νλ €λ μνκ° ν¬ν¨λμ΄ μμΌλ©΄ SavedStateHandleμ μ¬μ©νμ¬ μ μ§νλ€.

### ViewModel and state holders

Android κ°λ°μμ ViewModelsμ μ΄μ μ λΉμ¦λμ€ λ‘μ§μ λν μ‘μΈμ€λ₯Ό μ κ³΅νκ³  νλ©΄μ νμν  μ νλ¦¬μΌμ΄μ λ°μ΄ν°λ₯Ό μ€λΉνλ λ° μ ν©νλ€.  
μ¦, μ΄μ μ λ€μκ³Ό κ°μ΄ νμ΄μ μΈ μ μλλ°,

- ViewModelμ μν΄ νΈλ¦¬κ±°λ μμμ κ΅¬μ± λ³κ²½ νμλ μ μ§λλ€.
- Navigation κ³Όμ ν΅ν©:
   - Navigation μ νλ©΄μ΄ λ°± μ€νμ μλ λμ ViewModelμ μΊμνλ€. λͺ©μ μ§λ‘ λμκ° λ μ΄μ μ λ‘λν λ°μ΄ν°λ₯Ό μ¦μ μ¬μ©ν  μ μλλ‘ νλ κ²μ΄ μ€μνλ€. μ΄κ²μ composable νλ©΄μ μλͺ μ£ΌκΈ°λ₯Ό λ°λ₯΄λ state holders λ‘ μννκΈ° λ μ΄λ €μ΄ μμμ΄λ€.
   - λμμ΄ λ°± μ€νμμ νλλ©΄ ViewModelλ μ§μμ§λ―λ‘ μνκ° μλμΌλ‘ μ λ¦¬λλ€. μ΄λ κ΅¬μ± λ³κ²½ λ±μΌλ‘ μΈν΄ μ νλ©΄μΌλ‘ μ΄λνλ λ± μ¬λ¬ κ°μ§ μ΄μ λ‘ λ°μν  μ μλ composable νκΈ°λ₯Ό λ°λΌλ³΄κ³  μλ κ²κ³Ό λ€λ₯΄λ€.
- Hiltμ κ°μ λ€λ₯Έ Jetpack λΌμ΄λΈλ¬λ¦¬μμ ν΅ν©.

> μ°Έκ³ : ViewModel μ΄μ μ΄ νλ‘μ νΈμ λ§μ§ μκ±°λ λ€λ₯Έ λ°©μμΌλ‘ μμμ μννλ κ²½μ° ViewModelμ μ±μμ state holders λ‘ μ΄λμν¬ μ μλ€.

State holders λ λ³΅ν© κ°λ₯νκ³  ViewModelκ³Ό μΌλ° state holders λ μ±μμ΄ λ€λ₯΄κΈ° λλ¬Έμ νλ©΄ μμ€ composable μλ λΉμ¦λμ€ λΌλ¦¬μ λν μ‘μΈμ€λ₯Ό μ κ³΅νλ ViewModelκ³Ό UI λ‘μ§ λ° UI μμμ μνλ₯Ό κ΄λ¦¬νλ state holders κ° λͺ¨λ μμ μ μλ€.  
ViewModelμ state holders λ³΄λ€ μλͺμ΄ λ κΈΈκΈ° λλ¬Έμ state holdersλ νμν κ²½μ° ViewModelμ μ’μμ±μΌλ‘ μ¬μ©ν  μ μλ€.

λ€μ μ½λλ ExampleScreenμμ ν¨κ» μλνλ ViewModel λ° μΌλ° state holders μ΄λ€.

``` kotlin
private class ExampleState(
    val lazyListState: LazyListState,
    private val resources: Resources,
    private val expandedItems: List<Item> = emptyList()
) { ... }

@Composable
private fun rememberExampleState(...) { ... }

@Composable
fun ExampleScreen(viewModel: ExampleViewModel = viewModel()) {

    val uiState = viewModel.uiState
    val exampleState = rememberExampleState()

    LazyColumn(state = exampleState.lazyListState) {
        items(uiState.dataToDisplayOnScreen) { item ->
            if (exampleState.isExpandedItem(item) {
                ...
            }
            ...
        }
    }
}
```
