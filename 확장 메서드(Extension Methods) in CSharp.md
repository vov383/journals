---
title: 확장 메서드(Extension Methods) in CSharp
created: 2024-05-Su 14:43:05
aliases: 
tags: [CSharp]
---
###### 확장 메서드 개요
기존 형식에 새로운 메서드를 추가하는 방법을 제공하는 
C# 기능입니다. 
원래 소스를 수정하지 않고도 
기존 클래스, 구조체 또는 인터페이스에 
메서드를 추가할 수 있습니다. 
이를 통해 코드의 가독성을 높이고, 
재사용성을 증대시킬 수 있습니다.

###### 확장 메서드 정의
확장 메서드는 정적 클래스 내에 정적 메서드로 정의됩니다. 
첫 번째 매개변수는 `this` 키워드를 사용하여 
확장할 **형식**을 지정합니다.

###### 확장 메서드 작성 예제
```csharp
using System;
using System.Collections;
using System.Collections.Generic;

public static class HashtableExtensions
{
    public static Dictionary<string, object> ConvertHt2Enumerable(this Hashtable hashtable)
    {
        Dictionary<string, object> dictionary = new Dictionary<string, object>();

        foreach (DictionaryEntry entry in hashtable)
        {
            if (entry.Key is string key)
            {
                dictionary.Add(key, entry.Value);
            }
        }

        return dictionary;
    }
}
```

##### 예제 설명
###### 정적 클래스
확장 메서드는 정적 클래스(`static class`) 내에 정의됩니다.
###### 정적 메서드
확장 메서드는 정적 메서드(`static method`)로 정의됩니다.
###### this 키워드
확장 메서드의 첫 번째 매개변수는 `this` 키워드를 사용하여 
확장할 형식을 지정합니다.

###### 확장 메서드 사용
확장 메서드를 사용하려면 해당 네임스페이스를 포함해야 합니다.

###### 확장 메서드 사용 예제
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

        // 확장 메서드를 사용하여 Hashtable을 Dictionary로 변환
        Dictionary<string, object> dictionary = hashtable.ConvertHt2Enumerable();

        // LINQ 쿼리 사용
        var query = dictionary.Where(kv => (int)kv.Value > 2)
                              .Select(kv => kv.Key);

        // 결과 출력
        foreach (var key in query)
        {
            Console.WriteLine(key);
        }
    }
}
```

##### 예제 설명
###### Hashtable 생성
네 개의 항목이 있는 `Hashtable`을 생성합니다.
###### 확장 메서드 사용
`ConvertHt2Enumerable` 확장 메서드를 사용하여 
`Hashtable`을 `Dictionary<string, object>`로 변환합니다.
###### LINQ 쿼리 사용
변환된 `Dictionary`에서 값이 2보다 큰 항목의 키를 선택하는 
LINQ 쿼리를 작성합니다.
###### 결과 출력
쿼리 결과를 출력합니다.

Q1 :
다른 컬렉션 형식에 확장 메서드를 추가할 때 고려해야 할 점은 무엇인가요?

Q2 :
확장 메서드를 사용하여 기존 형식의 기능을 확장할 때 주의해야 할 사항은 무엇인가요?

##### 요약
###### 확장 메서드 개요
###### 확장 메서드 정의
###### 확장 메서드 작성 예제
###### 예제 설명
###### 확장 메서드 사용 예제
###### 다른 컬렉션 형식에 확장 메서드를 추가할 때 고려할 점
###### 확장 메서드를 사용할 때 주의할 사항