---
title: 논리 연산자와 캐스팅을 사용하여 null값 처리
created: 2024-05-16 11:16
alias:
tags:
---
```cs
bool isChecked = cellValue != null && (bool)cellValue;
``` 

이 구문은 `cellValue`가 `null`이 아닌지 확인하고, 
`null`이 아닌 경우에는 `cellValue`를 `bool` 타입으로 캐스팅하여 `isChecked` 변수에 저장합니다. 
이 구문은 논리 연산자와 캐스팅을 사용하여 안전하게 값을 처리합니다.

### 구문 설명

1. **`cellValue != null`**:
   - 먼저 `cellValue`가 `null`인지 확인합니다.
   - `cellValue`가 `null`이 아니면 `true`를 반환합니다.
   - `cellValue`가 `null`이면 `false`를 반환합니다.

2. **`&&` (논리 AND 연산자)**:
   - 두 개의 조건이 모두 `true`일 때만 `true`를 반환합니다.
   - 첫 번째 조건(`cellValue != null`)이 `false`이면, 두 번째 조건은 평가되지 않습니다 (단락 평가, short-circuit evaluation).

3. **`(bool)cellValue`**:
   - `cellValue`가 `null`이 아닌 경우, `cellValue`를 `bool` 타입으로 캐스팅합니다.
   - 이 캐스팅이 성공하면 `cellValue`의 `bool` 값이 반환됩니다.

### 전체 구문의 의미
이 구문은 다음과 같은 의미를 가집니다
`cellValue != null`가 `true`인 경우에만 
`cellValue`를 `bool` 타입으로 캐스팅하고, 
`isChecked` 변수에 그 값을 저장합니다.

만약 `cellValue`가 `null`이면, 
`isChecked`는 `false`가 됩니다.

### 예제 코드
이 구문을 포함한 전체 코드는 다음과 같습니다:

```csharp
private bool _checkboxChangeProcessing = false; // 체크박스 변경 처리 플래그

private void changeCheckboxValue(object sender, int rIdx, int cIdx)
{
    if (_checkboxChangeProcessing)
        return;

    // 체크박스 변경 처리 시작
    _checkboxChangeProcessing = true;

    try
    {
        FpSpread fs = sender as FpSpread;
        SheetView ActiveSheet = fs.ActiveSheet;

        // 셀 값이 null인지 확인
        object cellValue = ActiveSheet.Cells[rIdx, cIdx].Value;
        bool isChecked = cellValue != null && (bool)cellValue;

        // 현재 셀이 체크되었다면 다른 셀들의 체크를 해제
        if (isChecked)
        {
            for (int i = 0; i < ActiveSheet.RowCount; i++)
            {
                if (i != rIdx && ActiveSheet.Cells[i, cIdx].CellType is FarPoint.Win.Spread.CellType.CheckBoxCellType)
                {
                    ActiveSheet.Cells[i, cIdx].Value = false;
                }
            }
        }
    }
    finally
    {
        // 체크박스 변경 처리 종료
        _checkboxChangeProcessing = false;
    }
}
```

### 요약
1. **`cellValue != null`**:
   - `cellValue`가 `null`인지 확인.
2. **`&&` (논리 AND 연산자)**:
   - 두 조건이 모두 `true`일 때만 `true` 반환.
3. **`(bool)cellValue`**:
   - `cellValue`를 `bool` 타입으로 캐스팅.
4. **결과**:
   - `cellValue`가 `null`이 아니고 `true`일 경우 `isChecked`는 `true`.
   - 그렇지 않으면 `isChecked`는 `false`.


