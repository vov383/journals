---
title: dotnet 윈폼 MessageBox 객체
created: 2024-02-22 01:34
alias:
tags:
---
.NET에서 `MessageBox` 객체는 사용자에게 메시지를 보여주거나 사용자의 입력을 받는 데 사용되는 대화상자를 생성하는 데 사용됩니다.
`System.Windows.Forms` 네임스페이스에 속해 있으며, GUI(그래픽 사용자 인터페이스) 기반의 응용 프로그램에서 주로 사용됩니다. 
여기에는 몇 가지 기본적인 사용 방법과 예제를 소개하겠습니다.

## 기본 사용법

1. **간단한 메시지 박스 표시하기**
   - 가장 기본적인 형태로, 사용자에게 메시지를 표시합니다.
   ```csharp
   MessageBox.Show("안녕하세요, 여기에 메시지를 입력하세요.");
   ```

2. **제목이 있는 메시지 박스**
   - 메시지와 함께 제목을 지정할 수 있습니다.
   ```csharp
   MessageBox.Show("안녕하세요, 여기에 메시지를 입력하세요.", "메시지 제목");
   ```

3. 
###### dotnet 윈폼 MessageBox 버튼 옵션 추가하기

## 예제: 사용자 결정에 따라 행동하기

```csharp
DialogResult result = MessageBox.Show("이 작업을 실행하시겠습니까?", "작업 확인", MessageBoxButtons.YesNoCancel, MessageBoxIcon.Question);

switch (result)
{
    case DialogResult.Yes:
        // '예'를 선택했을 때 실행될 코드
        MessageBox.Show("작업을 시작합니다.");
        break;
    case DialogResult.No:
        // '아니오'를 선택했을 때 실행될 코드
        MessageBox.Show("작업을 취소했습니다.");
        break;
    case DialogResult.Cancel:
        // '취소'를 선택했을 때 실행될 코드
        MessageBox.Show("작업을 중단합니다.");
        break;
}
```

이러한 방식으로 `MessageBox`는 사용자와의 간단한 상호작용을 구현하는 데 매우 유용합니다. 사용자의 결정에 따라 다른 행동을 취하거나, 중요한 정보를 알리는 데 사용할 수 있습니다.

심화.
MessageBox 로 입력 받기.



###### dotnet 메세지박스의 버튼과 아이콘 옵션
![[dotnet 메세지박스의 버튼과 아이콘 옵션]]

