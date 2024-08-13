---
title: FpSpread의 Cell EditMode에서 서브에디터 팝업 비활성화 방법
created: 2024-08-13 02:03
alias:
tags:
---
FpSpread의 NumberCellType 셀에서 기본적으로 사용자가 셀을 더블클릭하면 계산기 팝업이 나타납니다. 이 계산기 팝업이 실행되지 않도록 하려면 `SubEditorOpening` 이벤트를 처리하여 해당 이벤트를 취소할 수 있습니다.

#### 계산기 팝업 비활성화 방법 요약

1. **SubEditorOpening 이벤트 처리**:
   - `FpSpread`의 `SubEditorOpening` 이벤트를 처리합니다.
   - 이벤트 처리 메서드에서 `SubEditorOpeningEventArgs`의 `Cancel` 속성을 `True`로 설정하여 계산기 팝업을 비활성화합니다.

2. **코드 예시**:

```csharp
private void fpSpread_SubEditorOpening(object sender, SubEditorOpeningEventArgs e)
{
    // 계산기 팝업을 비활성화
    e.Cancel = true;
}
```

이 방법을 사용하면, 사용자가 셀을 더블클릭하거나 편집 모드로 들어갔을 때 계산기 팝업이 나타나는 것을 방지할 수 있습니다.

#### 추가 참고 사항

- **NumberCellType 클래스**: NumberCellType에 대한 추가적인 속성과 메서드를 확인하여, 셀의 숫자 입력과 관련된 다양한 기능을 사용자 지정할 수 있습니다.
- **디자인 타임에서의 설정**: 디자인 타임에서는 프로퍼티 창에서 `CellType`을 `NumberCellType`으로 설정한 후, 필요한 속성들을 지정할 수 있습니다.

### 요약

- `SubEditorOpening` 이벤트를 처리하여 계산기 팝업을 비활성화할 수 있습니다.
- 이벤트 핸들러에서 `e.Cancel = true;`로 설정하여 계산기 팝업을 막습니다.
- NumberCellType 셀에서 숫자 입력에 대한 사용자 정의 설정을 할 수 있습니다.


