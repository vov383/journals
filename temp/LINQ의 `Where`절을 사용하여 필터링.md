---
title: LINQ의 `Where`절을 사용하여 필터링
created: 2025-08-20 10:15
alias:
tags:
---
LINQ의 `Where`절을 사용하면 간단히 해결할 수 있습니다. `Cast<string>()`으로 키를 문자열로 변환한 직후, `ToList()`로 리스트를 만들기 전에 `Where`를 이용해 조건을 추가하면 됩니다.

`Where`절은 주어진 조건이 참(`true`)인 요소만 남겨 필터링하는 역할을 합니다.

### **방법 1: `Where` 절을 이용한 필터링 (권장)**

이 방법은 리스트를 생성하기 전에 필터링하므로 가장 효율적입니다.

C#

```CSharp 
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;

// 예제 Hashtable 생성
Hashtable hashtable = new Hashtable();
hashtable.Add("EMP_CODE", "E123");
hashtable.Add("EMP_NAME", "Kim");
hashtable.Add("EMP_CODE_ORIGIN", "E000"); // 제외하고 싶은 키
hashtable.Add("DEPT_CODE", "D456");

// Cast<string>()와 ToList() 사이에 Where 절을 추가
List<string> keyList = hashtable.Keys
                                .Cast<string>()
                                .Where(key => key != "EMP_CODE_ORIGIN")
                                .ToList();

// 결과 확인
Console.WriteLine("'EMP_CODE_ORIGIN' 키가 제외된 리스트:");
foreach (string key in keyList)
{
    Console.WriteLine(key);
}
```

**실행 결과:**

```
'EMP_CODE_ORIGIN' 키가 제외된 리스트:
DEPT_CODE
EMP_NAME
EMP_CODE
```

---

### **방법 2: 리스트 생성 후 `Remove` 메서드 사용**

전체 키를 포함한 리스트를 먼저 만든 다음, `List<T>.Remove()` 메서드를 사용하여 특정 항목을 제거할 수도 있습니다.

C#

```CSharp 
// 먼저 모든 키를 포함한 리스트를 생성
List<string> originalKeyList = hashtable.Keys.Cast<string>().ToList();

// 그 다음, 원하지 않는 키를 제거
originalKeyList.Remove("EMP_CODE_ORIGIN");

// 결과 확인
Console.WriteLine("\n리스트 생성 후 Remove() 사용:");
foreach (string key in originalKeyList)
{
    Console.WriteLine(key);
}
```

두 방법 모두 동일한 결과를 내지만, **방법 1**이 하나의 LINQ 표현식으로 모든 작업을 처리하므로 더 간결하고 메모리 사용 측면에서도 약간 더 효율적일 수 있습니다.
