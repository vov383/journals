---
title: fpSpread의 EditModeReplace 속성
created: 2024-09-09 03:06
alias:
tags:
---
셀에 입력한 기존 값이 선택되지 않고 덮어씌워지도록 설정하고 싶을 때
```cs
	// 기존 값이 선택되지 않고 덮어씌워지도록 설정
	fpSpread.EditModeReplace = true;
```

### 해결 방법: `NumberCellType` 덮어쓰기 방식
이 방식에서는 사용자가 입력하는 숫자가 덧붙여지지 않고 기존 값이 새 값으로 대체되도록 합니다. 
아래 코드를 적용해 볼 수 있습니다:

```csharp
fpSpread.EditModeOn += (s, e) =>
{
    // 현재 활성화된 셀을 가져옴
    var activeCell = fpSpread.ActiveSheet.ActiveCell;
    
    if (activeCell.CellType is FarPoint.Win.Spread.CellType.NumberCellType)
    {
        // 셀에 새로운 값 입력 시 기존 값 덮어쓰기 설정
        activeCell.EditorMode = true;
        
        // 기존 값이 선택되지 않고 덮어씌워지도록 설정
        fpSpread.EditModeReplace = true;
    }
};
```


