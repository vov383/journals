---
title: 유니티 Transform Component
created: 2024-12-06 04:24
alias:
tags:
---
### 1. **Transform**

모든 게임 오브젝트에 기본으로 포함되는 컴포넌트로, 위치, 회전, 크기를 정의합니다.

#### 주요 속성

- **Position (X, Y, Z):** 월드 공간에서의 위치.
- **Rotation (X, Y, Z):** 오브젝트의 회전 각도.
- **Scale (X, Y, Z):** 오브젝트의 크기 비율.
- **RectTransform (UI 전용):** UI 오브젝트의 위치와 크기 조정.

### Transform 컴포넌트 심화학습

**Transform**은 Unity에서 모든 게임 오브젝트의 위치, 회전, 크기를 관리하는 핵심 컴포넌트입니다. 이 컴포넌트를 잘 이해하면 오브젝트의 이동, 회전, 스케일링을 더 효과적으로 제어할 수 있습니다.


### 1. **Transform의 주요 속성**

#### **1.1 Position**

- 오브젝트의 **월드 공간**에서 위치를 나타냅니다.
- `transform.position`으로 접근하며, **Vector3** 값을 반환합니다.
- **지역 좌표(Local Position):**
    - 부모 오브젝트가 있는 경우, 위치는 부모를 기준으로 한 상대적인 값으로 나타납니다.
    - `transform.localPosition`으로 접근.

#### **1.2 Rotation**

- 오브젝트의 회전 각도를 나타냅니다.
- `transform.rotation`: **쿼터니언(Quaternion)**으로 반환됩니다.
    - **쿼터니언**은 회전을 처리하기 위한 복잡한 수학적 구조로, 짐벌 락(Gimbal Lock) 문제를 방지합니다.
- `transform.eulerAngles`: **Vector3**로 반환하며, 사용하기 더 직관적입니다.
    - 오브젝트의 X, Y, Z축 각도를 조작할 때 사용.

#### **1.3 Scale**

- 오브젝트의 크기를 나타냅니다.
- `transform.localScale`으로 접근하며, **Vector3** 값을 반환합니다.
- 주의: 부모 오브젝트가 있는 경우, 자식 오브젝트의 크기는 부모의 크기에 영향을 받습니다.


### 2. **Transform 관련 메서드**

#### **2.1 이동 관련**

1. **Translate**
    
    - 오브젝트를 지정된 방향으로 이동.
    - 로컬 좌표계 또는 월드 좌표계를 기준으로 이동 가능.
    
    ```csharp
    transform.Translate(Vector3.forward * Time.deltaTime);
    transform.Translate(Vector3.right * 2.0f, Space.World); // 월드 좌표
    ```
    
2. **SetPositionAndRotation**
    
    - 오브젝트의 위치와 회전을 동시에 설정.
    
    ```csharp
    transform.SetPositionAndRotation(new Vector3(0, 5, 0), Quaternion.Euler(0, 90, 0));
    ```
    


#### **2.2 회전 관련**

1. **Rotate**
    
    - 지정된 축을 기준으로 오브젝트를 회전.
    - 로컬 또는 월드 좌표계 기준 선택 가능.
    
    ```csharp
    transform.Rotate(Vector3.up * 90 * Time.deltaTime); // Y축 기준으로 회전
    transform.Rotate(0, 90, 0, Space.World); // 월드 기준 Y축 회전
    ```
    
2. **LookAt**
    
    - 특정 대상 방향으로 오브젝트를 회전.
    
    ```csharp
    GameObject target = GameObject.Find("Target");
    transform.LookAt(target.transform);
    ```
    


#### **2.3 부모-자식 관계 관련**

1. **SetParent**
    
    - 부모 오브젝트를 설정하거나 변경.
    
    ```csharp
    GameObject child = new GameObject("Child");
    child.transform.SetParent(this.transform);
    ```
    
2. **DetachChildren**
    
    - 현재 Transform의 모든 자식 오브젝트를 부모-자식 관계에서 분리.
    
    ```csharp
    transform.DetachChildren();
    ```
    
3. **GetChild**
    
    - 특정 인덱스의 자식 Transform을 가져옴.
    
    ```csharp
    Transform child = transform.GetChild(0); // 첫 번째 자식
    ```
    
4. **childCount**
    
    - 현재 Transform에 연결된 자식 개수를 반환.
    
    ```csharp
    Debug.Log(transform.childCount);
    ```
    


### 3. **RectTransform(UI 전용)**

UI 요소는 **RectTransform**을 사용하며, 기본 Transform과는 조금 다릅니다.

#### **3.1 주요 속성**

- **anchoredPosition**: 부모 Canvas 또는 부모 RectTransform 기준으로 오브젝트의 위치.
- **sizeDelta**: 오브젝트의 크기 (Anchor를 기준으로 조정됨).
- **pivot**: UI 요소의 기준점을 설정 (0~1 사이의 값).

#### **3.2 주요 메서드**

1. **SetInsetAndSizeFromParentEdge**
    
    - 부모의 특정 가장자리에서 거리와 크기를 설정.
    
    ```csharp
    rectTransform.SetInsetAndSizeFromParentEdge(RectTransform.Edge.Left, 10, 100);
    ```
    
2. **RectTransformUtility.ScreenPointToLocalPointInRectangle**
    
    - 화면 좌표(Screen Point)를 UI 로컬 좌표(Local Point)로 변환.
    
    ```csharp
    Vector2 localPoint;
    RectTransformUtility.ScreenPointToLocalPointInRectangle(
        rectTransform,
        Input.mousePosition,
        Camera.main,
        out localPoint
    );
    ```
    


### 4. **Transform과 좌표계**

#### **4.1 로컬(Local) vs 월드(World) 좌표계**

- **Local Position, Local Rotation, Local Scale:**
    - 부모 오브젝트를 기준으로 한 상대적인 값.
- **World Position, Rotation, Scale:**
    - 전역 좌표계 기준 값.

#### **4.2 Transform 방향**

1. **forward, right, up**
    
    - Transform의 축 방향을 반환.
    
    ```csharp
    Debug.Log(transform.forward); // Z축 방향
    Debug.Log(transform.right);   // X축 방향
    Debug.Log(transform.up);      // Y축 방향
    ```
    
2. **TransformDirection**
    
    - 로컬 좌표를 월드 좌표로 변환.
    
    ```csharp
    Vector3 worldDirection = transform.TransformDirection(Vector3.forward);
    ```
    
3. **InverseTransformDirection**
    
    - 월드 좌표를 로컬 좌표로 변환.
    
    ```csharp
    Vector3 localDirection = transform.InverseTransformDirection(Vector3.forward);
    ```
    


### 5. **Transform 사용 시 주의사항**

1. **성능 최적화**:
    
    - `transform` 속성은 프로퍼티로 매번 호출 시 내부적으로 연산을 수행하므로, 반복 호출 시 캐싱하여 사용하는 것이 좋습니다.
    
    ```csharp
    Transform myTransform = transform;
    myTransform.position = new Vector3(0, 5, 0);
    ```
    
2. **부모-자식 관계 고려**:
    
    - 자식의 Transform은 부모의 영향을 받으므로 부모의 Scale, Rotation이 자식에게 적용됩니다.
    - 필요하다면 `worldPositionStays` 매개변수를 사용해 월드 좌표를 유지하며 부모를 설정할 수 있습니다:
        
        ```csharp
        childTransform.SetParent(parentTransform, worldPositionStays: true);
        ```
        
3. **Update 내 Translate/Rotate 사용 시 주의**:
    
    - 이동이나 회전이 Frame-Rate 의존적이지 않도록 `Time.deltaTime`을 곱하여 사용.


### 요약

1. **Transform 속성**:
    - `Position`: 월드 및 로컬 위치.
    - `Rotation`: EulerAngles 또는 Quaternion.
    - `Scale`: 크기 비율.
2. **Transform 메서드**:
    - `Translate`, `Rotate`, `LookAt`, `SetParent`, `DetachChildren` 등.
3. **RectTransform(UI)**:
    - `anchoredPosition`, `sizeDelta`, `pivot` 등 UI 전용 속성.
4. **좌표 변환**:
    - `TransformDirection`, `InverseTransformDirection`으로 로컬 ↔ 월드 변환.
5. **주의사항**:
    - Transform 접근 최적화와 부모-자식 관계의 영향을 이해.

**Q1:** 부모 오브젝트가 실시간으로 움직이는 상황에서 자식 오브젝트의 위치를 고정하려면 어떤 방법을 사용할 수 있을까요?  
**Q2:** Transform을 이용해 특정 경로를 따라 움직이는 애니메이션을 구현하려면 어떤 방식이 효율적일까요?







### 2. **Camera**

씬을 렌더링하는 역할을 하는 컴포넌트.

#### 주요 속성

- **Projection (Perspective/Orthographic):** 원근감을 사용할지 평면적으로 렌더링할지 결정.
- **Field of View (FOV):** 카메라의 시야각 (Perspective 모드에서 사용).
- **Clipping Planes (Near, Far):** 카메라가 렌더링할 범위(가까운/먼 거리).
- **Background:** 카메라 배경색.
- **Culling Mask:** 카메라가 렌더링할 Layer 설정.
- **Depth:** 카메라의 렌더링 순서.

### 카메라 컴포넌트 심화학습

Unity에서 **Camera 컴포넌트**는 씬(Scene)을 렌더링하는 역할을 하며, 게임의 시야와 화면에 표시되는 모든 것을 관리합니다. 카메라의 주요 속성과 그 속성의 역할, 활용 방법을 심화적으로 살펴보겠습니다.


### 1. **Projection (투영 방식)**

#### **1.1 Perspective (원근 투영)**

- 원근감을 표현하는 기본 투영 방식.
- 화면에서 멀리 있는 오브젝트는 작게, 가까운 오브젝트는 크게 보입니다.
- **Field of View (FOV)**:
    
    - 카메라의 수평 또는 수직 시야각을 설정 (단위: °).
    - 일반적으로 60~90 사이의 값이 사용됩니다.
    - 너무 작으면 화면이 답답해 보이고, 너무 크면 왜곡이 심해질 수 있습니다.
    
    ```csharp
    Camera.main.fieldOfView = 60f;
    ```
    

#### **1.2 Orthographic (직교 투영)**

- 원근감을 무시하고 오브젝트를 같은 크기로 렌더링.
- 주로 2D 게임, UI, 미니맵 등에 사용됩니다.
- **Orthographic Size**:
    
    - 카메라가 렌더링할 영역의 크기를 설정.
    - 이 값은 카메라 뷰의 절반 높이를 나타냅니다.
    
    ```csharp
    Camera.main.orthographic = true;
    Camera.main.orthographicSize = 5f;
    ```
    


### 2. **Clipping Planes (클리핑 평면)**

#### **2.1 Near Clipping Plane**

- 카메라에서 가장 가까운 렌더링 가능한 거리.
- Near 값보다 가까운 오브젝트는 렌더링되지 않습니다.
- 일반적으로 0.01~0.1 사이로 설정.

#### **2.2 Far Clipping Plane**

- 카메라에서 가장 먼 렌더링 가능한 거리.
- Far 값보다 먼 오브젝트는 렌더링되지 않습니다.
- 일반적으로 500~1000 사이로 설정.

#### **활용**

- Near와 Far 값을 적절히 설정해 **Depth Precision**을 최적화.
- 너무 큰 범위를 설정하면 깊이 버퍼가 부정확해지고 렌더링 품질에 문제가 발생할 수 있습니다.

```csharp
Camera.main.nearClipPlane = 0.1f;
Camera.main.farClipPlane = 500f;
```


### 3. **Culling Mask (컬링 마스크)**

- 카메라가 렌더링할 Layer를 선택.
- 특정 오브젝트를 보이지 않게 하거나 특정 Layer만 렌더링할 때 유용.
- **활용 예시**:
    - UI 전용 카메라에서 `UI Layer`만 렌더링.
    - 미니맵 카메라에서 `Minimap Layer`만 렌더링.

```csharp
Camera.main.cullingMask = LayerMask.GetMask("UI", "Player");
```

#### **LayerMask 팁**

- `LayerMask.GetMask("LayerName")`: Layer 이름을 기반으로 마스크 생성.
- `Camera.main.cullingMask = ~(1 << 3);`: 특정 Layer(3번 Layer)만 제외.


### 4. **Depth**

- 카메라의 렌더링 순서를 결정.
- Depth 값이 낮은 카메라가 먼저 렌더링되고, 값이 높은 카메라가 나중에 렌더링됩니다.
- 주로 **다중 카메라 시스템**에서 사용:
    - 예: UI 카메라(Depth = 1)가 월드 카메라(Depth = 0) 위에 렌더링.
- **Clear Flags**와 함께 설정하여 복합 화면 효과 구현 가능.

```csharp
Camera.main.depth = 1;
```


### 5. **Clear Flags**

카메라가 렌더링 전에 화면을 어떻게 지울지 설정합니다.

#### **옵션**

1. **Skybox**:
    - 기본값. Skybox가 화면의 배경으로 렌더링.
2. **Solid Color**:
    - 단색으로 화면 초기화. `Background` 색상을 사용.
3. **Depth Only**:
    - 카메라의 깊이 버퍼만 초기화.
    - 주로 다중 카메라 설정에서 사용.
4. **Don't Clear**:
    - 이전 카메라가 렌더링한 결과를 유지.

```csharp
Camera.main.clearFlags = CameraClearFlags.SolidColor;
Camera.main.backgroundColor = Color.black;
```


### 6. **Viewport Rect**

- 카메라가 렌더링하는 화면 공간의 비율과 위치를 설정.
- **Rect (X, Y, Width, Height)** 형식:
    - X, Y: 카메라 화면 시작 좌표 (0 ~ 1).
    - Width, Height: 카메라가 차지할 너비와 높이 비율 (0 ~ 1).
- 주로 **멀티플레이어 화면 분할** 또는 **미니맵** 구현에 사용.

```csharp
Camera.main.rect = new Rect(0.5f, 0.5f, 0.5f, 0.5f); // 화면의 오른쪽 하단에 렌더링
```


### 7. **Target Texture**

- 렌더링 결과를 화면 대신 **RenderTexture**에 출력.
- 주로 **포스트 프로세싱**, **미니맵**, **보안 카메라** 구현에 사용.

```csharp
Camera.main.targetTexture = myRenderTexture;
```


### 8. **Post-Processing**

- 카메라에 적용되는 후처리 효과.
- Unity의 Post-Processing Stack 또는 URP/HDRP의 Post-Processing Volume을 통해 설정.


### 9. **Field of View (FOV)와 Zoom 구현**

#### FOV를 활용한 줌:

```csharp
void Update()
{
    if (Input.GetMouseButton(1)) // 우클릭으로 줌
    {
        Camera.main.fieldOfView = Mathf.Lerp(Camera.main.fieldOfView, 30f, Time.deltaTime * 5f);
    }
    else
    {
        Camera.main.fieldOfView = Mathf.Lerp(Camera.main.fieldOfView, 60f, Time.deltaTime * 5f);
    }
}
```

#### Orthographic Size를 활용한 줌:

```csharp
void Update()
{
    if (Input.GetAxis("Mouse ScrollWheel") > 0)
    {
        Camera.main.orthographicSize -= 0.5f;
    }
    else if (Input.GetAxis("Mouse ScrollWheel") < 0)
    {
        Camera.main.orthographicSize += 0.5f;
    }
    Camera.main.orthographicSize = Mathf.Clamp(Camera.main.orthographicSize, 2f, 10f);
}
```


### 10. **Camera 이벤트 및 활용**

1. **OnPreCull**
    - 카메라가 오브젝트를 렌더링하기 전에 호출.
2. **OnPreRender**
    - 카메라가 렌더링하기 직전에 호출.
3. **OnPostRender**
    - 카메라가 렌더링을 완료한 후 호출.

#### 활용 예:

```csharp
void OnPreRender()
{
    Debug.Log("카메라 렌더링 시작");
}
```


### 요약

1. **Projection**: 원근(Perspective)과 직교(Orthographic) 투영 방식.
2. **Clipping Planes**: Near와 Far로 렌더링 범위 설정.
3. **Culling Mask**: 특정 Layer만 렌더링.
4. **Depth**: 다중 카메라 렌더링 순서.
5. **Clear Flags**: 화면 초기화 방식 설정.
6. **Viewport Rect**: 화면 분할 렌더링.
7. **Target Texture**: RenderTexture로 출력.
8. **FOV와 Zoom**: 카메라 확대/축소 구현.

**Q1:** 카메라의 `Depth`를 활용하여 UI와 월드 렌더링을 혼합할 때 발생할 수 있는 문제와 해결 방법은 무엇인가요?  
**Q2:** 여러 카메라를 사용해 특정 오브젝트만 별도로 렌더링하려면 어떤 설정을 추가해야 할까요?


