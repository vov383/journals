---
title: WinForms Panel을 활용한 커스텀 컨트롤 테두리 색상 표시 가이드
created: 2025-02-28 01:41
alias:
tags:
---
# WinForms Panel을 활용한 커스텀 컨트롤 테두리 색상 표시 가이드

## 개요
WinForms에서 `TextBox`, `ComboBox`와 같이 기본적으로 **`BorderColor`를 직접 설정할 수 없는 컨트롤**에 대해,  
`Panel`을 외곽에 배치하고, 해당 `Panel`의 테두리를 원하는 색상으로 설정하여 **커스텀 테두리 효과**를 구현하는 방법을 정리한다.


## 방식 
- **컨트롤 (TextBox 등)**을 `Panel` 내부에 위치시킴.
- `Panel`의 `Padding`을 조절해 내부 컨트롤과 테두리 간 간격을 확보.
- `Panel`의 `BorderColor`를 원하는 색상으로 설정해 테두리 표시.


## 장점
- 기존 컨트롤의 기능 유지 (입력, 포커스, 이벤트 등)
- 디자인 및 테마 변경 용이 (색상, 두께 등)


## 구조 예시

```plaintext
[ Panel ]
 └ [ TextBox ]
```


## 구현 예제 - C#

```csharp
public class BorderedTextBox : Panel
{
    private TextBox innerTextBox;

    public BorderedTextBox()
    {
        this.Padding = new Padding(1);  // 테두리 두께
        this.BackColor = Color.Red;     // 테두리 색상 (기본)

        innerTextBox = new TextBox
        {
            Dock = DockStyle.Fill,
            BorderStyle = BorderStyle.None  // TextBox 자체 테두리는 제거
        };
        this.Controls.Add(innerTextBox);
    }

    // 텍스트 접근 프로퍼티
    public string Text
    {
        get => innerTextBox.Text;
        set => innerTextBox.Text = value;
    }

    // 테두리 색상 프로퍼티
    public Color BorderColor
    {
        get => this.BackColor;
        set => this.BackColor = value;
    }
}
```


## 설명

|항목|설명|
|---|---|
|`Padding`|테두리 두께 조절|
|`BackColor`|테두리 색상 지정|
|`BorderStyle`|내부 컨트롤의 기본 테두리 제거|
|`DockStyle.Fill`|내부 컨트롤이 패널 내부를 꽉 채우도록 설정|


## 추가 기능 (선택적 구현)

- **포커스 상태일 때 테두리 색 변경**
- **에러 상태일 때 테두리 색 빨간색 표시**
- **입력 모드 전환 (읽기 전용일 때 테두리 회색 등)**

```csharp
protected override void OnEnter(EventArgs e)
{
    base.OnEnter(e);
    this.BackColor = Color.Blue;  // 포커스 시 파란색 테두리
}

protected override void OnLeave(EventArgs e)
{
    base.OnLeave(e);
    this.BackColor = Color.Red;  // 포커스 해제 시 원래 색
}
```


## 활용 예시

```csharp
var borderedTextBox = new BorderedTextBox
{
    Width = 200,
    Height = 30,
    BorderColor = Color.Gray  // 기본 테두리 색
};
this.Controls.Add(borderedTextBox);
```


## 정리 요점

|항목|내용|
|---|---|
|목적|테두리 색상 커스터마이징|
|구성|Panel + 내부 컨트롤(TextBox 등)|
|조절 가능 요소|테두리 색, 두께, 내부 컨트롤 위치 등|
|확장성|포커스/에러 상태에 따른 동적 색상 변경 가능|


## 참고

- TextBox 외에도 ComboBox, ListBox 등 다른 컨트롤에도 동일 기법 적용 가능
- 필요 시 테두리 스타일(점선, 실선 등) 확장 가능 (OnPaint 활용)


## 마무리

이 방식은 WinForms 기본 컨트롤의 한계를 우회하면서도, 유지보수와 확장성 면에서 유리한 기법이다.  
디자인 컨셉과 프로그램 성격에 맞춰 자유롭게 응용 가능하다.