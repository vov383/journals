---
title: c DataTable 클래스
created: 2024-03-04 01:25
alias:
tags:
---
**DataTable 클래스는 메모리상에 테이블을 표현하는 클래스**로서, DataSet.Tables 컬렉션에 포함되어 사용되는 경우가 많다. 
DataSet은 여러개의 DataTable들을 포함하여 마치 메모리상의 간이 데이타베이스와 같은 개념으로 이해될 수 있다. 
DataSet에 있는 DataTable을 엑세스하기 위해서는 dataSet.Tables[0]과 같이 인덱스를 사용할 수 있으며, 
아래 예와 같이 테이블명을 이용해서 엑세스할 수도 있다.
```cs
DataSet ds = new DataSet();
adapter.Fill(ds, "Tab1");
DataTable dt = ds.Tables["Tab1"];
```




