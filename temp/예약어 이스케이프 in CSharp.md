---
title: 변수명, 파라미터 명에 예약어를 사용할 때 이스케이프
created: 2025-03-06 03:55
alias:
tags:
---
## @ 기호를 this앞에 붙여서 변수명으로 사용
변수명, 파라미터 명에 예약어를 사용할 때
`@` 기호를 붙이면 예약어와 동일한 이름을 변수명으로 사용 가능.

```csharp
public static void UIThread(this 
	System.Windows.Forms.Control @this, 
	Action code) 
{ 
	if (@this.InvokeRequired) 
		@this.BeginInvoke(code); 
	else 
		code.Invoke(); 
}
```


