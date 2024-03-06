---
title: HashTable 클래스
created: 2024-03-06 09:04
alias: 
tags: 
---
키의 해시 코드에 따라 구성된 키/값 쌍의 컬렉션을 나타냅니다.
`HashTable` 클래스는 C#에서 키-값 쌍(key-value pairs)을 저장하는 데 사용되는 컬렉션입니다. 
각 키는 해시 테이블 내에서 유일하며, 이를 통해 해당 키에 연결된 값을 빠르게 검색할 수 있습니다. 
`HashTable`은 내부적으로 해싱 메커니즘을 사용하여 키의 해시 코드를 계산하고, 이 해시 코드를 기반으로 키-값 쌍을 저장합니다.

###### `HashTable`의 주요 특징
![[journals/temp/`HashTable`의 주요 특징]]

`List<HashTable>`는 `HashTable` 객체들의 리스트를 나타냅니다. 이를 통해 여러 해시 테이블을 순차적으로 관리할 수 있으며, 각 해시 테이블은 독립적인 키-값 쌍의 집합을 포함할 수 있습니다.

###### `HashTable`과 `DictionaryTKey, TValue` 비교
![[HashTable과 Dictionary＜TKey, TValue 비교＞]]

###### Dictionary＜TKey, TValue＞
![[journals/temp/Dictionary＜TKey, TValue＞]]
