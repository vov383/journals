---
title: HorizantalLayoutGroup in Unity
created: 2025-07-21 02:24
alias:
tags:
---
유니티 가로로 버튼 패널을 만들 때 좌 우에 여백 넣고 균등한 간격으로 버튼 배치

![[../../noGitSync/Attachments/Pasted image 20250721145354.png]]
좌 우에 여백 패널을 넣고 
LayoutElement 속성값을 다음과 같이 수정
FlexibleWidth = true, 
LaoutPriority = 1

	
개별 버튼은 속성값 다음과 같이 수정
MinWidth Check, value = 74
PreferredWidth Check, value = 74


