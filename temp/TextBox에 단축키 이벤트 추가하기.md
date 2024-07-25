---
title: TextBox에 단축키 이벤트 추가하기
created: 2024-07-25 08:07
alias:
tags:
---
Windows Forms 애플리케이션에서 TextBox에 단축키 이벤트를 추가하려면 `KeyDown` 이벤트를 사용하여 특정 키 조합을 감지하고 원하는 동작을 수행할 수 있습니다. 다음은 예제 코드입니다.

### 예제 코드
```csharp
// Form 생성자에서 TextBox와 이벤트 핸들러를 설정합니다.
public Form1()
{
    InitializeComponent();

    // TextBox를 만듭니다.
    TextBox textBox = new TextBox
    {
        Location = new Point(10, 10),
        Width = 200
    };

    // KeyDown 이벤트 핸들러를 추가합니다.
    textBox.KeyDown += TextBox_KeyDown;

    // Form에 TextBox를 추가합니다.
    this.Controls.Add(textBox);
}

// KeyDown 이벤트 핸들러
private void TextBox_KeyDown(object sender, KeyEventArgs e)
{
    // 예: Ctrl + S 단축키
    if (e.Control && e.KeyCode == Keys.S)
    {
        // 단축키가 눌렸을 때 수행할 동작을 여기에 작성합니다.
        MessageBox.Show("Ctrl + S pressed!");
        
        // 다른 키 처리를 막기 위해 이벤트를 처리했다고 표시합니다.
        e.Handled = true;
    }
    // 예: Alt + C 단축키
    else if (e.Alt && e.KeyCode == Keys.C)
    {
        // 단축키가 눌렸을 때 수행할 동작을 여기에 작성합니다.
        MessageBox.Show("Alt + C pressed!");

        // 다른 키 처리를 막기 위해 이벤트를 처리했다고 표시합니다.
        e.Handled = true;
    }
}
```

### 설명
1. **TextBox 생성 및 설정**: Form 생성자에서 TextBox를 생성하고 위치와 크기를 설정합니다.
2. **KeyDown 이벤트 핸들러 추가**: TextBox의 `KeyDown` 이벤트에 핸들러를 추가합니다.
3. **KeyDown 이벤트 핸들러 구현**: 특정 키 조합(Ctrl + S, Alt + C 등)을 감지하고, 해당 단축키가 눌렸을 때 수행할 동작을 정의합니다.
4. **이벤트 처리 표시**: `e.Handled = true;`로 설정하여 다른 키 처리를 막습니다.

### 요약
1. TextBox를 생성하고 Form에 추가합니다.
2. KeyDown 이벤트 핸들러를 추가합니다.
3. 특정 키 조합을 감지하고 원하는 동작을 수행합니다.
4. 이벤트가 처리되었음을 표시하여 다른 키 처리를 막습니다.


