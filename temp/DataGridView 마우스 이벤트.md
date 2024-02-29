---
title: DataGridView 마우스 이벤트
created: 2024-02-29 03:04
alias:
tags:
---
`DataGridView`에서 제공하는 다양한 마우스 이벤트를 사용하여, 사용자의 다양한 마우스 동작에 대응하는 기능을 구현할 수 있습니다. 
여기서는 로우 전체를 선택하도록 설정했다는 전제 하에, 마우스로 더블 클릭하면 수정하기 기능을 활성화하고, 우클릭하면 수정 또는 삭제를 선택할 수 있는 컨텍스트 메뉴를 제공하는 방법을 설명하겠습니다. 한 번 클릭하면 로우가 선택되도록 설정하는 것도 포함됩니다.

# 이벤트 비교
- **Click**: `DataGridView` 컨트롤 자체가 클릭될 때 발생합니다.
- **CellClick**: 어떤 셀이든 클릭될 때 발생합니다.
- **CellDoubleClick**: 셀이 더블 클릭될 때 발생합니다.
- **CellContentClick**: 셀 내부의 내용(텍스트나 이미지 등)을 클릭할 때 발생합니다.
- **CellContentDoubleClick**: 셀 내부의 내용이 더블 클릭될 때 발생합니다.
- **CellMouseClick**: 마우스 버튼(왼쪽, 오른쪽, 중앙)을 사용하여 셀을 클릭할 때 발생합니다. 클릭한 마우스 버튼의 종류를 구분할 수 있습니다.
- **CellMouseDown**: 셀 위에서 마우스 버튼이 눌렸을 때 발생합니다. 이 이벤트는 클릭 이벤트보다 먼저 발생하며, 마우스 버튼을 누르는 동작 자체를 캡처할 수 있습니다.
- **DoubleClick**: `DataGridView` 컨트롤 자체가 더블 클릭될 때 발생합니다.
- **MouseClick**: `DataGridView` 위의 아무 위치나 마우스로 클릭할 때 발생합니다.

# 구현 방법

## 1. 로우 전체 선택 설정
`DataGridView`의 `SelectionMode` 속성을 `FullRowSelect`로 설정하여, 로우 전체가 선택되도록 합니다.

```csharp
dataGridView1.SelectionMode = DataGridViewSelectionMode.FullRowSelect;
```

## 2. 더블 클릭으로 수정하기
`CellDoubleClick` 이벤트를 사용하여 더블 클릭 시 수정하기 기능을 활성화합니다.

```csharp
private void dataGridView1_CellDoubleClick(object sender, DataGridViewCellEventArgs e)
{
    this.btnUpdate_Click(sender, e);
}
```

## 3. 우클릭으로 수정/삭제 메뉴 제공
`CellMouseClick` 이벤트를 사용하여 우클릭 시 컨텍스트 메뉴를 표시합니다. 컨텍스트 메뉴에는 수정 및 삭제 옵션이 포함됩니다.

```csharp
private void dataGridView1_CellMouseClick(object sender, DataGridViewCellMouseEventArgs e)
{
    if (e.Button == MouseButtons.Right)
    {
        // 컨텍스트 메뉴를 생성하고 표시
        ContextMenuStrip contextMenu = new ContextMenuStrip();
        contextMenu.Items.Add("수정", null, this.btnUpdate_Click); // 수정버튼 클릭 이벤트
        contextMenu.Items.Add("삭제", null, this.btnDelete_Click); // 삭제버튼 클릭 이벤트

        // 메뉴를 마우스 위치에 표시
        var relativeMousePosition = dataGridView1.PointToClient(Cursor.Position);
        contextMenu.Show(dataGridView1, relativeMousePosition);
    }
}
```

이러한 방식으로 `DataGridView`의 다양한 이벤트를 활용하여, 사용자의 마우스 동작에 따라 적절한 기능을 구현할 수 있습니다. 이벤트를 올바르게 사용하면, 사용자에게

 직관적이고 효율적인 인터페이스를 제공하는 데 큰 도움이 됩니다.

[[MySqlDataAdapter]]
