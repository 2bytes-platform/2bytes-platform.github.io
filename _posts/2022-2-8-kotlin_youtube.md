---
layout: post
title: "π Kotlin κ°μλΈνΈ - 20κ°κΉμ§"
excerpt: "λλͺ¨μ Kotlin κ°μ’ μμ½λ³Έμλλ€ "
subtitle: "Kotlin youtube lecture"
toc: true
toc_sticky: true
toc_label: "νμ΄μ§ μ£Όμ λͺ©μ°¨"
date: 2022-2-8
tags: [Kotlin]
---

#### Generic

- ν΄λμ€λ ν¨μμμ μ¬μ©νλ μλ£νμ μΈλΆμμ μ§μ ν  μ μλ κΈ°λ₯
> μΊμ€ν μ΄μ© μ νλ‘κ·Έλ¨ μλλ₯Ό μ νμν¬ μ μμ

```kotlin
fun main() {
    UsingGeneric(A()).doShouting() // Sashaλ μ½νλ¦°μ λν΄μ λ μκ³  μΆμ΄μ!
    UsingGeneric(C()).doShouting() // Lisaλ μΈκ³΅μ§λ₯μ λ κ³΅λΆν©λλ€!
    
    doShouting(A()) // μΊμ€ν μμ΄ Aμ κ°μ²΄ κ·Έλλ‘ ν¨μμμ μ¬μ©
}

fun <T: A> doShouting(t: T) {
    t.shout()
}

open class A {
    open fun shout() {
        println("Sashaλ μ½νλ¦°μ λν΄μ λ μκ³  μΆμ΄μ!") 
    }
}

class C: A() {
    override fun shout() {
        println("Lisaλ μΈκ³΅μ§λ₯μ λ κ³΅λΆν©λλ€!") 
    }
}

class UsingGeneric<T: A> (val t: T) { // μνΌ ν΄λμ€λ₯Ό Aλ‘ μ νν μ λλ¦­ Tλ₯Ό μ μΈ
    fun doShouting() {
        t.shout()
    }
}
```

#### λ¦¬μ€νΈ

- List: λ°μ΄ν°λ₯Ό μ½λμμ μ§μ ν μμλλ‘ μ μ₯ν΄λλ ν΄λμ€. λ°μ΄ν°λ₯Ό λͺ¨μ κ΄λ¦¬νλ μ»¬λ μ ν΄λμ€μ μλΈ ν΄λμ€ μ€ κ°μ₯ λ¨μν νν.
- λ¦¬μ€νΈμ 2κ°μ§ νν  
  List<out T>: μμ± μμ λ£μ κ°μ²΄λ₯Ό λμ²΄, μΆκ°, μ­μ  ν  μ μμ
  MutableList<T>: κ°λ₯

```kotlin
fun main() {
	val family = listOf("μ¬μ€", "λ¦¬μ¬", "μ½μ½")

	println(family) // [μ¬μ€, λ¦¬μ¬, μ½μ½]

	for(ele in family) {
		println("${family}")
	}

	val b = mutableListOf(1, 2, 3)
	b.add(3, 5) // add(μ½μνκ³ μ νλ idx, value)
	println(b) // [1, 2, 3, 5]

	b.removeAt(3)
	println(b) // [1, 2, 3]

	b.shuffle()
	println(b) // λλ€ν κ°μ΄ λ°ν

	b.sort()
	println(b) // [1, 2, 3]
}
```

#### λ¬Έμμ΄ ν¨μ μ’λ₯

```kotlin
fun main() {
    val test1 = "Test.Kotlin.String"
    println(test1.length) // 18
    println(test1.lowercase()) // test.kotlin.string
    println(test1.uppercase()) // TEST.KOTLIN.STRING
    
    val test2 = test1.split(".")
    println(test2) // [Test, Kotlin, String]
    println(test2.joinToString()) // Test, Kotlin, String
    println(test2.joinToString("-")) // Test-Kotlin-String
    
    println(test1.substring(0..5)) // Test.K
    
    val nullString: String? = null
    val emptyString = ""
    val blankString = " "
    val normalString = "A"
    
    println(nullString.isNullOrEmpty()) // true, blankλ λΉμ΄μλ κ²μΌλ‘ μ·¨κΈX
    println(emptyString.isNullOrEmpty()) // true
    println(blankString.isNullOrEmpty()) // false
    println(normalString.isNullOrEmpty()) // false

    println(nullString.isNullOrBlank()) // true
    println(emptyString.isNullOrBlank()) // true
    println(blankString.isNullOrBlank()) // true, blank μνλ λΉμ΄μλ κ²μΌλ‘ μ·¨κΈ
    println(normalString.isNullOrBlank()) // false
  
    val test3 = "Sasha"
    val test4 = "Lisa"
    
    println(test3.startsWith("Sa")) // true
    println(test4.endsWith("Sa")) // false
    println(test4.contains("sa")) // true
}
```

#### null κ°μ μ²λ¦¬νλ λ°©λ²? λμΌνμ§λ₯Ό νμΈνλ λ°©λ²?

- null μνλ‘ μμ±μ΄λ ν¨μλ₯Ό μ°λ €κ³  νλ©΄ null pointer exception(null κ°μ²΄λ₯Ό μ°Έμ‘°νλ©΄ λ°μνλ μ€λ₯)μ΄ λ°μ
- null checkκ° μμ΄λ μ»΄νμΌ λμ§ μμ

- "?.": null safe operator, μ°Έμ‘°μ°μ°μ μ€ν μ , κ°μ²΄κ° nullμΈμ§ νμΈλΆν°νκ³  κ°μ²΄κ° nullμ΄λΌλ©΄ λ·κ΅¬λ¬Έμ μ€νX
- "?:": elvis operator, κ°μ²΄κ° nullμ΄ μλλΌλ©΄ κ·Έλλ‘ μ€ννλ©° λ°λμΌ κ²½μ° μ°μΈ‘μ κ°μ²΄λ‘ λμ²΄
- "!!.": non-null assertion operator, μ°Έμ‘°μ°μ°μ μ¬μ© μ null μ¬λΆλ₯Ό μ»΄νμΌ μ νμΈνμ§ μλλ‘ νμ¬ λ°νμ μ null pointer
  exceptionμ΄ λλλ‘ μΌλΆλ‘ λ°©μΉνλ μ°μ°μ

```kotlin
fun main() {
    val a: String? = null
    println(a?.uppercase()) // null
    println(a?:"default".uppercase()) // DEFAULT
    println(a!!.uppercase()) // Exception in thread "main" java.lang.NullPointerException
}
```

- null checkλ₯Ό μν΄ ifλ¬Έ λμ  μ°μ°μ + scope ν¨μ μ¬μ©νλ©΄ νΈλ¦¬

```kotlin
fun main() {
    var a: String? = null
    a?.run { // nullμ μ²΄ν¬νκΈ° μν΄ μ€μ½νν¨μ μ¬μ©
        println(uppercase())
        println(lowercase())
    }
}
```
- λ΄μ©μ λμΌμ±: heap μμ μ£Όμκ° λ¬λΌλ λ΄μ©μ΄ κ°λ€λ©΄ λ κ°μ²΄λ κ°μ a == b
- κ°μ²΄μ λμΌμ±: μλ‘ λ€λ₯Έ λ³μκ° λ©λͺ¨λ¦¬ μμ λμΌν κ°μ²΄λ₯Ό κ°λ₯΄ν¬ λ a === b

```kotlin
fun main() {
    val a = Product("μ½λΌ", 1000)
    val b = Product("μ½λΌ", 1000)
    var c = a
	var d = Product("μ¬μ΄λ€", 500)    
    
    println(a == b) // true
    println(a === b) // false 
    
    println(a == c) // true
    println(a === c) // true
    
    println(a == d) // false
    println(a === d) // false

}

class Product(val name: String, val price: Int) {
    override fun equals(other: Any?): Boolean {
        if (other is Product) {
    		return other.name == name && other.price == price 
        } else {
            return false
        }	
    }
}
```

#### μ€μ²© ν΄λμ€μ λ΄λΆ ν΄λμ€

- μ€μ²© ν΄λμ€μ λ΄λΆ ν΄λμ€λ ν΄λμ€ κ°μ μ°κ³μ±μ νννμ¬ μ½λμ κ°λμ± λ° μμ± νΈμμ±μ μ¦λνλλ° λͺ©μ μ΄ μμ
- μ€μ²© ν΄λμ€: ν΄λμ€ μλ‘ κ° κ°νκ² μ°κ΄λμ΄ μλ€λ μλ―Έλ₯Ό μ λ¬νκΈ° μν΄ λ§λ€μ΄μ§ νμ
- λ΄λΆ ν΄λμ€: νΌμμ κ°μ²΄λ₯Ό λ§λ€ μλ μκ³ , μΈλΆ ν΄λμ€μ κ°μ²΄κ° μμ΄μΌλ§ μμ±κ³Ό μ¬μ©μ΄ κ°λ₯

```kotlin
fun main() {
  Outer.Nested().introduce() // "Nested Class"

  val outer = Outer()
  val inner = outer.Inner()

  inner.introduceInner() // "Inner Class"
  inner.introduceOuter() // "Outer Class"

}

class Outer {
  var text = "Outer Class"

  class Nested() {
    fun introduce() {
      println("Nested Class")
    }
  }

  inner class Inner {
    var text = "Inner Class"

    fun introduceInner() {
      println(text)
    }

    fun introduceOuter() {
      println(this@Outer.text)
    }
  }
}
```