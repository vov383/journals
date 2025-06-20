---
title: CompareTo() in CSharp
created: 2025-06-18 04:14
alias:
tags:
---
정렬 가능한 값을 비교하는 메서드
`.CompareTo()`는 **정렬 가능한 값(예: 숫자, 문자열, 날짜 등)** 간의 **대소 비교**를 위해 사용되는 대표적인 메서드입니다. 
특히 **문자열 비교 시 정렬 순서대로 비교 가능**하기 때문에 
날짜 문자열 비교 외에도 다양한 곳에 유용하게 쓰입니다.

### 기본 구조

```csharp
int result = a.CompareTo(b);
```

### 반환 값 의미

- `result < 0` → a가 b보다 작음
- `result == 0` → a와 b가 같음
- `result > 0` → a가 b보다 큼
    

### 문자열에서의 비교

C#의 문자열은 기본적으로 **사전 순(Lexicographical Order)** 으로 비교됩니다. 예:

```csharp
"apple".CompareTo("banana");   // -1 → apple이 더 앞
"banana".CompareTo("apple");   //  1 → banana가 더 뒤
"cherry".CompareTo("cherry");  //  0 → 동일
```

**주의**: 대소문자 구분이 있음

```csharp
"Apple".CompareTo("apple");    // -1 → 대문자 A가 소문자 a보다 앞
```

→ 대소문자 무시하려면 `StringComparer.OrdinalIgnoreCase` 등 사용


### 날짜 형식 문자열 비교

날짜를 `yyyyMMddHHmm` 또는 `yyyy-MM-dd_HH:mm`처럼 **정렬 가능한 포맷**으로 문자열화해 놓으면 `.CompareTo()`로 대소 비교가 정확히 동작합니다.

```csharp
"20250618_1000".CompareTo("20250618_0900"); // 1 → 10:00이 더 늦음
"20250617".CompareTo("20250618"); // -1 → 더 이전 날짜
```

### 응용 예시

1. **범위 체크**

```csharp
if (target.CompareTo(rangeStart) >= 0 && target.CompareTo(rangeEnd) <= 0)
{
    // target은 범위 안에 있음
}
```

2. **정렬에 사용**

```csharp
list.Sort((a, b) => a.CompareTo(b));
```

3. **조건 분기**

```csharp
switch (str1.CompareTo(str2))
{
    case < 0:
        Console.WriteLine("str1 < str2");
        break;
    case 0:
        Console.WriteLine("str1 == str2");
        break;
    case > 0:
        Console.WriteLine("str1 > str2");
        break;
}
```


### `.CompareTo()`를 쓸 때 장점

- **정렬 기준을 직접 코드에 구현할 필요 없음**
- **사전식/날짜형 문자열을 바로 비교 가능**
- **조건문에서 직관적인 범위 체크가 가능**
    


### 대소문자 무시한 문자열 비교:

```csharp
string.Compare(a, b, StringComparison.OrdinalIgnoreCase);
```

또는:

```csharp
a.Equals(b, StringComparison.OrdinalIgnoreCase);
```


