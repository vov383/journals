---
title: dotnet 윈폼 MessageBox 버튼 옵션 추가하기
created: 2024-02-22 01:37
alias:
tags:
---
- 사용자에게 결정을 요구하는 메시지 박스를 생성할 때 사용할 수 있습니다. 예를 들어, `MessageBoxButtons.YesNo` 옵션을 사용할 수 있습니다.
   ```csharp
   DialogResult result = MessageBox.Show("계속하시겠습니까?", "확인", MessageBoxButtons.YesNo);
   if (result == DialogResult.Yes)
   {
       // '예' 버튼을 클릭했을 때의 로직
   }
   else
   {
       // '아니오' 버튼을 클릭했을 때의 로직
   }
   ```

