---
title: Delegate와 Action에 대한 기초 이해
created: 2024-08-26 02:25
alias:
tags:
---
#### 1. **Delegate란 무엇인가?**

###### Delegate**
델리게이트는 `C#`에서 메서드를 참조하는 형식으로, 
다른 언어의 함수 포인터와 유사합니다. 
Delegate를 사용하면 메서드를 변수처럼 다룰 수 있으며, 
메서드를 매개변수로 전달하거나 
런타임에 실행할 메서드를 동적으로 지정할 수 있습니다.

##### Delegate의 기본 사용법:

```csharp
// 1. Delegate 선언
public delegate void MyDelegate(string message);

// 2. 메서드 정의 (Delegate와 같은 시그니처)
public void ShowMessage(string message)
{
    Console.WriteLine(message);
}

// 3. Delegate 인스턴스 생성 및 메서드 참조
MyDelegate del = new MyDelegate(ShowMessage);

// 4. Delegate 호출
del("Hello, Delegate!");
```

이 예제에서 `MyDelegate`는 `string`을 매개변수로 받고 `void`를 반환하는 메서드를 참조할 수 있는 형식입니다. `ShowMessage` 메서드는 해당 시그니처와 일치하므로, 이 메서드를 `MyDelegate` 인스턴스에 할당하고 호출할 수 있습니다.

#### 2. **Action이란 무엇인가?**

###### Action
액션은 `Delegate`의 특수한 형태로, 
**반환 값이 없는 메서드**를 참조하는 데 사용됩니다. 
Action은 미리 정의된 Delegate로, 여러 가지 오버로드가 제공됩니다.

- **`Action`**: 매개변수가 없는 메서드를 참조할 때 사용합니다.
- **`Action<T>`**: 매개변수 한 개를 가지는 메서드를 참조할 때 사용합니다.
- **`Action<T1, T2>`**: 매개변수 두 개를 가지는 메서드를 참조할 때 사용합니다.
- ...

##### Action의 사용 예:

```csharp
// 1. Action 선언 및 메서드 참조
Action<string> action = ShowMessage;

// 2. Action 호출
action("Hello, Action!");
```

위의 예에서 `Action<string>`은 `string`을 매개변수로 받고 반환 값이 없는 메서드를 참조할 수 있습니다. `ShowMessage` 메서드는 이러한 시그니처에 맞기 때문에 `Action<string>`에 할당하고 실행할 수 있습니다.

#### 3. **DelegateCommand란?**

**DelegateCommand**는 WPF 및 MVVM 패턴에서 자주 사용되는 패턴으로, `ICommand` 인터페이스를 구현하는 Command 패턴의 일종입니다. 이를 통해 메서드를 인라인으로 지정할 수 있습니다. `DelegateCommand`를 사용하면 특정 메서드의 실행 로직과 실행 가능 여부를 동적으로 정의할 수 있습니다.

##### DelegateCommand 구현 예시:

```csharp
public class DelegateCommand : ICommand
{
    private readonly Action<object> _execute;
    private readonly Func<object, bool> _canExecute;

    // 생성자: 실행할 메서드와 실행 가능 여부를 판단하는 메서드를 받아들입니다.
    public DelegateCommand(Action<object> execute, Func<object, bool> canExecute = null)
    {
        _execute = execute ?? throw new ArgumentNullException(nameof(execute));
        _canExecute = canExecute;
    }

    // 실행 가능 여부를 반환하는 메서드
    public bool CanExecute(object parameter)
    {
        return _canExecute == null || _canExecute(parameter);
    }

    // 실제 메서드를 실행하는 메서드
    public void Execute(object parameter)
    {
        _execute(parameter);
    }

    // CanExecuteChanged 이벤트는 ICommand의 요구 사항이지만, 실제로 자주 사용되지는 않습니다.
    public event EventHandler CanExecuteChanged;
}
```

#### 4. **Delegate와 Action의 차이점 및 사용 시기**

- **Delegate**: 사용자 정의 메서드 서명을 만들고, 이 서명에 맞는 메서드를 참조하는 형식을 직접 정의하고 싶을 때 사용합니다. Delegate를 정의하면 매우 유연한 구조로 메서드 참조를 관리할 수 있습니다.
  
- **Action**: 반환 값이 필요 없는 간단한 메서드를 참조할 때 사용합니다. 별도의 Delegate를 정의할 필요 없이, C#에서 미리 정의된 형식을 사용할 수 있기 때문에 코드가 간결해집니다.

### 결론

- **Delegate**는 메서드를 참조할 수 있는 형식이며, 복잡한 시나리오에서 유연하게 사용됩니다.
- **Action**은 Delegate의 특수한 형태로, 반환 값이 없는 메서드를 참조할 때 간편하게 사용할 수 있습니다.
- **DelegateCommand**는 MVVM 패턴에서 자주 사용되며, 실행할 메서드를 인라인으로 정의할 수 있어 코드의 가독성과 관리성을 높입니다.

Q1: Delegate와 Action을 사용하여 동일한 동작을 구현할 때, 어떤 경우에 Delegate를 선택하고 어떤 경우에 Action을 선택하는 것이 더 적합할까요?
Q2: DelegateCommand와 같은 구조를 사용하지 않고도 커맨드 패턴을 구현할 수 있는 방법은 무엇이 있을까요?

#### 요약
1. **Delegate**는 메서드를 참조할 수 있는 형식을 정의합니다.
2. **Action**은 반환 값이 없는 메서드를 참조하는 미리 정의된 Delegate입니다.
3. **DelegateCommand**는 WPF 및 MVVM 패턴에서 자주 사용되는 패턴입니다.
4. Delegate와 Action은 유사하지만 사용 시나리오에 따라 선택할 수 있습니다.
5. **DelegateCommand**는 Command 패턴의 구현으로, 동적인 메서드 실행이 가능하게 해줍니다.
6. 코드의 가독성, 재사용성, 유지보수성을 높이기 위해 Delegate와 Action을 적절히 사용합니다.
