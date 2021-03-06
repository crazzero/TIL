# [π© Serialization](https://github.com/Kotlin/kotlinx.serialization/blob/master/docs/serialization-guide.md)

*serialization* μ application μμ μ¬μ©νλ λ°μ΄ν°λ₯Ό λ€νΈμν¬λ₯Ό ν΅ν΄ μ μ‘νκ±°λ λ°μ΄ν°λ² μ΄μ€ λλ νμΌμ μ μ₯ν  μ μλ νμμΌλ‘ λ³ννλ process μ΄λ€.  
*deserialization* λ μΈλΆ μμ€μμ λ°μ΄ν°λ₯Ό μ½κ³  μ΄λ₯Ό λ°νμ κ°μ²΄λ‘ λ³ννλ λ°λ process μ΄λ€.  
*serialization* κ³Ό *deserialization* μ λ°μ΄ν°λ₯Ό κ΅ννλ κ±°μ λͺ¨λ  application μμ νμμ μΈ λΆλΆμλλ€.

[JSON](https://www.json.org/json-en.html) λ° [protocol buffers](https://developers.google.com/protocol-buffers)μ κ°μ data serialization formats μ νΉν common νκ² μ¬μ©λμ΄μ§κ³  μλ€.   
λΆκ°μ€λͺ ν΄λ³΄μλ©΄ μμ serialization formats λ μΈμ΄ μ€λ¦½μ μ΄κ³  νλ«νΌ μ€λ¦½μ μ΄κΈ° λλ¬Έμ νλ μΈμ΄λ‘ μμ±λ μμ€ν κ°μ λ°μ΄ν° κ΅νμ΄ κ°λ₯νλ€.

Kotlinμμμ λ°μ΄ν° μ§λ ¬ν λκ΅¬λ λ³λμ κ΅¬μ±μμμΈ kotlinx.serialization μΌλ‘ μ¬μ©ν  μ μμΌλ©°,  
Gradle νλ¬κ·ΈμΈμΈ org.jetbrains.kotlin.plugin.serialization κ³Ό runtime libraries λ κ°μ§ μ£Όμ λΆλΆμΌλ‘ κ΅¬μ±λλ€.

## Libraries

kotlinx.serializationμ μ§μλλ λͺ¨λ  νλ«νΌ(JVM, JavaScript, Native)κ³Ό λ€μν μ§λ ¬ν νμ(JSON, CBOR, νλ‘ν μ½ λ²νΌ λ±)μ λν sets of libraries(λΌμ΄λΈλ¬λ¦¬ μΈνΈ)λ₯Ό μ κ³΅νλ€.  
μλ Formats μΉμμμ μ§μλλ μ§λ ¬ν νμμ μ μ²΄ λͺ©λ‘μ μ°Ύμ μ μλ€.

λͺ¨λ  Kotlin μ§λ ¬ν λΌμ΄λΈλ¬λ¦¬λ org.jetbrains.kotlinx: κ·Έλ£Ήμ μνλ©°, μ΄λ¦μ kotlinx-serialization-μΌλ‘ μμνκ³  μ§λ ¬ν νμμ λ°μνλ μ λ―Έμ¬κ° μλ€.
- org.jetbrains.kotlinx:kotlinx-serialization-jsonμ Kotlin projectμ λν JSON μ§λ ¬νλ₯Ό μ κ³΅νλ€.
- org.jetbrains.kotlinx:kotlinx-serialization-cborλ CBOR μ§λ ¬νλ₯Ό μ κ³΅νλ€.

νλ«νΌλ³ μν°ν©νΈλ μλμΌλ‘ μ²λ¦¬λκΈ° λλ¬Έμ, μλμΌλ‘ μΆκ°ν  νμκ° μκ³ , JVM, JS, Native λ° λ€μ€ νλ«νΌ νλ‘μ νΈμμ λμΌν μ’μμ±μ μ¬μ©νλ©΄ λλ€.

kotlinx.serialization λΌμ΄λΈλ¬λ¦¬λ Kotlinμ λ²μ  κ΄λ¦¬μ μΌμΉνμ§ μλ μμ²΄ λ²μ  κ΄λ¦¬ κ΅¬μ‘°λ₯Ό μ¬μ©νλ©°, μ΅μ  λ²μ μ μ°ΎμΌλ €λ©΄ [GitHubμ release](https://github.com/Kotlin/kotlinx.serialization/releases)λ₯Ό νμΈνλ©΄ λλ€.

## Formats

kotlinx.serializationμλ λ€μν μ§λ ¬ν νμμ λν λΌμ΄λΈλ¬λ¦¬κ° ν¬ν¨λμ΄ μλ€.

- JSON: kotlinx-serialization-json
- protocol buffers: kotlinx-serialization-protobuf
- CBOR: kotlinx-serialization-cbor
- properties: kotlinx-serialization-properties
- HOCON: kotlinx-serialization-hocon(only on JVM)

JSON μ§λ ¬ν(kotlinx-serialization-core)λ₯Ό μ μΈν λͺ¨λ  λΌμ΄λΈλ¬λ¦¬λ [Experimental](https://kotlinlang.org/docs/components-stability.html)μ΄λ―λ‘ μκ³  μμ΄ APIκ° λ³κ²½λ  μ μλ€.

YAML λλ Apache Avroμ κ°μ΄ λ λ§μ serialization formats λ₯Ό μ§μνλ community-maintained libraries λ μλ€.  
μ¬μ© κ°λ₯ν μ§λ ¬ν νμμ λν μμΈν λ΄μ©μ [kotlinx.serialization λ¬Έμ](https://github.com/Kotlin/kotlinx.serialization/blob/master/formats/README.md)λ₯Ό μ°Έμ‘°νλ©΄ λλ€.

## Example: JSON serialization

*serialization* μ μ¬μ©ν΄μ Kotlin κ°μ²΄λ₯Ό JSONμΌλ‘ μ§λ ¬ννλ λ°©λ²

μμνκΈ° μ μ νλ‘μ νΈμμ Kotlin serialization tools μ μ¬μ©ν  μ μλλ‘ λΉλ μ€ν¬λ¦½νΈλ₯Ό κ΅¬μ±ν΄μΌ νλ€.

1. Kotlin μ§λ ¬ν Gradle νλ¬κ·ΈμΈ org.jetbrains.kotlin.plugin.serialization μ μ μ©νλ€

```gradle
plugins {
    id 'org.jetbrains.kotlin.jvm' version '1.5.31'
    id 'org.jetbrains.kotlin.plugin.serialization' version '1.5.31'
}
```

2. JSON μ§λ ¬ν λΌμ΄λΈλ¬λ¦¬ μ’μμ± μΆκ°: org.jetbrains.kotlinx:kotlinx-serialization-json:1.3.0

```gradle
dependencies {
    implementation 'org.jetbrains.kotlinx:kotlinx-serialization-json:1.3.0'
}
```

μ΄μ  μ½λμμ μ§λ ¬ν APIλ₯Ό μ¬μ©ν  μ€λΉκ° λμκ³ , APIλ kotlinx.serialization ν¨ν€μ§μ kotlinx.serialization.jsonκ³Ό κ°μ νμλ³ νμ ν¨ν€μ§μ μλ€.

3. @Serializable μ£Όμμ λ¬μ ν΄λμ€λ₯Ό μ§λ ¬ν κ°λ₯νκ² λ§λ λ€
```kotlin
import kotlinx.serialization.Serializable

@Serializable
data class Data(val a: Int, val b: String)
```

4. Json.encodeToString()μ νΈμΆνμ¬ μ΄ ν΄λμ€μ μΈμ€ν΄μ€λ₯Ό μ§λ ¬ννλ€
```kotlin
import kotlinx.serialization.Serializable
import kotlinx.serialization.json.Json
import kotlinx.serialization.encodeToString

@Serializable
data class Data(val a: Int, val b: String)

fun main() {
   val json = Json.encodeToString(Data(42, "str"))
}
```

5. JSON νμμΌλ‘ json κ°μ²΄μ μνλ₯Ό ν¬ν¨νλ λ¬Έμμ΄μ μ»μ μ μλ€
`{"a": 42, "b": "str"}`

6. ν λ²μ νΈμΆλ‘ list μ κ°μ collections λ₯Ό μ§λ ¬νν  μ μλ€
```kotlin
val dataList = listOf(Data(42, "str"), Data(12, "test"))
val jsonList = Json.encodeToString(dataList)
```

7, JSONμμ κ°μ²΄λ₯Ό μ­μ§λ ¬ννλ €λ©΄ decodeFromString() ν¨μλ₯Ό μ¬μ©νλ©΄ λλ€
```kotlin
import kotlinx.serialization.Serializable
import kotlinx.serialization.json.Json
import kotlinx.serialization.decodeFromString

@Serializable
data class Data(val a: Int, val b: String)

fun main() {
   val obj = Json.decodeFromString<Data>("""{"a":42, "b": "str"}""")
}
```
