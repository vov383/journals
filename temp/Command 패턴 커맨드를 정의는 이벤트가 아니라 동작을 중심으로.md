---
title: Command 패턴 커맨드를 정의는 이벤트가 아니라 동작을 중심으로
created: 2024-08-28 08:08
alias:
tags:
---
Command 패턴 커맨드를 정의할 때 
이벤트 자체가 아니라 이벤트로 인해 발생하는 동작을 중심으로 커맨드를 정의하는 것이 핵심입니다. 
셀 클릭이나 마우스 다운 같은 이벤트는 단순히 사용자 인터페이스에서 발생하는 사건일 뿐이며, Command 패턴의 본질은 이러한 사건이 발생했을 때 수행되는 비즈니스 로직이나 작업을 캡슐화하는 데 있습니다.
### 1. **이벤트와 동작의 분리**

이벤트(예: 셀 클릭, 마우스 다운)는 단순히 트리거입니다. 이 이벤트가 발생하면 특정 작업이 수행되는데, Command 패턴에서 이 작업을 캡슐화하여 재사용 가능하고 독립적인 방식으로 정의하는 것이 중요합니다.

### 2. **동작 중심의 Command 정의**

동작 중심으로 Command를 정의하면, 동일한 작업을 다양한 이벤트에 연결하거나, 다른 상황에서 재사용할 수 있습니다. 예를 들어, **셀 클릭 시 셀의 색상을 변경하는 작업**을 정의할 수 있습니다. 이 작업은 셀 클릭뿐만 아니라 다른 이벤트나 조건에서도 실행될 수 있습니다.

### 3. **예시: 셀 색상 변경 작업을 중심으로 한 Command 정의**

아래 예시는 셀 클릭 이벤트를 중심으로 하지 않고, **셀의 색상을 변경하는 동작**을 중심으로 Command를 정의한 것입니다.

#### 3.1 **ChangeCellColorCommand**

```csharp
public class ChangeCellColorCommand : ICommand
{
    private readonly DataGridView _dataGridView;
    private readonly Color _newColor;
    private readonly int _rowIndex;
    private readonly int _columnIndex;
    private Color _previousColor;

    public ChangeCellColorCommand(DataGridView dataGridView, int rowIndex, int columnIndex, Color newColor)
    {
        _dataGridView = dataGridView;
        _newColor = newColor;
        _rowIndex = rowIndex;
        _columnIndex = columnIndex;
    }

    public bool CanExecute(object parameter)
    {
        // 셀이 존재하는지, 셀이 비어 있지 않은지 등 유효성 검사를 수행할 수 있습니다.
        return _dataGridView != null && _rowIndex >= 0 && _columnIndex >= 0;
    }

    public void Execute(object parameter)
    {
        // 현재 색상을 저장한 다음, 새 색상을 적용
        _previousColor = _dataGridView.Rows[_rowIndex].Cells[_columnIndex].Style.BackColor;
        _dataGridView.Rows[_rowIndex].Cells[_columnIndex].Style.BackColor = _newColor;
    }

    public void Undo(object parameter)
    {
        // 이전 색상으로 복원
        _dataGridView.Rows[_rowIndex].Cells[_columnIndex].Style.BackColor = _previousColor;
    }

    public void Redo(object parameter)
    {
        // 다시 새 색상으로 적용
        Execute(parameter);
    }
}
```

### 4. **이벤트와 Command 연결**

이제 이 Command를 셀 클릭, 마우스 다운 등 다양한 이벤트와 연결할 수 있습니다. 이때 이벤트는 단순히 Command를 실행하는 트리거 역할을 합니다.

#### 4.1 MainForm에서 Command 실행

```csharp
public partial class MainForm : Form
{
    private readonly CommandManager _commandManager = new CommandManager();

    public MainForm()
    {
        InitializeComponent();

        dataGridView1.CellClick += DataGridView1_CellClick;
        dataGridView1.MouseDown += DataGridView1_MouseDown;
    }

    private void DataGridView1_CellClick(object sender, DataGridViewCellEventArgs e)
    {
        if (e.RowIndex >= 0 && e.ColumnIndex >= 0)
        {
            var command = new ChangeCellColorCommand(dataGridView1, e.RowIndex, e.ColumnIndex, Color.Yellow);
            _commandManager.ExecuteCommand(command, null);
        }
    }

    private void DataGridView1_MouseDown(object sender, MouseEventArgs e)
    {
        // 필요한 경우 마우스 다운 이벤트에서 동일한 동작을 실행할 수 있습니다.
        var hitTest = dataGridView1.HitTest(e.X, e.Y);
        if (hitTest.RowIndex >= 0 && hitTest.ColumnIndex >= 0)
        {
            var command = new ChangeCellColorCommand(dataGridView1, hitTest.RowIndex, hitTest.ColumnIndex, Color.Red);
            _commandManager.ExecuteCommand(command, null);
        }
    }
}
```

### 5. **결론**

이러한 방식으로 동작 중심의 Command를 정의하면 다음과 같은 이점이 있습니다:

1. **재사용성**: 동일한 Command를 여러 이벤트에서 재사용할 수 있습니다. 예를 들어, 셀 클릭, 마우스 다운 등 다양한 이벤트에서 동일한 셀 색상 변경 작업을 실행할 수 있습니다.
   
2. **유지보수성**: 동작(비즈니스 로직)이 Command로 분리되어 있으므로, 로직을 수정해야 할 때 Command 클래스만 수정하면 됩니다.

3. **확장성**: 새로운 동작을 추가하거나 기존 동작을 수정할 때, 이벤트와 로직이 분리되어 있어 쉽게 확장할 수 있습니다.

4. **테스트 용이성**: Command는 독립적인 단위로 쉽게 테스트할 수 있으며, 이벤트 처리 로직과 비즈니스 로직을 분리함으로써 테스트의 복잡성을 줄일 수 있습니다.

이렇게 동작 중심의 Command 패턴을 사용하면, WinForms 애플리케이션에서 복잡한 이벤트 처리와 비즈니스 로직을 더욱 관리하기 쉽게 만들 수 있습니다.


