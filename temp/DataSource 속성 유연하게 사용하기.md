---
title: DataSource 속성 유연하게 사용하기
created: 2024-02-23 04:11
alias:
tags:
---
`DataGridView`의 `DataSource` 속성을 사용하면서도 
커스텀 셀 및 로우 스타일링, 이벤트 처리를 통해 유연성을 높이는 방법에는 여러 가지가 있습니다. 

# 셀 및 로우 스타일링

## 조건부 셀 스타일링

`DataGridView`의 `CellFormatting` 이벤트를 사용하여 조건에 따라 셀의 스타일을 동적으로 변경할 수 있습니다. 
예를 들어, 특정 조건을 만족하는 셀의 배경색이나 글꼴을 변경할 수 있습니다.

```csharp
private void dataGridView1_CellFormatting(object sender, DataGridViewCellFormattingEventArgs e)
{
    // 특정 컬럼("age" 컬럼 가정)의 셀 값에 따라 배경색 변경
    if (dataGridView1.Columns[e.ColumnIndex].Name == "age")
    {
        int age = Convert.ToInt32(e.Value);
        if (age > 50)
        {
            e.CellStyle.BackColor = Color.LightPink;
        }
        else
        {
            e.CellStyle.BackColor = Color.LightGreen;
        }
    }
}
```

## 로우 스타일링

로우의 데이터에 따라 전체 로우의 스타일을 변경하고 싶을 때는 `RowPostPaint` 이벤트를 사용할 수 있습니다.

```csharp
private void dataGridView1_RowPostPaint(object sender, DataGridViewRowPostPaintEventArgs e)
{
    var row = dataGridView1.Rows[e.RowIndex];
    if (row.Cells["gender"].Value.ToString() == "여자")
    {
        row.DefaultCellStyle.BackColor = Color.LightYellow;
    }
    else
    {
        row.DefaultCellStyle.BackColor = Color.LightBlue;
    }
}
```

# 이벤트 처리를 통한 데이터 조작

## 셀 클릭 이벤트

셀을 클릭했을 때 특정 동작을 수행하려면 `CellClick` 이벤트를 사용합니다. 예를 들어, 셀을 클릭하면 해당 셀의 정보를 다른 컨트롤에 표시할 수 있습니다.

```csharp
private void dataGridView1_CellClick(object sender, DataGridViewCellEventArgs e)
{
    // 클릭된 셀의 정보를 TextBox에 표시
    var cellValue = dataGridView1.Rows[e.RowIndex].Cells[e.ColumnIndex].Value.ToString();
    textBox1.Text = cellValue;
}
```

# 추가적인 사용자 정의 기능

`DataGridView`의 `CellPainting` 이벤트를 사용하면 셀을 그리는 방식을 완전히 사용자 정의할 수 있습니다. 예를 들어, 셀에 아이콘을 추가하거나, 텍스트 대신 그래픽을 표시할 수 있습니다.

이러한 기능들을 활용하면 `DataSource` 방식으로 데이터를 바인딩하면서도, 특정 셀이나 로우에 대한 세밀한 제어가 가능해져, 사용자 인터페이스의 유연성과 사용자 경험을 크게 향상시킬 수 있습니다.


[[DataGridView 컨트롤]]