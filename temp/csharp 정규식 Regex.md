---
title: csharp 정규식 Regex
created: 2024-02-28 09:41
alias:
tags:
---
정규식 설명
https://www.csharpstudy.com/Practical/Prac-regex-1.aspx

정규식 생성


입력된 정규식을 테스트할 수 있는 사이트
https://regex101.com/

흔히 복잡한 문자열 처리를 위해 Regular Expression을 사용하는데, .NET에서는 이 기능을 Regex 클래스를 중심으로 구현하고 있다. 
.NET의 Regular Expression기능은 대부분 Perl에서 진화한 것으로 Perl 5 Regular Expression과 호환되도록 설계되었다. 
###### 정규식
![[정규식(Regular Expression)]]
따라서 Regular Expression은 
Web Crawler나 로그 파싱 등에 매우 유용한 기능이라 할 수 있다.

###### Regex 메타문자  의미
![[Regex 메타문자  의미]]

Regex 클래스를 사용하여 특정 문자 패턴을 찾는 몇가지 예들
아래 Ex1 예제는 `강남`이라는 문자열을 입력문자열(str)에서 찾는 단순한 코드이다. 
Regex클래스 객체를 생성할 때, 특정 문자 패턴을 파라미터로 전달함.
###### Regex 객체의 Match()
![[Regex 객체의 Match()]]

Regex 메타문자
Regular Expression에는 일반 문자 리터럴(literal)과 특별한 의미를 갖는 메타문자(metacharacter)를 사용할 수 있다.
메타문자에는 외우기 힘들 정도로 매우 많은 문자들이 있는데, 그 중 많이 사용되는 몇 가지를 예로 들면 다음과 같다. 
예를 만약 문자패턴을 
	`^강\w*구$` 와 같이 정하면, 
	이는 한 라인에서 강으로 시작해서 구로 끝나는 문자열들을 찾게 된다.
```csharp
MatchCollection mc = Regex.Matches(str, @"^강\w*구$");
```





###### Regex 문자열 분리(Split)
![[Regex 문자열 분리(Split)]]

Regex - Group 클래스  
Regular Expression의 표현식 중에 `( )` 로 표현되는 `Group` 표현식이 있는데, 
이는 특히 유용한 기능을 제공한다. 
이 그룹 표현식은 괄호안에 있는 문자열들을 찾아내어 `Match` 클래스 객체의 `Match.Groups` 속성에 결과를 넣게 된다. 
`Match.Groups` 속성은 `GroupCollection` 클래스 객체로서 복수의 `Group` 클래스 객체를 갖는다.  

Ex1은 아파트 혹은 APT라는 문자열이 있는 부분의 문자열 위치 정보를 `Match.Groups`에 저장하고, 이를 출력해 보이는 예제이다. 
여기서 한가지 주의할 점은 `Match.Groups`는 `Match.Groups[1]`부터 각 그룹의 결과가 저장된다는 것이다. 
패턴이 발견되지 않았을 때에도 `Match.Groups[0]`는 존재하여 여기에 `Group.Success = false`를 저장하여 실패를 표현한다.  

Ex1. `named group (?<name> )`
```csharp
string str = "02-632-5432; 032-645-7361";
Regex regex = new Regex(@"(?<areaNo>\d+)-(?<phoneNo>\d+-\d+)");
MatchCollection mc = regex.Matches(str);
foreach (Match m in mc)
{                             
    string area = m.Groups["areaNo"].Value;
    string phone = m.Groups["phoneNo"].Value;
    Debug.WriteLine("({0}) {1}", area, phone);
}
```

Ex2 예제는 보다 실용적인 예로써 HTML 페이지에서 List 요소값을 모두 찾아내는 예이다.  
Ex3 예제는 전화번호의 패턴을 찾아내는 예로써 지역번호와 나머지 전화번호를 분리하여 2개의 그룹에 넣는 예를 보여주고 있다.
Ex2. 
 ```csharp
string str = "<div><a href='www.sqlmgmt.com'>SQL Tools</a></div>";
string patt = @"<a[^>]*href\s*=\s*[""']?(?<href>[^""'>]+)[""']?";
Match m = Regex.Match(str, patt);
Group g = m.Groups["href"];
Debug.WriteLine(g.Value);
```

나이 정규식
```
^(1[01][0-9]|[1-9]?[0-9])$
```

나이를 검증하기 위한 정규 표현식을 작성할 때, 몇 가지 가정을 해야 합니다. 
를 들어, 나이의 범위를 0세에서 120세로 제한한다고 가정할 수 있습니다. 
이 범위 내에서 유효한 나이 값을 검증하는 정규 표현식은 다음과 같이 작성할 수 있습니다:

이 정규 표현식을 분석해보겠습니다:

- `^`: 문자열의 시작을 의미합니다.
- `(1[01][0-9]|[1-9]?[0-9])`: 두 부분으로 나뉘는 메인 그룹입니다.
  - `1[01][0-9]`: `100`에서 `119`까지의 숫자와 일치합니다. 여기서 `1[01]`은 `10` 또는 `11`을 의미하며, 뒤의 `[0-9]`는 마지막 자리가 0에서 9까지의 어떤 숫자와도 일치할 수 있음을 의미합니다.
  - `[1-9]?[0-9]`: `0`에서 `99`까지의 숫자와 일치합니다. `[1-9]?`는 첫 번째 자리가 1에서 9까지의 숫자가 올 수도 있고, 아예 없을 수도 있음을 의미합니다(즉, 0으로 시작하는 숫자나 단일 자리 숫자를 허용). 두 번째 `[0-9]`는 두 번째 자리 숫자가 0에서 9까지임을 의미합니다.
- `$`: 문자열의 끝을 의미합니다.

이 정규 표현식은 나이가 0세에서 119세 사이의 숫자로 제한될 때 유효합니다. 이는 대부분의 실제 시나리오에서 합리적인 가정입니다. 그러나, 실제 애플리케이션에서 나이를 처리할 때는 더 많은 컨텍스트가 고려되어야 합니다. 예를 들어, 사용자 입력을 받는 폼에서는 입력 필드에 숫자 범위를 지정하는 등의 추가적인 검증이 필요할 수 있습니다. 

또한, 정규 표현식만으로는 사용자가 미래 날짜나 비현실적인 날짜(예: `0000-00-00`)를 입력하는 것을 완전히 방지할 수 없으므로, 날짜 입력을 처리할 때는 정규 표현식과 함께 논리적 검증 로직도 함께 구현하는 것이 좋습니다.

이메일 주소 체크
```csharp
public bool IsValidEmail(string email)
{    
    bool valid = Regex.IsMatch(email, @"[a-zA-Z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-zA-Z0-9!#$%&'*+/=?^_`{|}~-]+)*@(?:[a-zA-Z0-9](?:[a-zA-Z0-9-]*[a-zA-Z0-9])?\.)+[a-zA-Z0-9](?:[a-zA-Z0-9-]*[a-zA-Z0-9])?");
    return valid;
}
```
실무 프로그램에서 이메일을 입력 받을 때, 이 이메일이 타당한지를 체크하는 일이 많다. 
완벽하게 이메일을 체크하기 위해서는 프로그램에서 직접 이메일을 보내고 사용자가 이메일에 로그인한 후 확인 링크를 누르게 하는 것이다. 
이러한 이메일 확인 절차와 별도로 사전에 미리 이메일 주소가 문법적으로 타당한지를 검사할 수 있는데, 이때 보통 Regular Expression (RegEx)를 사용한다. 
이메일에 대한 공식적인 문법은 [RFC 5322](http://tools.ietf.org/html/rfc5322#section-3.4) 에 정의되어 있는데, 이를 실용적으로 구현하면 위와 같이 작성할 수 있다.
