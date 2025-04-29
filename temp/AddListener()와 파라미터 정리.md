---
title: AddListener()와 파라미터 정리
created: 2025-04-29 11:34
alias:
tags:
---
### AddListener() 는 파라미터x 델리게이트 요구

- `AddListener(BtnPanelClose_OnClick(pan))` 코드는 **즉시** `BtnPanelClose_OnClick(pan)`을 호출한 뒤 그 “반환값(void)”을 넘기려 하기 때문에, 실제로는 유효한 델리게이트가 전달되지 않습니다.
    
- `Button.onClick.AddListener`는 **파라미터 없는** `UnityAction` 델리게이트를 요구합니다.
    

### AddListener() 에서 파라미터가 있는 콜백을 등록하려면?

1. **람다(익명 함수) 사용**
    
```csharp
void Awake()
{
	string tag = "Btn_Close";
	foreach (PanelInfo p in panels)
	{
		GameObject pan = p.panelObject;
		GameObject btnGo = FindChildByTag(pan.transform, tag);
		if (btnGo == null) continue;

		var target = pan;  // foreach 변수 캡처 버그 예방
		Button btn = btnGo.GetComponent<Button>();
		btn.onClick.AddListener(() => BtnPanelClose_OnClick(target));
	}
}
```
    
2. **익명 델리게이트 사용**
    
```csharp
btn.onClick.AddListener(delegate {
	BtnPanelClose_OnClick(pan);
});
```



#### 요약 포인트

- **오류 원인**: `AddListener`에 함수를 호출한 결과를 전달 → 유효한 델리게이트가 아님
    
- **해결책**: 람다(`() => …`) 또는 `delegate { … }`로 “함수 호출을 감싼” 델리게이트 전달
    
- **주의**: `foreach` 내부 변수 캡처 시, 로컬 복사(`var target = pan;`)를 활용
    

#### 참고 링크

- Unity 공식 문서: [Button.onClick.AddListener](https://docs.unity3d.com/ScriptReference/UI.Button-onClick.html)


