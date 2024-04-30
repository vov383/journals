---
title: DATE 값을 UPDATE 하는 SQL in MariaDB
created: 2024-04-30 10:57
alias:
tags:
---
```SQL
UPDATE TB_PORT_ENTRY
SET DT_PLAN_ENTRY = ADDDATE(DT_PLAN_ENTRY, INTERVAL 1 MONTH)
WHERE YEAR(DT_PLAN_ENTRY) = 2024 AND MONTH(DT_PLAN_ENTRY) = 4;
```

###### ADDDATE 함수의 사용
MariaDB에서 날짜를 다루기 위한 함수 중 하나가 `ADDDATE` 입니다. 
이 함수는 특정 날짜에 일정 기간을 더하는 데 사용됩니다.

###### ADDDATE 함수 구조
`ADDDATE` 함수는 
날짜에 지정된 기간(일, 월, 년 등)을 더할 때 사용하며, 
`INTERVAL` 키워드와 함께 사용됩니다.

###### 쿼리 적용
`ADDDATE`를 사용하는 쿼리는 
기존 날짜 필드에 원하는 기간을 더하여 
그 결과를 날짜 필드에 저장합니다.

###### 결과 확인
쿼리 실행 후에는 `SELECT` 문을 사용하여 
날짜가 올바르게 업데이트 되었는지 확인할 수 있습니다.

###### 백업의 중요성
데이터베이스에 변경을 가하기 전에는 
항상 백업을 수행하여 데이터 손실을 예방해야 합니다.

###### 실행 전 주의사항
실제 데이터에 쿼리를 실행하기 전에 
테스트 환경에서 쿼리를 실행하여 예상대로 동작하는지 확인해야 합니다.

```sql
UPDATE 테이블명
SET DT_PLAN_ENTRY = ADDDATE(DT_PLAN_ENTRY, INTERVAL 1 MONTH)
WHERE YEAR(DT_PLAN_ENTRY) = 2024 AND MONTH(DT_PLAN_ENTRY) = 4;
```
여기서 `테이블명`은 실제 사용하고 있는 테이블 이름으로 바꾸어야 합니다.


