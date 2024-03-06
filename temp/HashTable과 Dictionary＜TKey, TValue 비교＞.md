---
title: HashTable`과 `DictionaryTKey, TValue 비교
created: 2024-03-06 09:05
alias:
tags:
---
`HashTable`과 `Dictionary<TKey, TValue>`는 C#에서 키-값 쌍을 저장하는 데 사용되는 컬렉션 유형입니다. 그러나 두 컬렉션 사이에는 몇 가지 주요 차이점이 있습니다:

1. **타입 안전성(Type Safety):**
   - `HashTable`은 비제네릭 컬렉션으로, 키와 값으로 모든 타입의 객체를 사용할 수 있습니다. 이는 타입 캐스팅 오류가 런타임에만 발견될 수 있음을 의미합니다.
   - `Dictionary<TKey, TValue>`는 제네릭 컬렉션으로, 컴파일 타임에 타입 안전성을 제공합니다. 즉, 키와 값의 타입을 명시적으로 지정해야 하며, 이는 타입 관련 오류를 더 일찍, 즉 컴파일 시점에 발견할 수 있게 해줍니다.

2. **성능:**
   - `Dictionary<TKey, TValue>`는 `HashTable`에 비해 약간 더 나은 성능을 제공하는 경향이 있습니다, 특히 타입 안전성으로 인해 발생하는 오버헤드가 없기 때문입니다.

3. **버전 호환성:**
   - `HashTable`은 .NET의 초기 버전부터 제공되어 왔습니다.
   - `Dictionary<TKey, TValue>`는 .NET 2.0부터 도입된 제네릭 컬렉션의 일부입니다.

4. **스레드 안전:**
   - 기본적으로 `HashTable`과 `Dictionary<TKey, TValue>` 모두 스레드 안전하지 않습니다. 그러나 `HashTable`은 `System.Collections` 네임스페이스에 있는 `Synchronized` 메서드를 통해 스레드 안전한 래퍼를 생성할 수 있습니다.
   - `Dictionary<TKey, TValue>`는 멀티 스레드 환경에서의 사용을 위해 `System.Collections.Concurrent` 네임스페이스 아래에 있는 `ConcurrentDictionary<TKey, TValue>`와 같은 스레드 안전한 대안을 사용하는 것이 권장됩니다.

5. **사용 용도:**
   - 타입 안전이 중요하고 .NET 2.0 이상을 대상으로 하는 경우 `Dictionary<TKey, TValue>`의 사용이 권장됩니다.
   - 구형 시스템이나 기존 코드와의 호환성이 필요한 경우에는 `HashTable`을 사용할 수 있습니다.

`Dictionary<TKey, TValue>`를 사용하면 컴파일 시간에 타입 체크를 할 수 있어 더 안전하고, 성능 면에서도 약간의 이점이 있어 대부분의 새로운 개발에서 선호됩니다.