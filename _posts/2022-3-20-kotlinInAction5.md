---
layout: post
title: "📅 Kotlin in Action - 5장 람다로 프로그래밍"
excerpt: "Kotlin in Action 5장 요약 노트입니다."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-3-20
tags: [Kotlin]
---

>목표: 컬렉션을 처리하는 패턴을 표준 라이브러리 함수에 람다를 넘기는 방식으로 대치하는 방법에 대해서 알아보자

### 5.1 람다식과 멤버 참조

#### 5.1.1 람다 소개: 코드 블록을 함수 인자로 넘기기

 - 함수형 프로그래밍: 함수를 값처럼 다루는 접근 방법을 택하여 이벤트 핸들러 같은 일련의 동작을 수행
  
 - java에서의 이벤트 리스너 구현
  ```java
    button.setOnClickListener(new OnClicklistener() {
	  @Override
      public void onClick(View view)   
    }
  ```
  - 코틀린에서의 이벤트 리스너 구현 
  ```kotlin
    button.setOnClickListener{}
  ```
#### 5.1.2 람다와 컬렉션

  - 컬렉션을 검색하는 직접적인 방법

    ```kotlin
    fun main() {
        val people = listOf(Person("Sasha", 34), Person("Lisa", 31))
        findTheOldest(people)
    }
    
    fun findTheOldest (people: List<Person>) {
        var maxAge = 0
        var theOldest: Person? = null
        for (person in people) {
            if (person.age > maxAge) {
                maxAge = person.age
                theOldest = person
            }   
        }
        println(theOldest)
    }
    ```
  
    - 람다를 이용해 컬렉션 검색하기

    ```kotlin
    fun main() {
        val people = listOf(Person("Sasha", 34), Person("Lisa", 31))
        println(people.maxBy{it.age}) // {it.age}는 비교에 사용할 값을 돌려주는 함수 
    }
    ```

  - 멤버 참조를 사용해 더 짧게 코드로 나타내자

    ```kotlin
    people.maxBy(Person::age)
    ```

#### 5.1.3 람다식의 문법

  - Lambda: 값처럼 여기저기 전달할 수 있는 동작의 모음 -> 함수형 프로그래밍의 핵심
  - 함수 호출 시 맨 뒤에 있는 인자가 람다 식이라면 괄호 밖으로 빼낼 수 있음

    ```kotlin
      // -> 기점으로 왼쪽이 전달인자, 오른쪽이 본문임
      {x: Int, y: Int -> x + y}
      
      // 코드 일부분을 블록으로 둘러싸 실행할 필요가 있다면 run 사용
      run {x: Int, y: Int -> x + y}
    
      // 람다식을 사용하여 상기 컬렉션 검색하기 구현 
      people.maxBy {p: Person -> p.age}
    ```
    
  - 이름 붙인 인자를 사용해 람다 넘기기
    
    ```kotlin
    fun main() {
        val people = listOf(Person("Sasha", 34), Person("Lisa", 31))
        val names = people.joinToString(separator = " ",
        transform = {p: Person -> p.name}
        )     
    }
    // 람다를 괄호 밖에 전달하기 
    people.joinToString(" ") {p: Person -> p.name}
    
    // 람다 파라미터 타입 제거하기
    people.maxBy {p -> p.age}
    ```
  
    - 람다의 전달인자가 하나뿐이고, 그 타입을 컴파일러가 추론할수 있는 경우 it 사용 
    
    > 너무 it을 남용하면, it을 파악하는데 어려움이 있음
    
    ```kotlin
    people.maxBy{ it.age }
    ```
    - 람다식 내 여러 줄인 경우, 가장 마지막에 있는 식이 람다의 결과 값이 됨
  
#### 5.1.4 현재 영역에 있는 변수에 접근

  - 람다를 함수 안에서 정의하면 함수의 파라미터 뿐만 아니라 람다 정의의 앞에 선언된 로컬 변수까지 람다에서 모두 사용 가능
  - 람다 안에서 사용하는 외부 변수를 **람다가 포획한 변수**라고 함
  - closure 함수: 내부 함수가 외부 함수의 맥락(context)에 접근할 수 있는 것 -> 함수에서 기존값을 잊지 않고 기억하기 위해서 만들어진 개념

  - 함수가 반환되면 스코프 내 로컬 변수의 생명 주기는 끝남. 하지만 포획한 변수가 있는 람다를 저장해서 함수가 끝난 뒤에 실행해도 포획한 변수를
    읽거나 쓸 수 있음 -> 파이널이 아닌 변수를 포획한 경우, 변수를 특별한 래퍼로 감싸서 래퍼에 대한 참조를 람다 코드와 함께 저장
   
  ```kotlin
  fun main() {
      val res = listOf("200 OK", "418 I'm a teapot", "500 Internal Server Error", "503 Service Unavailable")
      printProblemCounts(res)
  }

  fun printProblemCounts(res: Collection<String>) {
		var clientErrors = 0
		var serverErrors = 0 // 람다에 사용할 변수 혹은 람다가 포획한 변수
		res.forEach {
			if (it.startsWith("4")) {
				clientErrors++ // 람다 안에서 람다 밖의 변수에 접근하여 수정 
			} else if (it.startsWith("5")) {
				serverErrors++
			}
			println("$clientErrors client errors, $serverErrors server errors")
		}
  }
  ```
    
> 람다를 이벤트 핸들러나 다른 비동기적으로 실행되는 코드로 활용하는 경우, 함수 호출이 끝난 다음에 로컬 변수가 변경될 수 있음

#### 5.1.5 멤버 참조

- 함수를 값으로 바꾸기 위해서 이중 콜론(::)을 이용
```kotlin
val getAge = Person ::age
```