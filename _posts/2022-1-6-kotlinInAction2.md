---
layout: post
title: "π Kotlin in Action - 2μ₯"
excerpt: "Kotlin in Action 2μ₯ μμ½ λΈνΈμλλ€."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "νμ΄μ§ μ£Όμ λͺ©μ°¨"
date: 2022-1-6
tags: [Kotlin]
---

## 2.1 κΈ°λ³Έ μμ: ν¨μμ λ³μ

#### 2.1.1 Hello, World!

  ```kotlin
  fun main(args: Array<string>) {
      println("Hello, world!")
  }
  ```

  - ν¨μλ₯Ό μ μΈν  λμ fun ν€μλλ₯Ό μ¬μ©
  - μΈμ λ€μ νμμ μ¬μ©
  - ν¨μλ₯Ό μ΅μμ μμ€μ μ μν  μ μμΌλ©°, μλ°μ λ¬λ¦¬ κΌ­ ν΄λμ€ μμ ν¨μλ₯Ό λ£μ΄μΌ ν  νμκ° μμ
  - λ°°μ΄ μ²λ¦¬λ₯Ό μν λ¬Έλ²μ΄ λ°λ‘ μ‘΄μ¬νμ§ μμ
  - νμ€ μλ° λΌμ΄λΈλ¬λ¦¬ ν¨μλ₯Ό κ°κ²°νκ² μ¬μ©ν  μ μκ² κ°μΌ λνΌλ₯Ό μ κ³΅. λλΆμ System.out.println λμ μ printlnλΌκ³  κ°κ²°νκ² μ¬μ© κ°λ₯ 
  - μΈλ―Έμ½λ‘  μλ΅κ°λ₯

#### 2.1.2 ν¨μ

  ```kotlin
  fun max(a: Int, b: Int): Int {
      return if (a > b) a else b
  } // expression body: μλ³Έλ¬Έ
  println(max(1,2)) // 2
  
  fun max(a: Int, b: Int): Int = if(a > b) a else b // block body: λΈλ‘λ³Έλ¬Έ
  ```

  - μ½νλ¦°μμ ifλ μλ°μ λ€λ₯΄κ² κ°μ λ§λ€μ΄ λ΄λ©° λ€λ₯Έ μμ νμ μμλ‘ κ³μ°μ μ°Έμ¬ν  μ μλ expressionμ
  μ°Έκ³ λ‘ statementλ μμ μ λλ¬μΈκ³  μλ κ°μ₯ μμͺ½ λΈλ‘μ μ΅μμ μμμ΄λ©°, μ΄λ€ κ°λ λ§λ€μ΄λ΄μ§ μμ
  
  - type inference(νμμΆλ‘ ): μμ΄ λ³Έλ¬ΈμΈ ν¨μμ κ²½μ° λ°ν νμμ μ μ§ μμλ μ»΄νμΌλ¬κ° ν¨μ λ³Έλ¬Έ μμ λΆμν΄ κ²°κ³Ό νμμ 
  ν¨μ λ°ν νμμΌλ‘ μ ν΄μ£Όλ κ²μ λ»ν¨. μλ³Έλ¬Έ ν¨μμμλ§ νμ μλ΅ κ°λ₯

#### 2.1.3 λ³μ

  - var: λ³κ²½ κ°λ₯ν μ°Έμ‘°λ₯Ό μ μ₯νλ λ³μ. μλ°μ μΌλ° λ³μμ κ°λ€. λ³μμ κ°μ λ³κ²½ν  μ μμ§λ§ λ³μμ 
  νμμ κ³ μ λΌ λ°λμ§ μμ
  - val: λ³κ²½ λΆκ°λ₯ν μ°Έμ‘°λ₯Ό μ μ₯νλ λ³μ. μ΄κΈ°ν ν μ¬ν λΉμ λΆκ°νμ§λ§ κ°μ²΄μ λ΄λΆ κ°μ λ³κ²½ κ°λ₯
  μλ°μ final λ³μμ κ°μ
 
  ```kotlin
  val languages = arraylistOf("Java") 
  languages.add("Kotlin") // true
  
  var anwer = 42
  answer = "no answer" // Error: type mismatch
  ```

#### 2.1.4 λ μ½κ² λ¬Έμμ΄ νμ μ§μ : λ¬Έμμ΄ ννλ¦Ώ

  - λ¬Έμμ΄ λ¦¬ν°λ΄ μμμ λ³μλ₯Ό μ¬μ©νκΈ° μν΄μλ '$'λ₯Ό μμ λΆμ¬μ£Όμ
  - λ¬Έμμ΄ ννλ¦Ώ μμλ κ°λ¨ν λ³μλΏλ§μ΄ μλλΌ μλ λ€μ΄κ° μ μμΌλ―λ‘ κ°λ₯νλ©΄ '${λ³μ or μ}' ννλ‘ μ΄μ©  
  - λν '$'λ₯Ό νΉμλ¬Έμλ‘ μ°κ³  μΆλ€λ©΄ '\'λ₯Ό μ΄μ©νμ¬ escape μν€λ©΄ κ°λ₯

  ```kotlin
  fun main(args: Array<String>) {
      if (args.size > 0) {
          println("Hello, ${args[0]}")
      }
  }
  
  fun main(args: Array<String>) {
      println("Hello, ${if (args.size > 0) args[0] else "someone"}!")
  } //ννλ¦Ώ λ¦¬ν°λ΄ μμμ μλ°μ΄νλ μ¬μ© κ°λ₯
  ```

### 2.2 ν΄λμ€μ νλ‘νΌν°

  - κ°λ¨ν μλ°λΉ ν΄λμ€μΈ Personμ μ μνμΌλ©°, name μ΄λΌλ νλ‘νΌν°λ§ λ€μ΄μμ

    ```java
    public class Person {
        private final String name;
        public class Person(String name) {
            this.name = name;
        }
        public String getName() {
            return name;
        }
    }
    ```

  - μ½νλ¦°μΌλ‘ μΉνν μ½λμ΄λ©° μ½λλμ΄ **νμ°ν** μ μ΄μ§ κ²μ νμΈν  μ μμ. μ΄λ κ² μ½λμμ΄ λ°μ΄ν°λ§ μ μ₯νλ ν΄λμ€λ₯Ό value object(κ° κ°μ²΄)λΌ λΆλ¦

    ```kotlin
    class Person(val name: String)
    ```

#### 2.2.1 νλ‘νΌν°

  - μλ°μμλ νλμ μ κ·Όμλ₯Ό λ¬Άμ΄ **νλ‘νΌν°**λΌκ³  λΆλ₯΄λ©°, μ½νλ¦°μ κΈ°λ³Έ κΈ°λ₯μΌλ‘ μ κ³΅νλ©° νλμ μ κ·Όμλ₯Ό μμ ν λμ ν¨

    ```kotlin
    class Person(
        val name: String, // μ½κΈ° μ μ© νλ‘νΌν°, μ½νλ¦°μ νλμ κ²ν° μμ±
        val isMarried: Boolean // μΈ μ μλ νλ‘νΌν°, νλμ μΈν° κ·Έλ¦¬κ³  κ²ν° μμ± 
    )
  
    val person = Person("Bob", true)
    println(person.name) // Bob
    println(person.isMarried) // true
    ```

    > νλ: λ°μ΄ν°λ₯Ό μ μ₯νλ κ³³  
    > κ²ν°: νλλ₯Ό μ½λ κ²   
    > μΈν°: νλλ₯Ό λ³κ²½νλ κ² 
    > accessor method (μ κ·Όμ λ©μλ): ν΄λΌμ΄μΈνΈκ° ν΄λμ€λ₯Ό ν΅ν΄μ λ°μ΄ν°μ μ κ·Όν  μ μκ² μ κ³΅νλ ν΅λ‘

#### 2.2.2 μ»€μ€ν μ κ·Όμ

  - get(): μ»€μ€ν νλ‘νΌν° μ κ·Όμμ΄λ©°, ν΄λΌμ΄μΈνΈκ° ν΄λΉ μ κ·Όμλ₯Ό μ΄μ©νμ¬ νλ‘νΌν° κ°μ κ³μ°
    
    ```kotlin
    class Rectangle(val height: Int, val width: Int) {
        val isSquare: Boolean
        get() { //νλ‘νΌν° κ²ν° μ μΈ
            return height == width
        }
    }
  
    val rectangle = Rectangle(41, 43)
    println(rectangle.isSquare) // false
    ```

#### 2.2.3 μ½νλ¦° μμ€μ½λ κ΅¬μ‘°: λλ ν λ¦¬μ ν¨ν€μ§

  - μ½νλ¦°μ node.js μ²λΌ λͺ¨λνλ‘ κ΄λ¦¬ν  μ μκ³  μ΄λ₯Ό **ν¨ν€μ§**λΌκ³  ν¨. κ·Έλ¦¬κ³  μ΄ ν¨ν€μ§ μμλ ν΄λμ€, ν¨μ, νλ‘νΌν°
    λ±μ΄ μμΌλ©°, μμ λ‘­κ² κΊΌλ΄ μΈ μ μμ

  - νλ‘μ νΈμμ μλ°μ νΌμ©ν  κ²½μ°, μλ°μ κ°μ΄ ν¨ν€μ§ λ³λ‘ λλ ν°λ¦¬λ₯Ό κ΅¬μ±

    ```kotlin
    package geometry.shapes // ν¨ν€μ§ μ μΈ
    import java.util.Random // νμ€ μλ° λΌμ΄λΈλ¬λ¦¬ ν΄λμ€λ₯Ό import
    class Rectangle(val height: Int, val width: Int) {
        val isSquare: Boolean
            get() = height = width
    }
  
    fun createRandomRectangle(): Rectangle {
        val random = Random()
        return Retangle(random.nextInt(), random.nextInt())
    }
    ```

    ```kotlin
    pakage.* // ν¨ν€μ§ μμ λͺ¨λ  ν΄λμ€, ν¨μ, νλ‘νΌν°κΉμ§ λ€ λΆλ¬μ΄
    package geometry.example
    import geometry.shapes.createRandomRectangle // μ΄λ¦μΌλ‘ ν¨μ import
    fun main(args: Array<String>) {
        println(createRandomRectangle().isSquare)
    }
    ```
  
### 2.3 μ ν ννκ³Ό μ²λ¦¬: enumκ³Ό when

#### 2.3.1 μ ν ννκ³Ό μ²λ¦¬ - enum ν΄λμ€ μ μ

  - enumμ μμ±μμ νλ‘νΌν°λ₯Ό μ μΈνκ³  ν΄λμ€ μμ λ©μλλ₯Ό μ μνλ κ²½μ° λ°λμ μμ λͺ©λ‘κ³Ό λ©μλ μ μ μ¬μ΄μ μΈλ―Έμ½λ‘ 
  > enum - λ³΅μμ μμλ₯Ό λμ΄νλ€λ μ μμ JSμ λ°°μ΄κ³Ό μ μ¬νμ§λ§ νλ‘νΌν°λ λ©μλκΉμ§ μ μ κ°λ₯

    ```kotlin
    enum class Color (
        val r: Int, val g: Int, val b: Int // μμ νλ‘νΌν° μ μ
    ) {
        RED(255,0,0), ORANGE(255, 165, 0), // μμ μμ± μ μ΄μ λν νλ‘νΌν° κ° μ§μ 
        YELLOW(255, 255, 0), GREEN(0, 255, 0), BLUE(0, 255, 255); // λ°λμ !μΈλ―Έμ½λ‘ μΌλ‘ λ§λ¬Ό
        
        fun rgb() = (r * 256 + g) * 256 + b // enum ν΄λμ€ μμμ λ©μλλ₯Ό μ μ
    }
    ```

#### 2.3.2 / 2.3.3 whenμΌλ‘ enum ν΄λμ€ λ€λ£¨κΈ°

  - λΆκΈ°λ₯Ό μμ±νμ¬ ν΄λΉ μ‘°κ±΄μ λ§λ κ°μ λ°νν΄μ£Όλ κ°λ ₯ν κΈ°λ₯μ λ³΄μ . μλ°μ switchμ λμΌνλ, λΆκΈ° μ‘°κ±΄μ μμλ§
    μ¬μ©ν  μ μλ swithμ λ¬λ¦¬ whenμ λΆκΈ° μ‘°κ±΄μ μμμ κ°μ²΄λ₯Ό νμ©

    ```kotlin
    // when λΆκΈ° μ‘°κ±΄μ μ¬λ¬ κ° μ¬μ©νκΈ°
    fun getWarmth (color: Color) = when (color) {
        Color.RED, Color.ORANGE, Color.YELLOW -> "warm"
        Color.GREEN -> "neutral"
        Color.BLUE, Color.INDIGO, Color.VIOLET -> "cold"
    }
    println(getWarmth(Color.ORANGE)) // warm
  
    // when λΆκΈ° μ‘°κ±΄μ μ¬λ¬ λ€λ₯Έ κ°μ²΄ μ¬μ©νκΈ°
    fun mix(c1: Color, c2: Color) = 
        when (setof(c1,c2)) {
            setOf(RED, YELLOW) -> ORANGE γ
            setOf(YELLOW, BLUE) -> GREEN
            setOf(BLUE, VOILET) -> INDIGO
            else -> throw Exception("FUCKED")
        }
    println(mix(BLUE, YELLOW)) // GREEN
    ```

  - setOf ν¨μλ μΈμλ‘ μ λ¬λ°μ μ¬λ¬ κ°μ²΄λ₯Ό ν¬ν¨νλ μ§ν©μΈ set κ°μ²΄λ‘ λ§λ€μ΄ μ€. μ§ν©(set)μ μμκ° λͺ¨μ¬μλ μ»¬λ μμΌλ‘ μμλ μκ΄μμ

#### 2.3.4 μΈμμλ when μ¬μ©

  - μ μ μ ν¨μλ νΈμΆλ  λλ§λ€ μ¬λ¬ Set μΈμ€ν΄μ€λ₯Ό μμ±νκΈ° λλ¬Έμ λΉν¨μ¨μ±μ΄ λ°μ. μ΄μ λ€μκ³Ό κ°μ΄ μΈμκ° μλ when μμ
    μ¬μ©νλ©΄ λΆνμν κ°μ²΄(=κ°λΉμ§ κ°μ²΄) μμ±μ λ§μ μ μμ

    ```kotlin
    fun mixOptimized(c1: Color, c2: Color) = 
        when {
            (c1 == RED && c2 == YELLOW) || (c1 == YELLOW && c2 == RED) -> ORANGE
            (c1 == YELLOW && c2 == BLUE) || (c1 == BLUE && c2 == YELLOW) -> GREEN
            (c1 == BLUE && c2 == VIOLET) || (c1 == VIOLET && c2 == BLUE) -> INDIGO
          
            else -> throw Exception("FUCKED")
        }
    println(mixOptimized()(BLUE, YELLOW)) // GREEN
  
    fun main() {
        println(doWhen(1))
    }
  
    fun doWhen (a: Any): String { // μΆλ ₯κ° νμμ μ§μ νμ§ μμ κ²½μ° Type mismatch: inferred type is String but Unit was expected
        var result = when(a) {
            1 -> "1"
            "Sasha" -> "μ¬μ€"
            else -> "μ ν¨ν κ°μ μλ ₯νμ­μμ€"
        }
        return result
    }
    ```

#### 2.3.5 μ€λ§νΈ μΊμ€νΈ: νμ κ²μ¬μ νμ μΊμ€λ₯Ό μ‘°ν©

  - μ€λ§νΈμΊμ€νΈ: κ΅³μ΄ μνλ νμμΌλ‘ μΊμ€ν(νλ³ν) νμ§ μλλΌλ, μ»΄νμΌλ¬κ° μμμ μΊμ€ν ν΄μ£Όλ κ²

    ```kotlin
    fun eval(e: Expr): Int {
        if (e is Num) {
        val n = e as Num // λΆνμν νμ λ³ν
        return n.value
        }
        if(e is Sum) { // λ³μ eμ λν΄ νμ κ²μ¬ λ° μλμΌλ‘ μΊμ€ν μ€ν
            return eval(e.right) + eval(e.left)
        }
        throw IllegalArgumentException("λ³Έμ μλ μμΈλ°?")
    }
    
    println(eval(Sum(Sum(Num(1), Num(2)), Num(4)))) // 7
    ```

#### 2.3.6 λ¦¬ν©ν λ§: ifλ₯Ό whenμΌλ‘ λ³κ²½

  - if μμ μ΄μ©ν κ° μμ±
  - ifλ whenμ κ° λΆκΈ°μμ μνν΄μΌ νλ λ‘μ§μ΄ λ³΅μ‘ν΄μ§λ©΄ λΆκΈ° λ³Έλ¬Έμ λΈλ‘ μ¬μ© κ°λ₯

    ```kotlin
    fun eval(e: Expr): Int = 
        if (e is Num) {
            e.value
        } else if (e is Sum) {
            eval(e.right) + eval(e.left)
        } else {
            throw IllegalArgumentException("Unknown expression")
        }
    println(eval(Sum(Num(1), Num(2)))) // 3
    ```
    
  - if λμ μ whenμ μ¬μ©ν΄μ μ’ λ λ€λ¬μ΄λ³΄μ
    
    ```kotlin
    fun eval(e: Expr) : Int = 
        when (e) {
            is Num -> // μΈμ νμμ κ²μ¬νλ€ 
                e.value
            is Sum -> 
                eval(e.right) + eval(e.left)
        else ->         
            throw IllegalArgumentException("Unknown expression")
        }
    ```
  
#### 2.3.7 ifμ whenμ λΆκΈ°μμ λΈλ‘ μ¬μ©

  - ifλ when λͺ¨λ λΆκΈ°μ λΈλ‘ μ¬μ©μ΄ κ°λ₯νλ©°, κ·Έλ° κ²½μ° **λΈλ‘μ κ°μ₯ λ§μ§λ§ λ¬Έμ₯μ΄ λΈλ‘μ μ μ²΄ κ²°κ³Ό**κ° λ¨. returnμ
  λ°λ‘ μ¨μ€ νμκ° μμ.

    ```kotlin
    fun evalWithLogging(e: Expr) : Int = 
        when (e) {
            is Num -> {
                println("num: ${e.value}")
                e.value
            }
            is Sum -> {
                val left = evalWithLogging(e.left)
                val right = evalWithLogging(e.right)
                println("sum: ${left} + ${right}")
                left + right
            }
            else -> throw IllegalArgumentException("Unknown expression")
        }
    ```


### 2.4 λμμ iteration: whileκ³Ό for loop

  - forλ μλ°μ for-each λ£¨νμ ν΄λΉνλ ννλ§ μ‘΄μ¬νλ©°, ννλ for <μμ΄ν> in <μμλ€>

#### 2.4.1 while λ£¨ν

  ```kotlin
  // μ‘°κ±΄μ΄ μ°ΈμΈ λμ λ³Έλ¬Έμ λ°λ³΅ μ€ν
  while (μ‘°κ±΄) {
      /* μ€νλ¬Έ*/
  }
  
  // λ§¨ μ²μμ λ¬΄μ‘°κ±΄ λ³Έλ¬Έμ νλ² μ€νν λ€μ, μ‘°κ±΄μ΄ μ°ΈμΈ λμ λ³Έλ¬Έμ λ°λ³΅ μ€ν
  do {
      /* μ€νλ¬Έ*/    
  } while (μ‘°κ±΄)
  ```

#### 2.4.2 μμ λν μ΄ν°λ μ΄μ: λ²μμ μμ΄

  - μ½νλ¦°μλ μλ°μ for loopμ ν΄λΉνλ μμκ° μμΌλ©°, μ΄μ λ²μ(range)λ₯Ό λ°λ‘ μ§μ 
  - λ²μλ μ μ λ±μ μ«μ νμμ κ°μ΄λ©° μλμ ν¬ν¨

  ```kotlin
  val oneToTwenty = 1..20
  ```
  
  ```kotlin
  // whenμ μ¬μ©ν΄ fizzBuzz κ²μ κ΅¬ννκΈ°
  fun fizzBuzz(i: Int) = when {
      i % 15 == 0 -> "FizzBuzz"
      i % 3 == 0 -> "Fizz"
      i % 5 == 0 -> "Buzz"
      else -> "$i"
  }
  // μ¦κ° κ°μ κ°κ³  λ²μ μ΄ν°λ μ΄μ
  for (i in 1..100) {
      print(fizzBuzz(i))
  }
  // downTo 1μ μ­λ°©ν₯ μμ΄μ μ§μ νλ©°, step 2λ μ¦κ°κ°(κ°μκ°)μ΄ 2(-2)λ₯Ό λ»ν¨ 
  for (i in 200 downTo 1 step 2) {
      print(fizzBuzz(i))
  }
  // untilμ λ κ°μ ν¬ν¨νμ§ μλλ€
  for (i in 0 until size) {
      print(fizzBuzz(i))
  }
  ```

#### 2.4.3 λ§΅μ λν μ΄ν°λ μ΄μ

  - for loopλ₯Ό μ¬μ©ν΄ μ΄ν°λ μ΄μνλ €λ μ»¬λ μμ μμλ₯Ό ν μ μμ

  ```kotlin
  val binaryReps = TreeMap<Char, String>() 
  for (c in 'A'..'F') { // AλΆν° FκΉμ§ λ¬Έμλ²μ μ¬μ©
      val binary = Integer.toBinaryString(c.toInt()) // μμ€ν€ μ½λλ₯Ό 2μ§ ννμΌλ‘ λ³κ²½
      binaryReps[c] = binary
  }
  for ((letter, binary) in binaryReps) {
      println("$letter = $binary")
      
  }
  
  // κ°μ²΄λ₯Ό νννλ λ°©λ² 2κ°μ§
  binaryReps [c] = binary
  binaryReps.put (c, binary)
  ```

#### 2.4.4 inμΌλ‘ μ»¬λ μμ΄λ λ²μμ μμ κ²μ¬

  - in μ°μ°μλ₯Ό μ¬μ©ν΄ μ΄λ€ κ°μ΄ λ²μμ μνλμ§ μ μ μμ. !in μ°μ°μλ₯Ό μ¬μ©ν΄ λ°λμ κ²½μ°λ νμΈ κ°λ₯

  ```kotlin
  fun isLetter(c: Char) = c in 'a'..'z' || c in 'A'..'Z'
  fun isNotDigit(c: Char) = c !in '0'..'9'
  ```

  ```kotlin
  // whenμμ in μ¬μ©νκΈ°
  fun recognize(c: Char) = when (c) {
      in '0'..'9' -> "It's a digit"
      in 'a'..'z', in 'A'..'Z' -> "It's a letter!"
      else -> "Fucked"
  }
  ```
  - λΉκ΅κ° κ°λ₯ν ν΄λμ€λΌλ©΄ κ·Έ ν΄λμ€μ μΈμ€ν΄μ€ κ°μ²΄λ₯Ό μ¬μ©ν΄ λ²μ μμ± κ°λ₯

### 2.5 μ½νλ¦°μ μμΈμ²λ¦¬

- λ°μν μμΈλ₯Ό ν¨μ νΈμΆλ¨μμ **catch**νμ§ μμΌλ©΄ ν¨μ νΈμΆ μ€νμ κ±°μ¬λ¬ μ¬λΌκ°λ©΄μ μμΈλ₯Ό μ²λ¦¬νλ λΆλΆμ΄ λμ¬ λκΉμ§ μμΈλ₯Ό λ€μ λμ§

  ```kotlin
  val percentage =
      if (number in 0..100)
          number
      else
          throw IllegalArgumentException (
              "A percentage value must be between 0 and 100: $number")
  ```
  
#### 2.5.1 try, catch, finally

  - μλ°μ λ§μ°¬κ°μ§λ‘ νμΌμμ κ° μ€μ μ½μ΄ μλ‘ λ³ννλ κ·Έ μ€μ΄ μ¬λ°λ₯Έ μ ννκ° μλλ©΄ null λ°ν
  - μ²΄ν¬ μμΈ μ²λ¦¬λ₯Ό κ°μ νλ μλ°μλ λ¬λ¦¬ μ½νλ¦°μ μμ λ‘μ
  
  ```kotlin
  fun readNumber (reader: BufferReader) : Int? {
      try {
          val line = reader.readLine()
          return Integer.parseInt(line)
      }
      catch (e: NumberFormatException) {
          return null
      }
      finally {
          reader.close()
      }
  }
  ```

#### 2.5.2 tryλ₯Ό μμΌλ‘ μ¬μ©

  - μ½νλ¦°μ try ν€μλλ μμ΄λ―λ‘ λ³μμ λμν  μ μκ³ , λ³Έλ¬Έμ λ°λμ μ€κ΄νΈ {}λ‘ λλ¬μΈμΌν¨
  - JSμ try catch κ΅¬λ¬Έκ³Ό κ±°μ μ μ¬

  ```kotlin
  // tryλ₯Ό μμΌλ‘ μ¬μ©νκΈ°
  fun readNumber(reader: BufferedReader) {
      val number = try {
          Integer.parseInt(reader.readLine()) // try μμ κ°
      } catch (e: NumberFormatException) {
          return 
      }
      println(number)
  }
  
  // catchμμ κ° λ°ννκΈ°
  fun readNumber(reader: BufferedReader) {
      val number = try {
          Integer.parseInt(reader.readLine())
      } catch (e: NumberFormatException) {
          null // μμΈκ° λ°μνλ©΄ nullκ°μ μ¬μ© 
      }
  }
  ```
