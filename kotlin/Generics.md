# π¨βπ¦ Generics

μ΄ λ¬Έμλ [Kotlin-generics κ³΅μλ¬Έμ](https://kotlinlang.org/docs/generics.html) κΈ°λ°μΌλ‘ μμ±νμλ€.

## κ°μ

Genericμ΄λ Class μ κ°μ²΄ μμ±μλΆν° μ΄λ€ μλ£νμ μ¬μ©ν  κ±΄μ§ μ μ(κ°μ )νμ¬μ,  
ν΄λΉ Class μμ λ§€κ°λ³μμ μ¬μ©λλ μλ£νμ λ£°μ μ νκ³  κ·Έλ‘μΈν΄ μμ μ±μ λμ΄λ λκ΅¬λ₯Ό λ§νλ€.  

μλ μμμ²λΌ Kotlin μμμ ν΄λμ€λ Java μμ μ²λΌ Type μ κ°μ§ μ μκ³ , μΌλ°μ μΌλ‘ `<T>`λ‘ νκΈ°νλ€.  

```kotlin
class Sample<T>(t: T) {
    var value = t
}
```

νμμ κ°μ§κ³  μλ Class κ°μ²΄λ₯Ό μμ±νκ³  νμΈνκΈ° μν΄μλ μλμ²λΌ ν΄μ£Όλ©΄ λλ€.  
λλ² μ§Έ μ€μμ λ³λλ‘ νμμ λ£μ§ μμλ λλ μ΄μ λ "Sample" μ ν΅ν΄, νμ μΆλ‘ μ΄ κ°λ₯νκΈ° λλ¬Έμ΄λ€.

```kotlin
val firstSample: Sample<String> = Sample<String>("Sample")
val secondSample = Sample("Sample")
```

Generic μ μ¬μ©νλ©΄, μλμ μ΄μ μ μ±κΈΈ μ μλ€.

1. Type Safety λ₯Ό νλ³΄ ν  μ μλ€.
2. Runtime μλ¬κ° μλ, Compile νμμ μλ¬λ₯Ό λ°μμμΌμ λ³΄λ€ μμ ν μ½λμμ±μ΄ κ°λ₯νλ€.
3. νλνλ TypeCasting ν΄μ£Όλ λΆλΆμ μμ¨ μ μλ€.

κ·Έλ¦¬κ³  Generic μ¬μ©μμ νμμ΄ μ΄λ λ²μκΉμ§ μν₯μ λ―ΈμΉ  κ²μΈμ§ μ ν  μ μλλ°, μ΄λ₯Ό Type Bound λΌκ³  νλ€.  

Type Bound μ’λ₯ μλ μλ 3κ°μ§κ° μκ³ , μ§κΈλΆν° κ° λ΄μ©μ λν΄ μ λ¦¬ν΄λ³΄λ €κ³  νλ€.

- Invariant(λΆλ³, λ¬΄κ³΅λ³)
- covariant(κ³΅λ³)
- contravariant(λ°κ³΅λ³, λ°λ³)

## Invariant(λΆλ³, λ¬΄κ³΅λ³)

μΌλ¨ Variance(λ³ν) κ΄λ ¨ λ΄μ©μ λ€μ΄κ°κΈ° μμ, SubType μ λν κ°λμ μμμΌ νλ€.  
SubTypeμ΄λ μ΄λ€ Classκ° λ€λ₯Έν΄λμ€λ₯Ό μμλ°μκ²μ μλ―Ένλ€.  
λ€μκ³Ό κ°μ΄ Line, Surface Class κ° μλ€κ³  νμ λ, Surface λ Line μ μμλ°κ³  μμΌλ―λ‘ Surface λ Line μ SubType μ΄λΌκ³  ν  μ μλ€.  

```kotlin
open class Line() {
    val x = 0
}

class Surface : Line(){
    val y = 1
}
```

μ¦, Line μ΄ νμν κ³³μ Surface λ₯Ό λ£μ΄λ λ¬Έμ κ° μλ€λ©΄ Surface λ Line μ SubType μ΄λΌκ³  ν  μ μλ€.  

``` kotlin
var line = Line()
var surface = Surface()
line = surface // OK!!

var line = Line()
var surface = Surface()
surface = line // ERROR!!
```

μ΄μ  λ³Έλ‘ μΌλ‘ λμμ Invariant μ λν΄μ μμλ³΄λ©΄,  
Invariant λΌλ κ±΄ μμ κ΄κ³μ νλλ μκ΄μμ΄ λ± μκΈ° μμ μ νμλ§ νμ©νλ κ²μ λ»νλ€.  
**Kotlin** λΏλ§ μλλΌ **Java** μμλ Type κ΄κ³λ₯Ό λ³λλ‘ μ§μ ν΄μ£Όμ§ μμ κ²½μ°, λͺ¨λ  Generic Class λ κΈ°λ³Έμ μΌλ‘ Invariant λ‘ λλ€.  

μλ μμλ₯Ό λ³΄λ©΄, String μ Any μ SubType μ΄λ€.  
κ·Έλμ String κ°μ²΄λ₯Ό Any κ°μ²΄μ λ£μ΄μ€ μ μλ€.  

```kotlin
var str = "String"
var any = Any()
str = any // ERROR!!
any = str // OK!!
```

νμ§λ§, MutableList μ κ²½μ°λ₯Ό λ³΄λ©΄ λΆλͺν Generic μμ λ€μ΄κ° μλ νμμ΄ SubType κ΄κ³μμλ λΆκ΅¬νκ³ , λλ² μ§Έ μ€ λΆν° error κ° λ¨λ κ²μ νμΈν  μ μλ€.  
μ΄λ μ½κΈ° λ° μ°κΈ°κ° κ°λ₯ν MutableList μ κ²½μ° λ¬΄κ³΅λ³μ±μ κ°μ§κΈ° λλ¬ΈμΈλ°, λ§μ½ μ΄λ₯Ό νμ©ν΄μ£Όκ² λλ©΄, 4λ²μ§Έ μ€μμ λ°νμ Exception μ΄ λ°μνκ² λλ€.  
μ΄λ₯Ό νΌν΄μ£ΌκΈ° μν΄μ λ¬΄κ³΅λ³μ±μ κ°μ§κ³  μκ³  μ΄λ₯Ό ν΅ν΄ κ°λ°μλ€μ΄ μ’ λ μμ νκ² μ»΄νμΌλ¨μμ μλ¬λ₯Ό μ‘μ μ μκ²λ λμμ€λ€.

```kotlin
val strings: MutableList<String> = mutableListOf("1")
val anys: MutableList<Any> = strings // ERROR!!
anys.add(0)
val str1: String = anys[0] // class cast exception
```

## Covariant(κ³΅λ³)

Covariant μλ λ€μκ³Ό κ°μ νΉμ§μ΄ μλ€.

- λͺ¨λ  μ½κΈ°κ° κ°λ₯νκ³  λͺ¨λ  μ°κΈ°λ λΆκ°λ₯νλ€. (read-only)
- μκΈ° μμ  νΉμ μμμ κ°μ²΄λ₯Ό νμ©νλ€.
- Java μ `<? extends T>`
- Kotlin μ out

μλ κ³΅μ λ¬Έμμ λμμλ μμλ₯Ό λ³΄λ©΄, 
`interface Source<out T>` λ‘ λ§λ€μ΄ μ€μ,  
Any λ‘ νμμ κ°μ§λ €κ³  νλ objects μ SubType μΈ String μ νμμΌλ‘ κ°μ§κ³  μλ strs λ₯Ό λ£μ΄μ€ μ μλ κ²μ΄λ€.

```kotlin
interface Source<out T> {
    fun nextT(): T
}

fun demo(strs: Source<String>) {
    val objects: Source<Any> = strs // OK!!
    // ...
}
```

## Contravariant(λ°λ³)

Contravariant μλ λ€μκ³Ό κ°μ νΉμ§μ΄ μλ€.

- λͺ¨λ  μ°κΈ°κ° κ°λ₯νκ³  λͺ¨λ  μ½κΈ°λ λΆκ°λ₯νλ€. (write-only)
- μκΈ° μμ  νΉμ λΆλͺ¨μ κ°μ²΄λ₯Ό νμ©νλ€.
- Java μ `<? super T>`
- Kotlin μ in

μλ κ³΅μ λ¬Έμμ λμμλ μμλ₯Ό λ³΄λ©΄,
`interface Comparable<in T>` λ‘ λ§λ€μ΄ μ€μ,  
1.0 μ Type μΈ Double μ Number μ SubType μ΄κΈ° λλ¬Έμ, `x.compareTo(T)` μ T μμ λ£μ΄μ€ μ μκ³ ,  
`y: Comparable<Double>` μλ€κ° `x` λ₯Ό λ£μ΄μ€ μ μλ€.  

```kotlin
interface Comparable<in T> {
    operator fun compareTo(other: T): Int
}

fun demo(x: Comparable<Number>) {
    x.compareTo(1.0)
    val y: Comparable<Double> = x // OK!
}

```

## μ μΈλΆ Variance

μμμ μΈκΈν μμμ²λΌ out κ³Ό in ν€μλλ₯Ό μ μΈλΆμμ μ¬μ©νλ κ²μ μ μΈλΆ Variance λΌκ³  νλ€.  
μ΄λ₯Ό ν΅ν΄, νμ μΈμλ‘ μ μν Tμ λν΄ Tλ₯Ό μ¬μ©νλ ν΄λμ€κ° Tμ producer λ‘λ§ μ°μΌ κ²μΈμ§ consumerλ‘λ§ μ°μΌ κ²μΈμ§λ₯Ό μ μΈλΆμμ μ μλ₯Ό ν΄μ€ μ μλ€.

## μ¬μ©λΆ Variance

μ μΈλΆ Variance κ° μΌλ°μ μΌλ‘ μ¬μ©λλ λ°©μμ΄κ³  κ΅μ₯ν μ μ©νμ§λ§ λ€μκ³Ό κ°μ κ²½μ°μλ μ¬μ©νμ§ λͺ»νλ€.

```kotlin
class Array<T>(val size: Int) {
    fun get(index: Int): T { ... }
    fun set(index: Int, value: T) { ... }
}
```
TλΌλ νμ μΈμκ° ν¨μμ μΈμλ‘λ λ€μ΄κ°κ³  `fun set(index: Int, value: T) { ... }`  
ν¨μμ λ°νκ°μΌλ‘λ λ€μ΄κ°κΈ° λλ¬Έμ `fun get(index: Int): T { ... }`  
μμ κ°μ κ²½μ°μλ covariant(κ³΅λ³), contravariant(λ°λ³) λ λ€ μ¬μ©μ΄ λΆκ°λ₯νλ€.  
κ·Έλ λ€κ³  μ¬μ©μ μνμ±λ‘ invariant(λΆλ³) μΈ μνλ‘ λ¨κ²¨λλ©΄ λ€μκ³Ό κ°μ λΆνΈν¨μ΄ μλ€.

```kotlin
fun copy(from: Array<Any>, to: Array<Any>) {
    assert(from.size == to.size)
    for (i in from.indices)
        to[i] = from[i]
}
val ints: Array<Int> = arrayOf(1, 2, 3)
val any = Array<Any>(3) { "" } 
copy(ints, any)
//   ^ type is Array<Int> but Array<Any> was expected
```
copyλ ClassCastExceptionμ μ λ°νμ§λ μμ§λ§ λͺνν κ·Έλ λ€λκ±Έ μ»΄νμΌλ¬μκ² μ λ¬ν΄μ€ μ μμ΄μΌ νλ€.  
κ·Έλ μ§ μμΌλ©΄ μμ²λΌ μ»΄νμΌ μλ¬κ° λ°μνκ² λλ€.  
μ΄ λ μ¬μ©νλ κ²μ΄ μ¬μ©λΆ variance μ΄λ€.  

```kotlin
fun copy(from: Array<out Any>, to: Array<Any>) { ... }
```
μμ κ°μ μ μΈμ from λ§€κ°μΈμκ° producerλ‘μ¨λ§ μ¬μ©λ  μ μλ€λ κ²μ λͺμν΄μ£ΌκΈ° λλ¬Έμ, κ°μ μ μΌλ‘ copyλ΄μμλ consumeνλ λ©μλ(set)λ€μ μ¬μ©μ΄ μ νλλ€.

## Star-projections

`*` μ μ΄μ©ν projectionμ λ€μ μμμ κ°μ΄ κ°λ₯ν λͺ¨λ  νμμ μ¬μ©ν  μ μκ² ν΄μ€λ€.  

```kotlin
interface Function<in T, out U>
Function<*, String> = Function<in Nothing, String>
Function<Int, *> = Function<Int, out Any?>
Function<*, *> =Function<in Nothing, out Any?>
```

covariant λ `*` λ₯Ό λ§λλ©΄ `out Any?` λ‘ λ³νκ³ , contravariantλ `*`λ₯Ό λ§λλ©΄ `in Nothing` μΌλ‘ λ³νλ€.  
μ¦, νμμ λͺ¨λ₯Ό λ μΈ μλ μμ§λ§ μ°λ¦¬κ° projection μ μ μ©μμΌλ¨κΈ° λλ¬Έμ out μμλ set κ°μ consume λ©μλλ₯Ό μ¬μ©ν  μ μκ² λκ³ , in μμλ get κ³Ό κ°μ produce λ©μλλ₯Ό μ¬μ©ν  μ μκ² λλ€.

## Why in, out?

κ·Έλ λ€λ©΄ Kotlin μμλ μ Convariant μ Contravariant μ outκ³Ό in μ΄λΌλ ν€μλλ₯Ό μ¬μ©ν κΉ?  
μΌλ¨, C#μμλ Kotlinκ³Ό κ°μ΄ convariant μ contravariant λ₯Ό out, in ν€μλλ‘ μ¬μ©νλλ°,  
κ³΅μ ννμ΄μ§μμ μλμ κ°μ΄ μ€λͺνκ³  μλ κ²μ λ³΄λ©΄ Kotlin μμ μ΄ κ°λμ κ·Έλλ‘ κ°μ Έμ¨λ― νλ€.  

>The words in and out seem to be self-explanatory (as theyβve already been used successfully in C# for quite some time)

μ¬κΈ°μ Joshua Blochλ convariant(out) μ contravariant(in) μ μ­ν μ λν΄μ λ€μκ³Ό κ°μ΄ μ λ¦¬νλ€. 

>PECS (Producer Extends Consumer Super)
>Producersμμ μ½κ³ , Consumersμμ μ΄λ€.  
>μ λ€λ¦­μ μ΅λμ μ μ©μ±μ μν΄, μΈμλ₯Ό producersμ consumersλ‘ κ΅¬λΆνμ¬ μ¬μ©νλΌ.

μ¦, producer μ consumer μ κ΄κ³λ μλμ κ°μ΄ μ λ¦¬ν  μ μλ€.
- Producer == out == μ½κΈ°
- Consumer == in == μ°κΈ°



