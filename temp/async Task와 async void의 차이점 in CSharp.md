---
title: async Task와 async void의 차이점 in CSharp
created: 2024-05-14 02:02
alias:
tags:
---
C#에서 `async` 메서드의 반환 형식으로 `Task`와 `void`를 사용할 수 있으며, 
이 둘은 중요한 차이점을 가지고 있습니다. 
각 용도의 차이를 이해하면 비동기 프로그래밍을 보다 효율적으로 사용할 수 있습니다.

###### async Task
![[journals/temp/async Task]]


###### async void
![[journals/temp/async void]]


###### 언제 task 또는 void를 사용할지 결정하는 법
![[journals/temp/언제 task 또는 void를 사용할지 결정하는 법]]


### 예제 코드 통합
앞서 설명한 셀 클릭과 셀 더블 클릭 이벤트를 구분하여 처리하는 코드를 포함한 예제:

```csharp
private bool isDoubleClick = false;
private bool isProcessing = false;

private async void dataGridView1_CellClick(object sender, DataGridViewCellEventArgs e)
{
    if (isProcessing) return;
    isProcessing = true;

    await Task.Delay(300); // 더블 클릭 감지 대기 시간
    if (!isDoubleClick)
    {
        await HandleClickAsync(e); // 클릭 이벤트 처리
    }

    isDoubleClick = false;
    isProcessing = false;
}

private async void dataGridView1_CellDoubleClick(object sender, DataGridViewCellEventArgs e)
{
    isDoubleClick = true;
    await HandleDoubleClickAsync(e); // 더블 클릭 이벤트 처리
}

private async Task HandleClickAsync(DataGridViewCellEventArgs e)
{
    // 클릭 이벤트 처리 비동기 로직
    await Task.Delay(1000); // 예시: 1초 대기
    // 추가 로직
}

private async Task HandleDoubleClickAsync(DataGridViewCellEventArgs e)
{
    // 더블 클릭 이벤트 처리 비동기 로직
    await Task.Delay(1000); // 예시: 1초 대기
    // 추가 로직
}
```

### Summary
###### `async Task`와 `async void`
- `Task`는 호출자가 비동기 작업을 기다리거나 예외를 처리할 수 있도록 사용.
- `void`는 이벤트 핸들러에서 주로 사용, 호출자는 작업의 완료 여부나 예외를 처리할 수 없음.

###### 예외 처리
- `Task`는 호출자에게 예외를 전달할 수 있음.
- `void`는 예외 발생 시 애플리케이션이 종료될 수 있음.

###### 호출 방법
- `Task`는 `await`로 호출.
- `void`는 이벤트 핸들러로 호출.

Q1 : `Task`와 `void`를 사용하는 비동기 메서드에서 발생할 수 있는 다른 잠재적인 문제는 무엇인가요?

Q2 : 비동기 메서드에서 예외 처리를 더욱 효율적으로 하는 방법은 무엇이 있을까요?


특정 문자열과 일치하는 항목의 인덱스를 하나만 찾고자 할 때는 LINQ의 `FirstOrDefault`와 `IndexOf`를 함께 사용하면 됩니다. 이 방법을 사용하면 첫 번째로 일치하는 항목의 인덱스를 반환할 수 있습니다.

다음은 해당 기능을 구현하는 예제입니다:

### LINQ를 사용한 첫 번째 일치 항목의 인덱스 찾기

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<string> _portShipList = new List<string> { "Ship1", "Ship2", "Ship3", "Ship4", "Ship2" };
        string sh_nm = "Ship2";

        // LINQ를 사용하여 문자열과 일치하는 첫 번째 항목의 인덱스 찾기
        int index = _portShipList
            .Select((item, index) => new { Item = item, Index = index })
            .FirstOrDefault(x => x.Item == sh_nm)?.Index ?? -1;

        // 결과 출력
        if (index != -1)
        {
            Console.WriteLine($"'{sh_nm}' found at index: {index}");
        }
        else
        {
            Console.WriteLine($"'{sh_nm}' not found.");
        }
    }
}
```

### 코드 설명
- `Select((item, index) => new { Item = item, Index = index })`: 리스트의 각 항목과 그 인덱스를 익명 객체로 반환합니다.
- `FirstOrDefault(x => x.Item == sh_nm)`: 일치하는 첫 번째 항목을 찾고, 없으면 `null`을 반환합니다.
- `?.Index ?? -1`: `null` 체크를 통해 일치하는 항목이 없을 경우 -1을 반환합니다.

이 코드는 일치하는 첫 번째 항목의 인덱스를 반환하고, 만약 일치하는 항목이 없다면 -1을 반환합니다.

### 요약
#### LINQ를 사용한 첫 번째 일치 항목의 인덱스 찾기
- `Select`와 `FirstOrDefault`를 사용하여 리스트 항목과 그 인덱스를 익명 객체로 반환.
- 특정 문자열과 일치하는 첫 번째 항목을 찾음.
- 일치하는 항목이 없으면 -1을 반환.


Q1: 리스트에서 특정 문자열과 일치하는 모든 항목의 인덱스를 찾는 방법은 무엇인가요?
Q2: LINQ를 사용하지 않고 특정 문자열과 일치하는 첫 번째 항목의 인덱스를 찾는 다른 방법은 무엇인가요?