---
title: Parametized Query
created: 2024-02-27 08:16
alias:
tags:
---
Parameterized Query는 SQL 쿼리에서 직접 값들을 입력하는 대신, 파라미터를 사용하여 쿼리를 구성하는 방법입니다. 
이 방법은 SQL Injection 공격을 방지하는 데 매우 효과적이며, 데이터베이스 쿼리의 안정성과 보안성을 크게 향상시킵니다. 각 파라미터 앞에 '@' 기호를 사용하여, 실행 시점에 해당 파라미터의 값을 바인딩하고, 이를 통해 데이터베이스에 쿼리를 보냅니다.

예시
```CSharp
    string updateQuery =
"UPDATE employee_list " +
"SET emp_name = @name, gender = @gender, age = @age, home_address = @home, department = @dept" +
    ", rank_position = @rank, com_call_num = @com,  phone_num = @phone, mail_address = @email" +
"WHERE id = @index;";
    MySqlCommand cmd = new MySqlCommand(updateQuery, conn);
```
