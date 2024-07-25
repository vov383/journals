---
title: Dictionary 확장 메서드에서 Nullable DateTime 값 처리하기
created: 2024-07-25 08:06
alias:
tags:
---
`DateTime?` (nullable) 값을 처리할 수 있도록 기존 `GetValue` 메서드를 확장할 수 있습니다. 다음은 이를 구현한 코드입니다:

```csharp
public static T GetValue<T>(this Dictionary<string, object> dictionary, string key)
{
    if (dictionary.ContainsKey(key))
    {
        var value = dictionary[key];
        if (value is T returnValue)
        {
            return returnValue;
        }
        else if (value != null)
        {
            try
            {
                // 대상 타입이 nullable 타입인지 확인합니다.
                var targetType = Nullable.GetUnderlyingType(typeof(T)) ?? typeof(T);
                return (T)Convert.ChangeType(value, targetType);
            }
            catch (InvalidCastException)
            {
                throw new InvalidCastException($"The value for key '{key}' cannot be cast to type {typeof(T)}.");
            }
        }
        else if (value == null)
        {
            // T가 nullable value type인 경우 처리합니다.
            if (typeof(T).IsValueType && Nullable.GetUnderlyingType(typeof(T)) == null)
            {
                throw new InvalidCastException($"The value for key '{key}' cannot be cast to type {typeof(T)}.");
            }
            return default;
        }
    }
    throw new KeyNotFoundException($"The key '{key}' was not found in the dictionary.");
}
```

### 설명
1. **키 존재 여부 확인**: [::딕셔너리]에 해당 키가 있는지 확인합니다.
2. **직접 타입 일치**: 값이 직접적으로 `T` 타입이면 그대로 반환합니다.
3. **널이 아닌 경우 변환**: 값이 널이 아닌 경우, 원하는 타입으로 변환을 시도합니다.
4. **Nullable 타입 처리**: `Nullable.GetUnderlyingType(typeof(T)) ?? typeof(T)`을 사용하여 nullable 타입을 올바르게 처리합니다.
5. **널 값 처리**: 값이 널인 경우, `T`가 널을 수용할 수 있는지 (참조 타입 또는 nullable value type인지) 확인합니다.
6. **예외 처리**: 타입 캐스팅이 불가능하거나 키가 없는 경우 적절한 예외를 발생시킵니다.

### 사용 예제
다음은 nullable `DateTime` 값을 포함한 [[Dictionary＜TKey, TValue＞|딕셔너리]]와 함께 이 메서드를 사용하는 예제입니다:

```csharp
var dictionary = new Dictionary<string, object>
{
    { "date1", new DateTime(2023, 7, 24) },
    { "date2", null }
};

DateTime? date1 = dictionary.GetValue<DateTime?>("date1");
DateTime? date2 = dictionary.GetValue<DateTime?>("date2");
```

### 요약
1. nullable 타입을 처리할 수 있도록 메서드 확장.
2. `Nullable.GetUnderlyingType`를 사용하여 올바른 타입 변환.
3. 참조 타입 및 nullable value 타입과 호환되는 null 값 처리.
4. 타입 캐스팅 문제와 키가 없는 경우 예외 처리.


