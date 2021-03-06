---
layout: post
title: "π Kotlin κ°μλΈνΈ - 30κ°κΉμ§"
excerpt: "λλͺ¨μ Kotlin κ°μ’ μμ½λ³Έμλλ€ "
subtitle: "Kotlin youtube lecture"
toc: true
toc_sticky: true
toc_label: "νμ΄μ§ μ£Όμ λͺ©μ°¨"
date: 2022-2-14
tags: [Kotlin]
---

#### DATA class & ENUM class 
- data class: λ°μ΄ν°λ₯Ό κ΄λ¦¬νλλ° μ΅μ ν λ classμ΄λ©° 5κ°μ§ κΈ°λ₯μ λ΄λΆμ μΌλ‘ μλ μμ±. λ°°μ΄μ΄λ λ¦¬μ€νΈ λ±μ λ°μ΄ν° νμμ μν΄ μ κ³΅λλ λ©μλ
  - equals: λ΄μ©μ λμΌμ±μ νλ¨
  - hashcode(): κ°μ²΄μ λ΄μ©μμ κ³ μ ν μ½λλ₯Ό μμ±
  - toString(): ν¬ν¨λ μμ±μ λ³΄κΈ°μ½κ² λνλ
  - copy(): κ°μ²΄λ₯Ό λ³΅μ¬νμ¬ μ κ°μ²΄λ₯Ό λ§λ€ μ μλ κΈ°λ₯ -> μ λ¬μΈμλ₯Ό λ°λ‘ λ£μ΄μ μΌλΆ μμ± λ³κ²½ κ°λ₯
  - componentX(): μμ±μ μμλλ‘ λ΄μ©μ λ°ν
  
- enum(erated) class: μ΄κ±°ν μλ£μ μνλ₯Ό κ°κ° λνλ΄κΈ° μν λ°©λ², enum class ν΄λμ€ μμ κ°μ²΄λ€μ κ΄νμ μΌλ‘ λλ¬Έμλ‘ κΈ°μ 


```kotlin
fun main() {
   	val list = listOf(Data("Sasha", 88),
                     Data("Lisa", 91),
                     Data("Coco", 18))

    for((a, b) in list) { //component1, component2
        println("${a}, ${b}")
    }
    
    var state = State.SING
    println(state)// SING
    
    state = State.SLEEP
    println(state.isSleeping())// true 
    
    state = State.EAT
    println(state.message)// λ°₯μ λ¨Ήλλ€
}

data class Data(val name: String, val id: Int)

enum class State(val message: String) {
    SING("λΈλλ₯Ό λΆλ₯Έλ€"),
    EAT("λ°₯μ λ¨Ήλλ€"),
    SLEEP("μ μ μ‘λλ€"); // λ§μ§λ§ κ°μ²΄μ μΈλ―Έμ½λ‘ μ λ£μ΄μ£Όμ
    
    fun isSleeping() = this == State.SLEEP
}
```

#### μ»¬λ μ ν΄λμ€: Set & Map

- Set: μμκ° μ μ΄λμ΄ μμ§ μκ³ , μ€λ³΅μ΄ νμ©λμ§ μλ μ»¬λ μ. μ»¨νμΈ κ° set μμ μλμ§ νμΈ
- Map: κ°μ²΄λ₯Ό λ£μ λ μ°Ύμ μ μκ² keyλ₯Ό μμΌλ‘ λ£μ΄μ£Όλ μ»¬λ μ

```kotlin
fun main() {
	val a = mutableSetOf("μ¬μ€", "λ¦¬μ¬", "μ½μ½")
    
    for(ele in a) {
        println(a)
    }
    
    a.add("λ°λ‘μ")
    a.remove("μ½μ½")
    a.contains("λ λΌ")
	
    val b = mutableMapOf(
    	"μ¬μ€" to "νλ‘κ·Έλλ¨Έ",
        "λ¦¬μ¬" to "μμ§λμ΄",
        "μ½μ½" to "λμΉμ΄") 
    
    for(ele in b) {
        println("${ele.key}:${ele.value}")
    }
    
    b.put("λ°λ‘μ", "νμΌλΏ")
    println(b) // [(μ¬μ€, νλ‘κ·Έλλ¨Έ), (λ¦¬μ¬, μμ§λμ΄), (μ½μ½, λμΉμ΄), (λ°λ‘μ, νμΌλΏ)]
    
    b.remove("νλ‘κ·Έλλ¨Έ")
    println(b)
    
    println(b["λ¦¬μ¬"])
    
}
```

#### μ»¬λ μ ν¨μ μ’λ₯

- μ»¬λ μ ν¨μ: λλ€ν¨μλ₯Ό μ¬μ©νμ¬ μ»¬λ μμ μ’ λ νΈλ¦¬νκ² μ‘°μν  μ μλ ν¨μ. JSμ κ³ μ°¨ ν¨μλ₯Ό μκ°νμ

```kotlin
fun main() {

  data class Person(val name: String, val birthYear: Int)
  val personList = listOf(Person("μ¬μ€", 1988),
    Person("λ¦¬μ¬", 1991),
    Person("μ½μ½", 2018))

  // associateBy: μμ΄νμμ keyλ₯Ό μΆμΆνμ¬ mapμΌλ‘ λ³ννλ ν¨μ 
  println(personList.associateBy{ it.birthYear }) // {1988=Person(name=μ¬μ€, birthYear=1988), 1991=Person(name=λ¦¬μ¬, birthYear=1991), 2018=Person(name=μ½μ½, birthYear=2018)}

  // groupBy: keyκ° κ°μ μμ΄νλΌλ¦¬ λ°°μ΄λ‘ λ¬Άμ΄ mapμΌλ‘ λ§λλ ν¨μ 
  println(personList.groupBy{ it.name }) // {μ¬μ€=[Person(name=μ¬μ€, birthYear=1988)], λ¦¬μ¬=[Person(name=λ¦¬μ¬, birthYear=1991)], μ½μ½=[Person(name=μ½μ½, birthYear=2018)]}

  // partition: μ‘°κ±΄μ κ±Έμ΄ boolean κ°μ λ°λΌ λ μ»¬λ μμΌλ‘ λλμ΄μ£Όλ ν¨μ 
  val (over00, under00) = personList.partition { it.birthYear > 2000}
  println(over00) // [Person(name=μ½μ½, birthYear=2018)]
  println(under00) // [Person(name=μ¬μ€, birthYear=1988), Person(name=λ¦¬μ¬, birthYear=1991)]

  val numbers = listOf(1, 0 , -3, 14, 100)

  // flatMap: μμ΄νλ§λ€ λ§λ€μ΄μ§ μ»¬λ μμ ν©μ³μ λ°ννλ ν¨μ 
  println(numbers.flatMap{listOf(it*10, it+10, it/3)}) // [10, 11, 0, 0, 10, 0, -30, 7, -1, 140, 24, 4, 1000, 110, 33]

  // getOrElse: idx μμΉμ μμ΄νμ΄ μμΌλ©΄ μμ΄νμ λ°ννκ³  μλ κ²½μ° μ§μ ν κΈ°λ³Έκ°μ λ°ννλ ν¨μ
  println(numbers.getOrElse(1){ 50 }) // 0
  println(numbers.getOrElse(100) { 50 }) // 50

  // zip: μ»¬λ μ λ κ°μ μμ΄νμ 1:1λ‘ λ§€μΉ­νμ¬ μ μ»¬λ μμ λ§λ€μ΄ μ€. μμ΄νμ κ°μκ° μ μ μ»¬λ μμ΄ μ°μ λ¨  
  println(personList zip numbers) // [(Person(name=μ¬μ€, birthYear=1988), 1), (Person(name=λ¦¬μ¬, birthYear=1991), 0), (Person(name=μ½μ½, birthYear=2018), -3)]
}
```

#### λ³μμ κ³ κΈ κΈ°μ , μμ, lateinit, lazy

- valμ ν λΉλ κ°μ²΄λ₯Ό λ°κΏ μ μμ λΏμ΄μ§ κ°μ²΄ λ΄λΆμ μμ±μ λ³κ²½ κ°λ₯
- μμ: μ»΄νμΌ μμ μ κ²°μ λμ΄ μ λλ‘ λ°κΏ μ μλ κ°μ΄λ©°, κΈ°λ³Έ μλ£νλ§ μ μΈ κ°λ₯νλ©° λ°νμμ μμ±λ  μ μλ μΌλ°μ μΈ ν΄λμ€ κ°μ²΄λ€μ λ΄μ μ μμ. 
λλ¬Έμμ μΈλλ°λ§ μ¬μ©
- μμλ₯Ό μ°λ μ΄μ : λ³μμ κ²½μ° λ°νμ μ κ°μ²΄λ₯Ό μμ±νκΈ° λλ¬Έμ μ±λ₯ νλ½ μ΄μ 

```kotlin
fun main() {
    val foodCourt = FoodCourt()
    
    foodCourt.searchPrice(FoodCourt.FOOD_CREAM_PASTA) // ν¬λ¦Όνμ€νμ κ°κ²©μ 13000μ μλλ€!
    foodCourt.searchPrice(FoodCourt.FOOD_STEAK) // μ€νμ΄ν¬μ κ°κ²©μ 30000μ μλλ€!
    foodCourt.searchPrice(FoodCourt.FOOD_PIZZA)	// νΌμμ κ°κ²©μ 15000μ μλλ€!
}

class FoodCourt {
  fun searchPrice(foodName: String) {
    val price = when (foodName) {

      FOOD_CREAM_PASTA -> 13000
      FOOD_STEAK -> 30000
      FOOD_PIZZA -> 15000
      else -> 0
    }
    println("${foodName}μ κ°κ²©μ ${price}μ μλλ€!")
  }

  companion object {
    const val FOOD_CREAM_PASTA = "ν¬λ¦Όνμ€ν"
    const val FOOD_STEAK = "μ€νμ΄ν¬"
    const val FOOD_PIZZA = "νΌμ"
  }
}
```

- lateinit: λ³μμ κ°μ²΄λ₯Ό ν λΉνλ κ²μ μ μΈκ³Ό λμμ ν  μ μμ λ μ¬μ©, String ν΄λμ€μλ μ¬μ© κ°λ₯νλ κΈ°λ³Έ μλ£νμλ μ¬μ© λΆκ°
- lateinit var λ³μμ μ νμ¬ν­: μ΄κΈ°κ° ν λΉ μ κΉμ§ λ³μλ₯Ό μ¬μ©ν  μ μμ -> μλ¬ λ°μ
- ::a.isInitialized: lateinit λ³μ μ΄κΈ°ν μ¬μ©μ¬λΆ νμΈνλ μ»¬λ μ 

```kotlin
fun main() {
	val a = LateInitSample()
    println(a.getLateInitText()) // κΈ°λ³Έκ°
    
    a.text = "new assigned"
    println(a.getLateInitText()) // new assigned   
}

class LateInitSample {
    lateinit var text: String
    
    fun getLateInitText(): String {
        if(::text.isInitialized) {
            return text
        } else {
            return "κΈ°λ³Έκ°"
        }
    }
}
```

- μ§μ° λλ¦¬μ μμ±(lazy delegate properties): λ³μλ₯Ό μ¬μ©νλ μμ κΉμ§ μ΄κΈ°νλ₯Ό μλμΌλ‘ λ¦μΆ°μ£Όλ κΈ°λ₯, μ μΈ μ μ¦μ κ°μ²΄λ₯Ό μμ± λ° ν λΉνμ¬ λ³μλ₯Ό 
μ΄κΈ°ννλ ννλ₯Ό κ°κ³  μμ§λ§ μ€μ  μ€ν μμλ λ³μ μ¬μ© μμ μ΄κΈ°νκ° μ§νλ¨. 

```kotlin
fun main() {
	val number: Int by lazy {
        println("μ΄κΈ°νλ₯Ό ν©λλ€")
        7
    }
    
    println("start the code") 
    println(number) // μ΄κΈ°νλ₯Ό ν©λλ€, 7 -> μ΄κΈ°ν μ§ν
    println(number) // 7 -> μ΄λ―Έ μ΄κΈ°νκ° μ§νλμμΌλ―λ‘ λλ€ ν¨μ lazy μλx
	    
}
```

#### λΉνΈμ°μ°

- λΉνΈμ°μ°: μ μλ³μλ₯Ό 2μ§λ²μΌλ‘ μ°μ°ν  μ μλ κΈ°λ₯. μ μνμ κ°μ λΉνΈλ¨μλ‘ λλμ΄ λ°μ΄ν°λ₯Ό μ’ λ μμ λ¨μλ‘ λ΄μ κ²½μ μ±μ νλ³΄νλλ° κ·Έ λͺ©μ μ΄ μμ.
μ£Όλ‘ νλκ·Έκ°(μ¬λ¬κ°μ μνκ°μ 01κ³Ό 1λ‘ λ΄λ λ°©λ²)μ μ²λ¦¬νκ±°λ λ€νΈμν¬ νν λ‘μ½μ λ°μ΄ν° μμ μ€μ΄λλ° μ΄μ©λ¨
- λΆνΈλΉνΈ: 2μ§μλ‘ μ νλ κ°μ κ°μ₯ μλΆλΆ λ°μ΄ν°μ΄λ©° λ³΄ν΅ λΆνΈλ₯Ό λνλ

```kotlin
fun main() {
    
    var bitData: Int = 0b1000
    bitData = bitData or(1 shl 2)
    println(bitData.toString(2))
   
    var result = bitData and(1 shl 4) // shift left λΆνΈλΉνΈλ₯Ό μ μΈν λλ¨Έμ§ λΉνΈλ€μ 4μΉΈ λ°μ΄μ£Όμ
    println(result.toString(2)) // 2μ§μ ννλ‘ μ ννμ¬ μΆλ ₯
    
    println(result shr 4) // shift right 4μΉΈ λ°μ΄μ£Όμ 
    
    bitData = bitData and((1 shl 4).inv()) // shlμ μ¬μ©νμ¬ 1μ μ’μΈ‘μΌλ‘ 4λ² λ°μ΄μ£Όμ
    println(bitData.toString(2))
    
    println((bitData xor(0b10100)).toString(2))
}
```

#### μ½λ£¨ν΄μ ν΅ν λΉλκΈ° μ²λ¦¬

- μ½λ£¨ν΄: λΉλκΈ°μ²λ¦¬, λ©μΈ λ£¨ν΄κ³Ό λ³λλ‘ μ§νμ΄ κ°λ₯ν λ£¨ν΄μΌλ‘ κ°λ°μκ° μ€ν, μ’λ£λ₯Ό λ§μλλ‘ μ‘°μ 
- μ½λ£¨ν΄ scope
  - GlobalScope: νλ‘κ·Έλ¨ μ΄λμλ μ μ΄, λμμ΄ κ°λ₯ν κΈ°λ³Έ λ²μ
  - CoroutineScope: νΉμ ν λͺ©μ μ λμ€ν¨μ²λ₯Ό μ§μ νμ¬ μ§μ , λμμ΄ κ°λ₯

- λ£¨ν΄μ λκΈ°λ₯Ό μν μΆκ°μ μΈ ν¨μ. μ½λ£¨ν΄μ΄λ runBlockingμ²λΌ λ£¨ν΄ λκΈ°κ° κ°λ₯ν κ΅¬λ¬Έμμλ§ μλ
  - delay(miliseconde: Long): ms λ¨μλ‘ λ£¨ν΄ λκΈ°
  - Job.join(): Jobμ μ€νμ΄ λλ λκΉμ§ λκΈ°νλ ν¨μ
  - Deferred.await(): JSμ Promise κ°μ²΄μ λΉμ·νλ©° κ²°κ³Όκ°λ λ°ν

- cancel(): μ½λ£¨ν΄ λ΄λΆμ delay() or yield() ν¨μκ° μ¬μ©λ μμΉκΉμ§ μνλ λ€ μ’λ£λκ±°λ isActive μμ±μ΄ falseκ° λλ κ²μ μλμΌλ‘ νμΈ ν μ’λ£

```kotlin
import kotlinx.coroutines.*

fun main() {
	runBlocking { // μ½λ£¨ν΄μ΄ μ’λ£λ λκΉμ§ λ©μΈ λ£¨ν΄μ μ μ λκΈ°. μλλ‘μ΄λμμλ λ°μμ΄ μμ κ²½μ° μ±μ΄ κ°μ  μ’λ£ 
    	val a = launch {
            for(ele in 1..5) {
                println(ele)
                delay(100)
            }
        }
         val b = async {
            "async μ’λ£"
        }
         
        println("Hold async")
        println(b.await())
        
        println("launch μ·¨μ")
        a.cancel()
        println("Quit launch")
        
    }
}
```

- withTimeOutOrNull: μ ν μκ° λ΄μ μνλλ©΄ κ²°κ³Όκ°μ λ°ννκ³  μλλ©΄ nullκ°μ λ°ν
```kotlin
import kotlinx.coroutines.*

fun main() {
	runBlocking { 
    	var result = withTimeoutOrNull(50) {
            for(ele in 0..10) {
                println(ele)
                delay(10)
            }
            "Finish"
        }
        println(result)
    }
}
```