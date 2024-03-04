---
title: listView 컨트롤
created: 2024-02-22 12:43
alias:
tags:
---
`ListView` 컨트롤을 사용할 때 셀 클릭 동작이 제한적으로 느껴지는 경우, 
문제의 원인과 해결 방법은 `DataGridView` 사용 시와 다소 차이가 있을 수 있습니다. 
`ListView` 컨트롤은 기본적으로 항목(아이템)과 해당 아이템의 하위 항목(subitems)을 표시하는 데 사용되며, 사용 방식과 설정이 `DataGridView`와는 다릅니다. 
여기 `ListView`에서 특정 항목 또는 하위 항목의 클릭을 제한하는 일반적인 시나리오와 해결 방법을 소개합니다.

# 1. `ListView`의 Selection Mode 설정

`ListView` 컨트롤은 `SelectionMode` 속성이 없으며, 항목을 선택하는 방식은 `FullRowSelect` 속성을 통해 제어됩니다. `FullRowSelect`가 `true`로 설정되면, 사용자가 항목의 어느 부분을 클릭하든 전체 행이 선택됩니다. 만약 특정 하위 항목에 대한 클릭만 처리하려면, 이벤트 핸들러 내에서 클릭된 위치를 계산하여 해당 하위 항목을 식별해야 합니다.

# 2. `MouseClick` 이벤트 사용

`ListView` 컨트롤에서 특정 하위 항목의 클릭만 처리하려면 `MouseClick` 또는 `MouseDown` 이벤트를 사용하고, 이벤트 핸들러 내에서 클릭된 위치를 기반으로 해당 하위 항목을 찾아내야 합니다. 이를 위해 `HitTest` 메서드를 사용할 수 있습니다.

# 예제 코드: `ListView`에서 특정 하위 항목 클릭 처리

```csharp
private void listView1_MouseClick(object sender, MouseEventArgs e)
{
    ListViewHitTestInfo info = listView1.HitTest(e.X, e.Y);
    if (info.Item != null)
    {
        // 전체 아이템이 클릭됨
        if (info.SubItem != null)
        {
            // 특정 하위 항목이 클릭됨
            int columnIndex = info.Item.SubItems.IndexOf(info.SubItem);
            if (columnIndex == 0) // 예를 들어, 'id' 컬럼이 첫 번째 열에 있다고 가정
            {
                // 'id' 하위 항목 클릭 시의 처리 로직
            }
        }
    }
}
```

이 코드는 `MouseClick` 이벤트를 사용하여 사용자가 `ListView`의 특정 하위 항목을 클릭했는지 확인합니다. `HitTest` 메서드는 클릭된 위치에 대한 정보를 제공하며, 이를 통해 특정 열(하위 항목)에 대한 클릭을 식별할 수 있습니다.

# 3. 항목의 `Selected` 속성 조작

`ListView`에서는 각 항목의 `Selected` 속성을 통해 프로그래매틱하게 선택 상태를 변경할 수 있습니다. 특정 조건에서만 항목을 선택하도록 하려면, 이벤트 핸들러 내에서 해당 조건을 확인하고 `Selected` 속성을 적절히 설정하면 됩니다.

`ListView`와 `DataGridView`는 서로 다른 컨트롤로, 각각의 특성과 사용 방법에 맞게 이벤트 핸들링과 속성 설정을 고려해야 합니다. `ListView`의 경우, 사용자의 클릭에 따른 상세한 제어가 필요할 때는 이벤트 핸들러 내에서 클릭된 위치와 해당 위치에 해당하는 항목 또는 하위 항목을 정밀하게 식별하는 로직을 구현해야 합니다.


