---
title: SemaphoreSlim의 개요 및 사용법
created: 2024-05-31 01:22
alias:
tags:
---
###### SemaphoreSlim 이해하기
`SemaphoreSlim`은 .NET에서 제공하는 경량의 동기화 도구로, 
동시에 리소스에 접근할 수 있는 스레드의 수를 제한할 때 사용됩니다. 
이는 주로 동시 실행 흐름을 제어하여 자원의 과도한 사용을 방지하고, 
경쟁 상태를 관리하기 위해 사용됩니다.

###### 기본 구조와 사용법
`SemaphoreSlim`은 생성 시 최대 허용 스레드 수(`maxCount`)와 초기 스레드 수(`initialCount`)를 지정할 수 있습니다. 
이 세마포어는 스레드가 `Wait` 또는 `WaitAsync` 메서드를 호출할 때마다 
내부 카운터가 감소하며, 
`Release` 메서드를 호출할 때 카운터가 증가합니다.

- **생성**: `new SemaphoreSlim(initialCount, maxCount)`
- **대기**: `Wait()` 또는 `WaitAsync()`를 사용하여 리소스 접근을 시도하고, 세마포어가 0이 아닐 때까지 대기합니다.
- **릴리즈**: `Release()`를 호출하여 세마포어 카운트를 하나 증가시키고, 다른 대기 중인 스레드가 작업을 시작할 수 있도록 합니다.

###### 예제 코드
```csharp
SemaphoreSlim semaphore = new SemaphoreSlim(1, 1);  // 최대 1개의 스레드만 접근 허용

async Task AccessResource()
{
    await semaphore.WaitAsync();  // 리소스 접근을 위해 대기
    try
    {
        // 리소스 관련 작업 수행
    }
    finally
    {
        semaphore.Release();  // 작업 완료 후 세마포어 릴리즈
    }
}
```

###### 주의사항 및 특징
- **Deadlocks**: 모든 `Wait` 호출은 `Release`로 균형을 이뤄야 합니다. 그렇지 않으면 데드락이 발생할 수 있습니다.
- **비동기 지원**: `WaitAsync`는 비동기 작업에서 세마포어를 기다릴 때 사용되며, UI 스레드를 차단하지 않고 백그라운드에서 대기합니다.

###### 실제 사용 시 고려할 점
`SemaphoreSlim`은 
기화를 필요로 하는 다양한 시나리오에서 유용하게 사용될 수 있지만, 
자원에 대한 접근을 제어하는 로직을 설계할 때는 세심한 주의가 필요합니다. 
올바른 사용은 시스템의 안정성과 효율성을 크게 향상시킬 수 있습니다.

Q1 : 다른 동기화 메커니즘과 `SemaphoreSlim`의 차이점은 무엇인가요?
Q2 : `SemaphoreSlim`을 사용할 때 성능에 미치는 영향은 어떤 것들이 있을까요?

##### 요약
`SemaphoreSlim`은 동시 실행을 제어하는 경량 동기화 도구입니다.
스레드 수를 제한하여 리소스 접근을 관리합니다.
생성 시 최대 및 초기 스레드 수를 지정합니다.
`Wait` 및 `Release` 메서드로 리소스 접근을 제어합니다.
`WaitAsync`를 사용하여 비동기적으로 리소스 접근 대기가 가능합니다.
데드락 방지를 위해 사용된 `Wait`는 반드시 `Release`로 균형을 맞춰야 합니다.
세마포어의 올바른 사용은 시스템의 안정성과 효율성을 향상시킬 수 있습니다.


