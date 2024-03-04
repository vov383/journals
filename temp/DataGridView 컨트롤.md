---
title: DataGridView 컨트롤
created: 2024-02-23 16:28
aliases: 
tags:
---
WinForms 에서 기본적으로 제공하는 그리드 컨트롤로서 DataGridView 컨트롤이 있다. 
이 그리드 컨트롤은 테이블 형태의 데이타를 화면에 뿌려주는데 사용하는데, 데이타를 데이타소스와 바인딩해서 사용하는 Binding 모드와 데이타를 개발자가 수동으로 갱신해주는 Unbound 모드가 있다. 
많은 개발 환경에서 바인딩 모드를 자주 사용하지만, 어떤 모드로 사용할 지는 개발자가 시스템 요구사항을 보고 결정한다. 
Binding 모드에서는 **DataSource 속성**을 테이블등의 소스에 설정하여 바인딩을 하게 되며, 
Unbound 모드에서는 **Rows 컬렉션**을 수동으로 갱신함으로써 데이타를 핸들링하게 된다



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

