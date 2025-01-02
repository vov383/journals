---
title: Unity GameObject 비활성화 트러블슈팅 가이드
created: 2024-12-23 11:18
alias:
tags:
---
## 문제 상황
GameObject의 `SetActive(false)`를 호출했음에도 불구하고 게임 뷰에서 오브젝트가 계속 표시되는 현상이 발생했습니다. 디버그 로그에서는 `target.activeSelf`가 false로 정상적으로 변경되었음을 확인했으나, 실제 렌더링은 계속되었습니다.

## 원인 분석
1. GameObject 비활성화와 렌더링 시스템의 동작 차이
2. Outline 컴포넌트와 같은 추가 렌더링 요소의 영향
3. 복잡한 계층 구조에서의 컴포넌트 활성화 상태 관리 문제

## 해결 과정

### 1단계: 문제 진단
```csharp
private void DiagnoseGameObject(GameObject target)
{
    Debug.Log($"Object Active State: {target.activeSelf}");
    Debug.Log($"Renderer Enabled: {target.GetComponent<MeshRenderer>()?.enabled}");
    Debug.Log($"Outline Component Enabled: {target.GetComponent<Outline>()?.enabled}");
}
```

### 2단계: 컴포넌트 상태 확인
- MeshRenderer 활성화 상태
- Outline 컴포넌트 활성화 상태
- 부모-자식 관계에서의 활성화 상태

### 3단계: 순차적 비활성화 구현
```csharp
private void ToggleSampleDuctObject(GameObject target)
{
    // 1. 렌더러 비활성화
    MeshRenderer renderer = target.GetComponent<MeshRenderer>();
    if (renderer != null)
    {
        renderer.enabled = false;
        Debug.Log("Renderer disabled");
    }
    
    // 2. Outline 컴포넌트 비활성화
    Outline outline = target.GetComponent<Outline>();
    if (outline != null)
    {
        outline.enabled = false;
        Debug.Log("Outline disabled");
    }
    
    // 3. GameObject 비활성화
    target.SetActive(false);
    Debug.Log("GameObject deactivated");
    
    // 4. 대체 오브젝트 활성화
    sampleDuctPart.SetActive(true);
}
```

### 4단계: 계층 구조 처리
자식 오브젝트들의 컴포넌트도 함께 처리:
```csharp
private void DisableObjectHierarchy(GameObject target)
{
    // 모든 자식의 렌더러와 아웃라인 비활성화
    foreach (Transform child in target.GetComponentsInChildren<Transform>())
    {
        var childRenderer = child.GetComponent<MeshRenderer>();
        if (childRenderer != null)
        {
            childRenderer.enabled = false;
            Debug.Log($"Disabled renderer on child: {child.name}");
        }
            
        var childOutline = child.GetComponent<Outline>();
        if (childOutline != null)
        {
            childOutline.enabled = false;
            Debug.Log($"Disabled outline on child: {child.name}");
        }
    }
    
    target.SetActive(false);
}
```

## 검증 및 테스트
1. 디버그 로그 확인
2. Scene 뷰에서의 시각적 확인
3. Game 뷰에서의 최종 결과 확인

## 주의사항
1. 컴포넌트 순서
   - Renderer를 먼저 비활성화
   - 그 다음 Outline 컴포넌트 비활성화
   - 마지막으로 GameObject 비활성화

2. 성능 고려사항
   - GetComponent 호출 최소화
   - 대규모 계층 구조에서의 처리 주의

3. 디버깅 팁
   - 각 단계별 로그 기록
   - Scene 뷰에서 오브젝트 상태 확인
   - Frame Debugger 활용

## 문제 해결 체크리스트
- MeshRenderer 비활성화 확인
- Outline 컴포넌트 비활성화 확인
- GameObject 비활성화 확인
- 자식 오브젝트들의 상태 확인
- 시각적 결과 확인
- 성능 영향 검토

## 결론
GameObject의 완전한 비활성화를 위해서는 단순히 `SetActive(false)`만으로는 충분하지 않을 수 있습니다. 
렌더링 관련 컴포넌트들을 명시적으로 제어하고, 계층 구조를 고려한 체계적인 접근이 필요합니다.


