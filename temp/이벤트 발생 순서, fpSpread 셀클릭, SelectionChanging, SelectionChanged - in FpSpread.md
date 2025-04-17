---
title: 이벤트 발생 순서, fpSpread 셀클릭, SelectionChanging, SelectionChanged - in FpSpread
created: 2025-04-15 04:08
alias:
tags:
---
### Event Sequence in fpSpread: CellClick, SelectionChanging, and SelectionChanged

#### 1. CellClick 이벤트
사용자가 특정 셀을 클릭하면 이 이벤트가 발생합니다. 이 이벤트에서 특정 범위를 선택하도록 설정할 수 있습니다.

#### 2. SelectionChanging 이벤트
셀 선택이 변경되기 전에 이 이벤트가 발생합니다. 이 이벤트에서는 선택이 변경될 때의 유효성 검사를 수행하거나 선택 변경을 막을 수 있습니다.

#### 3. SelectionChanged 이벤트
셀 선택이 변경된 후에 이 이벤트가 발생합니다. 최종 선택된 셀 범위에 대한 후처리를 수행합니다.

### 이벤트 발생 순서

1. **CellClick 이벤트**:
   - 사용자가 셀을 클릭합니다.
   - 이 이벤트 핸들러에서 특정 범위를 선택하도록 코드를 작성합니다.
   - 선택 변경이 발생하면 `SelectionChanging` 이벤트가 자동으로 호출됩니다.

2. **SelectionChanging 이벤트**:
   - 선택이 변경되기 전에 호출됩니다.
   - 이 이벤트 핸들러에서 유효성 검사나 선택 변경을 취소하는 로직을 작성할 수 있습니다.
   - 선택이 유효한 경우, 선택 변경이 진행됩니다.

3. **SelectionChanged 이벤트**:
   - 선택 변경이 완료된 후에 호출됩니다.
   - 최종 선택된 범위에 대한 후처리를 수행합니다.

### 코드 예시

다음은 CellClick 이벤트에서 특정 범위를 선택하고, SelectionChanging 및 SelectionChanged 이벤트가 순차적으로 발생하는 예시입니다.

```csharp
// CellClick 이벤트 핸들러
void fpSpread_CellClick(object sender, CellClickEventArgs e)
{
    // 특정 셀 범위를 선택하도록 설정
    fpSpread.Sheets[0].SetSelection(e.Row, e.Column, 3, 3);
}

// SelectionChanging 이벤트 핸들러
void fpSpread_SelectionChanging(object sender, SelectionChangingEventArgs e)
{
    // 유효성 검사 또는 선택 변경 방지 로직
    // e.Cancel = true; // 선택 변경을 취소하려면 이 줄의 주석을 제거하세요.
}

// SelectionChanged 이벤트 핸들러
void fpSpread_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    // 최종 선택된 셀 범위에 대한 후처리
    MessageBox.Show("Selection Changed!");
}
```

### Q1:
CellClick 이벤트를 사용하여 특정 범위를 선택할 때 유효성 검사를 추가하려면 어떻게 해야 하나요?

### Q2:
SelectionChanging 이벤트에서 선택 변경을 취소해야 하는 경우, 어떤 조건을 체크할 수 있나요?

#### Summary
1. CellClick 이벤트는 사용자가 셀을 클릭할 때 발생
2. CellClick에서 특정 셀 범위를 선택하도록 설정 가능
3. SelectionChanging 이벤트는 선택 변경 전에 발생
4. SelectionChanging 이벤트에서 유효성 검사 가능
5. SelectionChanged 이벤트는 선택 변경 후에 발생
6. 선택 변경이 순차적으로 발생하며 각 이벤트가 호출됨
7. 이벤트 핸들러에서 각각의 작업을 처리하도록 설정 가능


