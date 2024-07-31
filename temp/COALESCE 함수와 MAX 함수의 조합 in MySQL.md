---
title: COALESCE 함수와 MAX 함수의 조합 in MySQL
created: 2024-07-31 02:54
alias:
tags:
---
`COALESCE` 함수와 `MAX` 함수의 조합은 SQL에서 흔히 사용되는 방법으로, `NULL` 값을 대체하고 그룹화된 데이터 중 최대 값을 선택하는 데 사용됩니다.

### COALESCE 함수
`COALESCE` 함수는 주어진 인자 중 첫 번째로 `NULL`이 아닌 값을 반환합니다. 만약 모든 인자가 `NULL`이라면, 마지막 인자를 반환합니다. 즉, `COALESCE(a, b)`는 `a`가 `NULL`이 아니면 `a`를 반환하고, `a`가 `NULL`이면 `b`를 반환합니다.

### MAX 함수
`MAX` 함수는 주어진 컬럼의 최대 값을 반환합니다. 일반적으로 그룹화된 데이터에서 가장 큰 값을 찾는 데 사용됩니다.

### COALESCE와 MAX의 조합
`COALESCE(MAX(UL_CD), '')`와 같은 표현은 다음과 같은 의미를 갖습니다:
- `MAX(UL_CD)`는 그룹화된 데이터에서 `UL_CD`의 최대 값을 선택합니다. 만약 `UL_CD`가 모두 `NULL`이라면 결과는 `NULL`입니다.
- `COALESCE(MAX(UL_CD), '')`는 `MAX(UL_CD)`의 결과가 `NULL`이면 빈 문자열 `''`을 반환하고, 그렇지 않으면 `MAX(UL_CD)`의 값을 반환합니다.

### 예시로 살펴보기
```sql
SELECT
    COALESCE(MAX(UL_CD), '') AS UL_CD,
    COALESCE(MAX(UL_NM), '') AS UL_NM
FROM 
    TB_UNLOAD_WORK
WHERE UW_KEY = '20240625-012'
GROUP BY
    BR_CD;
```

#### 예시 데이터
| BR_CD | UL_CD | UL_NM  |
|-------|-------|--------|
| BR1   | NULL  | NULL   |
| BR1   | UL1   | Name1  |
| BR1   | NULL  | NULL   |
| BR2   | UL2   | Name2  |
| BR2   | UL3   | Name3  |
| BR2   | NULL  | NULL   |

#### 결과
| BR_CD | UL_CD | UL_NM  |
|-------|-------|--------|
| BR1   | UL1   | Name1  |
| BR2   | UL3   | Name3  |

### 요약
- `COALESCE` 함수는 `NULL` 값을 대체합니다.
- `MAX` 함수는 그룹화된 데이터에서 최대 값을 선택합니다.
- `COALESCE(MAX(UL_CD), '')`는 그룹화된 데이터에서 `UL_CD`의 최대 값을 선택하고, `NULL`인 경우 빈 문자열을 반환합니다.

이렇게 하면 그룹화된 데이터에서 `NULL`이 아닌 최대 값을 선택하면서, `NULL` 값을 적절히 처리할 수 있습니다.

Q1: `COALESCE`와 `MAX` 함수를 결합하면 어떤 장점이 있을까요?
Q2: 이 방법을 사용하여 해결할 수 있는 다른 SQL 문제는 어떤 것이 있을까요?


