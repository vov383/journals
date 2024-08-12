---
title: DataGridView 관련 내용 정리
created: 2024-08-12 02:17
alias:
tags:
---
#### 1. **DataGridView 기본 설정**
   - DataGridView의 기본 설정을 처리하기 위한 메서드 `gridviewStyleBasic`이 소개되었습니다. 이 메서드는 전체 DataGridView의 스타일을 일관되게 설정하기 위해 공통으로 사용됩니다.
   - 기본적인 설정에는 `DockStyle`, `Margin`, `BorderStyle`, `CellBorderStyle`, `AllowUserToAddRows`, `SelectionMode`, `RowHeadersVisible`, `ColumnHeadersVisible` 등이 포함됩니다.
   - **색상 설정**: `DefaultCellStyle.ForeColor`, `GridColor`, `BackgroundColor`, `SelectionBackColor` 등의 색상 속성이 포함되어 DataGridView의 전반적인 시각적 스타일을 정의합니다.
   - **크기 및 사이즈 설정**: `AutoSizeColumnsMode`, `AllowUserToResizeColumns`, `AllowUserToResizeRows` 등의 속성을 통해 열 및 행 크기 조정을 제어합니다.

#### 2. **DataGridView의 행과 열 설정**
   - 특정 행이나 열에 대해 폰트 색상, 배경색, 크기 등을 설정하는 방법이 논의되었습니다.
   - `DefaultCellStyle.ForeColor`를 사용해 특정 행 또는 열의 폰트 색상을 설정하고, 행별로 개별적인 스타일을 적용할 수 있습니다.
   - 각 열이나 행의 너비 및 높이를 조정하는 방법이 포함되었으며, 열 너비 자동 조정 모드를 제어하기 위한 `AutoSizeColumnsMode`의 다양한 옵션이 설명되었습니다.

#### 3. **행 및 열의 크기 조정 방지**
   - 사용자가 DataGridView에서 마우스를 사용하여 행(Row) 또는 열(Column)의 크기를 조절하지 못하도록 설정하는 방법이 설명되었습니다.
   - `AllowUserToResizeColumns` 및 `AllowUserToResizeRows` 속성을 `false`로 설정하여 크기 조정을 비활성화할 수 있습니다.

#### 4. **그레이 에어리어 색상 설정**
   - DataGridView의 빈 영역(그레이 에어리어)의 배경색을 설정하는 방법이 포함되었습니다.
   - `BackgroundColor` 속성을 사용하여 그레이 에어리어의 색상을 지정할 수 있습니다.

#### 5. **첫 번째 행을 컬럼 헤더로 사용**
   - DataGridView에서 기본 컬럼 헤더를 숨기고, 첫 번째 행을 컬럼 헤더로 사용하는 방법이 논의되었습니다.
   - `ColumnHeadersVisible` 속성을 `false`로 설정한 후, 첫 번째 행의 각 셀의 값을 컬럼 헤더로 설정하고 첫 번째 행을 삭제하는 방법이 설명되었습니다.


#### 7. **마우스 이벤트 처리**
   - DataGridView에서 마우스 이벤트(`CellMouseEnter`, `CellMouseLeave`)를 사용하여 특정 셀에 마우스가 올라갔을 때 색상이나 스타일을 변경하는 방법이 포함되었습니다.
   - 이러한 이벤트는 셀에 동적인 반응을 추가하는 데 유용합니다.

#### 8. **UserControl 간 상호작용**
   - 여러 UserControl에서 각 UserControl의 DataGridView 간 선택 상태를 동기화하는 방법이 포함되었습니다.
   - 하나의 DataGridView에서 선택하면 다른 UserControl의 DataGridView 선택을 해제하는 방법이 제시되었습니다.


