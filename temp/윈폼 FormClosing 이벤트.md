---
title: 윈폼 FormClosing 이벤트
created: 2024-11-29 10:52
alias:
tags:
---
### 관련 [[dotnet WinForm]]

WinForms의 기본 `Form` 클래스에는 **`OnPopupClose`**와 같은 명시적인 이벤트는 없습니다. 하지만 **폼이 닫히는 시점**에 호출되는 이벤트는 존재하며, 이를 활용하면 팝업이 닫힐 때 특정 작업을 수행할 수 있습니다.

### 폼 닫힘 관련 이벤트

#### FormClosing 
- 폼이 닫히기 직전에 발생합니다.
- 닫힘을 취소할 수도 있습니다.
- 이 이벤트를 사용하면 닫히기 전에 작업을 수행할 수 있습니다.
#### FormClosed 
- 폼이 닫힌 후 발생합니다.
- 닫힌 이후의 후속 작업을 수행할 때 유용합니다.

---

### 코드 예제

아래는 `FormClosing` 또는 `FormClosed` 이벤트를 사용하여 `_pan_holdList`를 `null`로 설정하는 방법입니다.

```csharp
public partial class MyPopupForm : Form
{
    public MyPopupForm()
    {
        InitializeComponent();

        // FormClosing 이벤트 핸들러 등록
        this.FormClosing += MyPopupForm_FormClosing;

        // FormClosed 이벤트 핸들러 등록
        this.FormClosed += MyPopupForm_FormClosed;
    }

    // FormClosing: 닫히기 직전 호출
    private void MyPopupForm_FormClosing(object sender, FormClosingEventArgs e)
    {
        // 닫히기 직전에 작업 수행
        HoldSelectPanelFactory.ClearHoldList();
    }

    // FormClosed: 닫힌 후 호출
    private void MyPopupForm_FormClosed(object sender, FormClosedEventArgs e)
    {
        // 닫힌 후 작업 수행
        HoldSelectPanelFactory.ClearHoldList();
    }
}
```

---

### 언제 `FormClosing`과 `FormClosed`를 사용할까?

- **`FormClosing`**: 폼이 닫히기 직전에 리소스를 정리하거나 닫힘을 취소해야 할 때.
- **`FormClosed`**: 폼이 완전히 닫힌 후 후속 작업을 수행할 때.

---

### 팁

- **폼 닫힘 취소**: `FormClosing` 이벤트에서 `e.Cancel = true;`로 설정하면 폼이 닫히지 않게 할 수도 있습니다.
- **다른 리소스 해제**: 폼에서 사용하는 다른 리소스를 정리해야 한다면, `Dispose` 메서드나 `IDisposable` 구현을 고려하세요.

---

### 다른 리소스 해제 자세히
WinForms에서 폼이 닫힐 때 특정 리소스를 정리하거나 정적 필드를 초기화하려면 **`FormClosing`** 또는 **`FormClosed`** 이벤트를 활용할 수 있습니다.

### 폼 닫힘 이벤트 활용

- **`FormClosing` 이벤트**: 폼이 닫히기 직전에 발생하며, 이 시점에 리소스 정리나 특정 작업을 수행할 수 있습니다. 또한, `FormClosingEventArgs`의 `Cancel` 속성을 통해 닫힘을 취소할 수 있습니다.

- **`FormClosed` 이벤트**: 폼이 완전히 닫힌 후에 발생하며, 닫힌 이후의 후속 작업을 처리할 때 유용합니다.

### 코드 예시

아래는 `FormClosing` 이벤트를 사용하여 정적 필드를 초기화하는 방법의 예시입니다:

```csharp 
public partial class MyForm : Form { 
	public MyForm() { 
		InitializeComponent(); 
		this.FormClosing += MyForm_FormClosing; 
	 }
	private void MyForm_FormClosing(object sender, FormClosingEventArgs e)
	{
	    // 정적 필드 초기화
	    MyStaticClass.MyStaticField = null;
	}
}
```


위 코드에서 `FormClosing` 이벤트 핸들러를 통해 폼이 닫히기 직전에 정적 필드인 `MyStaticField`를 `null`로 설정하여 초기화합니다.

### 참고자료

- **리소스 해제**: 폼이 닫힐 때 사용한 리소스를 적절히 해제하지 않으면 백그라운드에서 계속 동작할 수 있으므로 주의가 필요합니다.
    [Kaizen](https://kaizen8501.tistory.com/151?utm_source=chatgpt.com)
    
- **이벤트 등록**: Visual Studio의 디자이너를 통해 폼의 이벤트를 설정할 수 있으며, 코드에서 동적으로 이벤트를 처리할 수도 있습니다.
    [Microsoft Learn](https://learn.microsoft.com/ko-kr/dotnet/desktop/winforms/controls/how-to-add-an-event-handler?view=netdesktop-9.0&utm_source=chatgpt.com)
    
- **닫힘 취소**: `FormClosing` 이벤트에서 `e.Cancel`을 `true`로 설정하면 폼의 닫힘을 취소할 수 있습니다.
    [김씨블로그](https://kimcblog.com/2017/04/26/c-winform-%EC%B0%BD-%EB%8B%AB%EA%B8%B0%EC%A2%85%EB%A3%8C-%EB%B0%A9%EC%A7%80/?utm_source=chatgpt.com)
    
- **이벤트 순서**: 폼이 닫힐 때 `FormClosing` 이벤트가 먼저 발생하고, 그 후에 `FormClosed` 이벤트가 발생합니다.
    [Nomad Programmer](https://nomad-programmer.tistory.com/229?utm_source=chatgpt.com)
    
- **리소스 정리 위치**: `Form.Load` 이벤트에서 할당한 리소스는 `FormClosed` 이벤트에서 해제하는 것이 일반적입니다.
    [Sarah The Dev](https://sarahthedev.tistory.com/58?utm_source=chatgpt.com)
    
- **이벤트 처리기 추가/제거**: 이벤트 처리기를 동적으로 추가하거나 제거할 수 있으며, 이를 통해 런타임 시 이벤트 처리를 유연하게 관리할 수 있습니다.
    [Microsoft Learn](https://learn.microsoft.com/ko-kr/dotnet/desktop/winforms/controls/how-to-add-an-event-handler?view=netdesktop-9.0&utm_source=chatgpt.com)
    
- **종료 원인 확인**: `FormClosed` 또는 `FormClosing` 이벤트를 통해 폼이 닫히는 원인을 구분할 수 있습니다.
    [춘일동안](https://chunildongan77.tistory.com/31?utm_source=chatgpt.com)