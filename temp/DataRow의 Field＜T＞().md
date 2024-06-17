---
title: DataRow의 Field＜T＞()
created: 2024-06-17 11:49
alias:
tags:
---
- `DataRow.Field<T>()` 메서드는 `DataRow` 객체에서 특정 타입의 값을 읽어올 때 사용됩니다.
- 제네릭 타입 `<T>`는 반환할 값의 데이터 타입을 지정합니다.
- 인자로는 필드 이름(열 이름)을 사용합니다.
```cs
T value = dataRow.Field<T>("ColumnName");

foreach (DataRow row in dataTable.Rows) 
{ 
	int id = row.Field<int>("ID"); 
	string name = row.Field<string>("Name"); 
	DateTime date = row.Field<DateTime>("Date"); 
}
```


