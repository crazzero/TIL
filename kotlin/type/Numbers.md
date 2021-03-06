# π’ [Numbers](https://kotlinlang.org/docs/basic-types.html#numbers)

## Integer types (μ μν νμλ€)

### types

| Type | Size(bits) | Min value | Max value |
| --- | --- | --- | --- |
| Byte | 8 | -128 | 127 |
| Short | 16 | -32768 | 32767 |
| Int | 32 | -2,147,483,648 (-2^31) | 2,147,483,647 (2^31 - 1) |
| Long | 64 | -9,223,372,036,854,775,808 (-2^63) | 9,223,372,036,854,775,807 (2^63- 1) |

### usages

```kotlin
val one = 1 // Int
val threeBillion = 3000000000 // Long
val oneLong = 1L // Long
val oneByte: Byte = 1
```

## Floating-point types (μμν νμλ€)

### types

| Type | Size (bits) | Significant bits | Exponent bits | Decimal digits |
| --- | --- | --- | --- | --- |
| Float | 32 | 24 | 8 | 6-7 |
| Double | 64 | 53 | 11 | 15-16 |

### usages

```kotlin
val pi = 3.14 // Double
// val one: Double = 1 // Error: type mismatch
val oneDouble = 1.0 // Double

val e = 2.7182818284 // Double
val eFloat = 2.7182818284f // Float, actual value is 2.7182817

fun main() {
    fun printDouble(d: Double) { print(d) }

    val i = 1
    val d = 1.0
    val f = 1.0f

    printDouble(d)
//    printDouble(i) // Error: Type mismatch
//    printDouble(f) // Error: Type mismatch
}
```

## Literal constants (λ¦¬ν°λ΄ μμ)

Kotlin μμλ μ μν κ°λ€μ λν΄μ, λ€μκ³Ό κ°μ΄ λ¦¬ν°λ΄ μμλ₯Ό μ§μν©λλ€.

- Decimals: 123
  - Longs are tagged by a capital L: 123L
- Hexadecimals: 0x0F
- Binaries: 0b00001011
>`0` prefix λ₯Ό λΆμ¬μ μ¬μ©νλ octal literal μ μ§μνμ§ μμ΅λλ€.

Kotlin μμλ μμν κ°λ€μ λν΄μ, κΈ°μ‘΄μ νκΈ°λ²(conventional notation)μ μ§μν©λλ€.

- Doubles by default: 123.5, 123.5e10
- Floats are tagged by f or F: 123.5f

`UnderScore(_)` λ₯Ό μ¬μ©ν΄μ readability λ₯Ό λλ¦΄ μ μμ΅λλ€.

```kotlin
val oneMillion = 1_000_000
val creditCardNumber = 1234_5678_9012_3456L
val socialSecurityNumber = 999_99_9999L
val hexBytes = 0xFF_EC_DE_5E
val bytes = 0b11010010_01101001_10010100_10010010
```

## Numbers representation on the JVM (JVM μμμ Numbers)

JVM νλ«νΌμμ, numbers λ int, double κ³Ό κ°μ primitive types λ‘ μ μ₯λλ€.  
μ¬κΈ°μ μ€μν ν¬μΈνΈλ nullable κ°μ²΄λ κ°μ number μΌμ§λΌλ λ€λ₯Έ κ°μ²΄λ‘ νλ¨λ  μ μλ€λ μ μ΄λ€.  
μλ μμμ κ°μ΄ κ²°κ³Όκ° λμ€λ μ΄μ λ, a μ κ²½μ° -128 κ³Ό 127 μ¬μ΄μ κ°μ΄λ―λ‘ JVM μμ λμΌν κ°μ²΄λ‘ μΈμν  μ μκΈ° λλ¬Έμ΄λ€.  
νμ§λ§ b μ κ²½μ°μλ ν΄λΉμ¬ν­μ΄ μκΈ° λλ¬Έμ λ€λ₯Έ κ°μ²΄λ‘ μΈμλλ€.  

```kotlin
val a: Int = 100
val boxedA: Int? = a
val anotherBoxedA: Int? = a

val b: Int = 10000
val boxedB: Int? = b
val anotherBoxedB: Int? = b

println(boxedA === anotherBoxedA) // true
println(boxedB === anotherBoxedB) // false
```

κ°μ²΄κ° λ€λ₯Ό λΏ, λ κ°μ κ°λ€λ κ²μ μ μ μλ€.
```kotlin
val b: Int = 10000
println(b == b) // Prints 'true'
val boxedB: Int? = b
val anotherBoxedB: Int? = b
println(boxedB == anotherBoxedB) // Prints 'true'
```

## Explicit conversions (λͺμμ  λ³ν)

μμ νμλ€μ΄ ν° νμλ€μ SubType μ΄λΌκ³  λ³Ό μλ μλ€. μ¦, Int λ³΄λ€ Long μ΄ λ λμ κ°λμ΄λΌκ³  ν΄μ, Int κ° Long μ SubType μ μλλ€.

```kotlin
// Hypothetical code, does not actually compile:
val a: Int? = 1 // A boxed Int (java.lang.Integer)
val b: Long? = a // implicit conversion yields a boxed Long (java.lang.Long)
print(b == a) // Surprise! This prints "false" as Long's equals() checks whether the other is Long as well
```

μ΄λ Byte μ Int μ κ΄κ³μμλ λμΌνλ€.

```kotlin
val b: Byte = 1 // OK, literals are checked statically
// val i: Int = b // ERROR
val i1: Int = b.toInt()
```

λͺ¨λ  Number νμλ€μμλ λ€λ₯Έ νμμΌλ‘μ μ νμ΄ κ°λ₯νλ€.

- toByte(): Byte
- toShort(): Short
- toInt(): Int
- toLong(): Long
- toFloat(): Float
- toDouble(): Double
- toChar(): Char

μλμ κ°μ΄ νμ μΆλ‘ μ΄ κ°λ₯ν κ²½μ°μλ λ³λλ‘ μ νμ μ μ©μμΌμ€ νμκ° μλ€.

```kotlin
val l = 1L + 3 // Long + Int => Long
```

## Operations

Kotlin Number μμλ λ€μμ Operator λ₯Ό μ κ³΅νλ€.  

- `+` 
- `-`
- `*`
- `/`
- `%`

### usages

```kotlin
println(1 + 2)
println(2_500_000_000L - 1L)
println(3.14 * 2.71)
println(10.0 / 3)
```

### Division of integers

- μ μλΌλ¦¬ λλλ©΄ νμμ λ§κ² μ μ κ°μ΄ λμ¨λ€.

```kotlin
val x = 5 / 2
//println(x == 2.5) // ERROR: Operator '==' cannot be applied to 'Int' and 'Double'
println(x == 2)

val x = 5L / 2
println(x == 2L)
```

- μμνμ νλλΌλ λ£μ΄μ£Όκ² λλ©΄ μμκ°μ΄ λμ¨λ€.

```kotlin
val x = 5 / 2.toDouble()
println(x == 2.5)
```

### Bitwise operations

Kotlin μμλ μ μνμ νν΄μ *Bitwise μ°μ°μ*λ₯Ό μ κ³΅νλ€.

- shl(bits) β signed shift left
- shr(bits) β signed shift right
- ushr(bits) β unsigned shift right
- and(bits) β bitwise and
- or(bits) β bitwise or
- xor(bits) β bitwise xor
- inv() β bitwise inversion

### Floating-point numbers comparison

μμνμλ λ€μκ³Ό κ°μ λ°©λ²μΌλ‘ λ κ°μ λΉκ΅ν  μ μλ€.

- Equality checks: `a == b` and `a != b`
- Comparison operators: `a < b`, `a > b`, `a <= b`, `a >= b`
- Range instantiation and range checks: `a..b`, `x in a..b`, `x !in a..b`

μ¬κΈ°μ λ°λμ μμλμ΄μΌ ν  λΆλΆμ 

- `NaN` μκΈ° μμ κ³Ό κ°μ μ μλ€.
- `NaN` λ `POSITIVE_INFINITY` λ₯Ό ν¬ν¨ν μ΄λ€ λ€λ₯Έ μμλ€λ³΄λ€ ν¬λ€.
- `-0.0` μ `0.0` λ³΄λ€ μλ€.

