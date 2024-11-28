---
title: CSharp Discard 용법
created: 2024-11-27 04:50
alias:
tags:
---
#### Discard('out_')용법의 이름

- **"Discard" (버리는 변수)**라고 부릅니다.
- `C# 7.0`부터 도입된 기능으로, **필요하지 않은 값**을 처리할 때 사용됩니다.
- 변수에 값을 저장하지 않고, 단순히 반환 결과만 확인하려는 상황에서 유용합니다.

---

#### 용도

`out _`은 **결과 값에 관심이 없을 때** 사용됩니다. `int.TryParse` 같은 메서드는 입력 값이 숫자로 변환 가능한지 확인하면서 변환된 값을 반환하기 위해 `out` 매개변수를 사용합니다. 하지만 변환된 값이 필요 없고, 성공 여부만 확인하려는 경우에 `out _`를 사용합니다.

---

#### 주요 사용 사례

1. **`TryParse` 계열 메서드**:
    
    - 입력 값이 유효한지 확인만 할 때.
    
    ```csharp
    if (int.TryParse("123", out _)) // 숫자 여부만 확인
    {
        Console.WriteLine("This is a valid number.");
    }
    ```
    
2. **메서드가 `out`을 사용하는 경우**:
    
    - 반환값의 일부만 필요할 때.
    
    ```csharp
    Dictionary<string, int> dict = new Dictionary<string, int>
    {
        { "key1", 10 },
        { "key2", 20 }
    };
    
    if (dict.TryGetValue("key1", out _)) // "key1"이 존재하는지 여부만 확인
    {
        Console.WriteLine("Key exists!");
    }
    ```
    
3. **LINQ와 함께 사용**:
    
    - 값 자체보다 조건 필터링에 관심이 있을 때.
    
    ```csharp
    List<string> items = new List<string> { "123", "abc", "456" };
    
    var validNumbers = items.Where(item => int.TryParse(item, out _)).ToList();
    Console.WriteLine(string.Join(", ", validNumbers)); // 출력: "123, 456"
    ```
    

---

#### 익숙해지기 위한 예제

##### 1. `int.TryParse`에서 `out _` 사용

숫자인지 확인만 하고, 숫자를 실제로 사용하지 않는 경우:

```csharp
string[] values = { "123", "abc", "456", "xyz" };

foreach (var value in values)
{
    if (int.TryParse(value, out _)) // 숫자인지 여부만 확인
    {
        Console.WriteLine($"{value} is a valid number.");
    }
    else
    {
        Console.WriteLine($"{value} is not a valid number.");
    }
}
```

**출력**:

```
123 is a valid number.
abc is not a valid number.
456 is a valid number.
xyz is not a valid number.
```

---

##### 2. `Dictionary`에서 `TryGetValue`와 함께 사용

딕셔너리 키가 존재하는지 확인하고, 값은 사용하지 않는 경우:

```csharp
var dictionary = new Dictionary<string, int>
{
    { "key1", 10 },
    { "key2", 20 }
};

if (dictionary.TryGetValue("key1", out _)) // 값은 필요하지 않음
{
    Console.WriteLine("Key 'key1' exists in the dictionary.");
}

if (!dictionary.TryGetValue("key3", out _)) // 값은 필요하지 않음
{
    Console.WriteLine("Key 'key3' does not exist.");
}
```

**출력**:

```
Key 'key1' exists in the dictionary.
Key 'key3' does not exist.
```

---

##### 3. LINQ와 `out _` 사용

리스트에서 숫자로 변환 가능한 항목만 필터링:

```csharp
List<string> items = new List<string> { "123", "abc", "456", "789xyz", "100" };

var validNumbers = items.Where(item => int.TryParse(item, out _)).ToList();

Console.WriteLine(string.Join(", ", validNumbers)); // 출력: "123, 456, 100"
```

---

#### 요약

1. **`out _` 정의**:
    - "Discard variable"로, 반환 값을 저장하지 않고 버릴 때 사용.
2. **주 용도**:
    - `TryParse` 또는 `TryGetValue` 같은 `out` 매개변수를 사용하는 메서드에서 값에 관심이 없을 때.
3. **LINQ와의 활용**:
    - 필터링 조건으로 값을 확인할 때 유용.
4. **예제**:
    - 숫자 여부 확인, 딕셔너리 키 존재 여부 확인, LINQ 필터링 등에서 사용.

---

#### 다음으로 이어질 질문

Q1. `out`을 활용한 다른 메서드 사용법이 필요하신가요?  
Q2. `out` 대신 `ref`를 사용하는 메서드 차이를 알고 싶으신가요?  
Q3. LINQ와 관련된 더 복잡한 필터링 조건 구현이 필요하신가요?

