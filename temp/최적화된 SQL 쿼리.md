---
title: 최적화된 SQL 쿼리
created: 2024-07-26 04:44
alias:
tags:
---
```sql
WITH common_join AS (
    SELECT p.*, h.*
    FROM tb_port_entry p
    JOIN tb_ship_hold h 
        ON p.SH_CD = h.SH_CD 
        AND p.SH_YEAR = h.SH_YEAR
        AND p.SH_CHASU = h.SH_CHASU
    WHERE p.SH_CD = 'ATE'
        AND p.SH_YEAR = '2024'
        AND p.SH_CHASU = '1'
)
SELECT b.*, cj.*
FROM tb_com_berth b
JOIN common_join cj
    ON b.SH_CD = cj.SH_CD
    AND b.SH_YEAR = cj.SH_YEAR
    AND b.SH_CHASU = cj.SH_CHASU;
```

### 설명
1. **WITH 절**: `WITH common_join AS (...)` 절을 사용하여 공통 조인 조건을 서브쿼리로 정의합니다.
2. **common_join 서브쿼리**: `tb_port_entry`와 `tb_ship_hold` 테이블을 조인하고 필터 조건을 적용하여 결과를 반환합니다.
3. **메인 쿼리**: 메인 쿼리에서는 `tb_com_berth` 테이블을 `common_join` 서브쿼리와 조인합니다.

이렇게 하면 중복된 조인 조건을 제거하고, 코드 가독성을 높일 수 있습니다.

### 요약
1. 서브쿼리를 사용하여 중복된 조인 조건을 제거.
2. `WITH` 절을 사용하여 가독성 향상.
3. 메인 쿼리에서 서브쿼리와 조인하여 간결하게 작성.

Q1: 서브쿼리를 사용할 때 성능에 미치는 영향은 무엇인가요?
Q2: 복잡한 조인 조건을 관리하기 위한 다른 방법은 무엇인가요?



### 모듈화된 SQL 코드 사용 방법

모듈화된 SQL 코드를 사용하면 복잡한 쿼리를 더 쉽게 관리하고 유지 보수할 수 있습니다. 이 방법은 SQL 스크립트를 작은 단위로 분리하고, 필요한 곳에서 호출하여 사용하는 방식입니다. 아래에 구체적인 예시와 단계를 제공하겠습니다.

#### 1. **뷰(View) 사용**

뷰를 사용하여 자주 사용하는 조인이나 서브쿼리를 모듈화할 수 있습니다.

```sql
-- Step 1: 뷰 생성
CREATE VIEW vw_port_entry_ship_hold AS
SELECT p.*, h.*
FROM tb_port_entry p
JOIN tb_ship_hold h 
    ON p.SH_CD = h.SH_CD 
    AND p.SH_YEAR = h.SH_YEAR
    AND p.SH_CHASU = h.SH_CHASU;
```

#### 2. **저장 프로시저(Stored Procedure) 사용**

저장 프로시저를 사용하여 복잡한 로직을 캡슐화하고, 필요할 때 호출할 수 있습니다.

```sql
-- Step 2: 저장 프로시저 생성
CREATE PROCEDURE sp_get_berth_info
    @SH_CD VARCHAR(10),
    @SH_YEAR INT,
    @SH_CHASU INT
AS
BEGIN
    SELECT b.*, v.*
    FROM tb_com_berth b
    JOIN vw_port_entry_ship_hold v
        ON b.SH_CD = v.SH_CD
        AND b.SH_YEAR = v.SH_YEAR
        AND b.SH_CHASU = v.SH_CHASU
    WHERE v.SH_CD = @SH_CD
        AND v.SH_YEAR = @SH_YEAR
        AND v.SH_CHASU = @SH_CHASU;
END
```

#### 3. **CTE(Common Table Expression) 사용**

CTE를 사용하여 쿼리 내에서 일시적으로 데이터를 모듈화할 수 있습니다.

```sql
-- Step 3: CTE 사용 예제
WITH common_join AS (
    SELECT p.*, h.*
    FROM tb_port_entry p
    JOIN tb_ship_hold h 
        ON p.SH_CD = h.SH_CD 
        AND p.SH_YEAR = h.SH_YEAR
        AND p.SH_CHASU = h.SH_CHASU
)
SELECT b.*, cj.*
FROM tb_com_berth b
JOIN common_join cj
    ON b.SH_CD = cj.SH_CD
    AND b.SH_YEAR = cj.SH_YEAR
    AND b.SH_CHASU = cj.SH_CHASU
WHERE cj.SH_CD = 'ATE'
    AND cj.SH_YEAR = '2024'
    AND cj.SH_CHASU = '1';
```

#### 4. **서브쿼리(Subquery) 사용**

서브쿼리를 사용하여 복잡한 조건을 캡슐화하고 메인 쿼리에서 사용할 수 있습니다.

```sql
-- Step 4: 서브쿼리 사용 예제
SELECT b.*, sub.*
FROM tb_com_berth b
JOIN (
    SELECT p.*, h.*
    FROM tb_port_entry p
    JOIN tb_ship_hold h 
        ON p.SH_CD = h.SH_CD 
        AND p.SH_YEAR = h.SH_YEAR
        AND p.SH_CHASU = h.SH_CHASU
    WHERE p.SH_CD = 'ATE'
        AND p.SH_YEAR = '2024'
        AND p.SH_CHASU = '1'
) sub
ON b.SH_CD = sub.SH_CD
AND b.SH_YEAR = sub.SH_YEAR
AND b.SH_CHASU = sub.SH_CHASU;
```

### 요약

1. **뷰(View) 사용**: 자주 사용하는 조인이나 서브쿼리를 뷰로 생성하여 재사용.
2. **저장 프로시저 사용**: 복잡한 로직을 저장 프로시저로 캡슐화하여 필요 시 호출.
3. **CTE 사용**: 일시적으로 데이터를 모듈화하여 복잡한 쿼리를 간단히 관리.
4. **서브쿼리 사용**: 복잡한 조건을 서브쿼리로 캡슐화하여 메인 쿼리에서 사용.

Q1: 뷰를 사용할 때 주의해야 할 성능 이슈는 무엇인가요?
Q2: 저장 프로시저를 활용한 복잡한 쿼리 관리의 장점은 무엇인가요?



### 여러 테이블에서 데이터를 가져와 화면에 표시하기

여러 테이블에서 데이터를 가져와 화면에 표시할 때, LEFT JOIN과 스칼라 서브쿼리 모두 사용할 수 있습니다. 각 방법은 특정 상황에 따라 장단점이 있습니다. 

#### LEFT JOIN
LEFT JOIN은 기본 테이블의 모든 행과 오른쪽 테이블의 일치하는 행을 반환하며, 일치하지 않는 경우 NULL을 반환합니다. 주로 다수의 행을 결합하여 표시할 때 유용합니다.

##### 예제
```sql
SELECT b.*, p.*, h.*
FROM tb_com_berth b
LEFT JOIN tb_port_entry p 
    ON b.SH_CD = p.SH_CD
    AND b.SH_YEAR = p.SH_YEAR
    AND b.SH_CHASU = p.SH_CHASU
LEFT JOIN tb_ship_hold h 
    ON p.SH_CD = h.SH_CD 
    AND p.SH_YEAR = h.SH_YEAR
    AND p.SH_CHASU = h.SH_CHASU
WHERE p.SH_CD = 'ATE'
    AND p.SH_YEAR = '2024'
    AND p.SH_CHASU = '1';
```

#### 장점
1. **모든 데이터를 한 번에 가져오기**: 한 번의 쿼리로 여러 테이블의 데이터를 결합하여 가져올 수 있습니다.
2. **성능**: 잘 최적화된 인덱스와 함께 사용하면 대규모 데이터 세트에서 성능이 좋습니다.
3. **가독성**: 조인 조건을 명확히 정의하여 쿼리의 가독성을 높입니다.

#### 단점
1. **복잡성 증가**: 많은 테이블을 조인하면 쿼리가 복잡해질 수 있습니다.
2. **불필요한 데이터**: 모든 열을 가져올 때 필요한 데이터보다 더 많은 데이터를 가져올 수 있습니다.

#### 스칼라 서브쿼리
스칼라 서브쿼리는 주 쿼리의 각 행에 대해 서브쿼리를 실행하여 단일 값을 반환합니다. 주로 특정 값을 계산하거나 검색할 때 유용합니다.

##### 예제
```sql
SELECT b.*, 
    (SELECT p.SomeColumn 
     FROM tb_port_entry p 
     WHERE p.SH_CD = b.SH_CD
       AND p.SH_YEAR = b.SH_YEAR
       AND p.SH_CHASU = b.SH_CHASU
       AND p.SH_CD = 'ATE'
       AND p.SH_YEAR = '2024'
       AND p.SH_CHASU = '1') AS PortEntryData,
    (SELECT h.SomeOtherColumn 
     FROM tb_ship_hold h 
     WHERE h.SH_CD = b.SH_CD
       AND h.SH_YEAR = b.SH_YEAR
       AND h.SH_CHASU = b.SH_CHASU) AS ShipHoldData
FROM tb_com_berth b;
```

#### 장점
1. **단순화된 메인 쿼리**: 메인 쿼리를 단순화할 수 있으며, 특정 컬럼만 필요할 때 유용합니다.
2. **부분 데이터 검색**: 필요한 데이터만 서브쿼리에서 검색하여 가져옵니다.

#### 단점
1. **성능**: 각 행에 대해 서브쿼리가 실행되므로 성능이 저하될 수 있습니다. 특히 대규모 데이터 세트에서 성능 문제가 발생할 수 있습니다.
2. **복잡성 증가**: 많은 서브쿼리를 사용하면 쿼리의 복잡성이 증가할 수 있습니다.

### 상황에 따른 선택
- **대규모 데이터 세트**: LEFT JOIN이 더 효율적입니다. 인덱스를 사용하여 성능을 최적화할 수 있습니다.
- **단일 값 검색**: 특정 컬럼의 값을 계산하거나 검색하는 경우 스칼라 서브쿼리가 유용합니다.
- **단순 데이터 결합**: 여러 테이블을 결합하여 데이터를 한 번에 가져오려면 LEFT JOIN을 사용합니다.
- **필요한 데이터만**: 필요한 데이터만 가져오고 싶다면 스칼라 서브쿼리를 사용합니다.

### 요약
1. LEFT JOIN은 여러 테이블의 데이터를 한 번에 결합하여 가져오는 데 유용합니다.
2. 스칼라 서브쿼리는 단일 값을 계산하거나 검색할 때 유용합니다.
3. 대규모 데이터 세트에서는 LEFT JOIN이 성능 면에서 더 효율적일 수 있습니다.
4. 필요한 데이터만 정확하게 가져오려면 스칼라 서브쿼리를 사용할 수 있습니다.
5. 쿼리 복잡성 증가를 피하기 위해 상황에 맞는 방법을 선택합니다.

Q1: LEFT JOIN을 사용할 때 인덱스를 최적화하는 방법은 무엇인가요?
Q2: 스칼라 서브쿼리의 성능을 개선하기 위한 방법은 무엇인가요?


