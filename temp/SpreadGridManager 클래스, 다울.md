---
title: SpreadGridManager 클래스, 다울
created: 2024-03-12 11:26
alias:
tags:
---
###### CommSpread 클래스
![[journals/temp/CommSpread 클래스]]

###### ColumnResizeFit()
빈 컬럼을 사용해서 sheet의 빈 곳을 채워주는 역할
sheet의 viewport에서 sheet의 크기가 비어있는 곳이 안보이도록 처리
```cs
public void ColumnResizeFit(string column_name)
{
    float sum_size = 0;
    try
    {
        int index = this.GetIndexofColHeader(column_name);
        if (index < 0)
        {
            this.AddHeaderColumn(column_name, " ", 0, true);
            index = this.GetIndexofColHeader(column_name);
        }

        //VScrollBar
        SpreadVScrollBar ssb = GridView.VerticalScrollBar;
        sum_size += ssb.Bounds.Width;

        //RowHeader
        for (int i = 0; i < GridSheetView.RowHeader.ColumnCount; i++)
        {
            if (GridSheetView.RowHeader.Columns[i].Visible)
            {
                sum_size += GridSheetView.RowHeader.Columns[i].Width;
            }
        }

        //Columns
        for (int i = 0; i < GridSheetView.ColumnCount - 1; i++)
        {
            if (GridSheetView.Columns[i].Visible && i != index)
            {
                sum_size += GridSheetView.Columns[i].Width;
            }
        }

        int sgm_size = GridView.Size.Width;
        if (sgm_size - sum_size > 0)
        {
            GridSheetView.Columns[index].Width = sgm_size - sum_size;
        }
    }
    catch { }
}
```

