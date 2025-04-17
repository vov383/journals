---
title: DataRowExtensions.Field≺T≻() 메서드의 DB null 값 처리
created: 2025-04-09 03:35
alias:
tags:
---
### 기본 개념
`DataRowExtensions.Field<T>()` 메서드는 지정한 열의 값을 T 형식으로 반환합니다.

- 만약 DB의 해당 열 값이 **DBNull.Value**이면, T가 참조형이면 기본값(default(T))을 반환합니다.
    
- **참조형의 기본값**은 `null`입니다.
    

---

### 코드 예시 및 동작 확인

```csharp
// DataRow에서 "REMARK" 컬럼의 값을 string 타입으로 추출
string remark = dr.Field<string>("REMARK");

// 만약 DB의 "REMARK" 값이 DBNull인 경우, remark 변수에는 null이 할당됩니다.
if (remark == null)
{
    // 필요에 따라 null 대신 string.Empty를 사용할 수 있음.
    remark = string.Empty;
}
```

- **설명:**
    
    - `dr.Field<string>("REMARK")`는 "REMARK" 컬럼의 값이 DBNull이면, `default(string)` 즉, `null`을 반환합니다.
        
    - 따라서, 별도의 null 처리 없이 사용하면 값이 null로 설정되며 예외는 발생하지 않습니다.
        
    - 만약 null 대신 빈 문자열(string.Empty)을 사용하고 싶다면, null 병합 연산자(`??`)를 활용할 수 있습니다.
        

---

### Q3. null 병합 연산자를 이용한 간결한 처리

```csharp
// null 병합 연산자를 이용하여 null은 string.Empty 처리
string ulcd = dr.Field<string>("UL_CD") ?? string.Empty; 
string rep_dev = dr.Field<string>("REP_DEV") ?? string.Empty; 
string rep_gubun = dr.Field<string>("REP_GUBUN") ?? string.Empty; 
string rep_group = dr.Field<string>("REP_GROUP") ?? string.Empty;
string remark = dr.Field<string>("REMARK") ?? string.Empty;
```

- **동작:**
    
    - DB의 값이 null이면 `string.Empty`로 대체되며, 그렇지 않으면 원래의 값을 할당합니다.
        

---

### 요약 포인트

- **DB null 처리:**
    
    - DB의 null 값은 `DBNull.Value`로 저장되며, `Field<string>()` 호출 시 null이 반환됨.
        
- **예외 발생 여부:**
    
    - 예외는 발생하지 않고, string 타입의 경우 null이 할당됨.
        
- **추가 처리:**
    
    - null 대신 빈 문자열이 필요하면 null 병합 연산자(`??`)를 사용하면 간편하게 처리할 수 있음.
        

이와 같이, `Field<string>("REMARK")`를 호출할 때 DB 값이 null이면 예외 발생 없이 null이 반환되며, 추가 처리를 통해 원하는 결과로 변환할 수 있습니다.


