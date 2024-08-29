---
title: FuncIBerthCommand, bool predicate 이해하기
created: 2024-08-29 05:09
alias:
tags:
---
`Func<IBerthCommand, bool> predicate`는 C#에서 사용되는 델리게이트(delegate) 타입입니다. 델리게이트는 함수에 대한 포인터와 비슷하며, 메서드를 다른 메서드에 인수로 전달할 때 사용됩니다. 이 경우 `Func<IBerthCommand, bool>`는 `IBerthCommand`를 입력으로 받아 `bool`을 반환하는 메서드를 나타내는 델리게이트입니다.

###### Predicate란 무엇인가
![[journals/temp/Predicate란 무엇인가]]


#### 타입을 분석하기
- `Func<IBerthCommand, bool>`:
  - `Func<...>`는 C#의 제네릭 델리게이트 타입입니다.
  - 첫 번째 타입 매개변수 (`IBerthCommand`)는 입력 타입을 지정합니다.
  - 두 번째 타입 매개변수 (`bool`)는 반환 타입을 지정합니다.

따라서 `IBerthCommand`를 입력으로 받아 `bool`을 반환하는 메서드라면 이 델리게이트에 전달할 수 있습니다.

### 사용 예제

다음은 predicate를 정의하고 사용하는 방법을 보여주는 간단한 예제입니다:

```csharp
// 예제 IBerthCommand 구현
public class SampleCommand : IBerthCommand
{
    public void Execute(object parameter)
    {
        // 명령 실행 로직
    }

    public void Undo(object parameter)
    {
        // 명령 취소 로직
    }

    public bool CanExecute(object parameter)
    {
        return true;
    }
}

// Func<IBerthCommand, bool> 델리게이트 서명을 만족하는 예제 메서드
bool IsSampleCommand(IBerthCommand command)
{
    return command is SampleCommand;
}

// CommandManager에서의 predicate 사용
Func<IBerthCommand, bool> predicate = IsSampleCommand;
```

이 예제에서:
- `IsSampleCommand`는 `IBerthCommand`를 입력으로 받아 그것이 `SampleCommand` 타입인지 확인하는 메서드입니다.
- `Func<IBerthCommand, bool> predicate = IsSampleCommand;`은 이 메서드를 `predicate` 델리게이트에 할당합니다.

### 실제 사용 예

`UndoSpecificCommand` 메서드 내에서:

```csharp
public void UndoSpecificCommand(Func<IBerthCommand, bool> predicate, object parameter)
{
    Stack<IBerthCommand> tempStack = new Stack<IBerthCommand>();
    IBerthCommand targetCommand = null;

    while (_undoStack.Count > 0)
    {
        IBerthCommand command = _undoStack.Pop();
        if (predicate(command))
        {
            targetCommand = command;
            break;
        }
        tempStack.Push(command);
    }

    if (targetCommand != null)
    {
        targetCommand.Undo(parameter);
        _redoStack.Push(targetCommand);
    }

    while (tempStack.Count > 0)
    {
        _undoStack.Push(tempStack.Pop());
    }
}
```

이 메서드에서는:
- 특정 조건을 정의하는 함수(`predicate`)를 전달하여 스택에서 명령을 찾습니다.
- 메서드는 스택의 각 명령을 `predicate`로 검사하여 조건에 맞는지 확인합니다.
- 일치하는 명령을 찾으면 그 명령을 `Undo`하고 `_redoStack`으로 이동시킵니다.

### 초기 학습 필요 사항

`Func<...>` 델리게이트와 predicate를 사용하는 데 익숙해지기 위해서는 다음과 같은 개념을 학습해야 합니다:

#### 델리게이트
- C#에서 [[temp/델리게이트 in CSharp|델리게이트]]가 무엇인지 이해합니다.
- 메서드를 전달하기 위해 델리게이트를 생성하고 사용하는 방법을 학습합니다.

#### 제네릭 델리게이트 (`Func`, `Action`, `Predicate`)
- `Func<...>`: 값을 반환하는 메서드를 나타냅니다.
- `Action<...>`: 값을 반환하지 않는 메서드를 나타냅니다.
- `Predicate<...>`: 항상 `bool`을 반환하는 `Func`의 특수한 버전입니다.

#### 람다 표현식
- 람다 표현식은 인라인 함수(간단한 함수)를 생성하는 간결한 방법을 제공합니다.
- 람다는 `Func` 및 `Action`과 같은 델리게이트와 함께 자주 사용됩니다.

### 요약

h3 `Func<IBerthCommand, bool>` 이해하기
h6 `Func<IBerthCommand, bool>`란?
이것은 `IBerthCommand`를 입력으로 받아 `bool`을 반환하는 메서드를 가리키는 델리게이트입니다.
h6 Predicate 사용하기
Predicate는 `bool`을 반환하는 함수로, 조건을 테스트하는 데 자주 사용됩니다.
h6 Predicate 만들기
Predicate 함수를 생성하여 `UndoSpecificCommand`와 같은 메서드에 인수로 전달할 수 있습니다.
h6 실제 예제
Predicate를 구현하고 특정 명령을 스택에서 찾는 방법을 설명하는 실제 예제입니다.
h6 델리게이트와 Predicate 학습하기
델리게이트, `Func`, `Action`, `Predicate` 및 람다 표현식에 익숙해져야 합니다.

Q1 : 람다 표현식이 C#에서 Predicate를 만드는 과정을 어떻게 간소화할 수 있을까요?
Q2 : 일상적인 프로그래밍 작업에서 델리게이트와 Predicate의 실용적인 사용 사례는 무엇일까요?


