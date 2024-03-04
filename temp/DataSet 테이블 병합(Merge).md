---
title: DataSet 테이블 병합(Merge)
created: 2024-03-04 02:12
alias:
tags:
---
DataSet 혹은 DataTable은 Merge() 메서드를 사용하여 다른 DataSet, DataTable 혹은 DataRow들을 병합할 수 있다. 
흔히 복수의 DataSet 객체가 있을 때 DataSet안의 데이타를 병합해야 하는 경우가 있는데, 이는 DataSet의 Merge() 메서드를 써서 해결할 수 있다. 
하나의 예로서, 만약 두 개의 데이타베이스에 동일한 테이블명이 있고 이를 클라이언트에서 병합해야 하는 경우에는, 아래와 같이 두 테이블을 DataSet에 가져와 이를 병합해서 사용하면 된다. (물론 서버에서 병합할 수도 있다). 
Merge() 메서드는 테이블의 Primary Key를 기준으로 추가/삭제/변경된 레코드들을 해당 테이블에 병합하게 된다.
```cs
DataSet ds1 = new DataSet();
DataSet ds2 = new DataSet();

string strConn1 = "Data Source=(local);Initial catalog=pubs;Integrated Security=SSPI;";
string strConn2 = "Data Source=(local);Initial catalog=pubs2;Integrated Security=SSPI;";

string sql = "SELECT * FROM authors";

// pubs DB에서 authors 테이블 가져오기 (23개 rows).
SqlDataAdapter adpt1 = new SqlDataAdapter(sql, strConn1);
adpt1.MissingSchemaAction = MissingSchemaAction.AddWithKey;
adpt1.Fill(ds1); 
adpt1.Dispose();

// pubs2 DB에서 authors 테이블 가져오기.
// (24개 rows : 1개 row가 추가되었고, 1 row가 Update됨)
SqlDataAdapter adpt2 = new SqlDataAdapter(sql, strConn2);
adpt2.MissingSchemaAction = MissingSchemaAction.AddWithKey;
adpt2.Fill(ds2); 
adpt2.Dispose();

// Merge후 authors에는 1개 추가 row와 갱신된 1개 row가 있음.
Console.WriteLine("Before Merge: {0}", ds1.Tables[0].Rows.Count);
ds1.Merge(ds2);
Console.WriteLine("After Merge: {0}", ds1.Tables[0].Rows.Count);

foreach (DataRow r in ds1.Tables[0].Rows)
{
    Console.WriteLine("{0}: {1} {2}", r[0], r[1], r[2]);
}
```

SqlDataAdapter가 DataSet에 데이타를 Fill 할 때, 디폴트로 MissingSchemaAction.Add 를 사용한다. 즉, DataSet에 (위의 예제와 같이) 컬럼들이 이미 수작업으로 정의하고 있지 않으면, 컬럼명과 타입을 자동으로 추가하게 된다. 
MissingSchemaAction.AddWithKey는 여기에 하나 더 Primary Key 정보를 데이타소스에서 읽어와 추가하게 된다. 즉, DataSet에 데이타가 Fill 되기 전에 기본 컬럼 스키마를 정의하고 또한 Primary Key를 미리 정의하게 된다. 
AddWithKey로 정의한 후 Fill이 실행될 때, 동일한 Primary Key값이 추가되면 Row는 Append되지 않고 Update된다.

![[../../4. Archive/attachment/Pasted image 20240304132720.png]]