---
title: CROSS JOIN in MySQL
created: 2025-04-07 04:33
alias:
tags:
---
### 요약 포인트

- **정의**: CROSS JOIN은 두 테이블의 모든 행을 서로 결합하는 조인방식.
- **결과**: 테이블1의 행 수 × 테이블2의 행 수 만큼 결과 행이 생성
- **용도**: 
	- 모든 조합을 만들어야 할 때, 
	- 예시
		- 인덱스 생성이나 
		- 매트릭스 형태의 데이터를 만들 때 유용
- **주의사항**: 
	- 결과 행의 수가 급격하게 늘어날 수 있으므로, 
	- 데이터량이 많은 경우 주의해서 사용해야 합니다.

#### Q1. CROSS JOIN이란?
- **CROSS JOIN**은 두 테이블의 
- 모든 조합(카테시안 곱, Cartesian Product)을 반환하는 
- **조인 방식**입니다.
    
- 두 테이블의 각각의 행이 서로 조합되어 결과에 포함되므로, 
- 결과 행의 총 개수는 **첫 번째 테이블 행 수 × 두 번째 테이블 행 수**가 됩니다.
    

#### Q2. CROSS JOIN의 동작 방식

- **예시**:
    - 테이블 A에 3개의 행, 테이블 B에 2개의 행이 있다면,
    - CROSS JOIN 결과는 3 × 2 = 6개의 행을 반환합니다.
        
- **동작 원리**:
    - 테이블 A의 각 행이 테이블 B의 **모든** 행과 결합됩니다.
    - 이를 통해 두 테이블 간에 명시적인 조건 없이 **모든 가능한 조합**을 생성합니다.
        

---

### CROSS JOIN의 활용 예제

#### 예제 1: 기본 사용법

```sql
SELECT
	* 
FROM tableA 
CROSS JOIN tableB;
```

- 위 쿼리는 tableA의 각 행과 tableB의 모든 행을 결합합니다.
    

#### 예제 2: 인덱스 생성용 CROSS JOIN

- 앞서 제시한 예제처럼, 브랜드와 인포 인덱스를 생성할 때 사용할 수 있습니다.
    

```sql
SELECT 
	* 
FROM (     
	SELECT 1 AS num 
		UNION ALL SELECT 2 
		UNION ALL SELECT 3 
		UNION ALL SELECT 4 
	) AS a 
CROSS JOIN (     
	SELECT 'A' AS letter 
		UNION ALL SELECT 'B' 
	) AS b;
```


- 이 쿼리의 결과는 `num`과 `letter`의 모든 조합(4 × 2 = 8개의 행)을 생성합니다.
    

---


	    

이와 같이 CROSS JOIN은 
명시적인 결합 조건 없이 모든 가능한 조합을 생성하여, 
복잡한 데이터 변환이나 
인덱스 생성을 간단하게 도와주는 기능입니다.