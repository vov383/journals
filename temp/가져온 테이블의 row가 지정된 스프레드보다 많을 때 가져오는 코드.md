---
title: 가져온 테이블의 row가 지정된 스프레드보다 많을 때 가져오는 코드
created: 2024-03-07 11:10
alias:
tags:
---
데이터셋에서 테이블 가져오고 row개수 셈
만약 20개보다 많으면 스프레드의 row개수를 그만큼 늘려준다.
```cs
if (ds.Tables[0].Rows.Count > 20)
{
    fpSpread1_Sheet1.AddRows(20, ds.Tables[0].Rows.Count - 20);
}
```
