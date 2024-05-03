---
title: TabControl in 윈폼
created: 2024-05-03 04:51
alias:
tags:
---
`TabControl`은 
윈도우 폼 어플리케이션에서 
여러 탭을 통해 다양한 정보를 그룹화하고 표시하는 데 사용되는 컨트롤
각 탭은 `TabPage`라는 컨트롤을 사용하여 구성됩니다.

###### 기본 속성
`TabPages` (탭 페이지의 컬렉션을 관리), 
`SelectedTab` (현재 선택된 탭 페이지), 
`Alignment` (탭의 위치), 
`Multiline` (여러 줄로 탭 표시 여부), 
`SizeMode` (탭 크기 조정 모드) 등이 있습니다.

###### 주요 이벤트
`TabControl`에서 사용할 수 있는 중요한 이벤트로는
`SelectedIndexChanged` (선택된 탭이 변경될 때 발생), 
`Selecting`과 `Selected` (탭 변경이 시작되고 완료될 때 발생) 등이 있습니다.

###### 심화 활용
심화 활용으로는 
탭을 동적으로 추가하거나 제거하는 기능, 
사용자 지정 탭 헤더를 만드는 방법, 
탭 간의 드래그 앤 드롭 기능을 구현하는 방법 등이 있습니다.

###### 예시 코드
C#을 사용한 간단한 `TabControl` 예시:
```csharp
TabControl tabControl = new TabControl();
TabPage tabPage1 = new TabPage("Tab 1");
TabPage tabPage2 = new TabPage("Tab 2");

tabControl.TabPages.Add(tabPage1);
tabControl.TabPages.Add(tabPage2);

this.Controls.Add(tabControl);
```

###### 동적 탭 관리
탭을 동적으로 추가하거나 삭제하는 기능은 `TabPages.Add()` 메서드와 `TabPages.Remove()` 메서드를 사용하여 구현할 수 있습니다.

###### 사용자 지정 탭 헤더
사용자 지정 탭 헤더를 만들기 위해서는 `DrawItem` 이벤트를 사용하고 `DrawMode` 속성을 `OwnerDrawFixed`로 설정해야 합니다.

Q1: `TabControl`의 `SizeMode` 속성에는 어떤 옵션이 있으며 각 옵션은 어떤 효과가 있나요?
Q2: 사용자가 탭 간에 드래그 앤 드롭을 할 수 있게 하려면 어떤 이벤트와 기술을 사용해야 하나요?


