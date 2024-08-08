---
title: Visual Studio 디자인뷰를 통해 이미지가 Control에 추가되는 방법
created: 2024-08-08 05:23
alias:
tags:
---
Visual Studio의 디자인 툴을 사용하여 이미지를 컨트롤에 첨부하면, 해당 이미지는 프로젝트 리소스에 포함되며, 코드에 자동으로 반영됩니다. 이를 이해하기 위해, 몇 가지 과정을 설명하겠습니다.

#### 디자인 툴을 통한 이미지 추가
1. **디자인 뷰 열기**: Visual Studio에서 폼을 디자인 모드로 엽니다.
2. **PictureBox 추가**: 도구 상자에서 PictureBox를 폼에 드래그 앤 드롭합니다.
3. **이미지 설정**: PictureBox의 속성 창에서 `Image` 속성을 선택하고, 로컬 파일 시스템에서 이미지를 선택합니다.

#### 이미지의 소스 추가 과정
이미지를 PictureBox에 추가하면 Visual Studio는 다음과 같은 작업을 수행합니다:

1. **프로젝트 리소스로 이미지 추가**:
   - 선택한 이미지는 프로젝트의 리소스 파일(`.resx`)에 포함됩니다.
   - 이 과정에서 이미지 파일은 프로젝트 폴더 내의 `Resources` 폴더에 저장됩니다.

2. **코드 업데이트**:
   - 디자이너 파일(`Form1.Designer.cs` 등)에서 PictureBox의 `Image` 속성이 설정됩니다.
   - 리소스 파일에서 이미지를 로드하는 코드가 자동으로 생성됩니다.

#### 자동 생성된 코드 예시
Visual Studio가 자동으로 생성하는 코드는 다음과 같습니다:

```csharp
// Form1.Designer.cs 파일
private void InitializeComponent()
{
    this.pictureBox1 = new System.Windows.Forms.PictureBox();
    ((System.ComponentModel.ISupportInitialize)(this.pictureBox1)).BeginInit();
    this.SuspendLayout();
    // 
    // pictureBox1
    // 
    this.pictureBox1.Image = global::YourProjectNamespace.Properties.Resources.이미지이름;
    this.pictureBox1.Location = new System.Drawing.Point(13, 13);
    this.pictureBox1.Name = "pictureBox1";
    this.pictureBox1.Size = new System.Drawing.Size(100, 50);
    this.pictureBox1.TabIndex = 0;
    this.pictureBox1.TabStop = false;
    // 
    // Form1
    // 
    this.AutoScaleDimensions = new System.Drawing.SizeF(6F, 13F);
    this.AutoScaleMode = System.Windows.Forms.AutoScaleMode.Font;
    this.ClientSize = new System.Drawing.Size(284, 261);
    this.Controls.Add(this.pictureBox1);
    this.Name = "Form1";
    this.Text = "Form1";
    ((System.ComponentModel.ISupportInitialize)(this.pictureBox1)).EndInit();
    this.ResumeLayout(false);
}
```

#### 프로젝트 리소스 파일 예시
리소스 파일(`Resources.resx`)에 이미지가 추가된 모습은 다음과 같습니다:

```xml
<!-- Resources.resx 파일 -->
<data name="이미지이름" type="System.Drawing.Bitmap, System.Drawing">
  <value>리소스 파일 경로</value>
</data>
```

### 요약
- Visual Studio 디자인 툴을 사용하여 이미지를 PictureBox에 추가하면, 이미지 파일은 프로젝트의 리소스 파일(`.resx`)에 포함됩니다.
- 자동 생성된 코드에서 `global::YourProjectNamespace.Properties.Resources.이미지이름`을 통해 이미지를 로드합니다.
- 리소스 파일(`Resources.resx`)에 이미지 경로가 저장됩니다.

Q1: 리소스 파일(.resx)에 추가된 이미지를 다른 폼에서도 사용하려면 어떻게 해야 하나요?
Q2: Visual Studio에서 리소스 파일을 수동으로 관리하는 방법은 무엇인가요?


