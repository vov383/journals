---
title: Fatal error encountered during command execution
created: 2024-02-27 01:56
alias:
tags:
---
![[../../4. Archive/attachment/Pasted image 20240227133752.png]]
catch로 넣은 exception에 잡힌 에러
sql문에 들어가야 할 공백이 빠져서 발생한 에러
```CSharp 
string updateQuery = "UPDATE employee_list " +
                    "SET emp_name = @name" +
                        ", gender = @gender" +
                        ", age = @age" +
                        ", home_address = @home" +
                        ", department = @dept" +
                        ", rank_position = @rank" +
                        ", com_call_num = @com" +
                        ", phone_num = @phone" +
                        ", mail_address = @email " +
                    "WHERE id = @index;";
```
`"... SET 컬럼명 = data WHERE 컬럼명 = 데이터;"`에서 `컬럼명 = data`와 `WHERE`절 사이에 공백이 들어가야 함. 
공백이 없이 SQL문을 실행하면 Fatal error 어쩌고 발생하고 sql 동작이 이뤄진다.

[[다울 과제 에러노트|다울 과제 에러노트]]
