---
title: dotnet 윈폼 폼 팝업으로 여러 개 사용
created: 2024-02-22 01:44
alias:
tags:
---
닷넷 윈폼(Windows Forms) 프로젝트에서 버튼 클릭 이벤트를 사용하여 새로운 폼을 팝업으로 띄우는 방법은 간단합니다. 이 과정을 몇 가지 단계로 나누어 설명드리겠습니다.

# 1. 새 폼 생성하기
먼저 새로 띄울 폼이 필요합니다. Visual Studio에서 프로젝트에 새 폼(Form)을 추가하세요. 이를 위해 솔루션 탐색기에서 프로젝트 이름을 우클릭하고, `[추가] > [새 항목] > [Windows 폼]`을 선택합니다. 새 폼의 이름을 지정하고 추가 버튼을 클릭하세요.

# 2. 버튼 추가 및 이벤트 핸들러 생성
기존 폼(메인 폼)에 버튼 컨트롤을 추가하고, 이 버튼이 클릭될 때 실행될 이벤트 핸들러를 생성합니다. 버튼을 폼에 드래그하여 추가한 후, 버튼을 더블 클릭하여 자동으로 생성되는 `Click` 이벤트 핸들러에 코드를 작성합니다.

# 3. 새 폼 띄우기
생성된 이벤트 핸들러 내에서, 첫 번째 단계에서 생성한 새 폼의 인스턴스를 생성하고 `Show` 또는 `ShowDialog` 메소드를 호출하여 새 폼을 띄웁니다. `Show` 메소드는 새 폼을 모달이 아닌 방식으로 띄우고, `ShowDialog` 메소드는 모달 방식으로 띄웁니다(모달 방식은 새 폼이 닫힐 때까지 기존 폼을 사용할 수 없게 합니다).

# 예제 코드
```csharp
// 버튼 클릭 이벤트 핸들러
private void button1_Click(object sender, EventArgs e)
{
    Form2 newForm = new Form2(); // Form2는 새로 추가한 폼의 클래스 이름입니다.
    newForm.Show(); // 모달이 아닌 방식으로 새 폼을 띄웁니다.
    // newForm.ShowDialog(); // 모달 방식으로 새 폼을 띄우려면 이 코드를 사용하세요.
}
```

이러한 단계를 통해, 닷넷 윈폼 프로젝트에서 버튼을 클릭했을 때 새로운 폼을 팝업으로 띄울 수 있습니다.

**프로젝트에 적용하면서 고려할 질문들:**




**Q3:** 여러 개의 폼을 동시에 관리하려면 어떤 방식이 효과적일까요?


![[윈폼 모달 vs 모달리스]]


새 폼에서 데이터를 전달하거나 받아오려면?

엑세스할 수 없는 문제가 발생하는 경우, 가장 먼저 확인해야 할 사항은 `FormEdit` 내의 컨트롤(예: `TextBox`, `ComboBox`)에 접근할 수 있는지 여부입니다. 
기본적으로, Windows Forms에서 폼의 컨트롤은 `private` 접근 제한자를 가지기 때문에 다른 폼에서 직접 접근할 수 없습니다. 
이 문제를 해결하는 두 가지 방법은 다음과 같습니다:

### 1. 공개 프로퍼티나 메서드 사용하기

`FormEdit` 내에 데이터를 설정할 수 있는 공개 메서드나 프로퍼티를 만드는 것입니다. 이 방법은 `FormEdit`의 캡슐화를 유지하면서도 외부에서 데이터를 전달할 수 있는 효과적인 방법입니다.

**예시:**

`FormEdit`에 다음과 같이 공개 프로퍼티나 메서드를 추가합니다.

```csharp
public string DataProperty1 {
    get { return textBox1.Text; }
    set { textBox1.Text = value; }
}

public void SetData(string data1, string data2) {
    textBox1.Text = data1;
    comboBox1.SelectedItem = data2;
}
```

그런 다음, `FormEdit`의 인스턴스를 생성하고 데이터를 전달할 때 이 메서드나 프로퍼티를 사용합니다.

```csharp
FormEdit formEdit = new FormEdit();
formEdit.DataProperty1 = "값";
// 또는
formEdit.SetData("값1", "값2");
formEdit.ShowDialog();
```

### 2. 컨트롤의 Modifiers 속성 변경하기

디자이너에서 `FormEdit`의 해당 컨트롤을 선택하고, 속성 창에서 `Modifiers` 속성을 `public`이나 `internal`로 변경합니다. 이렇게 하면 다른 클래스나 폼에서도 해당 컨트롤에 접근할 수 있게 됩니다.

하지만 이 방법은 컨트롤에 직접 접근하게 되므로, 객체 지향 설계 원칙 중 하나인 캡슐화를 위반할 수 있습니다. 가능하다면 첫 번째 방법을 사용하는 것이 더 좋습니다.

### 문제 해결 후

위의 방법들로도 문제가 해결되지 않는다면, 다음을 확인해 보세요:

- `FormEdit`의 인스턴스가 올바르게 생성되었는지
- 전달하려는 데이터가 유효한지 (예: `null`이 아닌지)
- `FormEdit`가 올바른 스레드에서 열리고 있는지 (특히, 멀티 스레딩을 사용하는 경우)

이러한 점들을 검토하여 문제를 해결하시길 바랍니다.