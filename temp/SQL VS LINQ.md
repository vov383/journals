---
title: SQL VS LINQ
created: 2025-04-22 05:07
alias:
tags:
---
### Q1. SQL 관점: 언피벗(Unpivot)·집계(Aggregation) 로직

#### 1) 원리
- **Set-based 연산**
    - SQL 엔진이 대량 데이터를 한 번에 처리하도록 최적화되어 있음
    - `UNION ALL`·`CROSS JOIN`·윈도 함수(window functions) 등으로 복수 컬럼→행 변환 및 집계 수행
        
- **윈도 함수 활용**
    - `ROW_NUMBER()`, `DENSE_RANK()`로 그룹 내 순서·등급 매김
    - `PARTITION BY`로 그룹화, `ORDER BY`로 정렬 기준 지정
        

#### 2) 대표적 구현 방식

- **UNION ALL**
    
    ```sql
    SELECT id, 'jan' AS month, jan AS amount FROM sales
    UNION ALL
    SELECT id, 'feb', feb       FROM sales;
    ```
    
- **CROSS JOIN + CASE**
    
    ```sql
    WITH nums AS (
      SELECT 1 AS n UNION ALL SELECT 2 UNION ALL SELECT 3
    )
    SELECT
      s.id,
      CASE n WHEN 1 THEN 'jan' WHEN 2 THEN 'feb' WHEN 3 THEN 'mar' END AS month,
      CASE n WHEN 1 THEN s.jan WHEN 2 THEN s.feb WHEN 3 THEN s.mar END AS amount
    FROM sales s
    CROSS JOIN nums;
    ```
    
- **MySQL 8.0+ `JSON_TABLE()`**
    
    ```sql
    SELECT s.id, jt.month, jt.amount
    FROM sales s
    JOIN JSON_TABLE(
      JSON_ARRAY(
        JSON_OBJECT('month','jan','amount',s.jan),
        JSON_OBJECT('month','feb','amount',s.feb)
      ), '$[*]'
      COLUMNS (
        month  VARCHAR(3) PATH '$.month',
        amount INT         PATH '$.amount'
      )
    ) AS jt;
    ```
    
#### 3) 장단점 비교

|            | 장점                          | 단점                                 |
| ---------- | --------------------------- | ---------------------------------- |
| UNION ALL  | MySQL 5.x 이하 호환, 직관적 구현     | 컬럼 수 만큼 SELECT 반복, 쿼리 길어짐          |
| CASE       | SELECT 구문 한 번으로 중앙집중 관리     | CASE 분기문 작성·유지보수 번거로움              |
| JSON_TABLE | 가독성 우수, 컬럼 추가·제거 시 JSON만 수정 | MySQL 8.0 이상 필요, JSON 직렬화 비용 소폭 발생 |


---

### Q2. 애플리케이션 관점: 동적 컬럼 처리·반복 구조

#### 1) 원리

- **Imperative vs Declarative**
    - SQL은 “무엇을 할지”(What)를 선언, 애플리케이션 코드는 “어떻게 할지”(How)를 명시
        
- **컬렉션 평탄화(flatten)**
    - `SelectMany` 등으로 1개 객체→N개 결과 열거
        
- **동적 컬럼 접근**
    - 문자열 보간(`$"COL{i}"`), 리플렉션, `Dictionary<string,object>` 등으로 유연 처리
        

#### 2) 주요 구현 패턴

- **LINQ `SelectMany`**
    
    ```csharp
    var list = Enumerable.Range(1,4)
      .SelectMany(b => Enumerable.Range(1,4)
        .Select(i => new {
          ShipKey = dr["SHIP_KEY"],
          BrIdx   = b,
          InfoIdx = i,
          Info    = dr[$"YARD_BRAND{b}_INFO{i}"]
        }))
      .Where(x => x.Info != null && x.Info != "---")
      .ToList();
    ```
    
- **Dictionary 매핑**
    
    ```csharp
    var maps = Enumerable.Range(1,11)
      .Select(i => new Dictionary<string,object> {
        ["SHIP_KEY"] = dr["SHIP_KEY"],
        ["IDX"]      = i,
        ["VAL"]      = dr[$"HOLD_BRAND{i}"]
      })
      .ToList();
    ```
    
- **유틸 메서드화**
    
    ```csharp
    IEnumerable<Dictionary<string,object>> Unpivot(
      DataRow dr, string prefix, int count)
    {
      return Enumerable.Range(1,count)
        .Select(i => new Dictionary<string,object> {
          ["Key"] = dr["SHIP_KEY"],
          ["Idx"] = i,
          [prefix] = dr[$"{prefix}{i}"]
        });
    }
    ```
    

#### 3) 장단점 비교

|            | 장점                          | 단점                        |
| ---------- | --------------------------- | ------------------------- |
| LINQ       | 코드에서 즉시 제어, 복잡 로직 테스트 용이    | 반복적 코드·익명객체 선언로직 장황       |
| Dictionary | 동적 스키마 대응, 코드에서 곧바로 행 단위 매핑 | 컴파일 타임 타입 안정성 저하, 키 오타 위험 |

---

### 요약 포인트

- **SQL**
    
    - 언피벗·집계에 강점, 대량 데이터에 최적화된 집합 연산 이용
        
    - CTE·윈도 함수·`JSON_TABLE()`로 가독성 높임
        
- **애플리케이션**
    - 동적 컬럼·반복 로직은 코드화로 유연성 확보
    - `SelectMany`·Dictionary·유틸 메서드로 중복 최소화
        
- **선택 기준**
    - **데이터 규모·성능 제약** → SQL에서 처리
    - **비즈니스 로직 변경 빈도·테스트 편의** → 애플리케이션에서 처리
        

---

### 참고 링크

- MySQL `JSON_TABLE()` 함수:  
    [https://dev.mysql.com/doc/refman/8.0/en/json-table-functions.html](https://dev.mysql.com/doc/refman/8.0/en/json-table-functions.html)
    
- .NET LINQ `SelectMany` 문서:  
    [https://learn.microsoft.com/dotnet/api/system.linq.enumerable.selectmany](https://learn.microsoft.com/dotnet/api/system.linq.enumerable.selectmany)


