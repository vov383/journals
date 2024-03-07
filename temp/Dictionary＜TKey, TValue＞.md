---
title: Dictionary＜TKey, TValue＞
created: 2024-03-06 09:56
alias:
tags:
---
`Dictionary<TKey, TValue>` 클래스는 
키-값 쌍을 저장하는 제네릭 컬렉션입니다. 
각 키는 사전(dictionary) 내에서 유일해야 하며, 이를 통해 해당 키와 연결된 값을 빠르게 검색할 수 있습니다. 
`Dictionary<TKey, TValue>`는 내부적으로 해싱 메커니즘을 사용하여 키의 해시 코드를 계산하고, 이 해시 코드를 기반으로 데이터를 저장하고 검색합니다.

`Dictionary<TKey, TValue>`의 주요 특징
- **제네릭:** 
	- `Dictionary<TKey, TValue>`는 제네릭 컬렉션으로, 키와 값의 타입을 컴파일 시간에 지정할 수 있습니다. 
	- 이는 타입 안전성을 보장하고, 런타임 오류의 가능성을 줄여줍니다.
- **빠른 검색 속도:** 
	- 해싱을 기반으로 하므로, 키를 사용한 검색, 추가, 삭제 작업이 매우 효율적입니다. 
	- 대부분의 경우 이러한 작업은 평균적으로 O(1) 시간 복잡도를 가집니다.
- **키의 유일성:** 
	- `Dictionary<TKey, TValue>` 내에서 모든 키는 유일해야 합니다. 
	- 이미 존재하는 키로 새 값을 추가하려고 하면, `ArgumentException`이 발생합니다.
- **컬렉션 초기화:** 
	- `Dictionary<TKey, TValue>`는 컬렉션 초기화 구문을 지원하여, 선언과 동시에 초기 데이터를 할당할 수 있는 편리한 방법을 제공합니다.
- **LINQ 연산:** 
	- `Dictionary<TKey, TValue>`는 LINQ (Language Integrated Query) 연산을 지원하여, 
	- 쿼리식을 사용한 데이터 검색, 필터링, 정렬 등이 가능합니다.

`Dictionary<TKey, TValue>` 사용 예제는 다음과 같습니다:

```csharp
Dictionary<string, int> ageOfFriends = new Dictionary<string, int>();

// 키-값 쌍 추가
ageOfFriends.Add("Michael", 29);
ageOfFriends.Add("Sarah", 24);

// 키를 사용한 값 검색
int michaelAge = ageOfFriends["Michael"];

// 키-값 쌍 업데이트
ageOfFriends["Sarah"] = 25;

// 키 존재 여부 확인
bool hasMichael = ageOfFriends.ContainsKey("Michael");
```

`Dictionary<TKey, TValue>`는 타입 안전성, 빠른 성능, LINQ 연산 지원 등으로 인해 데이터를 키-값 쌍으로 관리해야 하는 다양한 상황에서 널리 사용됩니다. 

**Q3:** `Dictionary<TKey, TValue>`와 `ConcurrentDictionary<TKey, TValue>`의 차이점은 무엇인가요?


