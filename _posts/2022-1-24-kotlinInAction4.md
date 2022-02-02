---
layout: post
title: "📅 Kotlin in Action - 4장 함수 정의와 호출"
excerpt: "Kotlin in Action 4장 요약 노트입니다."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-1-24
tags: [Kotlin]
---

### 4.1 클래스 계층 정의 

#### 4.1.1 코틀린 인터페이스

- 코틀린 인터페이스 안에는 추상 메서드 뿐만 아니라 구현이 있는 메서드도 정의 가능 
- override 변경자는 실수로 상위 클래스의 메서드를 오버라이드 하는 것을 방지
- 상위 타입의 이름을 꺽쇠 괄호 사이에 넣어서 super를 지정하면, 어떤 상위 타입의 멤버 메서드를 호출할지 지정 가능

```kotlin
fun main(args: Array<String>) {
	val button = Button()
    button.showOff() //  I'm clickable! I'm Focusable!
    button.setFocus(true) // I got focus.
    button.click() // I was clicked!
}

interface Clickable {
	fun click() // 일반 메서드 선언
	fun showOff() = println("I'm clickable!") // 디폴트 구현이 있는 메서드
}

interface Focusable {
	fun setFocus(b: Boolean) = println("I ${if (b) "got" else "lost"} focus.")
	fun showOff() = println("I'm Focusable!")
}


class Button: Clickable, Focusable {
	override fun click() = println("I was clicked!")
	override fun showOff(){ 
		super<Clickable>.showOff()
		super<Focusable>.showOff() // 
	}
}
```

#### 4.1.2 open, final, abstract 변경자: 기본적으로 final

- 하위 클래스에서 오버라이드하게 의도된 클래스와 메서드가 아니라면 기본적으로 final class로 만들 것

```kotlin
open class RichButton: Clickable { // 다른 클래스가 상속 가능하도록 열려있음
  	fun disable() {} // 하위 클래스에서 오버라이드 불가 
    open fun animate() {} // 하위 클래스에서 오버라이드 가능 
    override fun click() {} // 상위 클래스 메서드를 오버라이드
}
```

| 변경자      | 오버라이드 가능 유무             |               설명                |
|------------|:------------------------|:-------------------------------:|
| `final`    | 오버라이드 할 수 없음            |         클래스 멤버의 기본 변경자          |
| `open`     | 오버라이드 할 수 있음            |     반드시 open을 명시해야 오버라이드 가능     | 
| `abstract` | 반드시 오버라이드               | 추상 클래스의 멤버에만 사용 가능. 추상 멤버에는 구현X | 
| `override` | 상위 클래스나 인스턴스의 멤버를 오버라이드 |     오버라이드하는 멤버는 기본적으로 열려있음      | 

#### 4.1.3 가시성 변경자: 기본적으로 공개

- 코드 기반에 있는 선언에 대한 클래스 외부 접근을 제어


#### 4.1.4 내부 클래스와 중첩된 클래스: 기본적으로 중첩 클래스