---
title: 얕은 복사(shallow copy)와 깊은 복사(deep copy)
created: 2024-04-08 03:33
alias:
tags:
---
문제가 발생하는 이유는 
변수 `dict2`와 `dict3`가 사실상 같은 객체를 참조하기 때문입니다. 
C#에서 변수에 객체를 대입할 때에는 객체의 참조가 대입되므로, 두 변수가 동일한 객체를 가리키게 됩니다. 
그래서 `dict2`의 변경이 `dict3`에도 영향을 미치게 됩니다.

이를 해결하기 위해서는 `dict2`를 복사하여 새로운 객체를 생성하고 이를 `dict3`에 대입해야 합니다. 
이를 수행하는 방법으로는 여러 가지가 있지만, 여기서는 `dict2`의 복사본을 만들어서 `dict3`에 대입하는 방법을 사용하겠습니다.

```csharp
var dict3 = new Dictionary<string, object>(dict2); // dict2의 복사본을 생성하여 dict3에 대입

if (!IsValidColorChange(scheduleFs, rIdx, cIdx + 1, _dragOverBackColor))
{
    DragDropOperationFromPortEntryCompleted();
    return; 
}

Cell currentAdjacentCell = scheduleSheet.Cells[rIdx, cIdx + 1];
dict3["m_flag"] = "E"; // 작업 끝 칸
dict3["m_disp_text"] = "";

scheduleSheet.Cells[rIdx, cIdx + 1].Tag = dict3;
currentAdjacentCell.BackColor = _berthPlanBackColor;
```

위의 코드에서 `new Dictionary<string, object>(dict2)`는 `dict2`의 복사본을 생성하는 방법입니다. 
따라서 `dict3`는 `dict2`의 값을 복사한 새로운 객체를 참조하게 되므로, `dict2`의 변경이 `dict3`에 영향을 미치지 않게 됩니다.

###### 얕은 복사 (Shallow Copy)
![[journals/temp/얕은 복사 (Shallow Copy)]]

###### 깊은 복사 (Deep Copy)
![[journals/temp/깊은 복사 (Deep Copy)]]

위의 코드에서 `var dict3 = new Dictionary<string, object>(dict2);` 
부분은 얕은 복사를 수행합니다. 
즉, `dict2`의 키-값 쌍은 복사되지만, 그 값이 객체일 경우에는 해당 객체의 참조가 복사되기 때문에 
두 변수는 사실상 같은 객체를 참조하게 됩니다. 
따라서 하나를 변경하면 다른 하나도 변경되는 것이죠.

해결책으로는 `dict2`의 복사본을 만들 때 깊은 복사를 수행하면 됩니다. 
예를 들어, `dict2`의 모든 요소를 새로운 `Dictionary`에 추가하는 방법이나 
직접적인 깊은 복사 방식을 사용할 수 있습니다.


