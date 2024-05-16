---
title: sender 파라미터 in WinForm 이벤트
created: 2024-05-16 11:14
alias:
tags:
---
`sender` 파라미터는 이벤트가 발생한 객체를 나타냅니다. 
이를 통해 이벤트가 발생한 컨트롤에 접근할 수 있습니다.

```csharp
private void SomeEventHandler(object sender, EventArgs e)
{
    // 이벤트가 발생한 컨트롤을 가져옵니다.
    Control control = sender as Control;

    if (control != null)
    {
        // 이벤트가 발생한 컨트롤의 이름을 확인합니다.
        string controlName = control.Name;
        MessageBox.Show($"Event triggered by: {controlName}");
    }
}
```


