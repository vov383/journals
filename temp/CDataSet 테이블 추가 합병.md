---
title: CDataSet 테이블 추가 합병
created: 2024-03-04 02:11
alias:
tags:
---
두 DataSet 객체가 서로 다른 테이블들을 가지고 있을 때 Merge()를 실행하면, Merge()를 호출하는 DataSet 객체안으로 다른 DataSet에 있는 테이블들을 추가 복제하여 병합할 수 있다. 아래 예는 첫번째 DataSet객체에는 authors 테이블을 읽어 오고, 두번째 DataSet에는 titles과 employee 2개의 테이블들을 가져온다. 이후 첫번째 DataSet객체에 Merge()를 실행하여 두번째 DataSet의 2개의 테이블을 추가 합병하게되어 첫번째 DataSet은 총 3개의 DataTable을 갖게된다.
```cs
DataSet ds1 = new DataSet();
DataSet ds2 = new DataSet();
string strConn1 = "Data Source=(local);Initial catalog=pubs;Integrated Security=SSPI;";

// ds1 에는 authors 테이블
string sql = "SELECT * FROM authors";

SqlDataAdapter adpt1 = new SqlDataAdapter(sql, strConn1);
adpt1.MissingSchemaAction = MissingSchemaAction.AddWithKey;
adpt1.Fill(ds1); 
adpt1.Dispose();

// ds2 에는 titles 테이블과 employee 테이블 2개
sql = "SELECT * FROM titles; SELECT * FROM employee";

SqlDataAdapter adpt2 = new SqlDataAdapter(sql, strConn1);
adpt2.MissingSchemaAction = MissingSchemaAction.AddWithKey;
adpt2.Fill(ds2); 
adpt2.Dispose();

// ds2의 두 테이블을 ds1으로 병합
ds1.Merge(ds2);

// 병합 후 ds1에는 총 3개의 테이블이 존재
foreach (DataRow r in ds1.Tables[0].Rows)
{
    Console.WriteLine(r[0]);
}
foreach (DataRow r in ds1.Tables[1].Rows)
{
    Console.WriteLine(r[0]);
}
foreach (DataRow r in ds1.Tables[2].Rows)
{
    Console.WriteLine(r[0]);
}
```


