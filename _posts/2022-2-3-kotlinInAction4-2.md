---
layout: post
title: "📅 Kotlin in Action - 4장 클래스, 객체, 인터페이스"
excerpt: "Kotlin in Action 4장 요약 노트입니다."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-2-3
tags: [Kotlin]
---

#### 4.2.4 게터와 세터에서 뒷받침하는 필드에 접근 

- 특정 값을 저장하되 그 값을 변경하거나 읽을 때마다 정해진 로직을 실행하는 유형의 프로퍼티를 생성

```kotlin
fun main() {
    val user = User("Alitciia")
    user.address = "서울시 송파구 토성로 15길 10-1 바움빌 401호" 
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