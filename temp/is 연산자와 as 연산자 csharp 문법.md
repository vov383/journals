---
title: is 연산자와 as 연산자 csharp 문법
created: 2024-03-12 08:55
alias:
tags:
---
```cs
if (c is ToolStrip == false) continue; ToolStrip ts = c as ToolStrip;
```
1. `if (c is ToolStrip == false) continue;`: 이 줄은 조건문입니다. 'c' 변수가 'ToolStrip' 유형이 아닌지 확인합니다. `c`가 `ToolStrip` 유형이 아닌 경우 `continue` 키워드는 루프의 현재 반복의 나머지 부분을 건너뛰는 데 사용됩니다(이 코드가 루프 내에 있다고 가정).
    
2. `ToolStrip ts = c as ToolStrip;`: 이 줄은 `as` 연산자를 사용한 유형 캐스팅의 예입니다. 변수 `c`를 `ToolStrip` 유형으로 캐스팅하려고 시도합니다. `c`가 `ToolStrip`과 호환되지 않으면 `ts` 값은 `null`이 됩니다. 그렇지 않으면 `ts`는 `c`와 동일한 개체에 대한 참조를 보유하지만 명시적으로 `ToolStrip`으로 선언된 유형을 사용합니다.
    

요약하면 이 코드는 'c'가 참조하는 개체가 'ToolStrip' 유형이 아닌지 확인합니다. 그렇지 않은 경우 루프 반복을 건너뜁니다. 그렇다면 `c`는 `ToolStrip` 유형으로 캐스팅되고 결과 개체는 `ts` 변수에 저장됩니다.

###### 유형 검사(`is` 연산자)
![[유형 검사(is 연산자)]]

###### 형 변환(`as` 연산자)
![[형 변환(as 연산자)]]


```cs
// Type checking
if (someObject is SomeType)
{
    // Type casting
    SomeType typedObject = someObject as SomeType;
    if (typedObject != null)
    {
        // You can safely use typedObject here
    }
}
```
이렇게 하면 예상된 유형의 객체에 대해서만 작업을 수행하여 잘못된 유형 가정으로 인한 런타임 오류를 방지할 수 있습니다.
