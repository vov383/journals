---
title: FPSpread의 CellType Checkbox
created: 2024-04-15 12:57
alias:
tags:
---
FPSpread는 스프레드시트 기능을 제공하는 컨트롤로서, 
다양한 셀 형식을 지원합니다. 
`CellType` 중 `CheckBox`는 
사용자가 데이터 입력을 
체크박스 형태로 할 수 있게 해주는 기능입니다. 
이는 주로 사용자가 Yes/No 또는 True/False 선택을 할 때 사용됩니다.
###### 주요 기능
**데이터 바인딩**
CheckBox 셀은 일반적으로 Boolean 값(예: True/False)과 연동되어 
사용자의 입력을 데이터 모델에 자동으로 반영할 수 있습니다.
**상태 커스터마이징**
CheckBox의 상태(체크됨, 체크되지 않음, 중립)와 
표시 방법을 사용자 정의할 수 있습니다.

###### 주요 메서드
**SetCellType**
특정 셀 또는 셀 범위에 CheckBox 셀 타입을 설정합니다.
**GetCellType**
지정된 셀의 셀 타입을 조회합니다.
**SetCellValue**
CheckBox의 값을 설정합니다.
**GetCellValue**
CheckBox의 현재 값을 가져옵니다.

C#에서 CheckBox 셀 타입을 설정하는 예제 코드는 다음과 같습니다

```csharp
FarPoint.Win.Spread.CellType.CheckBoxCellType cbCellType = new FarPoint.Win.Spread.CellType.CheckBoxCellType();
spreadSheet.ActiveSheet.Cells[0, 0].CellType = cbCellType;
spreadSheet.ActiveSheet.Cells[0, 0].Value = true;  // 체크박스를 체크 상태로 설정
```

이 코드는 스프레드시트의 첫 번째 셀에 체크박스를 생성하고, 체크 상태로 초기화합니다.

Q1 : FPSpread에서 CheckBox 셀 타입을 사용할 때, 사용자 입력에 따라 자동으로 데이터를 업데이트하는 방법은 무엇입니까?

Q2 : 다른 셀 타입과 함께 CheckBox를 조합하여 사용할 때 주의해야 할 점은 무엇입니까?


