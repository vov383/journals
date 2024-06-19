---
title: Null 체크
created: 2024-06-19 08:35
alias:
tags:
---
Null 체크는 프로그래밍에서 매우 중요합니다. 
객체나 변수의 값이 null인지 확인하지 않고 접근하려 하면 
NullPointerException 같은 오류가 발생할 수 있기 때문입니다. 
C#에서는 이러한 상황을 방지하기 위해 
다양한 null 체크 방법을 제공합니다.

#### null 조건 연산자 
null 조건 연산자 `?.`
객체가 null인지 아닌지 확인하고 
null이 아닐 경우에만 그 뒤의 속성이나 메서드를 호출합니다. 
null이면 전체 식의 결과가 null이 됩니다.

```csharp
int? sum = dto.PlanDtos?.Sum(x => x.UW_TON);
```

#### null 병합 연산자 (??)
null 병합 연산자 `??`는 왼쪽 피연산자가 
null이면 오른쪽 피연산자의 값을 반환합니다. 
왼쪽 피연산자가 null이 아니면 왼쪽 피연산자의 값을 반환합니다.

```csharp
int sum = dto.PlanDtos?.Sum(x => x.UW_TON) ?? 0;
```

#### LINQ에서 null 항목 제거
LINQ를 사용할 때 null 항목을 제거하려면 
`Where` 조건을 사용하여 필터링할 수 있습니다.

```csharp
var filteredList = dto.PlanDtos?.Where(x => x != null);
```

### 예제 코드 설명

이제 null 체크를 추가하여 오류를 방지하는 예제 코드를 설명하겠습니다.

```csharp
var tempDtos = (from dto in joinGroup
               select new ulTempPlanSheetDto
               {    
                   UL_NM = dto.ComUlDto.UL_NM,

                   // PlanDtos가 null이 아니고 그 안에 null이 아닌 항목들의 UW_TON 합계
                   SumOfUwTon = dto.PlanDtos?.Where(x => x != null).Sum(x => x.UW_TON) ?? 0,

                   // PlanDtos가 null이 아니고 그 안에 null이 아닌 항목들의 UW_TON 합계에서 SH_HOLD가 0이 아닌 항목들의 UW_TON 합계를 뺀 값
                   RemainAble = dto.PlanDtos?.Where(x => x != null).Sum(x => x.UW_TON) ?? 0 
                                - dto.PlanDtos?.Where(x => x != null && x.SH_HOLD != 0).Sum(x => x.UW_TON) ?? 0,

                   ComUlDto = dto.ComUlDto,

                   // PlanDtos가 null이 아니고 그 안에 null이 아닌 항목들의 리스트
                   UlDtos = dto.PlanDtos?.Where(x => x != null).ToList()
               }).ToList();
```

#### 주요 포인트

###### PlanDtos가 null이 아닌 경우 체크
PlanDtos가 null인지 먼저 체크하고,
null이 아니면 그 안의 항목들에 접근하도록 하였습니다.

###### 항목별 null 체크 추가
PlanDtos의 각 항목이 null인지 체크하여 null이 아닌 항목들만 필터링하였습니다.

###### 기본값 설정
null 병합 연산자 `??`를 사용하여 null인 경우 기본값을 0으로 설정하였습니다.

#### 요약
1. null 조건 연산자 `?.` 사용
2. null 병합 연산자 `??` 사용
3. LINQ에서 null 항목 필터링

#### 참고
[[temp/Nullable in CSharp|Nullable in CSharp]]
[[temp/null 병합 연산자 in CSharp|null 병합 연산자 in CSharp]]
[[temp/논리 연산자와 캐스팅을 사용하여 null값 처리|논리 연산자와 캐스팅을 사용하여 null값 처리]]


