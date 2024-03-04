---
title: DataSet in CSharp
created: 2024-03-04 13:23
aliases: 
tags:
---
###### C# DataSet 클래스  
DataSet 클래스는 클라이언트 메모리 상에 존재하는 테이블들을 가지며, 서버와의 연결을 유지하지 않는다. 
DataSet 클래스는 개발자가 직접 모든 테이블 구조 만들고 데이타 삽입등을 할 수 있으나, 
일반적으로 DataAdapter를 이용하여 데이타를 서버로부터 가져와 메모리상의 DataSet에 할당 후 사용한다. 
DataSet 객체는 DataGridView같은 그리드에 데이타를 바인딩하여 사용할 수 있다.
```cs
SqlConnection conn = new SqlConnection(strConn);
conn.Open();
SqlDataAdapter adapter = new SqlDataAdapter("SELECT * FROM Tab1", conn);

// DataSet에 테이블 데이타를 넣음
DataSet ds = new DataSet();
adapter.Fill(ds, "Tab1");        

conn.Close();
```

###### DataView 클래스
![[journals/temp/DataView 클래스]]

###### c DataTable 클래스
![[DataTable 클래스]]

###### DataSet 테이블 병합(Merge)
![[journals/temp/DataSet 테이블 병합(Merge)]]


###### CDataSet 테이블 추가 합병
![[journals/temp/CDataSet 테이블 추가 합병]]

###### 특정 DataTable 병합
![[journals/temp/특정 DataTable 병합]]
