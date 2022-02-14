---
layout: post
title: "📅 Kotlin 강의노트 - 20강까지"
excerpt: "디모의 Kotlin 강좌 요약본입니다 "
subtitle: "Kotlin youtube lecture"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-2-8
tags: [Kotlin]
---


    





#### 리스트

- List: 데이터를 코드에서 지정한 순서대로 저장해두는 클래스. 데이터를 모아 관리하는 컬렉션 클래스의 서브 클래스 중 가장 단순한 형태. 
- 리스트의 2가지 형태  
List<out T>: 생성 시에 넣은 객체를 대체, 추가, 삭제 할 수 없음
MutableList<T>: 가능

```kotlin
fun main() {
	val family = listOf("사샤", "리사", "코코")

	println(a) // [사샤, 리사, 코코]

	for(ele in family)
	{
		println("${family}")
	}

	val b = mutableListOf(1, 2, 3)
	b.add(3, 5) // add(삽입하고자 하는 idx, value)
	println(b) // [1, 2, 3, 5]

	b.removeAt(3)
	println(b) // [1, 2, 3]

	b.shuffle()
	println(b) // 랜덤한 값이 반화

	b.sort()
	println(b) // [1, 2, 3]
}
```

#### 문자열을 다루는 법

- 








