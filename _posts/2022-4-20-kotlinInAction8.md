---
layout: post
title: "π Kotlin in Action - 8μ₯ κ³ μ°¨ ν¨μ: νλΌλ―Έν°μ λ°ν κ°μΌλ‘ λλ€ μ¬μ©"
excerpt: "Kotlin in Action 8μ₯ μμ½ λΈνΈμλλ€."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "νμ΄μ§ μ£Όμ λͺ©μ°¨"
date: 2022-4-24
tags: [Kotlin]
---

>λͺ©ν: κ³ μ°¨ ν¨μλ‘ μ½λλ₯Ό λ κ°κ²°νκ² λ€λ¬κ³  μ½λ μ€λ³΅μ μμ λ λ± λ λμ μΆμνλ₯Ό κ΅¬μΆνλ λ°©λ²μ λ°°μλ³΄μ.


### 8.1 κ³ μ°¨ ν¨μ μ μ 

  - κ³ μ°¨ ν¨μ: λ€λ₯Έ ν¨μλ₯Ό μΈμλ‘ λ°κ±°λ ν¨μλ₯Ό λ°ννλ ν¨μ, μ½νλ¦°μμλ λλ€λ ν¨μ μ°Έμ‘°λ₯Ό μΈμλ‘ λκΈ°κ±°λ λ°νν  μ μμ

#### 8.1.1 ν¨μ νμ

  - μ»΄νμΌλ¬λ sumκ³Ό actionμ΄ ν¨μ νμμμ μΆλ‘ ν¨ 

    ```kotlin
        val sum: (Int, Int) -> Int = {x, y -> x + y} // Int μΈμ 2κ°λ₯Ό λ°μμ Int κ°μ λ°ν 
        val action: () -> Unit = {println(42)} // No μΈμ, No λ¦¬ν΄ ν¨μ
    ```

  - ν¨μ νμμ μ μνλ €λ©΄ ν¨μ μΈμμ νμμ κ΄νΈ μμ λ£κ³ , κ·Έ λ€μ νμ΄νλ₯Ό μΆκ°ν λ€μ, ν¨μμ λ°ν νμμ μ§μ 
  - Unit νμμ μλ―Έ μλ κ°μ λ°ννμ§ μμ

    ```kotlin
    (Int, String) -> Unit 
    ```

  - ν¨μ νμμμλ λ°ν νμμ nullable νμμΌλ‘ μ§μ  κ°λ₯
  - λ§μ°¬κ°μ§λ‘ nullable ν¨μ νμ λ³μ μ μ κ°λ₯. λ¨, ν¨μ νμ μ μ²΄κ° nullable μ μΈνκΈ° μν΄ ν¨μ νμμ κ΄νΈλ‘ κ°μΈκ³  λ¬Όμν κΈ°μ¬

    ```kotlin
    var canReturnNull: (Int, Int) -> Int? = {x, y -> null}
    var funOrNull: ((Int, Int) -> Int)? = null
    ```

  - μΈμλͺμ νμ κ²μ¬ μ λ¬΄μλλ©°, λλ€ μ μ μ, μΈμλͺμ΄ ν¨μ νμ μ μΈμ νλΌλ―Έν° μ΄λ¦κ³Ό μΌμΉνμ§ μμλ λ¨ 

    ```kotlin
    fun performRequest(
        url: String,
        callback: (code: Int, content: String) -> Unit
    ) {/*...*/}
    
    val url = "https://2bytescorp.com"
    performRequest(url) {code, page -> /*...*/} // 2λ²μ§Έ μΈμλͺμ΄ pageλ‘ μ€μ λλ μκ΄x
    ```

#### 8.1.2 μΈμλ‘ λ°μ ν¨μ νΈμΆ 

  - ν¨μ μ΄λ¦ λ€μ κ΄νΈλ₯Ό λΆμ΄κ³  κ΄νΈ μμ μνλ μΈμλ₯Ό commaλ‘ κ΅¬λΆν΄ λ£μ΄μ£Όμ

    ```kotlin
    fun twoAndThree(operation: (Int, Int) -> Int) {
        val result = operation(2, 3)
        println("$result")
    }
    twoAndThree{a,b -> a+b} // 5
    twoAndThree{a,b -> a*b} // 6
    ```

  - filter λ©μλ κ΅¬ννκΈ°
    ```kotlin
    fun String.filter(predicate: (Char) -> Boolean): String
    /*  / μμ  κ°μ²΄ νμ /  μΈμλͺ  / μΈμν¨μμ μΈμνμ / μΈμν¨μμ λ°ν νμ/   */
    
    // filter ν¨μλ₯Ό λ¨μνκ² λ§λ  λ²μ  κ΅¬ννκΈ°
    fun String.filter(predicate: (Char) -> Boolean): String {
        val sb = StringBuilder()
        for (i in 0 until length) {
            val element = get(i)
            if (predicate(element)) sb.append(element) // predicate μΈμλ‘ μ λ¬λ°μ get()λ₯Ό νΈμΆ 
        }
        return sb.toString()
    }
    
    println("ablc".filter {it in 'a'..'z'}) // abc
    ```

#### 8.1.3 μλ°μμ μ½νΈλ¦° ν¨μ νμ μ¬μ© (pending)

  - ν¨μ νμμ λ³μλ FunctionN μΈν°νμ΄μ€λ₯Ό κ΅¬ννλ κ°μ²΄λ₯Ό μ μ₯
  
#### 8.1.4 λν΄νΈ κ°μ μ§μ ν ν¨μ νμ μΈμλ nullable ν¨μ νμ μΈμ

  - μΈμλ₯Ό ν¨μ νμμΌλ‘ μ μΈν  λλ λν΄νΈ κ°μ μ νκΈ° κ°λ₯
  - nullable ν¨μ νμ μΈμ μ¬μ©νκΈ°

    ```kotlin
    fun <T> Collection<T>.joinToString ( // μ λ€λ¦­ ν¨μ
            separator: String = ", ",
            prefix: String = "",
            postfix: String = "",
            transform: ((T) -> String)? = null // nullable ν¨μ νμμ μΈμλ₯Ό μ μΈ
    ): String {
        val result = StringBuilder(prefix)
        for((i, e) in this.withindex()) {
            if (i > 0) result.append(separator)
            var str = transform?.invoke(e) // μμ  νΈμΆμ μ¬μ©ν΄ ν¨μ νΈμΆ
                    ?: e.toString() // μλΉμ€ μ°μ°μλ₯Ό μ¬μ©ν΄ λλ€λ₯Ό μΈμλ‘ λ°μ§ μμ κ²½μ°λ₯Ό μ²λ¦¬
            result = append.append(str)
        }
        result.append(postfix)
        return result.toString()
    }
    
    val letters = listOf("Alpha", "Beta")
    println(letters.joinToString()) // Alpha, Beta
    println(letters.joinToString { it.toLowerCase() }) // alpha, beta
    println(letters.joinToString(separator = "! ", postfix = "! ", 
            ...transform = {it.toLowerCase()})) // ALPHA!, BETA!
    ```

#### 8.1.5 ν¨μλ₯Ό ν¨μμμ λ°ν

  - νλ‘κ·Έλ¨μ μνλ λ€λ₯Έ μ‘°κ±΄μ λ°λΌ λ¬λΌμ§ μ μλ λ‘μ§ κ΅¬ν

    ```kotlin
    enum class Delivery {STANDARD, EXPEDITED} 
    class Order(val itemCount: Int) 
    fun getShippingCostCalculator(delivery: Delivery): (Order) -> Double { // Order ν¨μλ₯Ό λ°μ Double ν¨μλ₯Ό λ°ν
        if (delivery == Delivery.EXPEDITED) {
            return {order -> 6 + 2.1 * order.itemCount} // λλ€ λ°ν1
        }
        return {order -> 1.2 * order.itemCount} // λλ€ λ°ν2
    }
    
    val calculator = getShippingCostCalculator(Delivery.EXPEDITED)
    println("Shipping costs ${calculator(Order(3))}") // Shipping costs 12.3
    ```

  - μ¬μ©μμ UI μλ ₯ μ°½μ μλ ₯ν λ¬Έμμ΄κ³Ό λ§€μΉλλ μ°λ½μ²λ§ νλ©΄μ νμνλ λ‘μ§ κ΅¬ν.

    ```kotlin
    data class Person(
        val firstName: String,
        val lastName: String, 
        val phoneNumber: String?
    )
    
    class ContactListFilters {
        var prefix: String = ""
        var onlyWithPhoneNumber: Boolean = false 
        
        fun getPredicate(): (Person) -> Boolean { // ν¨μλ₯Ό λ°ννλ ν¨μ μ μ
            val startsWithPrefix = { p: Person ->
                p.firstName.startsWith(prefix) || p.lastName.startsWith(prefix)
            }
            if (!onlyWithPhoneNumber) { // ν¨μ νμμ λ³μλ₯Ό λ°ν
                return startsWithPrefix
            }
            return { startsWithPrefix(it) && it.phoneNumber = null } // λλ€ λ°ν
        }
    }
    
    val contacts = listOf(Person("Sasha", "Park", "123-4567"), Person("Lisa", "Park", "321-3212"))
    val contactListFilters = ContactListFilters()
    with (contactListFilters) {
        prefix = "Sa"
        onlyWithPhoneNumber = true
    }
    println(contacts.filter( ... contactListFilters.getPredicate()))
    // [Person(firstName=Sasha, lastName=Park, phoneNumber=123-4567)]
    ```

#### 8.1.6 λλ€λ₯Ό νμ©ν μ€λ³΅ μ κ±° 

  - μ¬μ΄νΈ λ°©λ¬Έ λ°μ΄ν° μ μ 

    ```kotlin
    data class SiteVisit (
        val path: String,
        val duration: Double,
        val os: OS
    )
    enum class OS {WINDOWS, LINUX, MAC, IOS, ANDROID}
    val log = listOf (
        SiteVisit("/", 34.0, OS.WINDOWS)
        SiteVisit("/", 3.0, OS.MAC),
        SiteVisit("/login", 12.0, OS.IOS),
        SiteVisit("/signup", 76.0, OS.ANDROID),
        SiteVisit("/", 24.0, OS.LINUX)
    )
    
    val averageWindowsDuration = log
        .filter {it.OS == OS.WINDOWS}
        .map(SiteVisit::duration)
        .average()
    
    println(averageWindowsDuration) // 34.0
    ```

  - κ³ μ°¨ ν¨μλ₯Ό ν΅ν΄ μ€λ³΅ μ κ±°

    ```kotlin
    fun List<SiteVisit>.averageDurationFor (predicate: (SiteVisit) -> Boolean =
    filter(predicate).map(SiteVisit::duration).average()
    )
    
    println(log.averageDurationFor {
        ... it.os in setOf(OS.ANDROID, OS.IOS)
    }) // 12.15
    
    println(log.averageDurationFor {
        ... it.os == OS.IOS && it.patj == "/signup"
    }) // null
    ```

### 8.2 μΈλΌμΈ ν¨μ: λλ€μ λΆκ° λΉμ© μμ κΈ°

  - λλ€κ° μμ±λλ μμ λ§λ€ μλ‘μ΄ λ¬΄λͺ ν΄λμ€ κ°μ²΄ μκΈ°κ³  μ€ν μμ μ λ°λ₯Έ λΆκ° λΉμ©μ΄ λ¦
  - inline λ³κ²½μλ₯Ό ν¨μμ λΆμ΄λ©΄ μ»΄νμΌλ¬λ κ·Έ ν¨μλ₯Ό νΈμΆνλ λ¬Έμ₯μ ν¨μ λ³Έλ¬Έμ ν΄λΉνλ λ°μ΄νΈ μ½λλ‘ λ³ννμ¬ μ’ λ ν¨μ¨μ μΈ μ¬μ©μ΄ κ°λ₯

#### 8.2.1 μΈλΌμ΄λμ΄ μλνλ λ°©μ

  - inline: ν¨μ νΈμΆ μ½λλ₯Ό ν¨μ νΈμΆ λ°μ΄νΈμ½λ λμ μ ν¨μ λ³Έλ¬Έμ λ²μ­ν λ°μ΄νΈ μ½λλ‘ μ»΄νμΌ
  - λλ€ λ³Έλ¬Έμ μν΄ μμ±λλ λ°μ΄νΈμ½λλ λλ€ νΈμΆμ½λ(synchronized) μΌλΆλΆμΌλ‘ κ°μ£Ό -> λ¬΄λͺ ν΄λμ€λ‘ κ°μΈμ§ μμ, μ¦ μ±λ₯ ν₯μμ΄ μμ

    ```kotlin
    inline fun <T> synchronized(lock: Lock, action: () -> T): T {
        lock.lock()
        try {
            return action()
        } finally {
            lock.unlock()
        }
    }
    val 1 = lock()
    synchronized(1)
    ```

#### 8.2.2 μΈλΌμΈ ν¨μμ νκ³ 

  - μΈλΌμΈ ν¨μμ λ³Έλ¬Έμμ λλ€ μμ λ°λ‘ νΈμΆνκ±°λ λλ€ μμ μΈμλ‘ μ λ¬λ°μ νΈμΆνλ κ²½μ° μ΄μΈμλ λλ€ μΈλΌμ΄λ λΆκ° -> "Illegal usage of inline-parameter"
  - λ μ΄μμ λλ€λ₯Ό μΈμλ‘ λ°λ ν¨μμμ μΌλΆ λλ€λ§ μΈλΌμ΄λ μ μ©νκ³  μΆμ μ, noinline λ³κ²½μλ₯Ό μΈμ μ΄λ¦ μμ λΆμ

    ```kotlin
    inline fun foo (inlined: () -> Unit, noinline NotInlined: () -> Unit) { ... }
    ```

#### 8.2.3 μ»¬λ μ μ°μ° μΈλΌμ΄λ

    ```kotlin
    // λλ€λ₯Ό μ¬μ©ν΄ μ»¬λ μ κ±°λ₯΄κΈ°
    data class Person(val: Nameval : String, val age: Int)
    val people = listOf(Person("Alice", 29), Person("Bob", 31))
    println(people.filter {it.age < 30}) // Person(name=Alice, age=29)
    
    // λλ€μμ μ¬μ©νμ§ μκ³  μ»¬λ μ κ±°λ₯΄κΈ°
    val result = mutableListOf<Person>()
    for (person in people) {
        if (person.age < 30) result.add(person)  
    }
    println(result) // Person(name=Alice, age=29)
    ```

#### 8.2.4 ν¨μλ₯Ό μΈλΌμΈμΌλ‘ μ μΈν΄μΌ νλ κ²½μ°

  - λλ€λ₯Ό μΈμλ‘ λ°λ ν¨μλ§ (ex. νμ€λΌμ΄λΈλ¬λ¦¬ ν¨μ) μ±λ₯μ΄ μ’μμ§ κ°λ₯μ±μ΄ λμ 
  - inline λ³κ²½μλ₯Ό ν¨μμ λΆνγΉ λλ μ½λ ν¬κΈ°μ μ£Όμλ₯Ό κΈ°μΈμΌ κ² 

#### 8.2.5 μμ κ΄λ¦¬λ₯Ό μν΄ μΈλΌμΈλ λλ€ μ¬μ©

  - μμ (ex. νμΌ, λ½, λ°μ΄ν°λ² μ΄μ€ νΈλμ­μ λ±) κ΄λ¦¬ μ, λλ€λ‘ μ€λ³΅μ μμ¨ μ μλ λ©μΈ ν¨ν΄μ
  - λ³΄ν΅ try/finally λ¬Έμ μ¬μ©νμ¬ μμ κ΄λ¦¬ ν¨ν΄μ κ΅¬ν 
    
    ```kotlin
    // μλ° try-with-resource κΈ°λ₯μ μ κ³΅νλ use λΌμ΄λΈλ¬λ¦¬ ν¨μ
    fun readFirstLineFromFile(path: String) : String {
        BufferedReader(FileReader(path)).use { // BufferedReader κ°μ²΄λ₯Ό λ§λ€κ³ , use ν¨μ νΈμΆμ ν΅ν΄ λλ€λ‘ λκΉ
            br -> return br.readLine() // 
        }
    }
    ```

### 8.3 κ³ μ°¨ ν¨μ μμμ νλ¦ μ μ΄
#### 8.3.1 λλ€ μμ returnλ¬Έ: λλ€λ₯Ό λλ¬μΌ ν¨μλ‘λΆν° λ°ν 

  - λλ€ μμμ returnμ μ¬μ©νλ©΄ λλ€λ‘λΆν°λ§ λ°νλλκ² μλλΌ κ·Έ λλ€λ₯Ό νΈμΆνλ ν¨μκ° μ€νμ λλ΄κ³  λ°ν
  - non-local return: μμ μ λλ¬μΈκ³  μλ λΈλ‘λ³΄λ€ λ λ°κΉ₯μ μλ λΈλ‘μ λ°ννκ² λ§λλ return λ¬Έ
  - λλ€λ₯Ό μΈμλ‘ λ°λ ν¨μκ° μΈλΌμΈ ν¨μμΌλλ§ non-local return μ¬μ© κ°λ₯ 

    ```kotlin
    data class Person(val name: String, val age: Int)
    val people = listOf(Person("Sasha", 33), Person("Lisa", 30))
    
    fun lookForSasha(people: List<Person>) {
        people.forEach { 
            if (it.name == "Sasha") {
                println("Found!")
                return 
            }
        }
        println("Found!")
    }
    ```

### 8.3.2 λλ€λ‘λΆν° λ°ν: λ μ΄λΈμ μ¬μ©ν return 

  - λλ€ μμμλ local return μ¬μ© κ°λ₯ -> for λ£¨νμ breakμ λΉμ·ν μ­ν  
  - local / non-local return κ΅¬λΆμ μν΄ label@ μ¬μ© 
  - λλ€ μμ λ μ΄λΈμ λͺμνλ©΄ ν¨μ μ΄λ¦ λ μ΄λΈλ‘ μ¬μ© λΆκ°, λν λλ€ μμλ λ μ΄λΈμ΄ 2κ° μ΄μ λΆμ μ μμ

    ```kotlin
    fun lookForSasha(people: List<Person>) {
        people.forEach label@ { // λλ€ label
            if (it.name == "Sasha") {
                println("Found!")
                return@label // return μ label, μ¬κΈ°μ loop νμΆ
            }
        }
        println("Found!") // ν­μ ν΄λΉ μ€μ΄ μΆλ ₯
    }
    ```

> #### labelμ΄ λΆμ this μ  
> μμ  κ°μ²΄ μ§μ  λλ€ λ³Έλ¬Έμμλ this μ°Έμ‘°λ₯Ό μ¬μ©ν΄ λλ€λ₯Ό λ§λ€ λ μ§μ ν μμ κ°μ²΄λ₯Ό κ°λ¦¬ν¬ μ μμ  
    
    ```kotlin
    StringBuilder().apply sb@ { // this@sbλ₯Ό ν΅ν΄ λλ€μ λ¬΅μμ  μμ  κ°μ²΄μ μ κ·Όν  μ μμ
        listOf(1, 2, 3).apply { 
            this@sb.append(this.toString())
        }
    }
    ```

### λ¬΄λͺ ν¨μ: κΈ°λ³Έμ μΌλ‘ λ‘μ»¬ return

  - μ₯ν©ν non-local λ°νλ¬Έμ μ¬λΏ μ¬μ©ν΄μΌ μ½λ λΈλ‘μ μ½κ² μμ±νλ λ°©λ²
  - λ¬΄λͺ ν¨μλ μ½λ λΈλ‘μ ν¨μμ λκΈΈ λ μ¬μ©ν  μ μλ λ€λ₯Έ λ°©λ²

    ```kotlin
    fun lookForSasha (people: List<Person>) {
        people.forEach(fun(person) { // λλ€ μ λμ μ λ¬΄λͺν¨μ μ¬μ©
            if (it.name == "Sasha") return // returnμ κ°μ₯ κ°κΉμ΄ μκΈ° λ¬΄λͺν¨μλ₯Ό κ°λ¦¬ν΄ 
            println("${person.name} is not Sasha!")
        })
    }
    lookForSasha(people) // Sasha is not Sasha!
    ```

  - λ¬΄λͺ ν¨μλ μΌλ° ν¨μμ κ°μ λ°ν νμ μ§μ  κ·μΉμ λ°λ¦ 
  - λΈλ‘μ΄ λΆλ¬Έμ΄ λ¬΄λͺ ν¨μλ λ°ν νμμ λͺμν΄μΌνμ§λ§, μμ λ³Έλ¬ΈμΌλ‘ νλ κ²½μ° λ°ν νμ μλ΅ κ°λ₯

    ```kotlin 
    people.filter(fun(person):Boolean {
        return person.age < 30
    }) 
    
    people.filter(fun(person) = person.age < 30)
    ```

  - fun ν€μλλ‘ μ μλ ν¨μλ₯Ό λ°νμν€λ return μ

    ```kotlin
    fun lookForSasha (people: List<Person>) {
        people.forEach(fun(person) {
            if (person.name == "Sasha") return // returnμ κ°μ₯ κ°κΉμ΄ λ¬΄λͺν¨μλ₯Ό λ°νν¨
        })
    }
    
    fun lookForSasha (people: List<Person>) {
        people.forEach {
            if (it.name == "Sasha") return // returnμ lookForSashaμ λ°ν
        }
    }
    ```

