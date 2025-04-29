---
title: 컨트롤의 좌표 변환 in WinForm
created: 2025-04-18 02:06
alias:
tags:
---
### DataGridView → UserControl 좌표 변환 과정

직접 “DataGridView 내부 좌표 ⇒ UserControl 내부 좌표” 로 변환하는 단일 API는 없음.  
다음의 두 단계를 거쳐야 한다.

###### PointToScreen()
**DataGridView 내부 좌표 ⇒ 화면(Screen) 좌표**
###### PointToClient()
**화면(Screen) 좌표 ⇒ UserControl 내부 좌표**

###### 예시
```csharp
// 1) 셀 내부 좌표
var cellRect = dataGridView.GetCellDisplayRectangle(colIndex, rowIndex, true);
Point dgvClientPt = cellRect.Location;

// 2) 화면 좌표로 변환
Point screenPt = dataGridView.PointToScreen(dgvClientPt);

// 3) UserControl 기준 좌표로 변환
Point ucClientPt = this.PointToClient(screenPt);
panel.Location = ucClientPt;
panel.BringToFront();
```

### 중간 Screen 좌표가 필요한 이유
- **윈폼 좌표계 분리**
    - 각 컨트롤은 독립된 클라이언트(Client) 좌표계(왼쪽 위가 (0,0))를 가짐
    - 서로 다른 컨트롤 사이에 직접 매핑 로직이 없음
    - 공용 기준인 “화면 좌표”를 중개점으로 사용
        
- **일관된 변환 메서드**
    - `Control.PointToScreen` ⇔ `Control.PointToClient` 조합으로만 안전하게 좌표가 변환
    - 중간 단계를 생략하면 위치가 어긋나거나 예외가 발생할 수


#### 요약 포인트

| 단계                | 메서드                            | 설명                          |
| ----------------- | ------------------------------ | --------------------------- |
| ① DGV 내부 ⇒ Screen | `PointToScreen`                | 셀 위치를 모니터 기준 좌표로 변환         |
| ② Screen ⇒ UC 내부  | `PointToClient`                | 화면 좌표를 UserControl 기준으로 변환  |
| 결과 활용             | `panel.Location = ucClientPt;` | UserControl 내부에 맞춰 Panel 배치 |
