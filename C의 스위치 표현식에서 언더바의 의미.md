---
title: C의 스위치 표현식에서 언더바의 의미
created: 2024-05-Su 14:41:35
aliases: 
tags:
---
c# 버전 8.0부터 사용가능한 표현
그 아래는 일반적인 스위치문에 default 쓰면 된다.

###### 언더바의 역할
언더바(`_`)는 C#의 스위치 표현식에서 **디폴트 매칭 패턴**으로 사용됩니다.
이는 이전의 모든 경우에 매칭되지 않는 
나머지 모든 값들을 처리하기 위해 사용됩니다. 
다른 언어에서의 `default` 케이스와 유사합니다.

###### 스위치 표현식 예제
`_`를 사용한 스위치 표현식의 예제를 다시 설명하겠습니다.
```csharp
public static IButtonState GetButtonState(ButtonState state)
{
    return state switch
    {
        ButtonState.UnloadPlanOn => new UnloadPlanOnState(),
        ButtonState.UnloadPlanOff => new UnloadPlanOffState(),
        ButtonState.BerthShiftOn => new BerthShiftOnState(),
        ButtonState.BerthShiftOff => new BerthShiftOffState(),
        ButtonState.LockOn => new LockOnState(),
        ButtonState.LockOff => new LockOffState(),
        _ => throw new ArgumentException("Invalid state"), // 나머지 모든 경우를 처리
    };
}
```

###### 예제 설명
- **`ButtonState.UnloadPlanOn => new UnloadPlanOnState()`**: `state`가 `ButtonState.UnloadPlanOn`인 경우, `UnloadPlanOnState` 객체를 반환합니다.
- **`_ => throw new ArgumentException("Invalid state")`**: `state`가 이전에 정의된 어떤 경우에도 해당하지 않으면, 예외를 던집니다.

###### 스위치 표현식의 장점
- **간결성**: 기존의 `switch` 구문보다 코드가 더 간결하고 읽기 쉽습니다.
- **패턴 매칭**: 다양한 패턴 매칭을 지원하여 복잡한 조건도 간단하게 표현할 수 있습니다.
- **컴파일러 경고**: 모든 경우를 처리하지 않으면 컴파일러가 경고를 발생시켜 놓치는 경우를 방지합니다.

###### `_`의 다른 사용 예시
언더바(`_`)는 다른 상황에서도 다양한 용도로 사용됩니다:
- **디스크카드**: 값을 무시할 때 사용합니다.
  ```csharp
  var (_, _, lastName) = GetNameParts(); // firstName과 middleName을 무시
  ```
- **명명 규칙**: 특별한 의미 없이 변수명을 강조하거나 구분할 때 사용합니다.
  ```csharp
  int _unusedVariable = 42;
  ```

Q1 :
C#의 스위치 표현식에서 언더바(`_`) 외에 다른 패턴 매칭 방법은 무엇이 있나요?

Q2 :
언더바(`_`)를 디스크카드로 사용할 때의 주의사항은 무엇인가요?

#### 요약
###### 언더바(`_`)의 역할
###### 스위치 표현식 예제
###### 예제 설명
###### 스위치 표현식의 장점
###### `_`의 다른 사용 예시
###### C#의 패턴 매칭 기능 소개
###### 디스크카드 사용 시 주의사항