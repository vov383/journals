---
title: Pen과 Brush 클래스의 차이
created: 2024-03-12 10:06
alias:
tags:
---
###### Pen 클래스
- Pen 클래스는 선을 그릴 때 사용됩니다.
- 선의 속성을 설정하여 선의 색상, 두께 및 스타일을 조절할 수 있습니다.
- 주로 선을 그릴 때 사용되며, 도형의 외곽선을 그릴 때 유용합니다.

###### Brush 클래스
- Brush 클래스는 도형 내부를 채울 때 사용됩니다.
- 도형의 내부를 채우는 데 사용되며, 색상, 그라데이션, 패턴 등을 설정하여 도형을 채울 수 있습니다.
- 선이 아닌 도형의 내부를 채울 때 사용됩니다.

###### 예시

```csharp
using System.Drawing;
using System.Windows.Forms;

namespace PenVsBrushExample
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

            // Pen을 사용하여 선 그리기
            Pen pen = new Pen(Color.Red, 2);
            graphics.DrawLine(pen, 10, 10, 100, 100);

            // Brush를 사용하여 사각형 내부 채우기
            Brush brush = new SolidBrush(Color.Blue);
            graphics.FillRectangle(brush, 120, 10, 80, 80);
        }
    }
}
```

이 예시에서는 Pen 클래스를 사용하여 빨간색 선을 그리고, Brush 클래스를 사용하여 파란색 사각형을 채웠습니다.


