---
title: 윈에서 row 데이터를 List에 담아서 넘기는 코드
created: 2024-02-27 09:12
alias:
tags:
---
```CSharp 
public void SetItem(List<string> item)
{
    for (int i = 1; i < item.Count; i++) {
        listItem.Add(item[i]);
    }
}
```

Form1(메인폼) 데이터를 SetItem에 넣어서 다시 여기 리스트로 add함
