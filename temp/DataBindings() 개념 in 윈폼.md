---
title: DataBindings() 개념 in 윈폼
created: 2024-08-28 09:08
alias:
tags:
---
WinForms에서 `DataBindings`와 `Add` 메서드는 데이터 바인딩을 설정하는 데 사용됩니다. 이 개념을 이해하면 WinForms에서 UI 요소와 데이터(또는 ViewModel)의 속성 간의 동기화를 쉽게 관리할 수 있습니다. 하지만 WinForms에서는 `Command` 바인딩이 기본적으로 지원되지 않으며, WPF에서 사용되는 기능입니다. WinForms에서는 버튼 클릭 이벤트를 커맨드에 바인딩하려면 다른 방법이 필요합니다.

### 1. **DataBindings 개요**

- **DataBindings**: WinForms 컨트롤의 속성을 데이터 소스(예: 객체의 속성, 데이터베이스의 필드)와 연결하는 방법을 제공합니다. 이를 통해 UI와 데이터 간의 동기화가 자동으로 이루어집니다.
  
- **Add() 메서드**: `DataBindings.Add()` 메서드를 사용하여 특정 컨트롤의 속성을 데이터 소스의 속성과 연결합니다.

### 2. **DataBindings 사용 예시**

가장 일반적인 사용 예는 텍스트 박스의 `Text` 속성을 ViewModel의 속성과 바인딩하는 것입니다. 예를 들어, 텍스트 박스에 입력된 값이 ViewModel의 속성에 자동으로 반영되도록 설정할 수 있습니다.

```csharp
// ViewModel 정의
public class MyViewModel : INotifyPropertyChanged
{
    private string _name;
    public string Name
    {
        get { return _name; }
        set
        {
            if (_name != value)
            {
                _name = value;
                OnPropertyChanged(nameof(Name)); // Name 속성이 변경되면 알림
            }
        }
    }

    public event PropertyChangedEventHandler PropertyChanged;

    protected virtual void OnPropertyChanged(string propertyName)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
}

// MainForm에서 ViewModel과 텍스트 박스 바인딩
public partial class MainForm : Form
{
    private MyViewModel _viewModel;

    public MainForm()
    {
        InitializeComponent();

        _viewModel = new MyViewModel();

        // 텍스트 박스의 Text 속성을 ViewModel의 Name 속성과 바인딩
        textBox1.DataBindings.Add("Text", _viewModel, nameof(_viewModel.Name), true, DataSourceUpdateMode.OnPropertyChanged);
    }
}
```

### 3. **DataBindings.Add() 설명**

`DataBindings.Add()` 메서드는 컨트롤의 특정 속성과 데이터 소스(예: ViewModel의 속성)를 연결하는 역할을 합니다.

```csharp
textBox1.DataBindings.Add("Text", _viewModel, nameof(_viewModel.Name), true, DataSourceUpdateMode.OnPropertyChanged);
```

#### 각 매개변수의 역할:
1. **"Text"**: `textBox1` 컨트롤의 `Text` 속성입니다. 이 속성은 텍스트 박스에 표시되는 텍스트를 나타냅니다.
  
2. **_viewModel**: 바인딩할 데이터 소스입니다. 이 경우, `MyViewModel` 클래스의 인스턴스입니다.

3. **nameof(_viewModel.Name)**: ViewModel의 `Name` 속성 이름입니다. `nameof` 연산자를 사용하여 문자열로 속성 이름을 가져옵니다. 이 속성은 `textBox1`의 `Text` 속성과 바인딩됩니다.

4. **true**: 데이터 바인딩의 방향을 설정합니다. 이 값이 `true`이면, 데이터 소스에서 컨트롤로의 데이터 흐름뿐만 아니라 컨트롤에서 데이터 소스로의 흐름도 지원됩니다. 즉, 사용자가 텍스트 박스에 입력한 내용이 ViewModel의 `Name` 속성에 자동으로 반영됩니다.

5. **DataSourceUpdateMode.OnPropertyChanged**: 데이터 소스의 속성 값이 변경될 때마다 데이터 바인딩이 업데이트되도록 설정합니다. 이 옵션은 `INotifyPropertyChanged`를 구현한 경우에 유용합니다.

### 4. **WinForms에서 Command와의 차이점**

WPF에서는 버튼의 `Command` 속성에 커맨드를 바인딩할 수 있지만, WinForms에서는 기본적으로 이러한 기능이 없습니다. WinForms에서 커맨드 패턴을 사용하려면 버튼의 `Click` 이벤트를 ViewModel의 커맨드 실행 메서드에 연결해야 합니다.

### 5. **WinForms에서 Command 패턴 사용**

WinForms에서 커맨드 패턴을 사용하려면, `Click` 이벤트를 ViewModel의 커맨드 실행 메서드에 수동으로 연결해야 합니다.

```csharp
public partial class MainForm : Form
{
    private MyViewModel _viewModel;

    public MainForm()
    {
        InitializeComponent();
        _viewModel = new MyViewModel();

        // 버튼 클릭 이벤트를 ViewModel의 커맨드 실행 메서드에 연결
        button1.Click += (sender, e) => _viewModel.MyCommand.Execute(null);
    }
}
```

### 6. **결론**

- **DataBindings**: WinForms에서 데이터 바인딩을 통해 UI와 데이터 모델(ViewModel)의 속성을 연결합니다.
- **Add() 메서드**: `DataBindings.Add()`를 사용하여 특정 컨트롤의 속성을 데이터 소스의 속성과 연결합니다.
- **WinForms에서 Command 바인딩**: WinForms에서는 WPF처럼 버튼의 `Command` 속성을 직접 바인딩할 수 없으므로, 버튼의 `Click` 이벤트를 ViewModel의 커맨드 메서드에 연결하는 방식으로 처리해야 합니다.

이러한 개념을 이해하면 WinForms에서 더 복잡한 UI 동작을 쉽게 관리할 수 있으며, MVVM 패턴을 부분적으로 적용할 수도 있습니다.


