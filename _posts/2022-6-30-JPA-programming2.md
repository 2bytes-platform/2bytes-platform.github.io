---
layout: post
title: "자바 ORM 표준 JPA 프로그래밍 - 기본편"
excerpt: "자바 ORM 표준 JPA 프로그래밍 강의노트 요약입니다."
subtitle: "JPA"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-6-30
tags: [JPA]
---
### 다양한 연관관계 맵핑

- 연관관계 맵핑 시 고려할 사항
  - 다중성: @ManyToOne, @OneToMany, @OneToOne, @ManyToMany (거의 안쓰임)
  - 단방향, 양방향
  - 연관관계의 주인
    - 객체의 양방향 관계는 A->B, B->A처럼 참조가 2군데이며, 둘 중 테이블의 외래 키를 관리할 곳을 지정
    - 외래 키를 관리하는 참조가 연관관계의 주, 주인의 반대편은 읽기만 가능

#### N:1 [일대일]

- 


#### 1:N [일대다]

- 단방향
  - 엔티티가 관리하는 외래키가 다른 테이블에 있음
  - 연관관계 관리를 위해 추가로 UPDATE SQL 실행
  - 일대다 단방향 맵핑은 지양하고 **다대일 양방향**을 지향

- 양방향
  - 공식적으로 존재 X
  - @JoinColumn(insertable=false, updatable=false)
  - 읽기 전용 필드를 사용해서 양방향 처럼 사용하는 얍삽이 방법 존재
  

