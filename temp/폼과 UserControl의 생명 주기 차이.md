---
title: 폼과 UserControl의 생명 주기 차이
created: 2025-04-18 09:27
alias:
tags:
---
- **폼(Form)의 닫힘**
    
    - `FormClosed` 이벤트가 발생하며, 자식 컨트롤이 자동으로 `Dispose()`됩니다.
        
    - 이때 팝업 폼에서 쓴 `PanelFactory.Reset()`를 `FormClosed`에서 호출했다면 싱글톤이 확실히 초기화됩니다.
        
- **UserControl의 제거**
    
    - UserControl이 호스트 폼에서 제거되는 순간 반드시 `Dispose()`나 `HandleDestroyed`가 호출되지 않습니다.
        
    - 단순히 `Controls.Remove(...)`나 `Visible = false`만으로는 내부 `Disposed` 이벤트가 불리지 않아 팩토리 초기화 타이밍을 놓칩니다.


