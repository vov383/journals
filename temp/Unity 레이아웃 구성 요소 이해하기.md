---
title: Unity 레이아웃 구성 요소 이해하기
created: 2025-05-07 01:50
alias:
tags:
---
### Vertical Layout Group과 Layout Element
`Vertical Layout Group`은 자식 오브젝트들을 수직으로 배치
`Layout Element`은 각 자식 오브젝트의 크기와 위치를 조정하는 역할 

두 컴포넌트를 사용하려면 
우선 UI 요소들이 
어떤 방식으로 부모-자식 관계를 형성하는지 이해해야 하고, 
각 컴포넌트가 어떻게 올바르게 동작하는지 알고 있어야 합니다.

**참고 링크**: [Unity Layout Group](https://docs.unity3d.com/Manual/UI-LayoutElement.html)


Unity UI 레이아웃을 제대로 활용하려면, 
먼저 전체 UI 시스템의 근간이 되는 
#### Canvas와 RectTransform
`Canvas`와 `RectTransform`에 대한 이해가 필요합니다. 

##### RectTransform
`Canvas` 위에 배치된 모든 UI 오브젝트는 
RectTransform 컴포넌트를 통해 위치와 크기를 결정하고, 
이때 앵커(anchor)와 피벗(pivot)의 개념이 핵심이 됩니다. 

###### anchor
앵커는 부모 영역 대비 상대적 위치 기준을, 

###### pivot
피벗은 자체 사각형의 기준점을 나타내기 때문에, 

사이드바처럼 
일정한 폭을 유지하면서 높이가 가변적인 메뉴를 만들 때는 
앵커를 좌우에 고정하고 
위아래 피벗을 적절히 설정하는 것이 첫걸음입니다.

#### Vertical Layout Group
Vertical Layout Group은 
자식 요소들을 수직으로 자동 정렬·배치해 주는 컨테이너 컴포넌트로, 
다음 항목들을 사전에 알고 있어야 합니다. 

##### Padding과 Spacing
우선 Padding과 Spacing으로 외부 여백과 요소 간 간격을 조절할 수 있으며, 

##### Child Alignment
Child Alignment를 통해 전체 정렬 방향(왼쪽·가운데·오른쪽 정렬 및 상·중·하 정렬)을 지정할 수 있습니다. 

##### Control Child Size
`Control Child Size` 옵션을 켜면 `Layout Group`이 자식의 크기를 강제로 조절하고, 

##### Child Force Expand
`Child Force Expand`를 활성화하면 여분의 공간을 분배해 균등하게 늘려주는데, 
이 두 기능의 온·오프 조합에 따라 사이드바 메뉴의 버튼이나 아이콘 크기와 분포가 크게 달라집니다.

#### Layout Element
반면 `Layout Element`는 개별 자식 오브젝트에 붙여서 
최소(min), 권장(preferred), 유연(flexible) 크기를 지정할 수 있는 컴포넌트입니다. 

###### Preferred Height
예컨대 버튼마다 가로폭은 고정하되 세로폭은 콘텐츠에 맞춰 늘어나게 하려면 `Preferred Height`만 설정하고 

###### Flexible Height
`Flexible Height`를 0으로 두면 되고, 
반대로 공간이 허용되는 한 최대한 확장되길 원한다면 `Flexible Width/Height` 값을 1 이상으로 지정합니다. 

Layout Element의 값은 부모 Layout Group의 설정—특히 Control Child Size나 Force Expand—과 결합되어 최종 배치 결과를 만들어 내므로, 
두 컴포넌트가 어떻게 상호작용하는지 실험해 보면서 적절한 우선순위를 익혀야 합니다.

#### UI 레이아웃 시스템의 동작 순서
UI 레이아웃 시스템의 동작 순서도 중요합니다. 
##### LateUpdate
매 프레임 LateUpdate 단계에서 레이아웃이 재계산되고 
Canvas가 갱신되기 때문에, 
런타임에 자식 요소를 추가·제거하거나 크기를 변경하면 

##### Layout Rebuilder
`Layout Rebuilder`가 자동으로 실행되어 재정렬을 수행합니다. 
이 과정이 잦으면 퍼포먼스에 부담이 될 수 있으므로, 
가능한 정적 레이아웃은 에디터에서 설치해 두고, 
동적으로 변해야 할 부분만 코드나 스크립트로 컨트롤하는 전략이 필요합니다.

실무에서는 Vertical Layout Group과 Layout Element를 Content Size Fitter나 Aspect Ratio Fitter 등 다른 레이아웃 툴과 조합해 쓰기도 합니다. 
#### Content Size Fitter
예를 들어 사이드바 항목이 텍스트 길이에 따라 높이가 달라져야 한다면, 
Layout Element의 Preferred Height를 텍스트 콘텐츠에 맞춰 계산한 뒤 
`Content Size Fitter`로 감싸서 자동으로 맞추게 할 수 있습니다. 
하지만 이런 조합이 너무 많아지면 설정이 복잡해지고 충돌이 발생할 수 있으니, 
가급적 핵심 두 컴포넌트만으로 해결 가능한 구조를 설계하는 편이 유지·보수에 유리합니다.

요약하자면, 사이드바 레이아웃을 위해 반드시 숙지해야 할 요소는 
먼저 RectTransform의 앵커·피벗 개념, 
Vertical Layout Group의 Padding·Spacing·Control Child Size·Force Expand·Alignment 설정, 
그리고 Layout Element의 Min/Preferred/Flexible Width·Height 속성입니다. 
여기에 레이아웃 갱신 순서와 퍼포먼스 영향, 필요 시 
Content Size Fitter 같은 보조 툴과의 조합 방안까지 감안하면, 
원하는 대로 사이드바 메뉴를 배치하고 관리하는 데 큰 어려움이 없을 것입니다.


