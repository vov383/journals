---
title: MySqlDataAdapter
created: 2024-02-22 01:00
alias:
tags:
---
- **Disconnected 모드**: 
	- `MySqlDataAdapter`는 Disconnected 모드에서 작동합니다. 
	- 이는 데이터베이스와의 연결을 유지하지 않고, 데이터를 `DataSet` 또는 `DataTable` 객체에 채운 후 연결을 바로 닫습니다. 
	- 이 방식은 데이터를 메모리에 저장하므로, 데이터베이스 연결이 끊긴 상태에서도 데이터를 조작하고, 나중에 변경사항을 데이터베이스에 일괄적으로 업데이트할 수 있습니다.
- **데이터 바인딩**: 
	- `MySqlDataAdapter`는 데이터 바인딩을 용이하게 합니다. 
	- 예를 들어, 윈폼이나 WPF 애플리케이션에서 데이터 그리드와 같은 컨트롤에 데이터를 쉽게 바인딩할 수 있습니다.
- **CRUD 작업**: 
	- `MySqlDataAdapter`를 사용하면, `DataSet`에 대한 CRUD(Create, Read, Update, Delete) 작업을 수행한 후, 
	- 이를 데이터베이스에 동기화할 수 있습니다.

###### MySqlDataAdapter() 생성자 오버로드
![[MySqlDataAdapter() 생성자 오버로드]]

[[MySqlDataAdapter와 MySqlDataReader의 차이점]]