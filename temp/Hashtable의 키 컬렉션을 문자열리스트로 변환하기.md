---
title: Hashtable의 키 컬렉션을 문자열리스트로 변환하기
created: 2025-08-20 10:13
alias:
tags:
---
`Hashtable`의 키 컬렉션을 LINQ를 사용하여 간단하게 `string[]` 또는 `List<string>`으로 변환할 수 있습니다. 
`Hashtable.Keys`는 `object` 타입의 컬렉션을 반환하므로, 각 요소를 `string`으로 캐스팅하는 과정이 필요합니다.

### LINQ를 이용한 변환 (권장)
#### Cast 사용
- `Cast<string>()`: `IEnumerable` 컬렉션의 각 요소를 `string` 타입으로 변환합니다. 
- 만약 컬렉션에 `string`이 아닌 타입이 포함되어 있다면 예외가 발생합니다.
    
- `ToArray()` / `ToList()`: 변환된 `IEnumerable<string>`을 각각 배열이나 리스트로 만듭니다.
    

C#
```CSharp 
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;

// 예제 Hashtable 생성
Hashtable hashtable = new Hashtable();
hashtable.Add("key1", "value1");
hashtable.Add("key2", "value2");
hashtable.Add("key3", "value3");

// 1. List<string>으로 변환
List<string> keyList = hashtable.Keys.Cast<string>().ToList();

// 2. string[] (문자열 배열)으로 변환
string[] keyArray = hashtable.Keys.Cast<string>().ToArray();

// 결과 확인
Console.WriteLine("List<string>:");
foreach (string key in keyList)
{
    Console.WriteLine(key);
}

Console.WriteLine("\nstring[]:");
foreach (string key in keyArray)
{
    Console.WriteLine(key);
}
```


### 다른 변환 방법

LINQ를 사용하지 않는 다른 접근 방식

#### 1. `ICollection.CopyTo` 메서드 사용

`Hashtable.Keys`가 구현하는 `ICollection` 인터페이스의 `CopyTo` 메서드를 사용하면 컬렉션의 요소를 기존 배열에 복사할 수 있습니다. 
이 방법은 배열을 생성할 때 가장 직접적이고 효율적일 수 있습니다.

C#

```CSharp 
// string 배열을 미리 생성
string[] keyArrayFromCopyTo = new string[hashtable.Count];

// Keys 컬렉션의 내용을 배열로 복사
hashtable.Keys.CopyTo(keyArrayFromCopyTo, 0);

// 결과 확인
Console.WriteLine("\nstring[] from CopyTo:");
foreach (string key in keyArrayFromCopyTo)
{
    Console.WriteLine(key);
}
```


### 제언

새로 작성하는 코드라면 `Hashtable` 대신 제네릭(Generic) 컬렉션인 `Dictionary<TKey, TValue>` 사용을 고려하는 것이 좋습니다.

`Dictionary<string, TValue>`를 사용하면 키가 컴파일 시점에 `string` 타입임이 보장되므로, 런타임에 별도의 캐스팅 과정 없이 `Keys` 프로퍼티(`ICollection<string>`)를 바로 `ToList()`나 `ToArray()`로 변환할 수 있어 더 안전하고 효율적입니다.

C#

```CSharp 
// Dictionary 사용 예
Dictionary<string, string> dictionary = new Dictionary<string, string>();
dictionary.Add("key1", "value1");
dictionary.Add("key2", "value2");

// 캐스팅 없이 바로 변환 가능
List<string> keyListFromDict = dictionary.Keys.ToList();
string[] keyArrayFromDict = dictionary.Keys.ToArray();
```
