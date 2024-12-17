---
title: 유니티 ScrollView Scroll Rect 컴포넌트
created: 2024-12-09 11:14
alias:
tags:
---
### Scroll Rect 컴포넌트의 주요 속성

#### **1. Content**

- **설명**: 스크롤할 실제 콘텐츠가 들어 있는 **RectTransform**.
- 이 필드에 스크롤 가능한 콘텐츠를 참조로 설정해야 합니다. 보통 `Vertical Layout Group`이나 `Horizontal Layout Group`을 포함하는 `Content` 객체를 사용합니다.

#### **2. Horizontal / Vertical**

- **설명**: 콘텐츠를 수평(Horizontal) 또는 수직(Vertical)으로 스크롤할 수 있는지 여부를 설정합니다.
    - `Horizontal`: 체크하면 콘텐츠를 가로로 스크롤 가능.
    - `Vertical`: 체크하면 콘텐츠를 세로로 스크롤 가능.

#### **3. Movement Type**

- 콘텐츠가 뷰포트 안에서 어떻게 움직이는지를 정의합니다.
    - **Unrestricted**: 콘텐츠가 뷰포트 밖으로 무한히 이동할 수 있음.
    - **Elastic**: 콘텐츠가 뷰포트 밖으로 약간 넘어갈 수 있으며, 다시 원래 위치로 돌아옵니다.
    - **Clamped**: 콘텐츠가 뷰포트 밖으로 나가지 못하게 제한됩니다.

#### **4. Inertia**

- **설명**: 스크롤 시 관성이 적용되어 스크롤이 부드럽게 멈추는 동작을 활성화합니다.
- 체크를 해제하면 사용자가 스크롤을 멈췄을 때 즉시 정지합니다.


#### **5. Deceleration Rate**

- **설명**: 관성으로 스크롤할 때 감속 비율을 설정합니다.
- 값이 작을수록 스크롤이 더 오래 유지되고, 값이 클수록 더 빨리 멈춥니다.


#### **6. Scroll Sensitivity**

- **설명**: 스크롤 휠이나 터치 입력에 대한 민감도를 조정합니다.
- 값이 높을수록 스크롤 입력이 더 크게 반응합니다.


#### **7. Viewport**

- **설명**: 사용자가 실제로 볼 수 있는 스크롤 영역(창)을 설정하는 **RectTransform**.
- 일반적으로 `Scroll View`의 **Viewport** GameObject를 참조로 설정합니다.


#### **8. Horizontal Scrollbar / Vertical Scrollbar**

- **설명**: 콘텐츠를 스크롤할 때 사용할 가로/세로 스크롤바를 설정합니다.
- 스크롤바를 연결하면 스크롤 동작에 따라 스크롤바가 업데이트됩니다.
- **Missing**으로 표시되면 스크롤바가 연결되지 않았음을 의미합니다.


#### **9. On Value Changed**

- **설명**: 스크롤이 변경될 때 호출되는 콜백 이벤트입니다.
- 이벤트는 `Vector2` 값을 반환하며, 이는 콘텐츠의 스크롤 위치를 나타냅니다.
    - `x`: 가로 위치 (0~1).
    - `y`: 세로 위치 (0~1).
- 이 이벤트를 사용하여 스크롤 위치에 따라 동작을 추가할 수 있습니다.


### Scroll Rect 동작 원리

1. **Content**가 스크롤 영역에 배치됩니다.
    - `Vertical Layout Group`, `Horizontal Layout Group` 또는 `Grid Layout Group`을 사용해 콘텐츠를 정렬.
2. **Viewport**는 스크롤 가능한 영역을 제한하는 역할을 합니다.
    - 콘텐츠가 Viewport 영역을 벗어나면 Scroll Rect가 스크롤을 관리합니다.
3. 사용자는 마우스 스크롤, 드래그, 터치 등으로 콘텐츠를 이동할 수 있습니다.
4. Scroll Rect는 스크롤 동작을 처리하며, 필요한 경우 스크롤바를 업데이트합니다.


### 예제 설정

#### **Scroll View 기본 구조**

```
Scroll View (Scroll Rect)
    └ Viewport (Mask + RectTransform)
        └ Content (RectTransform)
```

1. **Scroll View**:
    
    - Scroll Rect 컴포넌트를 포함.
    - `Content`와 `Viewport`를 설정.
2. **Viewport**:
    
    - Mask 컴포넌트를 추가하여 콘텐츠가 뷰포트를 벗어나면 보이지 않게 처리.
3. **Content**:
    
    - `Vertical Layout Group`을 추가하여 리스트 아이템을 정렬.
    - `Content Size Fitter`를 추가하여 콘텐츠 크기를 동적으로 조정.


### 요약

1. **Content**는 스크롤할 콘텐츠 영역을 설정.
2. **Viewport**는 스크롤 가능한 영역(사용자가 보는 부분).
3. **Horizontal/Vertical**로 스크롤 방향을 설정.
4. **Movement Type**으로 스크롤 동작(탄성, 제한 등)을 설정.
5. **On Value Changed** 이벤트로 스크롤에 따라 추가 작업을 수행.

Q1: 여러 아이템이 있는 콘텐츠를 동적으로 추가하려면 어떻게 구성하는 것이 효율적일까요?  
Q2: 스크롤 이벤트를 활용해 특정 위치에서 애니메이션이나 효과를 추가하려면 어떤 방법을 사용할 수 있을까요?


