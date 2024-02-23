---
title: MySqlDataAdapter와 MySqlDataReader의 차이점
created: 2024-02-22 01:00
alias:
tags:
---
`MySqlDataAdapter`와 `MySqlDataReader`는 
.NET 애플리케이션에서 
MySQL 데이터베이스와 상호 작용할 때 사용되는 두 가지 중요한 객체입니다. 
각각은 데이터를 읽고, 쓰고, 갱신하는 방법에서 차이점을 가지며, 
사용 사례에 따라 적합한 객체를 선택해야 합니다.

###### MySqlDataAdapter
![[MySqlDataAdapter]]

###### MySqlDataReader
![[MySqlDataReader]]

# 사용 사례에 따른 선택

- **`MySqlDataAdapter` 사용 사례**: 
	- 데이터를 메모리에 저장하고, 여러 작업(조회, 수정, 업데이트)을 한 번에 처리해야 할 때, 또는 데이터 바인딩이 필요한 경우에 적합합니다.
- **`MySqlDataReader` 사용 사례**: 
	- 대량의 데이터를 빠르게 읽어야 하고, 데이터 변경이 필요 없는 읽기 전용 액세스가 필요한 경우에 적합합니다.

데이터의 양, 애플리케이션의 성능 요구 사항, 데이터 조작의 필요성 등을 고려하여 두 객체 중 적합한 것을 선택해야 합니다.
