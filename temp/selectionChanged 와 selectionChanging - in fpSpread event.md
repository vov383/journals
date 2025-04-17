---
title: selectionChanged 와 selectionChanging - in fpSpread event
created: 2025-04-15 04:07
alias:
tags:
---
#### selectionChanged 이벤트
선택이 변경된 후에 발생합니다. 셀이나 셀 범위가 변경된 이후에 실행됩니다. 선택이 완료된 상태에서 수행할 작업에 적합합니다.

- **발생 시점**: 선택이 변경된 후
- **주 용도**: 선택된 데이터 처리, UI 업데이트, 데이터 저장

#### selectionChanging 이벤트
선택이 변경되기 전에 발생합니다. 셀이나 셀 범위가 변경되기 전에 실행됩니다. 선택을 막거나 사용자 확인을 요구하는 작업에 적합합니다.

- **발생 시점**: 선택이 변경되기 전
- **주 용도**: 선택 변경 방지, 사용자 확인, 유효성 검사

### 주요 차이점

1. **발생 시점**:
   - `selectionChanged`: 선택 변경 후
   - `selectionChanging`: 선택 변경 전

2. **용도**:
   - `selectionChanged`: 선택된 데이터 후처리
   - `selectionChanging`: 선택 변경 전처리 및 유효성 검사

3. **유효성 검사**:
   - `selectionChanging`에서 선택 변경을 막을 수 있음

### Q1:
fpSpread에서 selectionChanging 이벤트를 사용하여 특정 셀 범위로의 선택을 막는 방법은 무엇인가요?

### Q2:
selectionChanged 이벤트를 사용하여 선택된 셀의 데이터를 실시간으로 업데이트하는 방법은 무엇인가요?

#### Summary
1. selectionChanged 이벤트는 선택 후 발생
2. selectionChanging 이벤트는 선택 전 발생
3. selectionChanged는 후처리에 적합
4. selectionChanging는 전처리에 적합
5. selectionChanging로 선택 변경을 막을 수 있음


