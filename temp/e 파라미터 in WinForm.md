---
title: e 파라미터 in WinForm
created: 2024-05-16 11:14
alias:
tags:
---
`e` 파라미터는 이벤트와 관련된 추가 정보를 제공합니다. 
이벤트 유형에 따라 `e`의 타입이 다릅니다.

###### MouseEventArgs 
마우스 이벤트와 관련된 정보를 제공합니다.
###### KeyEventArgs 
키보드 이벤트와 관련된 정보를 제공합니다.
###### CellClickEventArgs 
FarPoint Spread의 셀 클릭 이벤트와 관련된 정보를 제공합니다.

```csharp
private void fpSpread1_Sheet1_CellClick(object sender, FarPoint.Win.Spread.CellClickEventArgs e)
{
    // 클릭된 셀의 행과 열 인덱스를 가져옵니다.
    int rowIndex = e.Row;
    int columnIndex = e.Column;

    // 클릭된 셀이 속한 시트를 가져옵니다.
    FarPoint.Win.Spread.SheetView sheetView = fpSpread1.ActiveSheet;

    MessageBox.Show($"Cell clicked at row {rowIndex}, column {columnIndex}");
}
```


