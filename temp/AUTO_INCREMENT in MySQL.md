---
title: AUTO_INCREMENT in MySQL
created: 2024-09-12 03:22
alias:
tags:
---
의 다음에 들어갈 값을 확인하는 방법은 `SHOW TABLE STATUS` 명령어를 사용하면 됩니다. 이 명령어는 테이블의 상태를 보여주며, 여기서 `Auto_increment` 필드에 해당 테이블에서 다음으로 입력될 `AUTO_INCREMENT` 값이 표시됩니다.

다음과 같은 SQL 쿼리를 사용할 수 있습니다:

```sql
SHOW TABLE STATUS LIKE 'your_table_name';
```

여기서 `'your_table_name'`은 확인하고 싶은 테이블의 이름입니다. 이 쿼리를 실행하면 해당 테이블의 상태 정보를 포함한 결과가 반환되며, 그중 `Auto_increment` 열에 다음에 들어갈 값이 표시됩니다.

또는 특정 테이블의 `AUTO_INCREMENT` 값을 직접 확인하고 싶다면, 다음과 같은 쿼리도 사용할 수 있습니다:

```sql
SELECT AUTO_INCREMENT
FROM information_schema.TABLES
WHERE TABLE_SCHEMA = 'your_database_name'
AND TABLE_NAME = 'your_table_name';
```

이 쿼리는 `information_schema`에서 테이블의 정보를 가져와서 `AUTO_INCREMENT` 값을 보여줍니다.


