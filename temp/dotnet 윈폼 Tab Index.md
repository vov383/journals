---
title: dotnet 윈폼 Tab Index
created: 2024-02-22 01:18
alias:
tags:
---
Windows Forms(윈폼) 애플리케이션에서 탭 키를 눌렀을 때 요소(컨트롤) 간에 포커스가 이동하는 순서는 "Tab Index" 속성을 통해 관리됩니다. 
각 컨트롤의 "Tab Index" 속성 값은 그 컨트롤이 포커스를 받는 순서를 결정합니다. 
값이 작을수록 먼저 포커스를 받게 되며, 같은 폼 내의 모든 컨트롤은 고유한 "Tab Index" 값을 가져야 합니다.

1. **디자인 뷰에서 설정하기**: Visual Studio의 디자인 뷰에서 컨트롤을 선택한 후, 속성 창에서 "Tab Index" 속성을 찾아 값을 설정할 수 있습니다. 이 값은 0부터 시작하며, 순차적으로 증가합니다. 사용자가 탭 키를 누를 때, "Tab Index" 값이 작은 컨트롤에서 큰 컨트롤 순으로 포커스가 이동합니다.

2. **프로그래밍 방식으로 설정하기**: 코드를 통해서도 각 컨트롤의 "Tab Index" 값을 설정할 수 있습니다. 이 방법은 동적으로 컨트롤을 생성하거나, 실행 시간에 "Tab Index"를 변경해야 할 때 유용합니다.

```csharp
// 예시: textBox1의 Tab Index를 0으로, textBox2의 Tab Index를 1로 설정
textBox1.TabIndex = 0;
textBox2.TabIndex = 1;
```

###### Tab Order 
![[dotnet 윈폼 Tab Order 도구]]

