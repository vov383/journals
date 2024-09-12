---
title: MySQL IFNULL()과 COALESCE 비교
created: 2024-09-12 03:25
alias:
tags:
---
`IFNULL`과 `COALESCE`는 둘 다 **NULL 값을 처리**하기 위해 사용되며, 특정 값이 NULL일 경우 대체 값을 반환하는 역할을 합니다. 하지만 두 함수 사이에는 몇 가지 차이점이 있습니다.

### 1. **`IFNULL`**
`IFNULL`은 **첫 번째 인수가 NULL인지 확인**하고, NULL이면 두 번째 인수를 반환합니다. 첫 번째 인수가 NULL이 아니면 그 값을 그대로 반환합니다.

- 구문:
  ```sql
  IFNULL(expression, value)
  ```

- 특징:
  - **매개변수 2개**만 받습니다.
  - 첫 번째 인수가 NULL일 때 두 번째 인수를 반환합니다.
  - 간단한 NULL 체크에서 자주 사용됩니다.

- 예시:
  ```sql
  SELECT IFNULL(NULL, 'Default Value');  -- 결과: 'Default Value'
  SELECT IFNULL('Hello', 'Default Value');  -- 결과: 'Hello'
  ```

### 2. **`COALESCE`**
`COALESCE`는 **여러 개의 인수**를 받아서, 그중 **첫 번째로 NULL이 아닌 값**을 반환합니다. 만약 모든 인수가 NULL이면 NULL을 반환합니다.

- 구문:
  ```sql
  COALESCE(expression1, expression2, ..., expressionN)
  ```

- 특징:
  - **여러 인수**를 받을 수 있습니다.
  - 가장 처음으로 NULL이 아닌 값을 반환합니다.
  - 복잡한 NULL 처리에서 유용하며, 여러 값 중 하나를 선택할 때 사용됩니다.

- 예시:
  ```sql
  SELECT COALESCE(NULL, NULL, 'Value', 'Default Value');  -- 결과: 'Value'
  SELECT COALESCE(NULL, NULL, NULL);  -- 결과: NULL
  ```

### 주요 차이점

1. **인수의 수**:
   - `IFNULL`은 **2개의 인수**만 허용합니다.
   - `COALESCE`는 **여러 개의 인수**를 받을 수 있으며, 이 중 가장 첫 번째로 NULL이 아닌 값을 반환합니다.

2. **표준성**:
   - `COALESCE`는 **SQL 표준**에서 정의된 함수입니다.
   - `IFNULL`은 **MySQL 고유**의 함수로, 다른 DBMS에서는 사용할 수 없을 수도 있습니다.

3. **동작 방식**:
   - `IFNULL`은 첫 번째 인수가 NULL이면 두 번째 인수를 반환하는 단순한 기능을 수행합니다.
   - `COALESCE`는 여러 인수 중에서 첫 번째로 NULL이 아닌 값을 찾고, 그 값을 반환합니다. 즉, 더 복잡한 로직을 처리할 수 있습니다.

4. **성능 차이**:
   - `IFNULL`은 두 인수만 비교하기 때문에 성능상 이점이 있을 수 있습니다.
   - `COALESCE`는 여러 인수를 처리할 수 있지만, 그만큼 더 많은 인수를 비교하므로 약간 더 성능 부담이 있을 수 있습니다. 하지만 일반적으로 눈에 띄는 성능 차이는 없습니다.

### 예시 비교

#### `IFNULL` 사용:
```sql
SELECT IFNULL(SH_CHASU, '0') FROM TB_PORT_ENTRY;
```
- `SH_CHASU`가 NULL이면 '0'을 반환하고, 그렇지 않으면 `SH_CHASU` 값을 반환합니다.

#### `COALESCE` 사용:
```sql
SELECT COALESCE(SH_CD, SH_YEAR, SH_CHASU, 'Default Value') FROM TB_PORT_ENTRY;
```
- `SH_CD`, `SH_YEAR`, `SH_CHASU` 중에서 첫 번째로 NULL이 아닌 값을 반환합니다. 모든 값이 NULL이면 'Default Value'를 반환합니다.

### 결론

- **`IFNULL`**: NULL 처리 로직이 간단하고, **두 개의 값만** 비교할 때 사용합니다.
- **`COALESCE`**: 여러 값 중 **첫 번째로 NULL이 아닌 값**을 찾고 싶을 때 사용합니다. 더 복잡한 NULL 처리 상황에 적합합니다.


