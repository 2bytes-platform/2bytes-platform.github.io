---
layout: post
title: "📅 Kotlin 강의노트 - 15강까지"
excerpt: "디모의 Kotlin 강좌 요약본입니다 "
subtitle: "Kotlin youtube lecture"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-1-18
tags: [Kotlin]
---

#### Object
 
  - Singleton Pattern: 클래스의 인스턴스를 단 하나만 만들어 사용하는 아키텍쳐 패턴
  - 오브젝트로 선언된 객체는 최초 사용 시 자동으로 생성
  - 따라서, 공통적으로 사용할 수 있는 공용 속성 및 함수를 묶어서 생성  
  
  - Companion Object: 기존 class 안에 생성하여 인스턴스 간 공용할 수 있는 속성과 함수를 별도 생성
  - Static Member와 비슷 -> 공용으로 사용가능한 속성이나 함수

```kotlin
fun main() {
    var a = FoodPoll("짜장")
    var b = FoodPoll("짬뽕")
    
    a.vote()
    a.vote()
    a.vote()
    a.vote()
    b.vote()
    
    println("짜장면의 카운트 수: ${a.count} \n 짬뽕의 카운트 수: ${b.count}")
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