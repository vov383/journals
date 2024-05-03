---
title: csharp 유저컨트롤탭
created: 2024-05-03 15:32
aliases: 
tags:
---

유저컨트롤을 만들 때 가장 거슬렸던 건
property에 main폼에서 접근할 수 있도록 이것저것 설정하는거
```cs
public Button btnDel => btn_del;
```
람다 처럼 => 기호를 사용해서 접근할 수 있는 프로퍼티 접근자를 설정해준다.

탭에 마우스오버 시 backColor를 변경할 수 있도록
MouseEnter와 MouseLeave를 사용해서 색상을 변경해준다.

###### 메인폼에서 탭 컨트롤을 Add 해주고
```cs
 panel_ucTab.Controls.Add(myTab);
  ucShipInfoTab shipInfoTab = new ucShipInfoTab();
 ucShipToAiList ship2AiTab = new ucShipToAiList();
 myTab.AddTab(_shipInfoTabText, shipInfoTab);
 myTab.AddTab(_aiListTabText, ship2AiTab);
 ```

property를 추가해주면 끝
```
 _tabPanels = myTab.getListPanels;

 fpSpread2 = shipInfoTab.fp1;
 fpSpread3 = shipInfoTab.fp2;
 fpSpread4 = ship2AiTab.fp3;
_spgShipSpread = new SpreadGridManager(shipInfoTab.fp1); // 선박 정보 spread
_spgHoldSpread = new SpreadGridManager(shipInfoTab.fp2); // 홀드 정보 spread
_spgSendToAiSpread = new SpreadGridManager(ship2AiTab.fp3); // send to ai spread

btn_del = ship2AiTab.btnDel;
btn_ai_register = ship2AiTab.btnAiRegister;
btn_planClear = ship2AiTab.btnPlanClear;
btn_aiFormOpen = ship2AiTab.btnAiReq;

btn_del.Click += btnDelShip_Click;
btn_ai_register.Click += btnRegisterShip_Click;
btn_planClear.Click += btn_planClear_Click;
btn_aiFormOpen.Click += button_AiFromOpen;
```


###### uc입항예정정보탭 코드
```cs
namespace DW_SDMS.Presentation.UserControls
{
    public partial class uc입항예정정보탭 : UserControl
    {
        private List<Button> tabButtons = new List<Button>();
        private List<Panel> tabPanels = new List<Panel>();
        
        private Color _clickedTabColor = Color.SteelBlue;
        private Color _normalTabColor = Color.FromArgb(26, 42, 69);
        private Color _mouseOverTabColor = Color.FromArgb(126, 42, 69);
        private Color _btnForeColor = Color.White;
        Font _FontButtonText { get { return new Font("맑은 고딕", 11, System.Drawing.FontStyle.Bold, System.Drawing.GraphicsUnit.Point, ((byte)(129))); } }

        public uc입항예정정보탭()
        {
            InitializeComponent();
        }

        public List<Panel> getListPanels => tabPanels;

        public void AddTab(string tabName, Control content)
        { 
            Button newTabButton = new Button();
            newTabButton = buttonStyleSet(newTabButton);
            
            newTabButton.Text = tabName;
            newTabButton.Click += TabButton_Click;
            newTabButton.MouseEnter += TabButton_MouseEnter;
            newTabButton.MouseLeave += TabButton_MouseLeave;

            tableLayoutPanel_btnTabs.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 100f / tableLayoutPanel_btnTabs.ColumnCount));
            tableLayoutPanel_btnTabs.Controls.Add(newTabButton, tableLayoutPanel_btnTabs.ColumnCount - 1, 0); // 버튼을 추가
            tableLayoutPanel_btnTabs.ColumnCount++;

            Panel newTabPanel = new Panel();
            newTabPanel.Dock = DockStyle.Fill;
            newTabPanel.Visible = false;  // 기본적으로 패널을 숨깁니다.
            newTabPanel.Controls.Add(content);  // 사용자가 제공한 컨트롤을 패널에 추가

            tableLayoutPanel2.Controls.Add(newTabPanel, 0, 1);  // 패널을 추가

            tabButtons.Add(newTabButton);
            tabPanels.Add(newTabPanel);

            if (tabPanels.Count == 1)
            {   
                // 첫 탭을 기본적으로 활성화
                newTabPanel.Visible = true;
                newTabButton.BackColor = _clickedTabColor;
            }
        }

        private void TabButton_MouseEnter(object sender, EventArgs e)
        {
            Button btn = sender as Button;
            if (btn.BackColor != _clickedTabColor)
            {
                btn.BackColor = _mouseOverTabColor; // Temporary hover color
            }
            //btn.BackColor = ;
        }

        private void TabButton_MouseLeave(object sender, EventArgs e)
        {   
            Button btn = sender as Button;
            if (btn.BackColor != _clickedTabColor)
            {
                btn.BackColor = _normalTabColor; // Revert to normal color
            }
        }

        private Button buttonStyleSet(Button myButton)
        {
            myButton.Dock = DockStyle.Top;  // 버튼을 상단에 배치
            myButton.Height = 30;  // 버튼의 높이 설정
            myButton.BackColor = _normalTabColor;  // 기본 색상 설정
            myButton.Font = _FontButtonText;
            myButton.ForeColor = _btnForeColor;
            myButton.Margin = new System.Windows.Forms.Padding(0, 0, 4, 0);
            myButton.FlatStyle = FlatStyle.Flat;
            myButton.TextAlign = ContentAlignment.MiddleCenter;
            return myButton;
        }

        private void TabButton_MouseOver()
        {   
            Color quickmenu_mousedownColor = Color.FromArgb(26, 42, 69);
            //Color quickmenu_noneSelectionColr = Color.FromArgb(50, 42, 69);
        }

        private void TabButton_Click(object sender, EventArgs e)
        {
            for (int i = 0; i < tabButtons.Count; i++)
            {
                if (sender == tabButtons[i])
                {
                    tabPanels[i].Visible = true;
                    tabButtons[i].BackColor = _clickedTabColor;  // 활성 탭 색상
                }
                else
                {
                    tabPanels[i].Visible = false;
                    tabButtons[i].BackColor = _normalTabColor;  // 비활성 탭 색상
                }
            }
        }

    }
}

```


###### 선박정보탭
```cs
namespace DW_SDMS.Presentation.UserControls
{
    public partial class ucShipInfoTab : UserControl
    {
        public FpSpread fp1 => fpSpread2; // FPSpread에 대한 참조를 반환하는 프로퍼티 접근자
        public FpSpread fp2 => fpSpread3;

        public ucShipInfoTab()
        {
            InitializeComponent();
        }
    }
}

```

###### aiListTab
```cs
namespace DW_SDMS.Presentation.UserControls
{
    public partial class ucShipToAiList : UserControl
    {
        public FpSpread fp3 => fpSpread5; // FPSpread에 대한 참조를 반환하는 프로퍼티 접근자
        public Button btnDel => btn_del;
        public Button btnAiRegister => btn_ship_register;
        public Button btnPlanClear => btn_planClear;
        public Button btnAiReq => btn_ai_req;

        public ucShipToAiList()
        {
            InitializeComponent();
        }
    }
}
```