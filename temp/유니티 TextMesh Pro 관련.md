---
title: 유니티 TextMesh Pro 관련
created: 2024-12-09 10:05
aliases: 
tags:
---

#### 기본 폰트 설정
경로
```
Assests/TextMesh Pro/Resources/TMP Settings
```

TMP Settings 클릭 시 Inspector창

여기서 
![[Pasted image 20241209100745.png]]

Default Font Asset의 값을 기본 폰트로 지정할 폰트로 설정해주면 된다.

UI에서 Text를 생성하든, 
3D GameObject로 Text를 생성하든 기본 Font가 반영되어 있다.

출처 : 황유빈 사원

#### UI Object로 Text와 3D GameObject로 Text 차이점
UI로 만들어서 UI 영역에서 사용하는 것과
3D GameObject로 만들어서 사용하는것 구별 필요

왜?

일반적인 GameObject위에 UI text를 올리면 해당 게임오브젝트에 마우스 클릭 등 이벤트를 사용할 수 없는 문제가 발생한다.

출처 : 황유빈 사원

