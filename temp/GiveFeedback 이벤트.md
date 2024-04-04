---
title: GiveFeedback 이벤트
created: 2024-03-28 10:20
alias:
tags:
---
드래그 앤 드롭 작업 중에 발생하며, 
드래그 앤 드롭 작업의 외양을 사용자에게 피드백하는 데 사용됩니다. 
이 이벤트는 드래그 소스 컨트롤에서 발생하며, 드래그 작업이 시작될 때 활성화됩니다. 
주로 커서의 모양을 변경하거나, 
드래그 앤 드롭 작업 중에 사용자에게 추가적인 시각적 피드백을 제공할 때 사용됩니다.
###### 정의
드래그 앤 드롭 작업 중에 발생하며, 
드래그 앤 드롭 작업의 외양을 사용자에게 피드백하는 데 사용됩니다. 
이 이벤트는 드래그 소스 컨트롤에서 발생하며, 드래그 작업이 시작될 때 활성화됩니다. 
주로 커서의 모양을 변경하거나, 드래그 앤 드롭 작업 중에 사용자에게 추가적인 시각적 피드백을 제공할 때 사용됩니다.
###### 효과
`GiveFeedback` 이벤트를 적절히 사용하면 
사용자가 드래그 앤 드롭 작업을 더 명확하게 인지할 수 있게 하며, 
어떤 드래그 앤 드롭 효과가 발생하고 있는지를 시각적으로 표현할 수 있습니다.
###### GiveFeedback 이벤트의 사용법
`GiveFeedback` 이벤트는 다음과 같이 사용됩니다:

1. **이벤트 핸들러 등록**: 드래그를 시작하기 전에 소스 컨트롤에 `GiveFeedback` 이벤트 핸들러를 등록합니다.
2. **커서 변경**: 사용자가 드래그 앤 드롭 작업을 시작할 때 적절한 커서로 변경하려면 이 이벤트 내에서 `Cursor.Current`를 설정합니다.
3. **피드백 제공**: `GiveFeedbackEventArgs` 매개변수를 통해 드래그 앤 드롭 작업의 현재 상태에 대한 정보를 얻고, 이를 바탕으로 사용자에게 적절한 피드백을 제공합니다.
4. **기본 커서 사용 방지**: 사용자 정의 커서를 사용하려면 `GiveFeedbackEventArgs`의 `UseDefaultCursors` 속성을 `false`로 설정합니다.

### 예제 코드

다음은 `GiveFeedback` 이벤트를 사용하는 간단한 예제입니다:

```csharp
// 드래그 시작 전에 이벤트 핸들러를 등록합니다.
someControl.MouseDown += (sender, e) =>
{
    someControl.DoDragDrop(someData, DragDropEffects.Move);
};

// GiveFeedback 이벤트 핸들러
someControl.GiveFeedback += (sender, e) =>
{
    // 드래그 중에 특정 커서를 사용하고 싶을 때
    e.UseDefaultCursors = false;
    if ((e.Effect & DragDropEffects.Move) == DragDropEffects.Move)
    {
        Cursor.Current = Cursors.SizeAll; // 예를 들어 'SizeAll' 커서로 설정
    }
};
```

이 이벤트는 `DoDragDrop` 메서드가 호출되어 드래그 앤 드롭 작업이 시작될 때 활성화되며, 드래그 작업이 진행되는 동안 여러 번 호출될 수 있습니다.

### GiveFeedback 이벤트 사용 시 주의사항

- **성능 고려**: `GiveFeedback` 이벤트는 드래그 작업 중 반복적으로 발생할 수 있으므로, 이벤트 핸들러 내에서 성능에 영향을 미칠 수 있는 무거운 작업을 피해야 합니다.
- **이벤트 버블링**: `GiveFeedback` 이벤트는 버블링이나 터널링이 일어나지 않습니다. 즉, 이 이벤트는 드래그 소스 컨트롤에만 한정되어 발생합니다.
[[버블링(bubbling)과 터널링(tunneling)]]
[[터널링(Tunneling)]]
[[버블링(Bubbling)]]



