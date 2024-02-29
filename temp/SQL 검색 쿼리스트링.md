---
title: SQL 검색 쿼리스트링
created: 2024-02-29 04:02
alias:
tags:
---
```csharp
string queryStr = string.Format("SELECT * FROM employee_list WHERE {0} LIKE '%{1}%';", cboxCondition.SelectedValue, tboxSearch.Text);`
```
''로 %{keyword}%를 감싸야 한다.


