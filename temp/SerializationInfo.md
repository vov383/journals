---
title: SerializationInfo
created: 2024-03-29 12:25
alias:
tags:
---
`SerializationInfo`는 
.NET 프레임워크에서 객체의 직렬화와 역직렬화 과정에서 
객체의 상태를 저장하고, 복원하기 위해 사용되는 클래스입니다. 
직렬화란, 객체의 상태를 저장하거나 전송 가능한 형태
(예: 바이트 스트림)로 변환하는 과정을 말하며, 
역직렬화는 이러한 데이터 스트림을 다시 객체로 복원하는 과정을 의미합니다.

###### SerializationInfo의 기본 개념
![[journals/temp/SerializationInfo의 기본 개념]]


###### SerializationInfo의 사용 방법 예시
![[journals/temp/SerializationInfo의 사용 방법 예시]]

#### 요약
###### SerializationInfo 개념
객체의 상태를 키-값 쌍으로 저장하여 
직렬화와 역직렬화를 지원하는 .NET 클래스입니다.
###### 기능과 이점
객체의 상태를 안전하게 저장하고 복원할 수 있으며, 
객체의 버전 관리와 호환성 유지에 유용합니다.
###### 사용법 
`ISerializable` 인터페이스를 구현하여 
객체의 상태를 `SerializationInfo`에 저장하고, 
역직렬화 시 이 정보를 사용하여 객체를 복원합니다.

이 개념은 데이터를 안전하게 저장하고, 
네트워크를 통해 전송하거나, 
파일 시스템에 저장할 때 중요합니다. 
또한, 애플리케이션의 다양한 버전 간의 호환성을 유지하는 데에도 필수적인 역할을 합니다.
