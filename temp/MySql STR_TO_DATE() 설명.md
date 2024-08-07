---
title: MySql STR_TO_DATE() 설명
created: 2024-07-22 01:51
alias:
tags:
---
`STR_TO_DATE` 함수는 MySQL에서 문자열을 날짜 형식으로 변환하는 함수입니다. 사용법은 다음과 같습니다:

```sql
STR_TO_DATE(날짜_문자열, 날짜_포맷)
```

여기서 `날짜_문자열`은 변환하고자 하는 날짜 문자열을 의미하며, `날짜_포맷`은 해당 문자열이 어떤 형식으로 되어 있는지를 나타냅니다. 예를 들어, `'%Y%m%d'` 포맷은 "20240122"와 같은 형식을 나타냅니다.

#### 사용 예제
```sql
SELECT STR_TO_DATE('20240122', '%Y%m%d');
```

이 예제는 문자열 '20240122'을 날짜 '2024-01-22'로 변환합니다.

#### 주요 포맷 옵션
- `%Y`: 4자리 연도 (예: 2024)
- `%m`: 2자리 월 (01-12)
- `%d`: 2자리 일 (01-31)

### 요약
- 첫 번째 부분은 `STR_TO_DATE` 함수를 사용하여 문자열을 날짜로 변환한 후 비교합니다.
- 두 번째 부분은 이미 날짜 형식으로 저장된 열을 직접 비교합니다.
- `STR_TO_DATE` 함수는 문자열을 날짜 형식으로 변환하는 데 사용됩니다.


#### 문자열을 날짜로 변환하지 않고 바로 비교할 수 있는 상황에서 STR_TO_DATE 함수를 사용하는 이유
1. **데이터 저장 형식이 문자열인 경우**: 데이터베이스에 날짜가 문자열 형식으로 저장되어 있다면, 이를 날짜 형식으로 변환해야 정확한 비교가 가능합니다. `STR_TO_DATE` 함수는 이러한 변환을 가능하게 합니다.
2. **날짜 형식이 일관되지 않은 경우**: 데이터가 다양한 형식으로 저장된 경우, `STR_TO_DATE` 함수를 사용하여 일관된 날짜 형식으로 변환한 후 비교할 수 있습니다.
3. **타입 안정성**: 문자열로 저장된 날짜는 직접 비교할 때 예상치 못한 결과를 초래할 수 있습니다. 날짜로 변환한 후 비교하면 이러한 문제를 피할 수 있습니다.
4. **쿼리 가독성**: 코드에서 날짜 형식을 명확히 하는 것은 쿼리의 가독성을 높이고 유지보수를 쉽게 합니다.

