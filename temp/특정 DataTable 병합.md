---
title: 특정 DataTable 병합
created: 2024-03-04 02:37
alias:
tags:
---
특정 DataTable을 병합하는 경우 해당 DataTable 객체에서 Merge()메서드를 호출하여 다른 테이블을 병합하게 된다. 
아래의 예처럼 하나의 데이타베이스 안에 동일한 구조를 가진 두 개의 테이블이 있는 경우, 이를 병합하기 위해 하나의 DataSet에 두 개의 DataTable을 생성하고 이를 한쪽으로 Merge할 수 있다.
```cs
DataSet ds1 = new DataSet();
string strConn2 = "Data Source=(local);Initial catalog=pubs2;Integrated Security=SSPI;";

// authors 테이블을 authors1 DataTable에 채움
string sql = "SELECT * FROM authors";
SqlDataAdapter adpt = new SqlDataAdapter(sql, strConn2);
adpt.MissingSchemaAction = MissingSchemaAction.AddWithKey;
adpt.Fill(ds1, "authors1"); 

// authors2 테이블을 authors2 DataTable에 채움
sql = "SELECT * FROM authors2";
adpt = new SqlDataAdapter(sql, strConn2);
adpt.MissingSchemaAction = MissingSchemaAction.AddWithKey;
adpt.Fill(ds1, "authors2");

// authors2 DataTable을 authors1 DataTable에 병합
ds1.Tables["authors1"].Merge(ds1.Tables["authors2"]);

foreach (DataRow r in ds1.Tables["authors1"].Rows)
{
    Console.WriteLine("{0}: {1} {2}", r[0], r[1], r[2]);
}
```


