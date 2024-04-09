---
title: Invalidate() 메서드
created: 2024-04-09 02:22
alias:
tags:
---
.NET Windows Forms 컨트롤에서 사용되며, 
컨트롤이나 컨트롤의 일부분을 다시 그려야 함을 시스템에 알리는 데 사용됩니다. 
이 메서드를 호출하면, 
컨트롤의 `Paint` 이벤트가 발생하여 컨트롤의 외관을 갱신할 수 있게 됩니다. 
`Invalidate()` 메서드는 컨트롤이 갱신되어야 할 때 
시스템에 그리기 요청을 하는 비동기적인 방법입니다.

### 사용 방법
`Invalidate()` 메서드는 여러 오버로드를 제공합니다:

**Invalidate()**
컨트롤 전체를 다시 그리도록 요청합니다.
**Invalidate(Rectangle rect)**
컨트롤의 지정된 사각형 영역만을 다시 그리도록 요청합니다. 
이 방법은 특정 영역만 갱신이 필요할 때 효율적입니다.
**Invalidate(bool invalidateChildren)**
컨트롤을 다시 그리도록 요청하며, 
`invalidateChildren` 매개변수가 `true`일 경우 
컨트롤의 자식 컨트롤들도 함께 다시 그리도록 요청합니다.
**Invalidate(Rectangle rect, bool invalidateChildren)**
지정된 사각형 영역과, 
선택적으로 자식 컨트롤들을 다시 그리도록 요청합니다.

### 사용 예

컨트롤의 특정 부분의 배경색이 변경되었을 때 해당 부분만을 다시 그리도록 할 수 있습니다:

```csharp
// 컨트롤의 특정 부분만 다시 그리기
Rectangle updatedArea = new Rectangle(10, 10, 100, 100);
this.Invalidate(updatedArea);
```

또는 컨트롤 전체를 다시 그리기 위해 다음과 같이 호출할 수 있습니다:

```csharp
// 컨트롤 전체를 다시 그리기
this.Invalidate();
```

### 주의사항

`Invalidate()` 메서드는 컨트롤을 즉시 다시 그리지 않습니다. 
대신, 다시 그리기를 위한 요청을 시스템에 등록하고, 
실제 그리기 작업은 나중에 비동기적으로 수행됩니다.
`Invalidate()` 후에 
`Update()` 또는 `Refresh()` 메서드를 호출하면, 
`Invalidate()`에 의해 등록된 다시 그리기 요청이 즉시 처리되어 
컨트롤이 갱신됩니다. 
`Refresh()` 메서드는 
내부적으로 `Invalidate(true)`와 `Update()`를 호출하여 
컨트롤과 그 자식 컨트롤들을 즉시 다시 그리도록 합니다.
불필요하게 자주 `Invalidate()`를 호출하는 것은 
성능에 부정적인 영향을 줄 수 있으므로, 
필요한 경우에만 사용하는 것이 좋습니다.


