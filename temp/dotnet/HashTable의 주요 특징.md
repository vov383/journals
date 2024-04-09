---
title: HashTable의 주요 특징
created: 2024-03-06 09:04
alias:
tags:
---
- **빠른 검색 속도
	- 키를 통해 값을 검색하는 과정이 매우 빠르다는 것입니다. 
	- 해시 함수를 사용하여 키의 저장 위치를 계산하기 때문에,
	- 평균적으로 O(1) 시간 복잡도에서 검색 작업을 수행할 수 있습니다.
- **키의 유일성
	- 각 키는 해시 테이블 내에서 유일해야 합니다. 
	- 같은 키로 여러 값을 저장하려고 하면, 
	- 마지막에 저장된 값으로 기존 값을 덮어씁니다.
- **동적 크기 조정
	- `HashTable`은 요소가 추가될 때 
	- 내부 배열의 크기를 자동으로 조정할 수 있습니다. 
	- 이는 저장 공간을 효율적으로 관리할 수 있게 해줍니다.
- **키 및 값의 다양성
	- `HashTable`은 다양한 타입의 키와 값에 대해 
	- 유연하게 사용될 수 있습니다. 
	- 즉, 키와 값으로 어떤 타입의 객체도 사용할 수 있습니다.

그러나 `HashTable`은 단일 스레드 환경에서 주로 사용되며, 
멀티 스레드 환경에서는 
`System.Collections.Concurrent` 네임스페이스 아래 있는 
스레드 안전한 컬렉션을 사용하는 것이 권장됩니다. 
또한, .NET 2.0 이상에서는 
`Dictionary<TKey, TValue>` 클래스가
`HashTable`에 비해 타입 안전성 및 성능 면에서 더 나은 대안으로 제시되고 있습니다.

[[../Dictionary＜TKey, TValue＞|Dictionary＜TKey, TValue＞]]

[[../HashTable과 Dictionary＜TKey, TValue 비교＞|HashTable과 Dictionary＜TKey, TValue 비교＞]]




