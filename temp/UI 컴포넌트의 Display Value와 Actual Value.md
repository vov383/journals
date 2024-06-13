---
title: UI 컴포넌트의 Display Value와 Actual Value
created: 2024-06-13 09:39
alias:
tags:
---
### 예제 설명

해당 메서드는 
`TB_YARD_STOCK` 테이블에서 `YARD_CD` 컬럼의 값을 그룹화하여 가져오고,
그 결과를 `DataSet`으로 반환합니다. 

**메서드 코드 예제**

```csharp
public DataSet Select_TB_YARD_STOCK_Combobox_YARD()
{
    StringBuilder sql = new StringBuilder();

    sql.Append($" SELECT YARD_CD code, YARD_CD value");
    sql.Append($" FROM TB_YARD_STOCK ");
    sql.Append($" GROUP BY YARD_CD");

    DataSet ds = CommMysql.ExecuteDataSet(sql.ToString());
    if (ds != null && ds.Tables.Count > 0 && ds.Tables[0].Rows.Count > 0)
    {
        return ds;
    }

    return null;
}
```

**코드 설명**
1. **SQL 쿼리 생성**: `YARD_CD` 컬럼을 선택하고 `code`와 `value`라는 별칭을 부여합니다.
2. **데이터베이스 조회**: `CommMysql.ExecuteDataSet` 메서드를 사용하여 SQL 쿼리를 실행하고 결과를 `DataSet`으로 가져옵니다.
3. **결과 반환**: 결과가 존재하면 `DataSet`을 반환하고, 그렇지 않으면 `null`을 반환합니다.

### `code`와 `value` alias 사용
`code`와 `value`로 컬럼명을 변경하는 이유는 
주로 UI 컴포넌트와의 연계성 때문입니다. 
이는 데이터베이스에서 가져온 데이터를 UI 요소
(예: 콤보박스)에서 쉽게 사용하기 위함입니다.

#### 구체적인 이유

**1. 사용자 친화적 데이터 바인딩**
UI 컴포넌트, 
특히 콤보박스(ComboBox)나 드롭다운리스트(DropDownList)는 
일반적으로 표시할 값(Display Value)과 실제 값(Actual Value)을 가지게 됩니다.
`code`는 일반적으로 콤보박스의 `Value` 속성에 바인딩됩니다. 
즉, 사용자가 선택한 항목의 실제 값입니다.
`value`는 콤보박스의 `Text` 속성에 바인딩됩니다. 
즉, 콤보박스에서 사용자에게 표시되는 값입니다.

**2. 직관적인 이해**
개발자나 다른 사용자들이 코드를 읽을 때, 
`code`와 `value`라는 명칭을 통해 데이터의 역할을 직관적으로 이해할 수 있습니다.
`code`는 일반적으로 데이터베이스의 **키나 식별자 역할**을 하고, 
`value`는 **사용자에게 표시**되는 읽기 쉬운 형식의 값입니다.

**3. 일관된 데이터 처리**
데이터베이스 쿼리 결과를 UI 요소에 바인딩할 때, 
특정한 명명 규칙을 따름으로써 
코드의 일관성을 유지하고 유지보수성을 높일 수 있습니다.
특히 여러 데이터 소스에서 데이터를 가져와 UI에 바인딩할 때, 
일관된 컬럼 명칭을 사용하면 데이터 바인딩 코드가 간소화됩니다.

### 요약
1. UI 컴포넌트와의 연계성을 위해 `code`와 `value`를 사용.
2. `code`는 실제 값, `value`는 표시할 값으로 사용.
3. 직관적인 데이터 바인딩을 가능하게 함.
4. 데이터 처리의 일관성을 높임.

Q1: 콤보박스 외에도 `code`와 `value`를 사용하는 다른 UI 컴포넌트 예시는 무엇이 있나요?  
Q2: 동일한 방법으로 다른 테이블의 데이터를 가져올 때 주의해야 할 점은 무엇인가요?


