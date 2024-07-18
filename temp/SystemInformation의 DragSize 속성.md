---
title: SystemInformation의 DragSize 속성
created: 2024-07-18 10:58
alias:
tags:
---
#### 설명
`SystemInformation.DragSize`는 사용자가 드래그 작업을 시작할 때 필요한 마우스 이동 거리(픽셀 단위)를 나타내는 `Size` 구조체입니다. 이 구조체에는 드래그 작업을 시작하기 위한 최소한의 너비(`Width`)와 높이(`Height`)가 포함됩니다. 

#### 용도
이 속성은 사용자가 의도하지 않은 드래그 작업을 시작하지 않도록 하기 위해 사용됩니다. 예를 들어, 사용자가 마우스를 약간 움직였을 때 드래그가 시작되지 않도록 하는데 유용합니다. 

`SystemInformation.DragSize.Width`는 드래그 작업을 시작하기 위해 마우스가 이동해야 하는 최소 거리를 가로 방향으로 측정한 값입니다. `SystemInformation.DragSize.Height`는 세로 방향의 최소 거리를 나타냅니다.

#### 예제
드래그 작업을 시작하기 위해 마우스가 이동해야 하는 최소 거리를 계산하는 예제입니다.

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;

public class DragExample : Form
{
    private bool isMouseDown = false;
    private Point initialMousePosition;

    public DragExample()
    {
        this.MouseDown += new MouseEventHandler(Form_MouseDown);
        this.MouseMove += new MouseEventHandler(Form_MouseMove);
    }

    private void Form_MouseDown(object sender, MouseEventArgs e)
    {
        if (e.Button == MouseButtons.Left)
        {
            isMouseDown = true;
            initialMousePosition = e.Location;
        }
    }

    private void Form_MouseMove(object sender, MouseEventArgs e)
    {
        if (isMouseDown)
        {
            int distanceX = Math.Abs(e.Location.X - initialMousePosition.X);
            int distanceY = Math.Abs(e.Location.Y - initialMousePosition.Y);

            if (distanceX >= SystemInformation.DragSize.Width ||
                distanceY >= SystemInformation.DragSize.Height)
            {
                isMouseDown = false;
                StartDrag();
            }
        }
    }

    private void StartDrag()
    {
        DataObject dataObject = new DataObject();
        // 예제 데이터 추가
        dataObject.SetData("ExampleData", "Drag started");

        this.DoDragDrop(dataObject, DragDropEffects.Copy);
    }

    [STAThread]
    public static void Main()
    {
        Application.Run(new DragExample());
    }
}
```

#### 요약
1. `SystemInformation.DragSize`는 사용자가 드래그를 시작하기 위해 마우스를 이동해야 하는 최소 거리를 정의합니다.
2. `Size` 구조체로 너비(`Width`)와 높이(`Height`) 값을 포함합니다.
3. 의도하지 않은 드래그 작업을 방지하는 데 유용합니다.
4. 코드 예제는 최소 거리 이동 후 드래그를 시작하는 방법을 보여줍니다.


