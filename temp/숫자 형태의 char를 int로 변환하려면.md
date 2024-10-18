---
title: 숫자 형태의 char를 int로 변환하려면
created: 2024-10-18 11:02
alias:
tags:
---
### C#에서 char 숫자를 int로 변환하기
###### 방법 1: 명시적 캐스팅
C#에서는 `char` 타입을 `int`로 명시적으로 캐스팅할 수 있습니다. 
숫자형 문자의 경우 아스키 값을 얻게 되므로, 숫자 값을 얻으려면 추가로 `48(숫자 0의 아스키 코드 값)`을 빼야 합니다. 

```csharp
char ch = '5';
int num = (int)ch - 48; // '5'의 아스키 값은 53이므로, 48을 빼서 5를 얻음
```

###### 방법 2: `Char.GetNumericValue()` 사용
`Char.GetNumericValue()` 메서드를 사용하면 
직접적으로 숫자 값을 가져올 수 있습니다. 
하지만 이 메서드는 반환값이 `double`이므로, 소수점을 제거하기 위해 형 변환이 필요할 수 있습니다.

```csharp
char ch = '5';
int num = (int)Char.GetNumericValue(ch); // 5를 얻음
```

###### 방법 3: `int.Parse()` 사용
문자열로 변환한 후, `int.Parse()`를 사용하는 방법도 있습니다.

```csharp
char ch = '5';
int num = int.Parse(ch.ToString()); // 5를 얻음
```

Q1 : `char` 외에도 다른 타입을 `int`로 변환할 때 주의할 점은 무엇일까요?
Q2 : 여러 개의 숫자 문자를 한꺼번에 변환해야 할 경우 어떤 방식이 효율적일까요?


