---
title: MySqlDataAdapter() 생성자 오버로드
created: 2024-02-28 09:14
alias:
tags:
---
```csharp
MySqlDataAdapter adapter = new MySqlDataAdapter(queryStr, conn); 
```
를 하면 

```csharp
MySqlDataAdapter adapter = new MySqlDataAdapter();
MySqlCommand cmd = new MySqlCommand(queryStr, conn);
adapter.SelectCommand = cmd; 
```
한것과 같음


