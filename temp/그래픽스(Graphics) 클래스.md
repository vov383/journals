---
title: 그래픽스(Graphics) 클래스
created: 2024-03-12 10:02
alias:
tags:
---
###### System.Drawing 네임스페이스
Windows Forms 응용 프로그램에서 그래픽을 그리고 조작하는 데 사용됩니다.

###### Graphics 클래스
그림 그리기와 관련된 메서드 및 속성을 제공합니다. 
이를 사용하여 선, 원, 사각형 등의 도형을 그리고 이미지를 조작할 수 있습니다.

###### Pen 클래스
선의 속성을 정의합니다. 
선의 색상, 두께 및 스타일을 설정하여 
Graphics 객체에 그릴 선을 정의할 수 있습니다.

###### Brush 클래스
도형을 채우는 데 사용됩니다. 
색상, 그라데이션, 패턴 등을 설정하여 도형을 채울 수 있습니다.

###### Font 클래스
텍스트를 그리는 데 사용됩니다. 
텍스트의 글꼴, 크기 및 스타일을 설정하여 
Graphics 객체에 텍스트를 추가할 수 있습니다.

###### 사용 예시
```csharp
using System.Drawing;
using System.Windows.Forms;

namespace WinFormsGraphicsExample
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Paint(object sender, PaintEventArgs e)
        {
            Graphics graphics = e.Graphics;

            // 선 그리기
            Pen pen = new Pen(Color.Red, 2);
            graphics.DrawLine(pen, 10, 10, 100, 100);

            // 원 그리기
            Brush brush = new SolidBrush(Color.Blue);
            graphics.FillEllipse(brush, 120, 10, 80, 80);

            // 사각형 그리기
            graphics.FillRectangle(Brushes.Green, 220, 10, 100, 50);

            // 텍스트 그리기
            Font font = new Font("Arial", 12, FontStyle.Bold);
            graphics.DrawString("Hello, WinForms!", font, Brushes.Black, 10, 150);
        }
    }
}
```
