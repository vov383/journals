---
title: Convert의 ToInt32()
created: 2024-05-09 02:03
alias:
tags:
---
###### 작동 방식 
`Convert.ToInt32` 메서드는 입력값을 `int` 타입으로 변환합니다. 
이 메서드는 `null` 값을 `0`으로 변환하며, 
다양한 수치 데이터 타입과 `string`, `bool` 등을 정수로 변환할 수 있습니다. 
문자열이 `null`인 경우 `0`을 반환합니다.
###### 예외 처리 
변환 과정에서 형식이 맞지 않거나, 변환 가능 범위를 벗어날 경우 
`System.FormatException` 또는 `System.OverflowException`을 발생시킵니다. 
따라서, 예외가 발생할 가능성이 있는 상황에서 
사용하기 전에 입력값을 철저히 검증해야 합니다.
###### 주요 활용 
입력값이 확실히 유효하고, 정수로의 변환이 보장되는 경우 
사용하기 적합합니다. 
오류 발생 시 예외 처리를 통해 명확하게 오류를 핸들링할 수 있습니다.

```csharp
string input = "123";
try
{
    int result = Convert.ToInt32(input);
    Console.WriteLine(result);
}
catch (FormatException)
{
    Console.WriteLine("입력 형식이 잘못되었습니다.");
}
catch (OverflowException)
{
    Console.WriteLine("입력 값이 너무 크거나 작습니다.");
}
```


