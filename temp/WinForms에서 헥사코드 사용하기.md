---
title: WinForms에서 헥사코드 사용하기
created: 2024-06-24 09:08
alias:
tags:
---
WinForms에서는 `System.Drawing.ColorTranslator` 클래스를 사용하여 
헥사코드를 `Color` 객체로 변환할 수 있습니다.

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;

public class MainForm : Form
{
    public MainForm()
    {
        // 헥사코드를 Color 객체로 변환
        Color color = ColorTranslator.FromHtml("#FF5733");

        // 배경색 설정
        this.BackColor = color;

        // 버튼 생성 및 설정
        Button button = new Button();
        button.Text = "Click Me";
        button.BackColor = ColorTranslator.FromHtml("#33FF57");
        button.Location = new Point(50, 50);
        
        this.Controls.Add(button);
    }

    [STAThread]
    static void Main()
    {
        Application.EnableVisualStyles();
        Application.Run(new MainForm());
    }
}
```


### 요약

#### WinForms에서의 헥사코드 사용
- `ColorTranslator.FromHtml("#헥사코드")` 사용


