---
title: UNITY timeScale 개념 정리
created: 2025-06-20 09:34
alias:
tags:
---
Unity의 `Time.timeScale` 개념과 관련된 영향 요소, 그리고 응용 프로그램 개발 시 주의할 점을 다음과 같이 정리할 수 있다.

### Time.timeScale이란

Unity의 전체 시간 흐름을 조절하는 계수 값이다.  
1.0f는 정상 속도, 0.5f는 절반 속도, 0.0f는 완전 정지 상태를 의미한다.

### Time.timeScale의 영향을 받는 대표 요소

1. Time.deltaTime  
    프레임 간 시간 간격. timeScale 값에 비례하여 영향을 받는다.  
    즉, timeScale이 0이면 deltaTime도 0이 된다.
    
2. WaitForSeconds()  
    코루틴에서 대기 시간으로 사용될 때, timeScale의 영향을 받아 실제 대기 시간도 늘어나거나 줄어든다.  
    예를 들어, timeScale이 0.5라면 1초를 기다리는데 실제로는 2초가 걸린다.
    
3. Animator  
    Animator의 updateMode가 기본값인 Normal일 경우 timeScale에 영향을 받는다.  
    updateMode를 UnscaledTime으로 설정하면 영향을 받지 않도록 할 수 있다.
    
4. FixedUpdate  
    물리 연산에 사용되는 FixedUpdate도 fixedDeltaTime이 timeScale에 영향을 받기 때문에, 시뮬레이션 속도에 영향을 줄 수 있다.
    
5. 일부 오디오 동기 로직  
    AudioSource 자체는 영향을 받지 않지만, 시간 기반 이벤트나 pitch 조절 등을 수동 제어할 때 영향을 받을 수 있다.
    

### Time.timeScale의 영향을 받지 않는 요소

1. Time.unscaledTime  
    애플리케이션 실행 이후 흐른 실제 시간 (scale에 무관함)
     
2. Time.unscaledDeltaTime  
    프레임 간 실제 시간 경과
    
3. WaitForSecondsRealtime  
    실제 시간 기준으로 작동하는 대기
    
4. DateTime.Now  
    시스템 시간 기반이므로 Unity 내부 시간과 무관
    
5. System.Diagnostics.Stopwatch  
    정밀한 타이머로 사용 가능. timeScale과 무관함
    

### 실시간 응용에서 주의할 점

1. UI에 시계, 경과시간, 타이머 등을 표시할 경우 deltaTime 또는 WaitForSeconds를 쓰면 안 되고 unscaledDeltaTime 또는 WaitForSecondsRealtime을 사용해야 한다.
    
2. Pause(일시정지)를 걸었을 때도 돌아가야 하는 기능은 전부 unscaled 기반 로직으로 따로 분리해야 한다.
    
3. 이동, 회전, 애니메이션 제어 로직에서도 필요 시 timeScale을 고려하여 unscaledDeltaTime으로 분기 처리할 수 있어야 한다.
    
4. 정지 상태에서도 지속적으로 실행되어야 하는 데이터 로깅, 이벤트 체크, 알람 타이머 등은 반드시 DateTime.Now 또는 Stopwatch.Elapsed 기반으로 작동하게 만들어야 한다.
    
5. Animator를 사용하는 경우 updateMode를 Normal이 아닌 UnscaledTime으로 설정해야 일시정지 중에도 애니메이션이 작동한다.
    

### 실무 대응 방식 예시

타이머나 시간 기반 로직을 유연하게 만들기 위해 다음처럼 분기 처리를 넣을 수 있다.

```csharp
float delta = isRealtimeMode ? Time.unscaledDeltaTime : Time.deltaTime;
```

또는 코루틴 기반의 실시간 대기를 다음처럼 구현할 수 있다.

```csharp
IEnumerator WaitRealSeconds(float seconds)
{
    float end = Time.realtimeSinceStartup + seconds;
    while (Time.realtimeSinceStartup < end)
        yield return null;
}
```

이상적으로는 UI, 알람, 애니메이션 등 각 기능별로 timeScale 영향을 받을지 여부를 분리하여 설계하는 것이 좋다.  
특히 Unity를 시뮬레이션 또는 HMI 플랫폼으로 사용할 경우 timeScale을 조작할 수 있는 상태(슬로우모션, 일시정지, 로그 재생 등)와 실제 시간 기반 기능들을 명확히 구분해야 시스템 전체의 안정성이 높아진다.


