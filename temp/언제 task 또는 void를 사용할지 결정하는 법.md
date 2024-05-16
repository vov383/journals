---
title: 언제 task 또는 void를 사용할지 결정하는 법
created: 2024-05-14 02:03
alias:
tags:
---
###### **Task**
메서드가 비동기 작업을 수행하고 
호출자가 이 작업이 완료될 때까지 기다리거나 
예외를 처리할 수 있어야 할 때 사용합니다.
###### **void**
주로 이벤트 핸들러에서 사용하며, 
이벤트 핸들러는 반환 값을 필요로 하지 않습니다. 
이 경우 호출자가 작업의 완료 여부나 예외를 처리할 필요가 없습니다.

### 예제: `Task`와 `void`의 사용
1. **Task** 예제:
```csharp
private async Task LoadDataAsync()
{
    // 데이터 로드 비동기 작업
    await Task.Delay(1000); // 예시: 1초 대기
    // 추가 로직
}

public async void button_Click(object sender, EventArgs e)
{
    await LoadDataAsync();
}
```

2. **void** 예제:
```csharp
private async void button_Click(object sender, EventArgs e)
{
    // 버튼 클릭 이벤트 핸들러
    await Task.Delay(1000); // 예시: 1초 대기
    // 추가 로직
}
```


