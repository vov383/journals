---
title: Unity Script의 헤더 기능
created: 2024-12-12 04:47
alias:
tags:
---
`[Header("string")]`

#### **기능**

`[Header("string")]`는 Unity Editor의 Inspector에서 변수를 그룹화하거나 설명을 추가하는 데 사용됩니다. 이 속성은 변수의 **위에 표시되는 텍스트 라벨**로 작동하여 가독성을 높입니다.

#### **사용 예**

```csharp
using UnityEngine;

public class Example : MonoBehaviour
{
    [Header("Player Settings")]
    public float speed = 5.0f;

    [Header("Enemy Settings")]
    public int enemyCount = 10;
}
```

#### **결과**

- Inspector에서 `speed` 위에 **"Player Settings"** 텍스트가 표시됩니다.
- `enemyCount` 위에 **"Enemy Settings"** 텍스트가 표시됩니다.
- 이를 통해 변수들을 **카테고리별로 구분**하여 관리하기 쉽습니다.


