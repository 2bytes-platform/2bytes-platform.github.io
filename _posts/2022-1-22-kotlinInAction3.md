---
layout: post
title: "๐ Kotlin in Action - 3์ฅ ํจ์ ์ ์์ ํธ์ถ"
excerpt: "Kotlin in Action 3์ฅ ์์ฝ ๋ธํธ์๋๋ค."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "ํ์ด์ง ์ฃผ์ ๋ชฉ์ฐจ"
date: 2022-1-22
tags: [Kotlin]
---

### 3.1 ์ฝํ๋ฆฐ์์ ์ปฌ๋ ์ ๋ง๋ค๊ธฐ

  - ์ฝํ๋ฆฐ์์๋ ์์ฒด ์ปฌ๋ ์์ ์ ๊ณตํ์ง ์์. ํ์ค ์๋ฐ ์ปฌ๋ ์์ ํ์ฉํ๋ฉด ๊ธฐ์กด ์๋ฐ ์ฝ๋์ ์ํธ์์ฉํ๊ธฐ๊ฐ ์ฝ๊ธฐ ๋๋ฌธ

    ```kotlin
    // ์ฝํ๋ฆฐ์ ์๋ฐ๋ณด๋ค ๋ ๋ง์ ์ปฌ๋ ์ ๊ธฐ๋ฅ์ ์ธ ์ ์์
    val strings = listOf("first", "second", "third")
    println(strings.last()) // third
    val numbers = setOf(1, 14, 2)
    println(numbers.max()) // 14
    ```

### 3.2 ํจ์๋ฅผ ํธ์ถํ๊ธฐ ์ฝ๊ฒ ๋ง๋ค๊ธฐ

  - ์์ ์ฌ์ด๋ฅผ ์ธ๋ฏธ์ฝ๋ก ์ผ๋ก ๊ตฌ๋ถํ๊ณ  ๊ดํธ๋ก ๋ฆฌ์คํธ๋ฅผ ๋๋ฌ์ธ๋ ํจ์๋ฅผ ๋ค์๊ณผ ๊ฐ์ด ์์ฑ
  - ํจ์๋ฅผ ํธ์ถ joinToString(list, "; ", "(", ")")์ ๊ฐ๋ตํ๊ฒ ๋ํ๋ด๋ณด์

    ```kotlin
    fun main() {
        val list = listOf(1,2,3)
        println(joinToString(list, "; ", "(", ")"))
    }
    
    fun <T> joinToString(
        collection: Collection<T>,
        separator: String,
        prefix: String,
        postfix: String
    ): String {
        
        val result = StringBuilder(prefix)
        for((idx, ele) in collection.withIndex()) {
            if (idx > 0) result.append(separator)
            result.append(ele)
        }
        result.append(postfix)
        return result.toString()
    }
    ```

#### 3.2.1 ์ด๋ฆ ๋ถ์ธ ์ธ์

  - ์ฝํ๋ฆฐ์ผ๋ก ์์ฑํ ํจ์๋ฅผ ํธ์ถํ  ๋๋ ์๋ ์ค๋ํซ๊ณผ ๊ฐ์ด ์ ๋ฌ ์ธ์์ ์ด๋ฆ์ ๋ช์ ๊ฐ๋ฅ
  - ์๋ฐ๋ก ์์ฑํ ์ฝ๋๋ฅผ ํธ์ถ ์, ์ธ์ ๋ฌธ์ ๋ก ์ธํด ์ด๋ฆ ๋ถ์ธ ์ธ์๋ฅผ ์ฌ์ฉํ  ์ ์์

    ```kotlin
    joinToString(list, separator = "; ", prefix = "(", postfix = ")")
    ```

#### 3.2.2 ๋ํดํธ ํ๋ผ๋ฏธํฐ ๊ฐ

  - ์ฝํ๋ฆฐ์ ํจ์ ์ ์ธ์์ ์ธ์์ default ๊ฐ์ ์ง์ ํ์ฌ ๋๋ฌด ๋ง์ ๋ฉ์๋ ์ค๋ฒ๋ก๋ฉ์ ํผํ  ์ ์์
  - ํจ์๋ฅผ ์ ์ธํ  ๋์ ๊ฐ์ ์์๋ก ์ธ์๋ฅผ ์ง์ 

    ```kotlin
    joinToString(list, ",", "", "")
    joinToString(list) // separator, prefix, postfix ์๋ต
    joinToString(list, "; ") // separator = ": "๋ก ์ง์ , prefix & postfix ์๋ต
    ```

    > ์๋ฐ์๋ default ์ธ์๊ฐ์ด๋ผ๋ ๊ฐ๋์ด ์์ด์ ์ฝํ๋ฆฐ ํจ์๋ฅผ ์๋ฐ์์ ํธ์ถํ๋ ๊ฒฝ์ฐ์๋ ๋ชจ๋  ์ธ์ ๋ช์ ํ์!

#### 3.2.3 ์ ์ ์ธ ์ ํธ๋ฆฌํฐ ํด๋์ค ์์ ๊ธฐ: ์ต์์ ํจ์์ ํ๋กํผํฐ

  - ์๋ฐ ๋ด์์๋ ๋ค์ํ ์ ์  ๋ฉ์๋๋ฅผ ๋ชจ์๋๊ธฐ๋ง ํ๊ณ , ํน๋ณํ ์ํ๋ ์ธ์คํด์ค ๋ฉ์๋๋ ์๋ ํด๋์ค๊ฐ ์กด์ฌ ex) JDK collections ํด๋์ค
  - API ์์ฑ ์, ์ฌํ์ฉํ๊ณ  ์ถ์ ๋ก์ง๋ค์ ๋ฐ๋ก ๋ชจ์๋๋ ์์์ ์๊ฐํ์ -> Util class ์ฐธ์กฐ
  - ํ์ง๋ง ์ฝํ๋ฆฐ์์๋ ์ต์์ ์์ค์ ํจ์๋ฅผ ์ด์ฉํด์ ๊ฐ๋จํ๊ฒ ์ ์ฅ ๋ฐ ๋ถ๋ฌ์ค๊ธฐ ๊ฐ๋ฅ    
    
    ```kotlin
    // ์์ฑ๋ join.kt ํ์ผ ๋ด joinToString() ํจ์๋ฅผ ์ต์์ ํจ์๋ก ์ ์ธ
    package strings
    fun joinToString(): String {}
    ```
    ```kotlin
    // ์ฝํ๋ฆฐ ์ต์์ ํจ์๊ฐ ํฌํจ๋๋ ํด๋์ค์ ์ด๋ฆ์ ๋ฐ๊พธ๊ณ  ์ถ๋ค๋ฉด ํ์ผ์ @JvmName Annotation ์ถ๊ฐ
    @file: JvmName("StringFunctions")
    package strings
    fun joinToString():String{}
    ```

  - ํจ์์ ๋ง์ฐฌ๊ฐ์ง๋ก ํ๋กํผํฐ๋ ํ์ผ์ ์ต์์ ์์ค์ ๋์ ์ ์์ผ๋ฉฐ, ํด๋น ๊ฐ์ ์ ์  ํ๋์ ์ ์ฅ

    ```kotlin
    var opCount = 0
    fun performOperation() {
        opCount++
    }
    fun reportOperationCount() {
        println("Operation performed $opCount times")
    }
    ```

### 3.3 ๋ฉ์๋๋ฅผ ๋ค๋ฅธ ํด๋์ค์ ์ถ๊ฐ: ํ์ฅ ํจ์์ ํ์ฅ ํ๋กํผํฐ

  - ํ์ฅ ํจ์: ๊ธฐ์กด ์๋ฐ API๋ฅผ ์ฌ์์ฑํ์ง ์๊ณ , ์ฝํ๋ฆฐ์ด ์ ๊ณตํ๋ ๋งค์๋๋ฅผ ์ด์ฉํ  ์ ์๊ฒ ๋ง๋ค์ด ์ค. ์ฆ, ์ด๋ค ํด๋์ค์ ๋ฉค๋ฒ
  ๋ฉ์๋์ธ ๊ฒ์ฒ๋ผ ํธ์ถ ๊ฐ๋ฅํ์ง๋ง ๊ทธ ํด๋์ค ๋ฐ์ ์ ์ธ๋ ํจ์

      ```kotlin
      package strings
      fun String.lastChar(): Char = get(length - 1) // this ์๋ต ๊ฐ๋ฅ 
      /**
       * receiver type(์์  ๊ฐ์ฒด ํ์): ํจ์๊ฐ ํ์ฅํ  ํด๋์ค์ ์ด๋ฆ
       * receiver object(์์  ๊ฐ์ฒด): ํ์ฅ ํจ์๊ฐ ํธ์ถ๋๋ ๋์์ด ๋๋ ๊ฐ(๊ฐ์ฒด)
       */
      ```

#### 3.3.1 import์ ํ์ฅ ํจ์

```kotlin
import strings.lastChar
import strings.*
val c = "Kotlin".lastChar()
```

```kotlin
// as ํค์๋ ์ด์ฉ ์ import ํด๋์ค๋ ํจ์๋ฅผ ๋ค๋ฅธ ์ด๋ฆ์ผ๋ก ํธ์ถ ๊ฐ๋ฅ
import strings.lastChar as last
val c = "Kotlin".last()
```

#### 3.3.3 ํ์ฅ ํจ์๋ก ์ ํธ๋ฆฌํฐ ํจ์ ์ ์


```kotlin
fun main() {
    val list = listOf(1,2,3)
    println(joinToString(list, "; ", "(", ")")) // joinToString์ ํด๋์ค์ ๋ฉค์ฒ์ธ ๊ฒ์ฒ๋ผ ํธ์ถ ๊ฐ๋ฅ
}
fun <T> collection<T> joinToString ( 
    separator: String = "",
    prefix: String = "",
    postfix: String = ""
): String {
    val result = StringBuilder(prefix)
    for((idx, ele) in collection.withIndex()) {
        if (idx > 0) result.append(separator)
        result.append(ele)
    }
    result.append(postfix)
    return result.toString()
}
```

#### 3.3.4 ํ์ฅ ํจ์๋ ์ค๋ฒ๋ผ์ด๋ ๋ถ๊ฐ

```kotlin
fun main() {
    val view: View = Button()
    view.click() // Button clicked -> ์ค๋ฒ๋ผ์ด๋o 
    view.showOff() // Sasha -> ์ค๋ฒ๋ผ์ด๋x
}

open class View {
    open fun click() = println("View clicked")
}
class Button: View() {
    override fun click() = println("Button clicked")
}
fun View.showOff() = println("Sasha") // Button clicked
fun Button.showOff() = println("Lisa")
``` 

> dynamic dispatch (๋์  ๋์คํจ์น): **์คํ** ์์ ์ ๊ฐ์ฒด ํ์์ ๋ฐ๋ผ ๋์ ์ผ๋ก ํธ์ถ๋  ๋์ ๋ฉ์๋๋ฅผ ๊ฒฐ์ ํ๋ ๋ฐฉ์  
> static dispatch (์ ์  ๋์คํจ์น): **์ปดํ์ผ** ์์ ์ ์๋ ค์ง ๋ณ์ ํ์์ ๋ฐ๋ผ ์ ํด์ง ๋ฉ์๋๋ฅผ ํธ์ถํ๋ ๋ฐฉ์


#### 3.3.5 ํ์ฅ ํ๋กํผํฐ

  - ๊ธฐ์กด ํด๋์ค ๊ฐ์ฒด์ ๋ํ ํ๋กํผํฐ ํ์์ ๊ตฌ๋ฌธ์ผ๋ก ์ฌ์ฉํ  ์ ์๋ API๋ฅผ ์ถ๊ฐ
      
  ```kotlin
    // ํ์ฅ ํ๋กํผํฐ ์ ์ธ
    val StringBuilder.lastChar: Char
    get() = get(length - 1) // ํ๋กํผํฐ ๊ฒํฐ
    set(value: Char) {
        this.setCharAt(length - 1. value) // ํ๋กํผํฐ ์ธํฐ
    }
  ```

### 3.4 ์ปฌ๋ ์ ์ฒ๋ฆฌ: ๊ฐ๋ณ ๊ธธ์ด ์ธ์, ์ค์ ํจ์ ํธ์ถ, ๋ผ์ด๋ธ๋ฌ๋ฆฌ ์ง์

  - vararg ํค์๋ ์ฌ์ฉ ๋ฐ ํธ์ถ ์, ์ธ์ ๊ฐ์๊ฐ ๋ฌ๋ฆฌ์ง ์ ์๋ ํจ์๋ฅผ ์ ์
  - infix(์ค์) ํจ์ ํธ์ถ ๊ตฌ๋ฌธ ์ฌ์ฉ ์, ํ๋์ ์ธ์๋ฅผ ๊ฐ๋ ๋ฉ์๋๋ฅผ ๊ฐํธํ๊ฒ ํธ์ถ
  - destructuring declaration(๊ตฌ์กฐ ๋ถํด ์ ์ธ) ์ฌ์ฉ ์, ๋ณตํฉ์ ์ธ ๊ฐ์ ๋ถํดํด์ ๋ค์์ ๋ณ์์ ํ ๋น ๊ฐ๋ฅ

#### 3.4.2 ๊ฐ๋ณ ์ธ์ ํจ์: ์ธ์์ ๊ฐ์๊ฐ ๋ฌ๋ผ์ง ์ ์๋ ํจ์ ์ ์

  - ๊ฐ๋ณ ๊ธธ์ด ์ธ์: ๋ฉ์๋๋ฅผ ํธ์ถํ  ๋ ์ํ๋ ๊ฐ์๋งํผ ๊ฐ์ ์ธ์๋ก ๋๊ธฐ๋ฉด ์๋ฐ ์ปดํ์ผ๋ฌ๊ฐ ๋ฐฐ์ด์ ๊ทธ ๊ฐ๋ค์ ๋ฃ์ด์ฃผ๋ ๊ธฐ๋ฅ
  - ์คํ๋ ๋ ์ฐ์ฐ์: ๋ฐฐ์ด ์์ *๋ฅผ ๋ถ์ฌ์ฃผ๋ฉด ์ด์ฉ ๊ฐ๋ฅ. ๊ทธ๋ฌ๋ ์๋ฐ์์ ์ฌ์ฉ ๋ถ๊ฐ

    ```kotlin
    fun main(args: Array<String>) {
        val list = listOf("args: ", *args)
        println(list)
    }
    ```

#### 3.4.3 ๊ฐ์ ์ ๋ค๋ฃจ๊ธฐ: ์ค์ ํธ์ถ๊ณผ ๊ตฌ์กฐ ๋ถํด ์ ์ธ

  - infix call (์ค์ ํธ์ถ): ์ผ๋ฐ์ ์ธ ํจ์ ํธ์ถ ์์ ๊ฐ๋ตํ๊ฒ ๋ํ๋ธ ๋ฐฉ๋ฒ. ์ธ์๊ฐ ํ๋๋ฟ์ธ ์ผ๋ฐ ๋ฉ์๋ or ํ์ฅ ํจ์์๋ง ์ฌ์ฉ ๊ฐ๋ฅ
  - destructuring declaration (๊ตฌ์กฐ ๋ถํด ์ ์ธ): js์ ๊ตฌ์กฐ ๋ถํด ํ ๋น๊ณผ ์ ์ฌ

      ```kotlin
      val map = mapOf(1 to "one", 7 to "seven", 53 to "fifty-three")
      1.to("one") // ํ์ฅ ํจ์ to๋ฅผ ์ผ๋ฐ์ ์ธ ๋ฐฉ์์ผ๋ก ํธ์ถ
      1 to "one" // ์ค์ ํธ์ถ 
    
      val (number, name) = 1 to "one" // ๊ตฌ์กฐ ๋ถํด ์ ์ธ number == 1, name == "one"
      ```

### 3.5 ๋ฌธ์์ด๊ณผ ์ ๊ท์ ๋ค๋ฃจ๊ธฐ

#### 3.5.1 ๋ฌธ์์ด ๋๋๊ธฐ

  - ์ฝํ๋ฆฐ ์ ๊ท์ ๋ฌธ๋ฒ์ ์๋ฐ์ ๊ฐ์ผ๋ฉฐ, ํ์ฅํจ์๋ฅผ ์ด์ฉํ์ฌ ๋์ฑ ๊ฐํธํ๊ฒ ๋ํ๋

    ```kotlin
    println("12.345-6.A".split("\\.|-".toRegex())) // ์ ๊ท์ ์ด์ฉ
    println("12.345-6+A".split('.', '-')) // ํ์ฅํจ์ ์ด์ฉ
    ```

#### 3.5.2 ์ ๊ท์๊ณผ 3์ค ๋ฐ์ดํ๋ก ๋ฌถ์ ๋ฌธ์์ด

  - 3์ค ๋ฐ์ดํ ๋ฌธ์์ด์์๋ ์ญ์ฌ๋์๋ฅผ ํฌํจํ ์ด๋ค ๋ฌธ์๋ ์ด์ค์ผ์ดํ ํ์ ์์

    ```kotlin
    fun main() {
        parsePath("/User/yole/kotlin-book/chapter.adoc")
    }
    
    fun parsePath(path: String) {
        val regex = """(.+)/(.+)\.(.+)""".toRegex() // (.+): ๋๋ ํฐ๋ฆฌ, ํ์ผ์ด๋ฆ, ํ์ฅ์๋ฅผ ๋ํ๋ธ๋ค
        val matchResult = regex.matchEntire(path)
        
        if(matchResult != null) {
            val (directory, filename, extension) = matchResult.destructured
            println("Dir: ${directory}, name: ${filename}, ext: ${extension}")
        }
    }
    ```
    
### 3.6 ์ฝ๋ ๋ค๋ฌ๊ธฐ: ๋ก์ปฌ ํจ์์ ํ์ฅ

  - ์ฝํ๋ฆฐ์์๋ ํจ์์์ ์ถ์ถํ ๋ก์ปฌ ํจ์๋ฅผ ์ ํจ์ ๋ด๋ถ์ ์ค์ฒฉ์์ผ DRY(์ฝ๋์ค๋ณต)๋ฅผ ์ง์

    ```kotlin
    class User(val id: Int, val name: String, val address: String)
    
    fun User.validateBeforeSave() {
        fun validate(value: String, fieldName: String) { // ๋ก์ปฌํจ์ ์ ์
            if(value.isEmpty()) {
                throw IllegalArgumentException("Can't save user ${id}: " + "empty $fieldName")
            }
    
        }
        // ๋ก์ปฌํจ์๋ฅผ ํธ์ถํด์ ๊ฐ ํ๋๋ฅผ ๊ฒ์ฆ
        validate(name, "Name")
        validate(address, "Address") 
    }
    
    fun saveUser(user: User) {
        user.validateBeforeSave() // ํ์ฅํจ์ ํธ์ถ
    }
    ```