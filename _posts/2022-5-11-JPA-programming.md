---
layout: post
title: "자바 ORM 표준 JPA 프로그래밍 - 기본편"
excerpt: ""
subtitle: "JPA"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-5-11
tags: [JPA]
---

#### Hello JPA - 프로젝트 생성

  - JPA는 특정 DB에 종속적이지 않게 설계되었음
  - 각각의 DB가 제공하는 SQL 문법과 함수는 조금씩 다름
    - MySQL은 LIMIT, Oracle은 ROWNUM 
  - 방언:SQL 표준을 지키지 않는 특정 DB만의 고유한 기능 
  - 엔티티의 생명주기
  - 영속상태: em.persist(member) DB에 저장되지는 않으며 트랜잭션 커밋 시(tx.commit())에 저장
  - 준영속: em.detach(member) 
  - 삭제: em.remove(member)


#### EntityManager(영속성 컨텍스트)의 이점

  - 1차 캐시
  - identity 동일성 보장
  - 트랜잭션을 지원하는 쓰기 지연
  - 변경 감지 dirty checking
  - 지연 로딩 lazy loading것

#### 엔티티 조회 

  - 1차 캐시(영속성 컨텍스트라고 생각할 )에 저장 

```kotlin
  try {
    // 비영속
    Member member = new Member();
    member.setId(100L);
    member.setName("HelloJPA");
    // 영속
    em.persist(member)
    // 엔티티 삭제
    em.remove(member)
  } catch (Exception e) {
    tx.rollback();
  } finally {
    tx.commit()    
  }
```
  - 영속 엔티티의 동일성 보장: 1차 캐시로 반복 가능한 읽기 등급의 트랜잭션 격리 수준을 DB가 아닌 application 차원에서 제공
  - 쓰기 지연 SQL 저장소
  - jdbc.batch: 버퍼링 기능, commit을 모아서 한번에 push 하는 기능? 
  - dirty checking (변경 감지): 굳이 db에 update 쿼리를 안날리고 값만 변경해도 알아서 저장해주는 기능
    - flush(): 영속성 컨텍스트의 변경 내용을 db에 반영
    - 엔티티와 스냅샷 비교
    - Update sql 생성
    - flush
    - commit

#### 플러시
  
  - flush: 영속성 컨텍스트의 변경 내용을 db에 반영
  - 영속성 컨텍스를 비우지 않음
  - 영속성 컨텍스트를 플러시하는 방법
    - em.flush()
    - em.commit()
    - JPQL 쿼리실행 

  