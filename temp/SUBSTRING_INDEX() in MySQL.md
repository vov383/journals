---
title: SUBSTRING_INDEX() in MySQL
created: 2025-04-07 02:34
alias:
tags:
---
`SUBSTRING_INDEX()` 함수는 MySQL에서 문자열을 
특정 구분자(delimiter)를  기준으로 분리하여 
원하는 부분만 추출할 때 사용하는 함수입니다.

### 함수 문법

```sql
SUBSTRING_INDEX(str, delim, count)
```

- **str**: 대상 문자열
    
- **delim**: 문자열을 나눌 구분자
    
- **count**:
    - **양수**: 왼쪽부터 구분자가 나타나는 횟수만큼 추출
    - **음수**: 오른쪽부터 구분자가 나타나는 횟수만큼 추출
    - **0**: 빈 문자열 반환
        


### 주요 특징 및 사용 예제

#### 1. 왼쪽부터 추출 (양수 count)

- **예시**:
    ```sql
    SELECT SUBSTRING_INDEX('B_150_200_20', '_', 2) AS result;
    ```
    - **설명**: 문자열 `'B_150_200_20'`에서 왼쪽부터 2번째 구분자까지의 부분인 `'B_150'`을 반환
        

#### 2. 오른쪽부터 추출 (음수 count)

- **예시**:
    
    ```sql
    SELECT SUBSTRING_INDEX('B_150_200_20', '_', -1) AS result;
    ```
    
    - **설명**: 문자열에서 오른쪽부터 첫 번째 구분자 이후의 부분인 `'20'`을 반환
        

#### 3. 중첩 사용
- **예시**: 특정 인덱스의 값을 추출하기 위해 중첩하여 사용
    
    - **YARD_CD 추출**:
        ```sql
        SUBSTRING_INDEX('B_150_200_20', '_', 1)  -- 결과: 'B'
        ```
        
    - **PILE_FROM 추출**:
        ```sql
        SUBSTRING_INDEX(SUBSTRING_INDEX('B_150_200_20', '_', 2), '_', -1)  -- 결과: '150'
        ```
        
    - **PILE_TO 추출**:
        ```sql
        SUBSTRING_INDEX(SUBSTRING_INDEX('B_150_200_20', '_', 3), '_', -1)  -- 결과: '200'
        ```
        
    - **CI_TON 추출**:
        ```sql
        SUBSTRING_INDEX(SUBSTRING_INDEX('B_150_200_20', '_', 4), '_', -1)  -- 결과: '20'
        ```
        

### 주의 사항

- **구분자가 없는 경우**: 지정된 구분자가 없으면 원본 문자열 전체가 반환됩니다.
    
- **중첩 사용**: 여러 구분자로 나누어 특정 부분만 추출할 때, 중첩 사용을 통해 단계별로 값을 분리합니다.
    
- **음수 count**: 음수 값을 사용하면 오른쪽부터 추출하므로, 원하는 값을 정확하게 추출하려면 count 값에 주의해야 합니다.
    


### 요약 포인트

- **목적**: 문자열을 구분자를 기준으로 분리하여 원하는 부분만 추출
- **구문**: `SUBSTRING_INDEX(str, delim, count)`
- **양수/음수 사용**: 양수는 왼쪽, 음수는 오른쪽부터 추출
- **중첩 사용**: 복잡한 문자열 분리에 효과적
    
이와 같이 `SUBSTRING_INDEX()` 함수는 문자열 분리 및 특정 부분 추출에 매우 유용하게 활용할 수 있습니다.
