---
title: ExecuteNonQuery 메서드
created: 2024-04-09 02:23
alias:
tags:
---
SQL 명령을 실행하고 영향을 받은 행의 수를 반환하는 데 사용됩니다. 
주로 데이터를 삽입(insert), 수정(update), 삭제(delete)하는 등의 작업을 할 때 사용됩니다. 
이 메서드는 `System.Data.SqlClient.SqlCommand` 클래스의 멤버입니다. 
MySQL을 사용할 경우, 
`MySql.Data.MySqlClient.MySqlCommand` 클래스에서 비슷한 기능을 제공합니다.

### MySQL에서 `ExecuteNonQuery` 사용 예

MySQL 데이터베이스에 접속하고 
데이터를 수정하는 기본적인 코드 예시는 다음과 같습니다. 
이 예제에서는 
MySQL 데이터베이스에 데이터를 삽입하는 간단한 예시를 보여줍니다:

```csharp
using MySql.Data.MySqlClient;

string connStr = "server=localhost;user=root;database=mydb;port=3306;password=mypass";
using (var conn = new MySqlConnection(connStr))
{
    try
    {
        conn.Open();

        string sql = "INSERT INTO table_name (column1, column2) VALUES (value1, value2)";
        using (var cmd = new MySqlCommand(sql, conn))
        {
            int affectedRows = cmd.ExecuteNonQuery();
            Console.WriteLine("Affected Rows: " + affectedRows);
        }
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.ToString());
    }
}
```

### 주의사항
데이터베이스 연결 문자열(`connStr`)에 
정확한 서버 주소, 사용자 이름, 데이터베이스 이름, 포트, 비밀번호를 기입해야 합니다.
`using` 문은 
`MySqlConnection`과 `MySqlCommand` 객체가 더 이상 필요 없을 때 
자동으로 리소스를 해제하여 메모리 누수를 방지합니다.
예외 처리를 사용하여 
데이터베이스 연결 시도 중 발생할 수 있는 오류를 처리합니다. 
이는 데이터베이스 서버에 연결할 수 없거나, 
SQL 명령어에 오류가 있을 경우 유용합니다.
`ExecuteNonQuery`는 
SELECT 문을 제외한 SQL 문을 실행하는 데 사용되며, 
영향 받은 행의 수를 반환합니다. 
SELECT 문을 실행할 때는 `ExecuteReader` 또는 `ExecuteScalar` 메서드를 사용합니다.
`ExecuteNonQuery`가 반환하는 "영향 받은 행의 수"는 
INSERT, UPDATE, DELETE 문을 실행할 때 데이터베이스에 실제로 반영된 행의 수입니다. 
예를 들어, 존재하지 않는 데이터를 삭제하려고 시도하면, 
반환 값은 0이 될 수 있습니다.

이렇게 `ExecuteNonQuery` 메서드를 사용하면, C# 응용 프로그램에서 MySQL 데이터베이스의 데이터를 프로그래매틱하게 관리할 수 있습니다.


