---
layout: post
title: "๐ Kotlin ๊ฐ์๋ธํธ - 20๊ฐ๊น์ง"
excerpt: "๋๋ชจ์ Kotlin ๊ฐ์ข ์์ฝ๋ณธ์๋๋ค "
subtitle: "Kotlin youtube lecture"
toc: true
toc_sticky: true
toc_label: "ํ์ด์ง ์ฃผ์ ๋ชฉ์ฐจ"
date: 2022-1-18
tags: [Kotlin]
---

#### Object
 
  - Singleton Pattern: ํด๋์ค์ ์ธ์คํด์ค๋ฅผ ๋จ ํ๋๋ง ๋ง๋ค์ด ์ฌ์ฉํ๋ ์ํคํ์ณ ํจํด
  - ์ค๋ธ์ ํธ๋ก ์ ์ธ๋ ๊ฐ์ฒด๋ ์ต์ด ์ฌ์ฉ ์ ์๋์ผ๋ก ์์ฑ
  - ๋ฐ๋ผ์, ๊ณตํต์ ์ผ๋ก ์ฌ์ฉํ  ์ ์๋ ๊ณต์ฉ ์์ฑ ๋ฐ ํจ์๋ฅผ ๋ฌถ์ด์ ์์ฑ  
  
  - Companion Object: ๊ธฐ์กด class ์์ ์์ฑํ์ฌ ์ธ์คํด์ค ๊ฐ ๊ณต์ฉํ  ์ ์๋ ์์ฑ๊ณผ ํจ์๋ฅผ ๋ณ๋ ์์ฑ
  - Static Member์ ๋น์ท -> ๊ณต์ฉ์ผ๋ก ์ฌ์ฉ๊ฐ๋ฅํ ์์ฑ์ด๋ ํจ์

    ```kotlin
    fun main() {
        var a = FoodPoll("์ง์ฅ")
        var b = FoodPoll("์งฌ๋ฝ")
        
        a.vote()
        a.vote()
        a.vote()
        a.vote()
        b.vote()
        
        println("์ง์ฅ๋ฉด์ ์นด์ดํธ ์: ${a.count} \n ์งฌ๋ฝ์ ์นด์ดํธ ์: ${b.count}")
    }
    
    class FoodPoll (val name: String) {
        companion object {
            var total = 0
        }
      
        var count = 0
      
        fun vote() {
            total ++
            count ++
        }
    }
    ```

#### ์ต์ ๋ฒ ํจํด

- ์ต์ ๋ฒ ํจํด: ์ด๋ฒคํธ ๋ฆฌ์ค๋๋ ๊ฐ์ผ๋ฉฐ ๊ตฌํ ์ ๋ ๊ฐ์ ํด๋์ค๊ฐ ํ์. ์ด๋ฒคํธ๋ฅผ ์์ ํ๋ ํด๋์ค, ์ด๋ฒคํธ์ ๋ฐ์ 
๋ฐ ์ ๋ฌ์ ๋ด๋นํ๋ ํด๋์ค์ 
- ๋ ํด๋์ค ์ฌ์ด์ ์ธํฐํ์ด์ค๋ฅผ ์ฝ์, ์ด ์ธํฐํ์ด์ค๋ฅผ ์ต์ ๋ฒ, ๋ฆฌ์ค๋๋ผ๊ณ  ๋ถ๋ฆ. ์ด๋ฒคํธ๋ฅผ ๋๊ฒจ์ฃผ๋ ํ์๋ฅผ callback์ด๋ผ๊ณ  ํจ

```kotlin
fun main() {
	EventPrinter().start()
    
}

// ์ด๋ฒคํธ ๋ฆฌ์ค๋, ํด๋์ค ๋๊ฐ๋ฅผ ์ฐ๊ฒฐํจ
interface EventListner {
    fun onEvent(count: Int)
} 

// ์ด๋ฒคํธ๋ฅผ ์์ ํ๋ ํด๋์ค
class Counter(var listener: EventListner) {
   fun count() {
       for(i in 1..100) {
           if(i % 5 == 0) listener.onEvent(i)
       }
   }
}

// ์ด๋ฒคํธ์ ๋ฐ์ ๋ฐ ์ ๋ฌ ๋ด๋นํ๋ ํด๋์ค
// class EventPrinter {

//     fun start() {
//         val counter = Counter(object: EventListner {
//             override fun onEvent(count: Int) {
//                 print("${count}-")
//             }
//         })
//         counter.count()
//     }
// }

// ์ต๋ช๊ฐ์ฒด๋ฅผ ์ด์ฉํ ๋ฆฌํฉํ ๋ง 
class EventPrinter: EventListner {
    override fun onEvent(count: Int) {
        print("${count}-")
    }
    fun start() {
        val counter = Counter(this)
        counter.count()
    }
}
```
#### polymorphysm(๋คํ์ฑ)

- ํด๋์ค๋ฅผ ์์ํ๋ค๋ณด๋ฉด ํ์ ํด๋์ค์์ ์์ ํด๋์ค์ ๋๊ฐ์ ์ด๋ฆ์ ํ๋กํผํฐ์ ๋ฉ์๋๋ฅผ ์ง์ ํ  ์ผ์ด ์๊น. **ํ์ ํด๋์ค์์ ์ด๋ฆ์ ๊ฐ์ง๋ง ํธ์ถ 
๋งค๊ฐ๋ณ์๊ฐ ๋ค๋ฅด๊ฑฐ๋ ์ ํ ๋ค๋ฅธ ๋์์ ๋ฉ์๋๋ฅผ ์ ์.** ํด๋์ค์ ์์๊ด๊ณ์์ ์ค๋ ์ธ์คํด์ค์ ํธํ์ฑ์ ์ ๊ทน ํ์ฉํ  ์ ์๋ ๊ธฐ๋ฅ์
- up/down casting: ํ์ ์ธ์คํด์ค๋ฅผ ์ํผํด๋์ค๋ก ๋ณํํ๋ ํ์. ๋ฐ๋์ ๊ฒฝ์ฐ down-casting์ด๋ฉฐ as, is ์ฐ์ฐ์ ํ์
- as: ๋ณ์๋ฅผ ํธํ๋๋ ์๋ฃํ์ผ๋ก ๋ณํ ํ ๋ฐํ๊น์ง ํด์ฃผ๋ ์บ์คํ ์ฐ์ฐ์

    ```kotlin
    var a: Drink = Cola()
    a as Cola
    ```
- is: ๋ณ์๊ฐ ์๋ฃํ์ ํธํ๋๋์ง๋ฅผ ๋จผ์  ์ฒดํฌํ ํ์ ๋ณํํด์ฃผ๋ ์ฐ์ฐ์. ์กฐ๊ฑด๋ฌธ๊ณผ ๊ฐ์ด ์ฐ์.

    ```kotlin
    var a:Drink = Cola()
    if(a is Cola) {
    "์ด ์์์๋ง a๊ฐ ์ฝ๋ผ"
    }
    ```

```kotlin
fun main() {
   
   var a = Drink() 
   var b: Drink = Cola()
   
   a.drink()
   b.drink()
   
   if(b is Cola){
     b.washDishes()
	 }
   
   var c = b as Cola
   c.washDishes()
   // as๋ฅผ ์ฐ๋ฉด ๋ณ์ ์์ฒด๋ ๋ค์ด๊ทธ๋ ์ด๋
   b.washDishes() 
}

open class Drink{
    var name = "์๋ฃ"
    
    open fun drink() {
        println("${name}์ ๋ง์ญ๋๋ค")
    }
}

class Cola: Drink() {
    var type = "์ฝ๋ผ"
    
    override fun drink() {
        println("${name}์ค์ ${type}๋ฅผ ๋ง์ญ๋๋ค")
    }
    
    fun washDishes() {
        println("${type}๋ก ๋ชฉ์์ ํฉ๋๋ค")
    }
}
```