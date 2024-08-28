---
title: INotifyPropertyChanged 이해하기
created: 2024-08-28 09:02
alias:
tags:
---
`INotifyPropertyChanged`와 MVVM 패턴을 처음 배우고 사용하는 것은 약간의 학습 곡선을 동반할 수 있습니다. 특히 WinForms 환경에서 이러한 개념을 도입할 때, 처음에는 다소 복잡하게 느껴질 수 있습니다. 하지만 이 학습 과정을 통해 데이터 바인딩과 UI 업데이트를 자동화하고, 코드를 더 깔끔하고 유지보수하기 쉽게 만들 수 있습니다.

아래에서는 `INotifyPropertyChanged`를 배우고 사용하는 데 필요한 초기 학습 내용을 간단하게 정리했습니다.

### 1. **INotifyPropertyChanged 이해하기**

#### 1.1 **기본 개념**

`INotifyPropertyChanged`는 C#에서 데이터 바인딩을 지원하는 인터페이스입니다. 이 인터페이스를 구현하면, 속성(Property)의 값이 변경될 때 `PropertyChanged` 이벤트가 발생하여 UI에 자동으로 그 변경 사항을 반영할 수 있습니다.

#### 1.2 **인터페이스 선언**

```csharp
public interface INotifyPropertyChanged
{
    event PropertyChangedEventHandler PropertyChanged;
}
```

- `PropertyChanged` 이벤트: 이 이벤트는 속성 값이 변경될 때 발생하며, UI나 다른 바인딩 대상이 변경을 감지할 수 있도록 합니다.

#### 1.3 **이벤트 호출**

속성이 변경될 때마다 `OnPropertyChanged` 메서드를 호출하여 `PropertyChanged` 이벤트를 발생시킵니다.

```csharp
protected virtual void OnPropertyChanged(string propertyName)
{
    PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
}
```

### 2. **INotifyPropertyChanged를 사용하는 이유**

#### 2.1 **자동 UI 업데이트**
- 속성 변경 시 UI가 자동으로 업데이트됩니다. 예를 들어, 사용자가 텍스트 박스에 입력한 값이 ViewModel의 속성에 바인딩되어 있고, 그 속성이 변경되면 UI가 자동으로 갱신됩니다.

#### 2.2 **MVVM 패턴 지원**
- MVVM 패턴에서 ViewModel은 모델과 UI 간의 중재 역할을 하며, `INotifyPropertyChanged`는 이 과정에서 중요한 역할을 합니다. 이 인터페이스를 통해 ViewModel이 UI와 효과적으로 상호작용할 수 있습니다.

### 3. **INotifyPropertyChanged의 기본 구현**

#### 3.1 **클래스에 인터페이스 구현하기**

먼저, ViewModel 또는 데이터 바인딩에 사용할 클래스에 `INotifyPropertyChanged` 인터페이스를 구현합니다.

```csharp
public class MyViewModel : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;

    protected virtual void OnPropertyChanged(string propertyName)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }

    private string _name;
    public string Name
    {
        get { return _name; }
        set
        {
            if (_name != value)
            {
                _name = value;
                OnPropertyChanged(nameof(Name)); // Name 속성 변경 시 알림
            }
        }
    }
}
```

#### 3.2 **데이터 바인딩**

WinForms에서 ViewModel과 UI 요소를 데이터 바인딩합니다.

```csharp
public partial class MainForm : Form
{
    private MyViewModel _viewModel;

    public MainForm()
    {
        InitializeComponent();

        _viewModel = new MyViewModel();
        textBoxName.DataBindings.Add("Text", _viewModel, nameof(_viewModel.Name), true, DataSourceUpdateMode.OnPropertyChanged);
    }
}
```

이렇게 하면, `Name` 속성이 변경될 때 `textBoxName`에 자동으로 반영됩니다.

### 4. **실습 예제**

1. **간단한 ViewModel 생성**: ViewModel 클래스를 만들고, `INotifyPropertyChanged`를 구현하여 속성 변경 시 알림을 발생시킵니다.
2. **WinForms 데이터 바인딩**: ViewModel의 속성을 WinForms의 컨트롤에 바인딩합니다. 예를 들어, 텍스트 박스나 레이블에 바인딩하여 ViewModel의 값이 변경될 때 UI에 반영되도록 합니다.
3. **속성 변경 감지**: UI에서 데이터를 변경하거나 ViewModel의 속성을 변경하여, 자동으로 UI가 갱신되는지 확인합니다.

### 5. **추가 학습**

#### 5.1 **MVVM 패턴의 개념**
- `INotifyPropertyChanged`는 MVVM 패턴의 일부로 사용됩니다. MVVM 패턴에 익숙해지면, ViewModel과 View 간의 상호작용이 더 명확해지고, 코드의 유지보수성과 확장성이 향상됩니다.

#### 5.2 **데이터 바인딩 및 이벤트 처리**
- 데이터 바인딩을 이해하고, 이벤트 처리와 `INotifyPropertyChanged`의 역할을 배우는 것이 중요합니다.

### 결론

- **INotifyPropertyChanged의 학습**: 처음에는 다소 복잡할 수 있지만, 데이터 바인딩을 자동화하고 MVVM 패턴을 구현하는 데 매우 유용합니다.
- **효율적인 UI 관리**: `INotifyPropertyChanged`를 구현하면, WinForms에서 UI 관리가 더 쉽고 직관적이 됩니다.
- **단계적 학습**: 기본적인 구현에서 시작하여, 점차 MVVM 패턴과 더 복잡한 데이터 바인딩 시나리오로 확장할 수 있습니다.

이러한 학습 과정을 통해 `INotifyPropertyChanged`와 MVVM 패턴을 효과적으로 활용할 수 있게 되며, WinForms 애플리케이션의 구조를 개선할 수 있습니다.


