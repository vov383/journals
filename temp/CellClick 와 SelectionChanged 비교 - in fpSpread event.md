---
title: CellClick 와 SelectionChanged 비교 - in fpSpread event
created: 2025-04-15 04:08
alias:
tags:
---
#### CellClick 이벤트
사용자가 특정 셀을 클릭할 때 발생합니다. 클릭된 셀에 대한 정보를 제공하며, 주로 사용자 입력이나 상호작용을 처리하는 데 사용됩니다.

- **발생 시점**: 셀을 클릭할 때
- **주 용도**: 클릭된 셀의 데이터 처리, 사용자 인터페이스 반응, 특정 셀 클릭에 대한 로직 실행

#### SelectionChanged 이벤트
선택이 변경된 후에 발생합니다. 여러 셀 또는 셀 범위의 선택이 완료된 상태에서 발생합니다. 셀 선택 변경에 따라 후처리를 해야 하는 경우 사용됩니다.

- **발생 시점**: 선택이 변경된 후
- **주 용도**: 선택된 셀의 데이터 처리, UI 업데이트, 선택된 범위에 대한 작업 실행

### 주요 차이점

1. **발생 시점**:
   - `CellClick`: 셀 클릭 시 발생
   - `SelectionChanged`: 선택 변경 후 발생

2. **용도**:
   - `CellClick`: 특정 셀 클릭에 반응, 단일 셀 작업
   - `SelectionChanged`: 선택 범위 변경 후 작업, 다중 셀 또는 범위 작업

3. **적용 범위**:
   - `CellClick`: 단일 셀
   - `SelectionChanged`: 여러 셀 또는 셀 범위

### Q1:
CellClick 이벤트를 사용하여 특정 셀을 클릭했을 때 해당 셀의 데이터를 어떻게 가져올 수 있나요?

### Q2:
SelectionChanged 이벤트를 사용하여 선택된 셀 범위의 데이터를 어떻게 실시간으로 업데이트할 수 있나요?

#### Summary
1. CellClick 이벤트는 셀 클릭 시 발생
2. SelectionChanged 이벤트는 선택 변경 후 발생
3. CellClick은 단일 셀 작업에 적합
4. SelectionChanged는 다중 셀 또는 범위 작업에 적합
5. CellClick은 사용자의 특정 셀 클릭에 반응
6. SelectionChanged는 선택된 셀 범위의 데이터 처리를 위해 사용
7. 두 이벤트 모두 사용자 상호작용에 따라 UI를 업데이트하는 데 사용됨


