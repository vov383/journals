---
title: Unity Button ColorBlock
created: 2024-12-10 03:34
alias:
tags:
---
###### ColorBlock의 기본 개념  
Unity의 Button에 정의된 `ColorBlock`은 UI 요소가 다른 상호작용 상태(Idle, Highlighted, Pressed, Selected, Disabled)에 놓일 때 
해당 상태를 시각적으로 구분하기 위해 색상을 지정하는 구조체다. 
이를 통해 같은 버튼이라도 마우스를 올려놓거나 클릭했을 때, 혹은 비활성화 상태일 때 서로 다른 색으로 표시될 수 있다.

###### ColorBlock 프로퍼티 구성  
ColorBlock은 normalColor, highlightedColor, pressedColor, selectedColor, disabledColor 등 상태별 색상 필드와 
색상 전환에 필요한 fadeDuration, colorMultiplier 등의 값을 포함한다. 
각 필드는 해당 상태가 될 때 버튼에 적용되는 색상을 지정한다.

###### ColorBlock 설정 방법  
Button 컴포넌트의 Inspector 상에서 Color Tint Transition을 선택하고, ColorBlock을 구성하는 각 색상을 원하는 컬러로 설정한다. 또는 C# 스크립트로 접근해 ColorBlock 인스턴스를 가져와 프로퍼티를 변경한 뒤 button.colors = 수정된 ColorBlock으로 할당할 수도 있다.

###### 코드 예시 (C#을 통한 ColorBlock 설정)  

```csharp
ColorBlock cb = myButton.colors;
cb.normalColor = Color.white;
cb.highlightedColor = Color.yellow;
cb.pressedColor = new Color(1f,0.5f,0f);
cb.disabledColor = Color.gray;
cb.colorMultiplier = 1.0f;
cb.fadeDuration = 0.1f;
myButton.colors = cb;
```

###### ColorTint Transition과 연동  
Button 컴포넌트의 Transition 옵션을 ColorTint로 설정하면 Button UI의 상태 변화 시 ColorBlock에 지정한 색상을 자동으로 적용한다. 이때, 상호작용 상태 변화에 따라 부드러운 색상 전환 애니메이션(fadeDuration)이 진행된다.

###### 사용 예시와 참고 링크  
상태별 시각 구분이 필요한 모든 인터랙티브 UI 요소에서 ColorBlock을 활용할 수 있다. Unity 공식 문서: [https://docs.unity3d.com/2019.4/Documentation/ScriptReference/UI.ColorBlock.html](https://docs.unity3d.com/2019.4/Documentation/ScriptReference/UI.ColorBlock.html)

###### 주의사항  
ColorBlock은 Transition이 ColorTint일 때만 적용된다. SpriteSwap 또는 Animation Transition을 사용한다면 ColorBlock을 통한 색 변경이 무의미하다.

Q1 : ColorBlock을 이용해 Button 상태 변화 외에 다른 UI 컴포넌트에도 적용할 수 있나?  
Q2 : 다른 Transition 옵션(SpriteSwap, Animation)과 ColorBlock을 함께 사용하는 방법은 존재하나?

summarise up to 7 points:  
###### ColorBlock은 Button 상태별 색상 정의 구조체다.  
###### normal, highlighted, pressed, disabledColor 등을 가진다.  
###### Inspector나 코드에서 ColorBlock 변경 가능하다.  
###### ColorTint Transition에서 자동 반영된다.  
###### fadeDuration으로 색 전환 속도 제어 가능하다.  
###### colorMultiplier로 색 강도 조절 가능하다.  
###### Transition이 ColorTint일 때만 색상 변경 효과가 유효하다.


