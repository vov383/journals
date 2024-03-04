---
title: DataView 클래스
created: 2024-03-04 01:30
alias:
tags:
---
DataView 클래스는 DaCSharp CSharp taTable객체를 소트하거나 필터링할 때 혹은 편집, 검색등을 할 때 사용된다. 즉, 만약 서버로부터 데이타를 가져다 클라인언트에 놓고 일부 데이타만 보여주는 필터링 혹은 데이타를 소트해서 보여주는 등의 일들을 할 때는 DataView를 사용할 수 있다. 
**DataTable은 기본적으로 DefaultView라고 하는 속성을 가지고 있는데, 이는 DataTable에서 기본으로 제공하는 DataView로서 이를 통해 소트나 필터링** 등을 할 수 있다.
```cs
DataSet ds = new DataSet();

using (SqlConnection conn = new SqlConnection(cn))
{
   conn.Open();
   SqlDataAdapter adpt = new SqlDataAdapter("SELECT * FROM AAA", conn);
   adpt.Fill(ds, "AAA");
}

// DataTable.DefaultView를 사용하여
// 필터링 (name컬럼이 L로 시직하는 경우)
DataTable dt = ds.Tables["AAA"];
dt.DefaultView.RowFilter = "name like 'L%'";

dataGridView1.DataSource = dt;
```


