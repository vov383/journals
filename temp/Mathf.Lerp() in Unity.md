---
title: Mathf.Lerp() in Unity
created: 2024-12-18 04:54
alias:
tags:
---
2. `Mathf.Lerp(minRotation, maxRotation, t)` 설명:
```csharp
// 예시
float minRotation = 90f;   // 시작 각도
float maxRotation = -90f;  // 끝 각도
float t = 0.5f;           // 보간값 (0~1)

// t가 0이면 minRotation(90도)
// t가 1이면 maxRotation(-90도)
// t가 0.5면 중간값(0도)
float result = Mathf.Lerp(minRotation, maxRotation, t);


