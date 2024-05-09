---
title: Int의 TryParse()
created: 2024-05-09 02:03
alias:
tags:
---
###### 작동 방식 
`int.TryParse` 메서드는 
**문자열을 정수로** 변환을 시도하고, 
변환의 성공 여부를 `bool` 값으로 반환합니다. 
이 메서드는 변환 성공 시 변환된 값을 출력 파라미터로 넘겨주며, 
실패 시 `0`을 출력 파라미터에 설정합니다.
###### 예외 처리 
`TryParse`는 변환 과정에서 예외를 발생시키지 않습니다. 
대신, 변환 가능 여부를 `bool` 값으로 반환하여 안전하게 처리할 수 있도록 합니다. 
이는 입력 데이터의 유효성을 검증하지 않고도 안전하게 사용할 수 있게 해줍니다.
###### 주요 활용 
입력 데이터의 유효성이 불확실하거나, 
사용자 입력과 같이 예측 불가능한 데이터를 처리할 때 사용하기 적합합니다. 
예외 처리 로직을 작성하지 않아도 되므로 코드가 간결해집니다.

```csharp
string input = "abc";
int result;
if (int.TryParse(input, out result))
{
    Console.WriteLine(result);
}
else
{
    Console.WriteLine("정수로 변환할 수 없습니다.");
}
```


