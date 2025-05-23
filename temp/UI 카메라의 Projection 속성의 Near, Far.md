---
title: UI 카메라의 Projection 속성의 Near, Far
created: 2024-12-10 11:13
alias:
tags:
---
UI 카메라의 **Projection 속성의 Near, Far 값**이 문제의 원인
UI 렌더링에서 중요한 속성


### Near와 Far의 역할

**Near**와 **Far**는 카메라의 클리핑(Clipping) 영역을 설정하는 값으로, 카메라가 렌더링할 수 있는 깊이(z축) 범위를 정의합니다.

#### 1. **Near (근평면, Near Clipping Plane)**

- 카메라에서 가장 가까운 렌더링 가능한 위치를 정의.
- Near보다 더 가까운 오브젝트는 렌더링되지 않고 잘립니다.

#### 2. **Far (원평면, Far Clipping Plane)**

- 카메라에서 가장 먼 렌더링 가능한 위치를 정의.
- Far보다 더 먼 오브젝트는 렌더링되지 않고 잘립니다.


### Near와 Far 값 문제의 원인

1. **UI 오브젝트가 Clipping 범위 밖에 있는 경우**
    
    - UI 요소의 `Z` 값이 `Near`보다 작거나 `Far`보다 크면 렌더링되지 않음.
    - 특히, `Z` 값이 0인데 Near 값이 0.3 등으로 설정된 경우 문제가 발생.
2. **Near와 Far 값의 차이가 지나치게 크거나 작은 경우**
    
    - Near와 Far 값의 차이가 크면 **깊이 버퍼(Depth Buffer)**의 정밀도가 떨어져 렌더링 문제가 발생.
    - 너무 작으면 많은 오브젝트가 Clipping 범위 밖으로 잘려 나감.


### Near와 Far 값을 설정할 때의 고려사항

#### 1. **적절한 범위 설정**

- UI 오브젝트의 `Z` 값을 기준으로 Clipping 범위를 설정합니다.
    - 일반적으로 **UI 카메라의 Near 값은 0.01 ~ 0.1, Far 값은 100 ~ 500** 사이로 설정.

#### 2. **UI 전용 카메라 설정**

- UI 전용 카메라에서는 **Render Mode**가 `Screen Space - Camera`일 경우 Near와 Far가 중요.
    - UI 오브젝트의 `Z` 값이 범위 내에 있도록 조정.

#### 3. **Depth Precision 최적화**

- Near와 Far 값의 차이를 최소화하면 Depth Buffer의 정밀도가 향상됩니다.
    - **Bad Example:** Near = 0.01, Far = 10000 (차이가 크면 정밀도 저하).
    - **Good Example:** Near = 0.1, Far = 500 (적당한 범위 설정).

#### 4. **World Space Canvas에서의 활용**

- World Space Canvas를 사용하는 경우, UI 오브젝트의 `Z` 값이 카메라의 Near와 Far 범위 내에 있어야 합니다.
    - UI 오브젝트의 `Z` 값을 월드 좌표에서 확인하고 조정.


### Unity에서 설정 방법

#### UI 카메라 설정:

1. **UI 카메라 선택** → **Inspector 창**에서 **Camera Component** 확인.
2. **Projection** 속성에서 **Near**와 **Far** 값 설정:
    - **Near:** 0.01 ~ 0.1.
    - **Far:** 100 ~ 500.


### 코드로 Near와 Far 값 설정

```csharp
using UnityEngine;

public class CameraClippingAdjuster : MonoBehaviour
{
    void Start()
    {
        Camera uiCamera = GetComponent<Camera>();
        if (uiCamera != null)
        {
            uiCamera.nearClipPlane = 0.1f; // Near 값 설정
            uiCamera.farClipPlane = 500f; // Far 값 설정
        }
    }
}
```


### 주의사항 및 추가 팁

1. **UI 카메라와 월드 카메라의 역할 분리**
    
    - UI 전용 카메라는 Depth Precision을 높이기 위해 Near와 Far 범위를 작게 설정.
    - 월드 카메라는 넓은 범위를 다룰 수 있도록 설정.
2. **Canvas Render Mode에 따른 영향**
    
    - `Screen Space - Overlay`: Near와 Far 값이 무시됨.
    - `Screen Space - Camera` 및 `World Space`: Near와 Far 값이 적용.
3. **툴팁과 같은 UI 요소**
    
    - `Z` 값을 0으로 유지하거나 Near와 Far 값 내에서 조정.


### 요약

1. **Near와 Far 정의**:
    - Near는 가장 가까운 렌더링 범위, Far는 가장 먼 렌더링 범위를 정의.
2. **문제 원인**:
    - UI 요소의 `Z` 값이 Near와 Far 범위를 벗어난 경우 발생.
3. **적절한 설정 값**:
    - Near: 0.01 ~ 0.1.
    - Far: 100 ~ 500.
4. **World Space와 Screen Space - Camera**:
    - Near와 Far 값이 World Space와 Screen Space - Camera 모드에서 중요.
5. **Depth Precision 최적화**:
    - Near와 Far 차이를 최소화해 렌더링 정확도를 높임.

**Q1:** Near와 Far 값을 동적으로 조정해 다양한 씬에서 최적의 Depth Precision을 유지하려면 어떻게 설계할 수 있을까요?  
**Q2:** UI 요소가 월드 오브젝트와 겹치는 상황에서 Depth 충돌을 방지하려면 어떤 추가적인 설정을 해야 할까요?


