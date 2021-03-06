---
layout: post
title: "π Kotlin in Action - 4μ₯ ν΄λμ€, κ°μ²΄, μΈν°νμ΄μ€"
excerpt: "Kotlin in Action 4μ₯ μμ½ λΈνΈμλλ€."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "νμ΄μ§ μ£Όμ λͺ©μ°¨"
date: 2022-2-3
tags: [Kotlin]
---

#### 4.2.4 κ²ν°μ μΈν°μμ λ·λ°μΉ¨νλ νλμ μ κ·Ό 

- νΉμ  κ°μ μ μ₯νλ κ·Έ κ°μ λ³κ²½νκ±°λ μ½μ λλ§λ€ μ ν΄μ§ λ‘μ§μ μ€ννλ μ νμ νλ‘νΌν°λ₯Ό μμ±

```kotlin
fun main() {
    val user = User("Alitciia")
    user.address = "μμμ λμκ΅¬ 110-5" 
    println(user) 
    println(user.address)
}

class User(val name: String) {
    var address: String = "unspecified"
    	set(value: String) {
            println("""
            	Address was changed for $name:
   				"$field" -> "$value".""".trimIndent())
            field = value
        }
}
```

#### 4.2.5 μ κ·Όμμ κ°μμ± λ³κ²½

- μ κ·Όμμ κ°μμ±μ κΈ°λ³Έμ μΌλ‘ νλ‘νΌν°μ κ°μμ±κ³Ό κ°μΌλ get, set μμ κ°μμ± λ³κ²½μλ₯Ό μΆκ°ν΄μ μ κ·Όμ κ°μμ± λ³κ²½ κ°λ₯

```kotlin
fun main() {
	val lengthCounter = LengthCounter()
	lengthCounter.addWord("Hi!")
	println(lengthCounter.counter) // 3
}

class LengthCounter {
	var counter: Int = 0
		private set // μΈλΆ μ½λμμ λ¨μ΄ κΈΈμ΄λ¦ ν©μ λ§μλλ‘ λ°κΎΈμ§ λͺ»νκ² νκΈ° μν΄μ λ΄λΆμμλ§ λ³κ²½ κ°λ₯μΌ ν¨
	fun addWord(word: String) {
		counter += word.length
	}
}
```

### 4.3 μ»΄νμΌλ¬κ° μμ±ν λ©μλ: λ°μ΄ν° ν΄λμ€μ ν΄λμ€ μμ

- ν΄λμ€μ κΈ°λ³Έμ μΌλ‘ λ€μ΄μλ λ©μλλ€μ μ€λ²λΌμ΄λνμ¬ μ»€μ€ν°λ§μ΄μ§ κ°λ₯

#### 4.3.1 λͺ¨λ  ν΄λμ€κ° μ μν΄μΌ νλ λ©μλ 

- λ¬Έμμ΄ νν: toString()

```kotlin
fun main() {
	val client1 = Client("μ¬μ€", 4122)
    println(client1) // Client(name = μ¬μ€, postalCode=4122)
}

class Client (val name: String, val postalCode: Int) {
	override fun toString() = "Client(name = $name, postalCode=$postalCode)"   
}
```

- κ°μ²΄μ λλ±μ±: equals(other: Any)
> 
> "=="λ μμ νμμΌ κ²½μ° νΌμ°μ°μμ κ°μ΄ κ°μμ§λ₯Ό λΉκ΅, μ°Έμ‘° νμμΈ κ²½μ° νΌμ°μ°μμ μ£Όμκ° κ°μμ§λ₯Ό λΉκ΅. μ½νλ¦°μμ 
> "=="λ λ΄λΆμ μΌλ‘ equalsλ₯Ό νΈμΆν΄μ κ°μ²΄ λΉκ΅

```kotlin
fun main() {
	val client1 = Client("μ€νμ", 4122)
    val client2 = Client("μ€νμ", 4122)
    println(client1 == client2) // false
}

class Client (val name: String, val postalCode: Int) {
	override fun toString() = "Client(name = $name, postalCode=$postalCode)"   
}
```

```kotlin
class Client(val name: String, val postalCode: Int) {
	override fun equals(other: Any?) : Boolean {
		if (other == null || other !is Client)
			return false
		return name == other.name && postalCode == other.postalCode
	}
	override fun toString() = "Client(name = $name, postalCode=$postalCode)"
}
```

- ν΄μ μ»¨νμ΄λ: hashCode()
> JVM μΈμ΄μμλ equals()κ° trueλ₯Ό λ°ννλ λ κ°μ²΄λ λ°λμ κ°μ hashCode()λ₯Ό λ°νν΄μΌ ν¨. λ κ°μ²΄μ idκ° κ°μμ§λ₯Ό κ²μ¬νλ νλ‘μΈμ€

```kotlin
class Client(val name: String, val postalCode: Int) {
    override fun hashCode(): Int = name.hashCode() * 31 + postalCode
}

```

#### 4.3.2 λ°μ΄ν° ν΄λμ€: λͺ¨λ  ν΄λμ€κ° μ μν΄μΌ νλ λ©μλ μλ μμ± 

- dataλΌλ λ³κ²½μλ₯Ό ν΄λμ€ μμ λΆμ΄λ©΄ νμν λ©μλλ₯Ό μ»΄νμΌλ¬κ° μλμΌλ‘ λ§λ€μ΄μ€. κ·Έλ¦¬κ³  μ΄λ¬ν ν΄λμ€λ₯Ό λ°μ΄ν° ν΄λμ€λΌκ³  ν¨
- νκΈ° ν΄λμ€λ λ€μκ³Ό κ°μ λ©μλλ₯Ό ν¬ν¨. μΈμ€ν΄μ€ λΉκ΅λ₯Ό μν equals, ν΄μ κΈ°λ° μ»¨νμ΄λμμ ν€λ‘ μ¬μ©ν  μ μλ hashCode, ν΄λμ€μ κ° νλλ₯Ό
μ μΈ μμλλ‘ νμνλ λ¬Έμμ΄ ννμ λ§λ€μ΄ μ£Όλ toString 

```kotlin
data class Client(val name: String, val postalCode: Int) 
```

- λ°μ΄ν° ν΄λμ€μ λΆλ³μ±: copy() λ©μλ: HashMap λ±μ μ»¨νμ΄λμ λ°μ΄ν° ν΄λμ€ κ°μ²΄λ₯Ό λ΄λ κ²½μ°μ λΆλ³μ±μ΄ νμ. ν΄λμ€ μΈμ€ν΄μ€λ₯Ό μ§μ 
λ°κΎΈλ κ² λ³΄λ€λ μ°¨λΌλ¦¬ λ³΅μ¬νμ¬ μΌλΆ νλ‘νΌν°λ₯Ό λ°κΎΈκ² νλ κ²μ΄ λ€λ£¨κΈ° λ μ¬μ°λ©° μ΄λ¬ν κΈ°λ₯μ μ κ³΅

```kotlin
fun main() {
      val lee = Client("μ¬μ€", 4122)
      println(lee.copy(postalCode = 400))
      Client(name = μ¬μ€, postalCode = 4000)
}
```

> μμ  JPA μν°ν°λ₯Ό data classλ‘ μμ±νμ§λ§, μμμ΄ κΉλ€λ‘μ΄ λ¬Έμ λ‘ μΈν΄ μΌλ° classλ‘ λ³κ²½ 
> 

### 4.3.3 ν΄λμ€ μμ: By ν€μλ μ¬μ©

- λκ·λͺ¨ κ°μ²΄μ§ν₯ μμ€νμ μ€κ³ν  λ μμ€νμ μ·¨μ½νκΈ° λ§λλ λ¬Έμ λ λ³΄ν΅ κ΅¬ν μμ(implementation inheritance)μμ λ°μ -> μ½νλ¦°μ κΈ°λ³Έμ μΌλ‘ ν΄λμ€λ₯Ό finalλ‘ μ·¨κΈ
- @(Decorator ν¨ν΄): μμμ νμ©νμ§ μλ ν΄λμ€μ μλ‘μ΄ λμμ μΆκ°ν  λ μ°μ΄λ λ°©λ². νμ§λ§ κ΅¬ν μ½λλμ΄ λ§κ³  λ³΅μ‘ν¨
- κ·Έλμ by ν€μλλ₯Ό μ΄μ©νμ¬ μΈν°νμ΄μ€μ λν κ΅¬νμ λ€λ₯Έ κ°μ²΄μ μμ μ€μ΄λΌλ κ²μ νμ

```kotlin
class CountingSet<T>(
    val innerSet: MutableCollection<T> = HashSet<T>()
): MutableCollection<T> by innerSet { // MutableCollectionμ κ΅¬νμ innerSetμκ² μμ
    var objectAdded = 0 
    override fun add(element: T): Boolean { // μμνμ§ μκ³  μλ‘μ΄ κ΅¬ν μ κ³΅
        objectAdded++	
        return innerSet.add(element)
    }
    override fun addAll(c: Collection<T>): Boolean { // μμνμ§ μκ³  μλ‘μ΄ κ΅¬ν μ κ³΅
        objectAdded += c.size
        return innerSet.addAll(c)
    }	  
}
```

### 4.4 object ν€μλ: ν΄λμ€ μ μΈκ³Ό μΈμ€ν΄μ€ μμ±

- ν΄λμ€λ₯Ό μ μνλ©΄μ λμμ μΈμ€ν΄μ€(κ°μ²΄)λ₯Ό μμ±
  - object declaration(κ°μ²΄ μ μΈ): singletonμ μ μνλ λ°©λ² μ€ νλ
- companion object (λλ° κ°μ²΄): μΈμ€ν΄μ€ λ©μλλ μλμ§λ§ νΉμ  ν΄λμ€μ κ΄λ ¨ μλ λ©μλμ ν©ν λ¦¬ λ©μλλ₯Ό λ΄μ λ μ°μ
- κ°μ²΄ μμ μλ°μ anonymous inner class (λ¬΄λͺ λ΄λΆ ν΄λμ€) λμ  μ°μ

#### 4.4.1 κ°μ²΄ μ μΈ: μ±κΈν΄μ μ½κ² λ§λ€κΈ° 

- μ½νλ¦°μ κ°μ²΄ μ μΈ κΈ°λ₯μ ν΅ν΄ μ±κΈν΄μ μΈμ΄μμ κΈ°λ³Έ μ§μ. μ¦, κ°μ²΄ μ μΈμ ν΄λμ€ μ μΈκ³Ό κ·Έ ν΄λμ€μ μν λ¨μΌ μΈμ€ν΄μ€μ μ μΈμ
ν©μΉ μ μΈ
- κ°μ²΄ μ μΈ μμ νλ‘νΌν°, λ©μλ, μ΄κΈ°ν λΈλ‘ λ±μ λ£μ μ μμΌλ μ£Ό/λΆ μμ±μλ κ°μ²΄ μ μΈμ μΈ μ μμ

```kotlin
object CaseInsensitiveFileComparator: Comparator<File> { 
    override fun compare(file1: File, file2: File): Int {
			return file1.path.compareTo(file2.path, ignoreCase = true)
	}
}
```
> **Singletonκ³Ό μμ‘΄κ΄κ³ μ£Όμ**: λκ·λͺ¨ μννΈμ¨μ΄ μμ€νμμλ κ°μ²΄ μ μΈμ΄ ν­μ μ ν©νμ§λ μμ. νΉν, μμ±μ μ μ΄ν  μ μκ³  μμ±μ
νλΌλ―Έν°λ₯Ό μ§μ ν  μ μμΌλ―λ‘ λ¨μ νμ€νΈλ₯Ό νκ±°λ μννΈμ¨μ΄ μμ€νμ μ€μ μ΄ λ¬λΌμ§ λ κ°μ²΄λ₯Ό λμ²΄νκ±°λ κ°μ²΄μ μμ‘΄κ΄κ³λ₯Ό λ°κΏ μ μμ.

- μ€μ²© κ°μ²΄λ₯Ό μ¬μ©ν΄ Comparator κ΅¬ννκΈ°

```kotlin
fun main() {
    val persons = listOf(Person("Bob"), Person("Alice"))
    println(persons.sortedWith(Person.NameComparator)) // [Person(name=Alice), Person(name=Bob)]
}

data class Person(val name: String) {
    object NameComparator : Comparator<Person> {
        override fun compare(p1: Person, p2: Person): Int = p1.name.compareTo(p2.name)
    }
}
```

#### 4.4.2 λλ° κ°μ²΄: ν©ν λ¦¬ λ©μλμ μ μ  λ©€λ²κ° λ€μ΄κ° μ₯μ 

- μ½νλ¦°μ μλ°μ static ν€μλλ₯Ό μ§μνμ§ μμ. λμ  ν¨ν€μ§ μμ€μ μ΅μμ ν¨μμ κ°μ²΄ μ μΈ νμ©
- νμ§λ§ μ΅μμ ν¨μλ privateμΌλ‘ νμλ ν΄λμ€ λΉκ³΅κ° λ©€λ²μ μ κ·Όν  μ μμ΄μ, ν©ν λ¦¬ λ©μλλ₯Ό μ΄μ©
- companion ν€μλλ₯Ό λΆμ¬ λλ° κ°μ²΄λ‘ μ§μ νλ©΄ μλ°μ μ μ  λ©μλ νΈμΆ / νλ μ¬μ© κ΅¬λ¬Έκ³Ό κ°μμ§ 

```kotlin
fun main() {
    val subscribingUser = User.newSubscribingUser("sasha@2bytescorp.com")
    val facebookUser = User.newFacebookUser(4) // ν΄λμ€ μ΄λ¦μ μ¬μ©ν΄ ν΄λΉ ν΄λμ€μ μν λλ° κ°μ²΄μ λ©μλ νΈμΆ κ°λ₯
    println(subscribingUser.nickname)
}

class User private constructor(val nickname: String) { // μ£Ό μμ±μλ₯Ό λΉκ³΅κ°λ‘ μμ±
    companion object { // λλ° κ°μ²΄ μ μΈ 
        fun newSubscribingUser(email: String) = User(email.substringBefore('@'))
        fun newFacebookUser(accountId: Int) = User(getFacebookName(accountId)) // facebook μ¬μ©μ idλ‘ μ¬μ©μλ₯Ό λ§λλ ν©ν λ¦¬ λ©μλ 
    }
}
```

#### 4.4.3 λλ° κ°μ²΄λ₯Ό μΌλ° κ°μ²΄μ²λΌ μ¬μ©

- ν΄λμ€ μμ μ μλλ λλ° κ°μ²΄μ μ΄λ¦μ λΆμ΄κ±°λ, μΈν°νμ΄μ€λ₯Ό μμνκ±°λ, λλ° κ°μ²΄ μμ νμ₯ ν¨μμ νλ‘νΌν° μ μ κ°λ₯
- λλ°κ°μ²΄: ν΄λμ€ μμ μ μλ μΌλ° κ°μ²΄

```kotlin
fun main() {
	person = Person.Loader.fromJSON("{name: 'Dmitry'}")
    println(person.name) // Dmitry
}

class Person(val name: String) {
	companion object Loader { // λλ° κ°μ²΄μ μ΄λ¦μ λΆμ 
        fun fromJSON(jsonText: String): Person = {}
    }
}
```
- λλ° κ°μ²΄μμ μΈν°νμ΄μ€ κ΅¬ν κ°λ₯

```kotlin
interface JSONFactory<T> {
	fun fromJSON(jsonText: String): T
}

class People(val name: String) {
	companion object: JSONFactory<Person> {
        override fun fromJSON(jsontext:String): Person
    }
}
```

- λλ° κ°μ²΄ νμ₯: ν΄λμ€μ λλ° κ°μ²΄κ° μμΌλ©΄ κ·Έ κ°μ²΄ μμ ν¨μλ₯Ό μ μν¨μΌλ‘μ¨ ν΄λμ€μ λν΄ νΈμΆν  μ μλ νμ₯ ν¨μ μμ± κ°λ₯

```kotlin
class Person(val firstName: String, val lastName: String) {
    companion object{} // λΉμ΄μλ λλ° κ°μ²΄λ₯Ό μ μΈ
}

fun Person.Companion.fromJSON(json: String): Person {}

val p = Person.fromJSON(json) // νμ₯ ν¨μ νΈμΆ
```

#### 4.4.4 κ°μ²΄ μ: λ¬΄λͺ λ΄λΆ ν΄λμ€λ₯Ό λ€λ₯Έ λ°©μμΌλ‘ μμ±

- λ¬΄λͺ κ°μ²΄λ object ν€μλλ₯Ό μ¬μ©νμ¬ μμ±νλ©°, μλ°μ λ¬΄λͺ λ΄λΆ ν΄λμ€λ₯Ό λμ ν¨
- μ½νλ¦° κ°μ²΄ μμ λ€μμ μΈν°νμ΄μ€ κ΅¬ν, scope λ΄ λ³μ λ³κ²½ν  μ μλ λ± μλ°λ³΄λ€ λ λ§μ κΈ°λ₯ μ κ³΅
- κ°μ²΄ μμ λ¬΄λͺ κ°μ²΄ μμμ μ¬λ¬ λ©μλλ₯Ό μ€λ²λΌμ΄λν΄μΌ νλ κ²½μ°μ ν¨μ¬ μ μ©
> κ°μ²΄ μ μΈκ³Ό λ¬λ¦¬ λ¬΄λͺ κ°μ²΄λ singletonμ΄ μλλ©° κ°μ²΄ μμ΄ μ°μΌλ λ§λ€ μλ‘μ΄ μΈμ€ν΄μ€κ° μμ±

```kotlin
// λ¬΄λͺ κ°μ²΄λ‘ μ΄λ²€νΈ λ¦¬μ€λ κ΅¬ννκΈ°
window.addMouseListener {
    object: MouseAdapter() { // MouseAdapterλ₯Ό νμ₯νλ λ¬΄λͺ κ°μ²΄ μ μΈ
        override fun mouseClicked(e: MouseEvent) {} // MouseAdapterμ λ©μλλ₯Ό μ€λ²λΌμ΄λ
        override fun mouseEntered(e: MouseEvent) {} // MouseAdapterμ λ©μλλ₯Ό μ€λ²λΌμ΄λ
    }   
}

// λ¬΄λͺ κ°μ²΄ μμμ λ‘μ»¬ λ³μ μ¬μ©
fun countClicks(window: Window) {
  var clickCount = 0
  window.addMouseListener(object : MouseAdapter() { 
      override fun mouseClicked(e: MouseEvent) {
          clickCount ++
      }
  })
}
```