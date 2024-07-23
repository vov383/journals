---
title: C에서 Type의 프로퍼티 이름을 문자열로 얻기
created: 2024-07-23 11:14
alias:
tags:
---
주어진 코드에서 `Type`의 프로퍼티 이름을 문자열로 얻고, 이를 `AddInsertColumnValueByDn` 메서드에 전달하고자 합니다. 이를 위해 `PropertyInfo`의 `Name` 속성을 사용하여 프로퍼티 이름을 가져오면 됩니다.

다음은 수정된 코드입니다:

```csharp
using System;
using System.Linq;
using System.Reflection;
using System.Text;
using System.Collections.Generic;

public class Example
{
    public static void Main()
    {
        StringBuilder columns = new StringBuilder();
        StringBuilder values = new StringBuilder();
        Type type = typeof(DockPlanOrderDto);

        var columnStrs = type.GetProperties()
            .Where(p => p.Name != "AdditionalInfo" &&
                        p.Name != "DT_INSERT" &&
                        p.Name != "DT_UPDATE" &&
                        p.Name != "fromTable" &&
                        p.Name != "DW_SEQ")
            .Select(p => p.Name)  // Name 속성을 사용하여 프로퍼티 이름을 가져옴
            .ToArray();

        string colName = string.Empty;
        var dict = new Dictionary<string, object>();  // dict 변수 초기화 예시

        for (int i = 0; i < columnStrs.Length; i++)
        {
            colName = columnStrs[i];
            AddInsertColumnValueByDn(dict, colName, columns, values);
        }

        Console.WriteLine("Columns: " + columns.ToString());
        Console.WriteLine("Values: " + values.ToString());
    }

    public static void AddInsertColumnValueByDn(Dictionary<string, object> dict, string colName, StringBuilder columns, StringBuilder values)
    {
        if (columns.Length > 0)
        {
            columns.Append(", ");
            values.Append(", ");
        }
        
        columns.Append(colName);
        
        if (dict.ContainsKey(colName))
        {
            values.Append(dict[colName]);
        }
        else
        {
            values.Append("NULL"); // 적절한 기본 값을 설정하세요.
        }
    }
}
```

### 설명
1. `Type`의 `GetProperties()` 메서드를 사용하여 모든 프로퍼티를 가져옵니다.
2. `Where` 절을 사용하여 특정 프로퍼티를 제외합니다.
3. `Select(p => p.Name)`를 사용하여 각 프로퍼티의 이름을 가져옵니다.
4. 프로퍼티 이름을 문자열 배열 `columnStrs`에 저장합니다.
5. 각 프로퍼티 이름을 순회하면서 `AddInsertColumnValueByDn` 메서드를 호출합니다.

이렇게 하면 `Type`의 프로퍼티 이름을 문자열로 가져와 원하는 로직을 구현할 수 있습니다.

#### 요약
1. `Type`의 프로퍼티 이름을 문자열로 가져오는 방법을 설명.
2. `PropertyInfo`의 `Name` 속성을 사용하여 프로퍼티 이름을 가져옴.
3. 특정 프로퍼티를 제외하는 `Where` 절 사용.
4. 프로퍼티 이름을 문자열 배열에 저장.
5. 각 프로퍼티 이름을 순회하며 메서드 호출.


