---
title: Regex 문자열 분리(Split)
created: 2024-02-28 01:20
alias:
tags:
---
`Regex` 클래스 `Split()` 메서드는 
특정 패턴의 문자열을 기준으로 입력문자열을 분리하는데 사용된다. 
예를 들어, 아래 예제는 공백(blank)을 기준으로 입력주소를 분리(split)하여 문자배열을 담아 리턴하는 예이다.
```csharp
string str = "서울시 강남구 역삼동 강남아파트";

Regex regex = new Regex(" ");
string[] vals = regex.Split(str);
foreach (string s in vals)
{
    Debug.WriteLine(s);
}
```

마지막에 regex 로 string을 split 할수 있지만
기존 String 클래스에 있는 split을 사용하는것이 더 좋습니다.

Regex 의 Split은 String의 Split보다 15배 가량 더 느립니다.

