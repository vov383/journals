---
title: async Task
created: 2024-05-14 02:02
alias:
tags:
---
###### 용도
일반적으로 비동기 메서드에서 사용됩니다.
###### 예외 처리
호출자에게 예외를 전달할 수 있으며, 
호출자는 `await`를 사용하여 예외를 처리할 수 있습니다.
###### 반환 값
비동기 작업이 완료될 때까지 기다릴 수 있습니다.
###### 용례
비동기 메서드에서, 비동기 작업을 수행하고 
호출자에게 작업 완료를 알리기 위해 사용됩니다.

```csharp
private async Task HandleClickAsync(DataGridViewCellEventArgs e)
{
    // 비동기 작업 수행
    await Task.Delay(1000); // 예시: 1초 대기
    // 추가 로직
}
```

호출 방법:
```csharp
await HandleClickAsync(e);
```


