---
title: async void
created: 2024-05-14 02:02
alias:
tags:
---
###### 용도
이벤트 처리기에서 주로 사용됩니다.
###### 예외 처리
호출자에게 예외를 전달할 수 없습니다. 
예외가 발생하면 애플리케이션이 종료될 수 있습니다.
###### 반환 값
호출자는 비동기 작업의 완료를 기다릴 수 없습니다.
###### 용례
주로 이벤트 핸들러에서 사용되며, 이벤트 핸들러는 반환 값을 필요로 하지 않습니다.

```csharp
private async void button_Click(object sender, EventArgs e)
{
    // 비동기 작업 수행
    await Task.Delay(1000); // 예시: 1초 대기
    // 추가 로직
}
```

호출 방법
```csharp
button_Click(this, EventArgs.Empty); // 이벤트 핸들러 호출
```