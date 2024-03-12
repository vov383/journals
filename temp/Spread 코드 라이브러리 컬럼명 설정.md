---
title: Spread 코드 라이브러리 컬럼명 설정
created: 2024-03-12 02:12
alias:
tags:
---
컬럼명 배열을 선언하고 컬럼인덱스, 컬럼명, width, visible을 설정하는 코드
```cs
string[] column_names = { "mw_cd", "ul_cd", "name",
    "day1a", "day1b",
    "day2a", "day2b",
    "day3a", "day3b",
    "day4a", "day4b",
    "day5a", "day5b",
    "day6a", "day6b",
    "day7a", "day7b" };
for (int i = 0; i < column_names.Length; i++)
{
    if (column_names[i] == "mw_cd")
        _comSpread.ColumnSet(i, column_names[i], 100, true);
    else if (column_names[i] == "ul_cd")
        _comSpread.ColumnSet(i, column_names[i], 100, true);
    else if (column_names[i] == "name")
        _comSpread.ColumnSet(i, column_names[i], 100, true);
    else
        _comSpread.ColumnSet(i, column_names[i], 110, true);
}

public void ColumnSet(int columnIndex, string columnName, int width, bool isVisible)
{
    fs.Sheets[0].ColumnHeader.Cells[0, columnIndex].Tag = columnName;
    fs.Sheets[0].Columns.Get(columnIndex).Tag = columnName;
    fs.Sheets[0].Columns[columnIndex].Tag = columnName;

    //fs.Sheets[0].Columns.Get(idx).Label = headerText;
    fs.Sheets[0].Columns.Get(columnIndex).Width = width;
    fs.Sheets[0].Columns.Get(columnIndex).Visible = isVisible;            
}
```


