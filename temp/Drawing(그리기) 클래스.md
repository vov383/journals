---
title: Drawing(그리기) 클래스
created: 2024-03-12 10:04
alias:
tags:
---
System.Drawing 네임스페이스에는 그래픽을 생성하고 조작하는 데 사용되는 여러 클래스가 있습니다. 
이 중 주요 클래스는 Graphics와 Bitmap입니다.

###### Graphics 클래스 

Graphics 클래스는 그래픽을 그리고 조작하는 데 사용됩니다. 
그래픽 디바이스 컨텍스트를 나타내며, 선, 도형, 텍스트 등을 화면이나 이미지에 그릴 수 있는 메서드를 제공합니다. 
이 클래스는 보통 Windows Forms 또는 GDI+ 기반 응용 프로그램에서 사용됩니다.
[[그래픽스(Graphics) 클래스]]
###### Bitmap 클래스

Bitmap 클래스는 이미지를 표현하고 처리하는 데 사용됩니다. 
비트맵 이미지를 생성하고 픽셀 수준에서 이미지를 수정하는 데 사용됩니다. 
이 클래스는 메모리 내에서 이미지를 로드하고 조작할 수 있는 기능을 제공하여 그래픽 작업에 유용합니다.

###### 예시 코드

```csharp
using System.Drawing;
using System.Windows.Forms;

namespace DrawingExample
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Paint(object sender, PaintEventArgs e)
        {
            // Graphics를 사용하여 선과 도형을 그리기
            Graphics graphics = e.Graphics;
            Pen pen = new Pen(Color.Red, 2);
            graphics.DrawLine(pen, 10, 10, 100, 100);
            graphics.FillEllipse(Brushes.Blue, 120, 10, 80, 80);

            // Bitmap을 사용하여 이미지 처리하기
            Bitmap bitmap = new Bitmap(200, 200);
            using (Graphics bitmapGraphics = Graphics.FromImage(bitmap))
            {
                bitmapGraphics.FillRectangle(Brushes.Green, 0, 0, 200, 200);
                bitmapGraphics.DrawString("Hello, Bitmap!", new Font("Arial", 12), Brushes.Black, new PointF(10, 10));
            }
            // 이미지를 PictureBox에 표시
            pictureBox1.Image = bitmap;
        }
    }
}
```
