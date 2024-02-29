---
title: dotnet DataGridView
created: 2024-02-23 16:28
aliases: 
tags:
---



###### DataGridView 속성
![[journals/temp/DataGridView 속성]]


###### DataGridView 이벤트
![[journals/temp/DataGridView 이벤트]]


![[journals/temp/dataGridView에 데이터를 표시하는 두 가지 방식|dataGridView에 데이터를 표시하는 두 가지 방식]]


DataGridView의 SelectionChanged 이벤트
윈폼 주소록 에러노트
이걸 사용해서 선택된 row가 변할 때 이벤트를 넣으려고 했는데
```CSharp 
private void dataGridView1_SelectionChanged(object sender, EventArgs e)
{
    DataGridViewRow row = dataGridView1.SelectedRows[0];
    DataGridViewCell cell;
    for (int i = 0; i < row.Cells.Count; i++)
    {
        listItem.Add(row.Cells[i].Value.ToString()); // listItem에 row의 정보 11개 담아.     
    }
}
```

Form이 로드되면서 `SelectedRows[0]`가 음수가 되면서 익셉션 발생.

