---
title: Regex 객체의 Match()
created: 2024-02-28 11:36
alias:
tags:
---
특정 패턴이 입력 문자열에 존재하는지 체크
`Regex.Match()` 메서드는 매치된 정보를 갖는 Match 클래스 객체를 리턴한다. 
만약 매치된 문자열이 존재하면 `Match.Success` 속성이 `True`가 되고, `Match.Index` 속성을 통해 문자 패턴 위치를 알 수 있다.  


Ex1은 첫 번째 매칭 문자열만을 리턴하는데, 복수개의 매칭 문자열이 존재할 수 있으므로, 
Ex2에서 처럼 계속 루프를 돌며 NextMatch()를 호출 모든 매칭 데이타를 찾아낼 수 있다.

Ex1. 첫 매치 문자열 출력
```csharp
string str = "서울시 강남구 역삼동 강남아파트";
Regex regex = new Regex("강남");
Match m = regex.Match(str);
if (m.Success)
{
    Debug.WriteLine("{0}:{1}", m.Index, m.Value); // 
}
```

Ex2. 매치된 문자열 계속 출력
```csharp
Regex regex = new Regex("강남");
Match m = regex.Match(str);
while (m.Success)
{
    Debug.WriteLine("{0}:{1}", m.Index, m.Value);
    m = m.NextMatch();
}
```

Ex3. Matches() 메서드
```csharp
Regex regex = new Regex("강남");
MatchCollection mc = regex.Matches(str);
foreach (Match m in mc)
{
    Debug.WriteLine("{0}:{1}", m.Index, m.Value);                
}
```

Match클래스는 하나의 매칭 데이타만을 갖는데, 이와 상응하는 컬렉션 클래스로 MatchCollection 클래스가 있다. Ex3 예제는 Regex.Matches() 메서드를 통해 모든 매칭 문자열들을 한꺼번에 MatchCollection 객체로 리턴하는 예를 보여주고 있다.


# Regex IsMatch(str, @"정규식")
리턴 타입 : bool
정규식이 입력 문자열에서 일치하는 항목을 찾을 것인지 여부를 나타냅니다.

