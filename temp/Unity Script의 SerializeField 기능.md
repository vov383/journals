---
title: Unity Script의 SerializeField 기능
created: 2024-12-12 04:47
alias:
tags:
---
### `[SerializeField]` 

#### **기능**

`[SerializeField]`는 **비공개(`private`) 변수**를 Unity Editor의 Inspector에 표시할 수 있게 합니다. Unity는 기본적으로 `public` 변수만 Inspector에 표시하지만, `[SerializeField]`를 사용하면 **캡슐화**를 유지하면서도 변수 값을 Inspector에서 설정할 수 있습니다.

#### **사용 예**

```csharp
using UnityEngine;

public class Example : MonoBehaviour
{
    [SerializeField]
    private int health = 100;

    [SerializeField]
    private string playerName = "Hero";
}
```

#### **결과**

- `health`와 `playerName`은 `private`이지만, **Inspector에서 값을 설정**할 수 있습니다.
- 캡슐화를 유지하므로 외부 클래스에서 직접 접근은 불가능합니다.
- Inspector에서 값을 설정한 뒤, 스크립트에서 이를 참조하여 사용 가능합니다.



헤더와 SerializeField를 함께 사용하면
두 속성을 조합하여 사용하면 Inspector를 더 구조적으로 정리할 수 있습니다.

#### **예시**

```csharp
using UnityEngine;

public class Example : MonoBehaviour
{
    [Header("Player Stats")]
    [SerializeField] private int health = 100;
    [SerializeField] private float speed = 5.0f;

    [Header("Weapon Settings")]
    [SerializeField] private string weaponName = "Sword";
    [SerializeField] private int damage = 50;
}
```

#### **결과**

- **"Player Stats"**와 **"Weapon Settings"**로 카테고리화하여 관리가 더 편리합니다.
- `health`, `speed`, `weaponName`, `damage` 변수는 **private**이지만, Inspector에서 값을 설정할 수 있습니다.


### 요약

1. `[Header("string")]`은 Inspector에서 가독성을 높이기 위한 **라벨**을 추가합니다.
2. `[SerializeField]`는 `private` 변수도 Inspector에서 설정할 수 있도록 만듭니다.
3. 두 속성을 함께 사용하면 Inspector를 **깔끔하고 체계적으로** 구성할 수 있습니다.


Q1: Inspector의 구조를 더 효율적으로 관리하기 위해 어떤 속성을 추가로 사용할 수 있을까요?  
Q2: `[SerializeField]`를 활용하여 캡슐화를 유지하면서 데이터를 유효성 검사하는 방법은 무엇일까요?