---
title: FpSpread의 GeneralCellType 주요 속성과 메서드
created: 2024-07-05 02:18
alias:
tags:
---
`GeneralCellType` 다양한 유형의 셀 데이터를 표시하는 데 사용됩니다. 
이 셀 타입은 특히 숫자 형식을 지정하는 데 유용합니다. 

#### 주요 속성 (Properties)
1. **FormatString**
   - **설명**: 셀의 값을 표시할 때 사용할 형식 문자열을 설정합니다.
   - **예제**: `generalCellType.FormatString = "#,##0";`

2. **DecimalPlaces**
   - **설명**: 소수점 이하 자릿수를 설정합니다.
   - **예제**: `generalCellType.DecimalPlaces = 2;`

3. **MaxValue**
   - **설명**: 셀에 입력할 수 있는 최대 값을 설정합니다.
   - **예제**: `generalCellType.MaxValue = 10000;`

4. **MinValue**
   - **설명**: 셀에 입력할 수 있는 최소 값을 설정합니다.
   - **예제**: `generalCellType.MinValue = 0;`

5. **Separator**
   - **설명**: 숫자 그룹 구분 문자를 설정합니다.
   - **예제**: `generalCellType.Separator = ",";`

6. **NegativeFormat**
   - **설명**: 음수 값을 표시하는 형식을 설정합니다.
   - **예제**: `generalCellType.NegativeFormat = "(#,##0)";`

7. **FractionCustomFormat**
   - **설명**: 분수로 값을 표시하는 형식을 설정합니다.
   - **예제**: `generalCellType.FractionCustomFormat = "# ???/???";`

#### 주요 메서드 (Methods)

1. **GetEditorControl**
   - **설명**: 셀에 편집 컨트롤을 반환합니다.
   - **예제**: `var editorControl = generalCellType.GetEditorControl();`

2. **IsValid**
   - **설명**: 셀 값이 유효한지 확인합니다.
   - **예제**: `bool isValid = generalCellType.IsValid(sheet, row, col, value);`

3. **Parse**
   - **설명**: 문자열을 해당 셀 타입의 데이터 형식으로 변환합니다.
   - **예제**: `var parsedValue = generalCellType.Parse("1,234");`

4. **ToString**
   - **설명**: 셀 값을 문자열로 변환합니다.
   - **예제**: `string strValue = generalCellType.ToString(sheet, row, col);`

5. **Format**
   - **설명**: 셀 값을 형식화된 문자열로 변환합니다.
   - **예제**: `string formattedValue = generalCellType.Format(value);`

### 예제 코드

다음은 `GeneralCellType`의 속성과 메서드를 사용하는 예제 코드입니다.

```csharp
using FarPoint.Win.Spread;
using FarPoint.Win.Spread.CellType;
using System.Globalization;
using System.Windows.Forms;

public class MainForm : Form
{
    public MainForm()
    {
        InitializeComponent();

        // 스프레드 시트 객체 생성
        FpSpread spread = new FpSpread();
        SheetView sheet = spread.Sheets[0];

        // 일반 셀 타입 설정
        GeneralCellType generalCellType = new GeneralCellType();
        generalCellType.FormatString = "#,##0"; // 3자리 단위로 콤마 추가
        generalCellType.DecimalPlaces = 0; // 소수점 이하 자릿수 설정
        generalCellType.MaxValue = 1000000; // 최대 값 설정
        generalCellType.MinValue = 0; // 최소 값 설정
        generalCellType.Separator = ","; // 그룹 구분 문자 설정
        generalCellType.NegativeFormat = "(#,##0)"; // 음수 형식 설정

        // 예제 데이터 추가
        sheet.Columns[0].CellType = generalCellType;
        sheet.Cells[0, 0].Value = 1234567; // 예제 데이터

        // 스프레드 시트에 추가
        this.Controls.Add(spread);
        spread.Dock = DockStyle.Fill;
    }

    private void InitializeComponent()
    {
        this.SuspendLayout();
        // 
        // MainForm
        // 
        this.ClientSize = new System.Drawing.Size(800, 450);
        this.Name = "MainForm";
        this.ResumeLayout(false);
    }

    [STAThread]
    static void Main()
    {
        Application.Run(new MainForm());
    }
}
```

### 요약

- **FormatString**: 셀 값을 표시할 형식 문자열을 설정합니다.
- **DecimalPlaces**: 소수점 이하 자릿수를 설정합니다.
- **MaxValue, MinValue**: 셀에 입력할 수 있는 값의 범위를 설정합니다.
- **Separator**: 숫자 그룹 구분 문자를 설정합니다.
- **NegativeFormat**: 음수 값을 표시하는 형식을 설정합니다.
- **FractionCustomFormat**: 분수 형식을 설정합니다.
- 주요 메서드는 셀 값을 형식화하거나 편집할 때 사용됩니다.


