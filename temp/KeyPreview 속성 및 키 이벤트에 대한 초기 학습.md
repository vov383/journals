---
title: KeyPreview 속성 및 키 이벤트에 대한 초기 학습
created: 2025-02-20 01:43
alias:
tags:
---
###### KeyPreview 속성 개요
KeyPreview 속성은 `System.Windows.Forms.Form` 클래스에서 제공되는 속성으로, 폼이 키보드 입력을 먼저 처리할지 여부를 결정합니다. 기본값은 `false`이며, 이 경우 자식 컨트롤이 키보드 입력을 우선 처리합니다. 만약 `true`로 설정하면, 폼이 자식 컨트롤보다 먼저 키 이벤트를 처리할 수 있습니다.

###### KeyPreview가 필요한 이유
폼에 여러 컨트롤이 있는 경우, 키보드 이벤트는 기본적으로 포커스를 가진 컨트롤에서 처리됩니다. 하지만, 폼 전체에서 키보드 입력에 반응해야 하는 경우(예: 단축키 처리)에는 KeyPreview를 `true`로 설정하여 폼이 키보드 이벤트를 먼저 받을 수 있게 해야 합니다.

###### KeyPreview 속성 사용 예
KeyPreview를 `true`로 설정하면, 폼에서 키다운, 키업, 키프레스와 같은 키 이벤트를 처리할 수 있습니다. 이 방식은 폼 전체에서 특정 키 입력을 처리하고자 할 때 유용합니다.

```csharp
// KeyPreview를 true로 설정하는 예시
this.KeyPreview = true;

// KeyDown 이벤트 처리 예시
private void Form1_KeyDown(object sender, KeyEventArgs e)
{
    if (e.KeyCode == Keys.Enter)
    {
        MessageBox.Show("Enter key pressed");
    }
}
```

###### KeyPreview 속성의 작동 방식
- KeyPreview가 `false`일 때: 키보드 입력은 먼저 포커스를 가진 자식 컨트롤에 전달됩니다. 예를 들어, 텍스트 박스에 포커스가 있을 경우, 입력된 키는 텍스트 박스에 의해 처리됩니다.
- KeyPreview가 `true`일 때: 폼이 먼저 키보드 입력을 처리합니다. 폼이 키 이벤트를 처리하지 않으면, 그 후 자식 컨트롤로 이벤트가 전달됩니다.



###### 키 이벤트 종류
![[journals/temp/키 이벤트 종류]]


###### KeyPreview를 사용할 때의 주의점
- 폼이 키 이벤트를 처리한 후 이벤트를 중단할지, 자식 컨트롤로 전달할지 결정해야 합니다. 이벤트 처리를 중단하려면 `e.Handled = true;`를 설정하여 자식 컨트롤로 이벤트가 전달되지 않도록 할 수 있습니다.

```csharp
// 키 이벤트를 처리하고 전파를 중단하는 예시
private void Form1_KeyDown(object sender, KeyEventArgs e)
{
    if (e.KeyCode == Keys.Enter)
    {
        MessageBox.Show("Enter key processed by the form");
        e.Handled = true;  // 자식 컨트롤로 이벤트 전달을 막음
    }
}
```

Q1 : KeyPreview가 `true`인 상태에서 키 이벤트를 폼에서 먼저 처리한 후에도 자식 컨트롤에서 키 이벤트를 처리하게 하려면 어떻게 해야 하나요?
Q2 : KeyPreview 속성이 `false`인 상황에서도 폼에서 특정 키 입력만을 받아 처리하려면 어떤 전략을 사용할 수 있을까요?
