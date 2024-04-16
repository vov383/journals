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



#### CheckBoxCellType의 속성 설명
`CheckBoxCellType`은 
FarPoint Spread 또는 유사 스프레드시트 컴포넌트에서 제공하는 
셀 타입으로, 
셀 내에 체크박스를 표시하는 기능을 제공합니다. 
이 셀 타입은 여러 속성을 통해 
체크박스의 동작과 표시 방식을 사용자가 정의할 수 있게 해줍니다. 
`SetEditorValue`, `TextTrue`, `TextFalse`는 이 중 체크박스와 관련된 주요 속성들입니다.

#### SetEditorValue
체크박스가 사용자에 의해 변경될 때 
셀 값의 업데이트 방식을 제어합니다. 
기본적으로, 사용자가 체크박스를 클릭하면, 
Spread는 체크 상태에 따라 셀 값에 자동으로 Boolean 값(`true` 또는 `false`)을 설정합니다. 
`SetEditorValue`를 사용하여 이 동작을 
사용자 정의 로직으로 대체할 수 있습니다.

#### TextTrue 및 TextFalse
체크박스와 함께 표시되는 텍스트를 정의합니다. 
`TextTrue`는 체크박스가 선택된 상태일 때 표시될 텍스트를 지정하며, 
`TextFalse`는 체크박스가 선택되지 않은 상태일 때 표시될 텍스트를 정의합니다. 
이 속성들을 사용하여 사용자에게 보다 명확한 시각적 피드백을 제공할 수 있습니다.

### 코드 예시
```csharp
CheckBoxCellType checkBoxCell = new CheckBoxCellType();
checkBoxCell.TextTrue = "활성화";  // 체크 시 표시될 텍스트
checkBoxCell.TextFalse = "비활성화";  // 체크 해제 시 표시될 텍스트
sheet.Cells[0, 0].CellType = checkBoxCell;
sheet.Cells[0, 0].Value = true;  // 초기값 설정
```

#### 실용적인 응용
이 속성들은 사용자 인터페이스에서 체크박스의 역할을 명확히 하는 데 유용합니다. 
예를 들어, 사용자가 어떤 설정을 '켜기' 또는 '끄기'로 전환할 때, 
각 상태를 설명하는 텍스트를 제공함으로써 
사용자 경험을 향상시킬 수 있습니다.

Q1 : `TextTrue`와 `TextFalse` 외에 다른 시각적 구분을 제공하는 방법은 무엇이 있을까요?
Q2 : `SetEditorValue`를 사용하여 사용자 입력을 다른 데이터 타입으로 변환하는 예제 코드를 작성할 수 있을까요?




