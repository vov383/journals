---
title: CSharp의 접근제어자(Access Modifier)
created: 2024-03-04 11:21
alias:
tags:
---
C#에서 public, protected, private, internal등은 클래스 혹은 클래스 멤버에 붙여서 접근 권한을 설정하는 Access Modifier로서, 누구에게 해당 클래스 혹은 클래스 멤버(속성, 메서드, 이벤트 등)를 접근 허용할 지를 지정하게 된다.

- public : 모든 외부 객체로부터 접근을 허용한다
- protected : 상속되는 파생클래스(derived class)에서만 접근할 수 있다
- private : 해당 클래스 내에서만 사용된다. 외부 혹은 파생클래스에서 접근 불가
- internal : 어셈블리(.NET Assembly)내에 있는 다른 클래스들에서 접근할 수 있다

네임스페이스안에 직접 생성되는 class는 public 혹은 internal로만 설정할 수 있고, Nested class는 이러한 제한이 없다.

`Q` 한 어셈블리의 internal class를 다른 어셈블리 DLL에서 호출하여 사용할 수 있는가? 있다면 어떻게 할 수 있는가?

`A` 가능하다. 한 어셈블리에 InternalsVisibleTo 속성(Attribute)를 지정하여 다른 어셈블리의 접근을 허용하면, 지정된 다른 어셈블리에서도 외부의 internal 클래스를 사용할 수 있다. Test Automation 프로그램에서 특히 많이 사용한다.


