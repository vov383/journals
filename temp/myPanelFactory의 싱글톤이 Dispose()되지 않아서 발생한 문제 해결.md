---
title: myPanelFactory의 싱글톤이 Dispose()되지 않아서 발생한 문제 해결
created: 2025-04-18 09:27
alias:
tags:
---
###### 폼과 UserControl의 생명 주기 차이
![[journals/temp/폼과 UserControl의 생명 주기 차이]]


### 문제 발생 원인

1. **Disposed 이벤트 미발생**
    
    - UserControl이 Parent 컬렉션에서 빠지더라도, 실제로 Dispose되지 않으면 `this.Disposed` 핸들러가 호출되지 않습니다.
        
2. **Reset() 호출 시점 누락**
    
    - 팝업 폼에서는 `FormClosed`에 묶었지만, UserControl 쪽에서는 제거 시점에 걸어놓은 이벤트가 동작하지 않아 싱글톤이 여전히 구 버전을 참조합니다.
        
3. **이벤트 언리싱(구독 해제) 미비**
    
    - UserControl 내부에서 팩토리의 이벤트를 구독했다면, 컨트롤이 사라질 때 해당 구독을 해제하지 않아 GC가 제대로 수거하지 못합니다.
        


### 확인 포인트 & 대응 방안

| 확인 항목               | 대응 방안                                                                     |
| ------------------- | ------------------------------------------------------------------------- |
| ① Disposed 발생 여부    | UserControl이 실제로 `Dispose()`되는지 브레이크포인트로 확인                               |
| ② ParentChanged 활용  | `ParentChanged` 이벤트에서 `if (Parent==null) YardListPanelFactory.Reset()` 호출 |
| ③ VisibleChanged 활용 | `VisibleChanged`에서 `if (!Visible) Reset()`로 제거 시점 보강                      |
| ④ 팩토리 내부 이벤트        | 팩토리에서 컨트롤 이벤트 구독 시 `Dispose` 혹은 `Reset()`에서 `control.Event -= …` 해제       |
| ⑤ IDisposable 패턴 적용 | 팩토리 클래스 자체에 `IDisposable`을 구현해 `Dispose()` 호출 시점 명확화                      |

```csharp
// UserControl 측 예시
public MyUserControl()
{
    InitializeComponent();
    this.ParentChanged += (s, e) =>
    {
        if (this.Parent == null)
            YardListPanelFactory.Reset();
    };
    // 이미 구독한 이벤트가 있다면 OnDisposed에서도 해제
    this.Disposed += (s, e) =>
    {
        // ex) button.Click -= OnButtonClick;
        YardListPanelFactory.Reset();
    };
}
```

---

#### 다양한 시각

- **안정성 관점**: 팩토리 초기화 책임을 컨트롤 제거 시점에 확실히 부여하면 재사용 에러 최소화
    
- **유지보수 관점**: `ParentChanged`·`VisibleChanged`로 리소스 해제 로직을 분산시키지 않고, 팩토리에 `Dispose()` 패턴을 적용해 단일 책임으로 관리
    
- **설계 관점**: UI 상태와 팩토리 상태를 느슨하게 결합(loose coupling)해, 팩토리는 순수 로직만 담당하도록 분리
    

---

### 요약 포인트

- **팝업 폼**은 `FormClosed`→`Dispose()`가 확실히 일어나지만, **UserControl**은 단순 제거만으론 `Dispose`가 불리지 않을 수 있음
    
- `ParentChanged`·`VisibleChanged` 이벤트를 활용해 제거 시점을 잡거나, 팩토리에 **IDisposable** 패턴을 적용해 해제 책임을 명확히 부여
    
- 이벤트 구독 해제까지 꼼꼼히 처리하면 “삭제된 개체” 예외를 완전히 방지 가능합니다.





