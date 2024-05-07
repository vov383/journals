---
title: IDictionary의 foreach 이슈
created: 2024-05-07 08:57
alias:
tags:
---
`IDictionary`를 `foreach`로 순회할 때 `KeyValuePair<string, object>`로의 타입 캐스팅 문제가 발생하는 이유는 
`IDictionary` 인터페이스가 `DictionaryEntry` 객체를 반환하기 때문입니다. 
따라서, 각 아이템을 `KeyValuePair<string, object>` 대신 `DictionaryEntry`로 캐스팅해야 합니다. 
`DictionaryEntry`는 `Key`와 `Value` 프로퍼티를 제공하여 각 키-값 쌍에 접근할 수 있습니다.



#### `foreach` 루프에서 `IDictionary`의 아이템을 효율적으로 처리하는 다른 방법
`IDictionary`를 순회할 때는 
`foreach` 루프 내에서 `DictionaryEntry` 대신 
일반적인 `KeyValuePair<TKey, TValue>` 구조를 사용하려면, 
`IDictionary`를 `IDictionary<TKey, TValue>`로 캐스팅하고 
이를 순회하는 것이 한 가지 방법입니다. 
이렇게 하면 각 항목을 `KeyValuePair`로 바로 접근할 수 있어 
코드의 가독성과 작성의 편리성이 증가합니다.

#### `KeyValuePair`와 `DictionaryEntry`의 주요 차이점
`KeyValuePair<TKey, TValue>`는 제네릭 컬렉션에서 사용되며, 
타입 안전성과 성능 이점을 제공합니다. 
반면, `DictionaryEntry`는 비제네릭 `IDictionary`에서 사용되며, 
강제 캐스팅이 필요할 수 있습니다. 
`KeyValuePair`는 타입이 명확한 경우에 사용하고, 
`DictionaryEntry`는 구형 코드나 타입 정보가 불분명할 때 
사용하는 것이 좋습니다.

딕셔너리 엔트리를 잘 써야할듯

KeyValuePair와 딕셔너리엔트리의 주요 차이점에 대해 알면 좋을듯


