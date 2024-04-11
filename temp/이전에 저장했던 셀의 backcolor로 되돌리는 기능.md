---
title: 이전에 저장했던 셀의 backcolor로 되돌리는 기능
created: 2024-04-11 04:42
alias:
tags:
---
```CS
foreach (var item in _dragedShipCellDict)
{
    item.Value.BackColor = (Color)data["backColor"];
    
}
```


