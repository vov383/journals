---
title: yield in CSharp
created: 2024-05-Su 14:45:44
aliases: 
tags:
---
###### `yield` 키워드 개요
`yield` 키워드는 
C#에서 반복자(iterator) 메서드를 쉽게 구현할 수 있게 하는 키워드입니다. 
반복자 메서드는 
컬렉션의 요소를 하나씩 반환하는 방법을 제공하며, 
이 과정에서 상태를 유지하여 다음 요소를 반환할 준비를 합니다.

###### `yield return`의 의미
호출자에게 값을 하나씩 반환합니다. 
이 키워드를 사용하면 메서드가 일시 중지되고, 
다음에 호출될 때 중지된 위치에서 다시 시작됩니다.

###### `yield break`의 의미
반복을 종료합니다. 이는 반복자를 종료하고, 
더 이상 요소를 반환하지 않게 합니다.

###### 확장 메서드 예제
`Hashtable`을 `IEnumerable<KeyValuePair<object, object>>`로 변환하는 확장 메서드를 예제로 설명하겠습니다.

###### 확장 메서드 구현
```csharp
using System.Collections;
using System.Collections.Generic;

public static class HashtableExtensions
{
    public static IEnumerable<KeyValuePair<object, object>> AsEnumerable(this Hashtable table)
    {
        foreach (DictionaryEntry entry in table)
        {
            yield return new KeyValuePair<object, object>(entry.Key, entry.Value);
        }
    }
}
```

##### 예제 설명
###### IEnumerable<KeyValuePair<object, object>>
확장 메서드의 반환 타입으로, LINQ 쿼리를 사용할 수 있는 컬렉션 타입입니다.
###### foreach (DictionaryEntry entry in table)
`Hashtable`의 모든 항목을 반복합니다.
###### yield return new KeyValuePair<object, object>(entry.Key, entry.Value;
각 항목을 `KeyValuePair<object, object>`로 변환하여 
호출자에게 반환합니다.

###### 예제 코드
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        // Hashtable 생성
        Hashtable hashtable = new Hashtable
        {
            { "One", 1 },
            { "Two", 2 },
            { "Three", 3 },
            { "Four", 4 }
        };

        // Hashtable을 AsEnumerable로 변환하여 LINQ 사용
        var query = hashtable.AsEnumerable()
                             .Where(kv => (int)kv.Value > 2)
                             .Select(kv => kv.Key);

        // 결과 출력
        foreach (var key in query)
        {
            Console.WriteLine(key);
        }
    }
}
```

###### 예제 설명
1. **`Hashtable` 생성**: 네 개의 항목이 있는 `Hashtable`을 생성합니다.
2. **`AsEnumerable` 확장 메서드 사용**: `Hashtable`을 `IEnumerable<KeyValuePair<object, object>>`로 변환합니다.
3. **LINQ 쿼리 사용**: 변환된 컬렉션에서 값이 2보다 큰 항목의 키를 선택하는 LINQ 쿼리를 작성합니다.
4. **결과 출력**: 쿼리 결과를 출력합니다.

Q1 :
`yield` 키워드를 사용하는 반복자 메서드의 장점은 무엇인가요?

Q2 :
`yield return`과 `yield break`를 함께 사용하여 복잡한 반복자를 구현하는 방법은 무엇인가요?

###### `yield` 키워드 개요
###### `yield return`의 의미
###### `yield break`의 의미
###### 확장 메서드 구현
###### 예제 설명
###### 반복자 메서드의 장점
###### 복잡한 반복자 구현 방법