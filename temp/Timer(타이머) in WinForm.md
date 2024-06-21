---
title: Timer(타이머) in WinForm
created: 2024-06-21 01:36
alias:
tags:
---
###### 요약
1. 타이머는 주기적으로 작업을 수행하기 위한 컨트롤입니다.
2. `Interval` 속성으로 타이머 간격을 설정합니다.
3. `Tick` 이벤트 핸들러에서 주기적으로 실행할 작업을 정의합니다.
4. 타이머는 `Start()`와 `Stop()` 메서드를 사용하여 제어할 수 있습니다.
#### 기본 개념
`Timer` 컨트롤은 일정 간격으로 이벤트를 발생시켜 
반복 작업을 수행할 수 있도록 합니다. 
주로 백그라운드 작업을 주기적으로 실행하거나, 
주기적인 상태 확인 작업에 사용됩니다.

#### 주요 속성
###### Interval
타이머가 `Tick` 이벤트를 발생시키는 간격을 밀리초 단위로 설정합니다. 
예를 들어, `Interval`을 1000으로 설정하면 1초 간격으로 
`Tick` 이벤트가 발생합니다.
###### Enabled
타이머가 활성화되었는지 여부를 나타냅니다. 
`true`로 설정하면 타이머가 시작되고, 
`false`로 설정하면 타이머가 중지됩니다.

#### 주요 메서드
###### Start()
타이머를 시작합니다. `Enabled` 속성을 `true`로 설정하는 것과 동일합니다.
###### Stop()
타이머를 중지합니다. `Enabled` 속성을 `false`로 설정하는 것과 동일합니다.

### Timer.Tick 이벤트

#### 기본 개념
`Tick` 이벤트는 타이머의 `Interval` 속성에 설정된 간격으로 발생합니다. 
`Tick` 이벤트 핸들러를 통해 
주기적으로 실행할 코드를 정의할 수 있습니다.

#### 사용 예시
타이머 컨트롤을 사용하여 1초마다 현재 시간을 라벨에 표시하는 예제를 살펴보겠습니다.

### 예제 코드

```csharp
using System;
using System.Windows.Forms;

public partial class MainForm : Form
{
    private Timer timer;

    public MainForm()
    {
        InitializeComponent();
        InitializeTimer();
    }

    private void InitializeTimer()
    {
        timer = new Timer();
        timer.Interval = 1000; // 1초 간격 설정
        timer.Tick += new EventHandler(Timer_Tick);
        timer.Start(); // 타이머 시작
    }

    private void Timer_Tick(object sender, EventArgs e)
    {
        // 현재 시간을 라벨에 표시
        lblCurrentTime.Text = DateTime.Now.ToString("HH:mm:ss");
    }

    private void MainForm_Load(object sender, EventArgs e)
    {
        // 폼 로드 시 타이머 초기화 및 시작
        InitializeTimer();
    }
}
```

### 설명
- `Timer` 객체를 생성하고, `Interval`을 1000밀리초(1초)로 설정합니다.
- `Tick` 이벤트 핸들러로 `Timer_Tick` 메서드를 등록합니다.
- `Start()` 메서드를 호출하여 타이머를 시작합니다.
- `Timer_Tick` 이벤트 핸들러에서는 현재 시간을 라벨(`lblCurrentTime`)에 표시합니다.

### 주요 포인트


Q1: 타이머 컨트롤을 이용하여 일정 시간이 경과한 후 특정 작업을 수행하려면 어떻게 해야 할까요?
Q2: 타이머의 `Interval` 값을 동적으로 변경하려면 어떻게 해야 할까요?


