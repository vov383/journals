---
title: SceneView, GameView의 Shader의 적용을 받는 Object의 filp문제
created: 2024-12-10 11:18
alias:
tags:
---
일단 원인은 모르겠음.
해결방법은 GameView 창에서 켜놓은 Gizmo 기능을 Off했더니 해결됨.

문제 원인에 대한 추측
### 근본적인 원인 분석

#### 1. **Gizmo와 카메라의 좌표계 충돌**

- **Scene View**와 **Game View**는 Unity에서 서로 다른 카메라를 사용합니다:
    - Scene View: Unity Editor의 카메라 (Editor Camera)
    - Game View: `Main Camera`와 다른 사용자 정의 카메라
- Gizmo는 주로 **Editor 카메라**에서 렌더링되는데, Game View에서 Gizmo가 활성화될 경우, Gizmo의 렌더링이 Main Camera의 좌표계에 간섭하거나 **Depth Buffer**에 영향을 미쳤을 가능성이 있습니다.

#### 2. **Depth Buffer 간섭**

- Gizmo는 Scene에서 시각적으로 보이도록 렌더링되며, 이는 Depth Buffer에 영향을 줄 수 있습니다.
- Game View에서 Gizmo가 활성화되면, Gizmo가 Outline이나 Material Shader와 동일한 Depth Layer를 공유하거나 Depth Write 설정에 간섭했을 가능성이 큽니다.

#### 3. **렌더링 순서(Render Queue) 문제**

- Gizmo는 Unity에서 별도로 관리되는 렌더링 요소로, 일반적으로 **Overlay Queue** 또는 특정 렌더링 레이어에서 동작합니다.
- Outline Shader나 Material Shader가 Gizmo의 렌더링 순서에 의해 간섭받았을 가능성이 있습니다. 특히, Shader가 `Queue="Transparent"`로 설정된 경우 렌더링 순서에 더 민감하게 반응합니다.

#### 4. **Camera Stack 및 Layer 충돌**

- Unity의 **Camera Stack**에서 Gizmo가 잘못된 Layer에서 렌더링되었거나, `Main Camera`와 `UICamera`가 동일한 Layer의 Gizmo를 렌더링하면서 충돌이 발생했을 수 있습니다.
- Game View에서는 Gizmo가 활성화되면 UI와 같은 Layer와 Depth 정보를 공유할 수 있으며, 이는 Outline이나 Material의 위치 문제를 초래할 수 있습니다.

#### 5. **Projection Matrix와 View Matrix 혼동**

- Gizmo는 Scene View의 **Projection Matrix** 및 **View Matrix**에 따라 렌더링됩니다.
- Game View에서 Gizmo가 활성화되면 카메라의 Projection Matrix가 예상과 다르게 동작하여 Outline이나 Material의 위치가 왜곡되었을 가능성이 있습니다.


### 원인에 따른 해결 방법 및 예방책

#### 1. **Gizmo와 Depth Buffer 문제 해결**

- Gizmo는 기본적으로 **ZTest Always**로 렌더링될 가능성이 높습니다. 따라서 Shader의 Depth 설정을 명시적으로 관리하여 Depth Buffer에 간섭하지 않도록 합니다:
    

#### 2. **Shader의 Render Queue 확인**

- Gizmo와 동일한 Queue에서 렌더링되지 않도록 Shader의 `Queue`를 명확히 설정합니다:
    
- `Transparent` Queue를 사용하는 경우, Gizmo의 렌더링 순서와 간섭할 수 있으므로, 가능한 한 Gizmo와 다른 Queue를 사용합니다.

#### 3. **Camera Stack 관리**

- Main Camera와 UI Camera가 동일한 Layer를 렌더링하지 않도록 Culling Mask를 분리합니다:
    - **Main Camera**: 3D 오브젝트 전용 Layer (예: Default)
    - **UICamera**: UI 전용 Layer (예: UI)

#### 4. **Projection Matrix 정리**

- Gizmo가 Game View에서 Projection Matrix에 영향을 미치지 않도록, Shader에서 좌표 변환을 명시적으로 처리합니다:
    

#### 5. **Gizmo 비활성화 유지**

- Game View에서 Gizmo를 비활성화하는 것이 가장 간단한 해결책입니다. Gizmo는 주로 디버깅 용도로 사용되며, Game View에서는 불필요한 경우가 많으므로 항상 꺼두는 것이 좋습니다.

### 결론

Game View에서 Gizmo가 Shader 및 Depth Buffer에 영향을 미쳤기 때문에 Outline과 Material의 위치 문제가 발생한 것으로 보입니다. 
이는 Unity의 **렌더링 순서, Depth Buffer 간섭, Projection Matrix 차이**에서 기인한 문제입니다. 근본적인 해결책은 Gizmo와 Shader 간의 충돌을 방지하는 것이며, 가장 쉬운 방법은 **Game View에서 Gizmo를 비활성화**하는 것입니다.


