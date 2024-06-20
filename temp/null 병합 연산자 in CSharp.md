---
title: null 병합 연산자 in CSharp
created: 2024-05-23 08:01
alias:
tags:
---
#### 2. `??` (null 병합 연산자)
`??` 연산자는 null 병합 연산자(null-coalescing operator)라고 불립니다. 
이 연산자는 왼쪽 피연산자가 `null`이 아닌 경우 그 값을 반환하고,
`null`인 경우 오른쪽 피연산자의 값을 반환합니다.

예를 들어:
```csharp
int? nullableInt = null;
int nonNullableInt = nullableInt ?? 10; // nullableInt가 null이므로 10을 반환
```

위의 코드에서 `nullableInt`가 `null`이기 때문에 `nonNullableInt`는 `10`이 됩니다. 
만약 `nullableInt`가 `null`이 아닌 값(예: 5)을 가지면, `nonNullableInt`는 그 값을 갖습니다.

```sql
{ SELECT SH_CD, BR_NM, 
	DATE_FORMAT(JOB_PLN_DT, '%Y-%m-%d') as JOB_DATE
	, YARD_NM
	, CI_TON
	, PILE_NO, PILE_FROM, PILE_TO 
FROM TB_COMEIN_PLAN 
WHERE (JOB_PLN_DT >= '2020-05-01 00:00:00' 
	   AND JOB_PLN_DT <='2024-06-31 23:59:59') 
	   AND SH_CD = 'hl' 
ORDER BY JOB_DATE}
```

