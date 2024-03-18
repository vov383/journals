---
title: Spread 코드 라이브러리 컬럼명 설정
created: 2024-03-12 02:12
alias:
tags:
---
컬럼명 배열을 선언하고 컬럼인덱스, 컬럼명, width, visible을 설정하는 코드
```cs
string[] column_names = { "mw_cd", "ul_cd", "name",
    "day1a", "day1b",
    "day2a", "day2b",
    "day3a", "day3b",
    "day4a", "day4b",
    "day5a", "day5b",
    "day6a", "day6b",
    "day7a", "day7b" };
for (int i = 0; i < column_names.Length; i++)
{
    if (column_names[i] == "mw_cd")
        _comSpread.ColumnSet(i, column_names[i], 100, true);
    else if (column_names[i] == "ul_cd")
        _comSpread.ColumnSet(i, column_names[i], 100, true);
    else if (column_names[i] == "name")
        _comSpread.ColumnSet(i, column_names[i], 100, true);
    else
        _comSpread.ColumnSet(i, column_names[i], 110, true);
}

public void ColumnSet(int columnIndex, string columnName, int width, bool isVisible)
{
    fs.Sheets[0].ColumnHeader.Cells[0, columnIndex].Tag = columnName;
    fs.Sheets[0].Columns.Get(columnIndex).Tag = columnName;
    fs.Sheets[0].Columns[columnIndex].Tag = columnName;

    //fs.Sheets[0].Columns.Get(idx).Label = headerText;
    fs.Sheets[0].Columns.Get(columnIndex).Width = width;
    fs.Sheets[0].Columns.Get(columnIndex).Visible = isVisible;            
}
```


## FpSpread의 컬럼헤더 텍스트와 컬럼 모양 설정하는 코드
```cs
private void SheetSetPortEntry()
{
    {
        FpSpread fs = _spgPortEntry.GridView;
        SheetView sheet = _spgPortEntry.GridSheetView;

        // 이벤트 추가
        fs.CellClick += fpSpread1_CellClick; // 셀클릭

        // 시트 스타일 관련
        fs.Sheets[0].SelectionStyle = FarPoint.Win.Spread.SelectionStyles.SelectionColors;
        fs.SetCursor(FarPoint.Win.Spread.CursorType.Normal, System.Windows.Forms.Cursors.Arrow);
        fs.Sheets[0].SelectionStyle = FarPoint.Win.Spread.SelectionStyles.SelectionColors;
        fs.Sheets[0].SelectionBackColor = Color.FromArgb(255, 150, 150, 255); // 선택 색상 설정
        fs.Sheets[0].RowHeader.Visible = false; //로우헤더 숨김
        
        // 컬럼헤더 로우 사이즈 조절, 폰트설정
        fs.Sheets[0].ColumnHeader.Rows[0].Height = 30;
        fs.Sheets[0].Rows.Default.Height = 30;
        fs.Sheets[0].ColumnHeader.DefaultStyle.Font = new Font("맑은 고딕", 11, FontStyle.Bold);
        
        fs.Sheets[0].ColumnCount = 0;

        fs.Sheets[0].OperationMode = OperationMode.ReadOnly;
        fs.Sheets[0].OperationMode = OperationMode.SingleSelect;
        
        _spgPortEntry.AddHeaderColumn("sh_cd", "sh_cd", 10, false);
        _spgPortEntry.AddHeaderColumn("sh_hold", "sh_hold", 10, false);
        _spgPortEntry.AddHeaderColumn("sh_nm", "선박명", 150, true);
        _spgPortEntry.AddHeaderColumn("dt_plan_entry", "입항예정일자", 120, true);
        _spgPortEntry.AddHeaderColumn("sh_year", "항차년도", 80, true);
        _spgPortEntry.AddHeaderColumn("sh_chasu", "항차수", 80, true);
        _spgPortEntry.AddHeaderColumn("br_nm", "BRAND", 120, true);
        _spgPortEntry.AddHeaderColumn("sh_tw", "총선적량", 120, true);

        //날짜형식
        _spgPortEntry.ColumnFormatDateTime("dt_plan_entry", "yyyy-MM-dd");

        //정렬
        for (int i = 0; i < _spgPortEntry.GridView.Sheets[0].ColumnCount; i++)
        { _spgPortEntry.ColumnAlignment(i, CellHorizontalAlignment.Center, CellHorizontalAlignment.Center); } //가운데정렬

        // 프로즌컬럼
        _spgPortEntry.GridView.Sheets[0].FrozenColumnCount = _spgPortEntry.GetIndexofColHeader("선박명") + 1;

        //개별 컬럼 정렬
        _spgPortEntry.ColumnAlignment("sh_nm", CellHorizontalAlignment.Center, CellHorizontalAlignment.Left);

        //사용자정렬기능
        //_spgPortEntry.GridView.Sheets[0].SetColumnAllowAutoSort(_spgPortEntry.GetIndexofColHeader("dt_plan_entry"), _spgPortEntry.GridView.Sheets[0].ColumnCount, true);

        // 폰트, 글자색 설정
        fs.Sheets[0].Columns["sh_nm"].Font = new Font("맑은 고딕", 11, FontStyle.Bold);
        fs.Sheets[0].Columns["sh_nm"].ForeColor = Color.Black;
        fs.Sheets[0].Columns["dt_plan_entry"].Font = new Font("맑은 고딕", 11, FontStyle.Bold);
        fs.Sheets[0].Columns["dt_plan_entry"].ForeColor = Color.Black;
        fs.Sheets[0].Columns["sh_year"].Font = new Font("맑은 고딕", 11, FontStyle.Bold);
        fs.Sheets[0].Columns["sh_year"].ForeColor = Color.Black;
        fs.Sheets[0].Columns["sh_chasu"].Font = new Font("맑은 고딕", 11, FontStyle.Bold);
        fs.Sheets[0].Columns["sh_chasu"].ForeColor = Color.Black;
        fs.Sheets[0].Columns["br_nm"].Font = new Font("맑은 고딕", 11, FontStyle.Bold);
        fs.Sheets[0].Columns["br_nm"].ForeColor = Color.Black;
        fs.Sheets[0].Columns["sh_tw"].Font = new Font("맑은 고딕", 11, FontStyle.Bold);
        fs.Sheets[0].Columns["sh_tw"].ForeColor = Color.Black;

    }
}
```


## 컬럼헤더의 text목록을 List로 가져오는 코드
```cs
List<String> columnHeaders = new List<string>();
for (int i = 0; i < sheet1.ColumnCount; i++)
{
    string columnHeader = sheet1.ColumnHeader.Cells[0, i].Text;
    columnHeaders.Add(columnHeader);
	    int iActiveRowIndex = main_sgm.GridSheetView.ActiveRowIndex;
}
```


 
## 새로고침 후 스크롤 원위치
```cs
int iTopRow = fpSpread1.GetViewportTopRow(0);
```


김종광이사님 코드 예제
```cs
 //그리드 초기화
        private void DataGridView_Set()
        {
            #region 생산목록
            {
                main_sgm = new SpreadGridManager(fpSpread1, 0);
				main_sgm.GridView.Sheets[0].ColumnHeader.Rows[0].Height = 42;
				main_sgm.GridView.Sheets[0].Rows.Default.Height = 60;
				main_sgm.GridView.Sheets[0].ColumnHeader.DefaultStyle.Font = new Font("맑은 고딕", 11, FontStyle.Regular);
                main_sgm.GridView.Sheets[0].ColumnCount = 0;

                //main_sgm.GridView.Sheets[0].OperationMode = OperationMode.ReadOnly;
                main_sgm.GridView.Sheets[0].OperationMode = OperationMode.SingleSelect;
                main_sgm.AddHeaderCheckBoxColumn("checkbox", "선택", 60, true);
                main_sgm.AddHeaderColumn("NO", " ", 40, false); //
                main_sgm.AddHeaderColumn("WORK_MNG_NUM", "생산관리번호", 120, true);
                main_sgm.AddHeaderColumn("WORK_PLAN_NUM", "생산계획번호", 90, false); //
                main_sgm.AddHeaderColumn("WORK_NUM", "자재코드", 60, true);
                main_sgm.AddHeaderColumn("WORK_NAME", "자재명", 150, true);
                main_sgm.AddHeaderColumn("WORK_TYPE", "자재분류", 90, true);
                main_sgm.AddHeaderColumn("WORK_KIND", "자재구분", 90, false); //
                main_sgm.AddHeaderColumn("WORK_KIND_NAME", "자재구분", 110, false); //
                main_sgm.AddHeaderColumn("WORK_STD", "자재규격", 90, true);
                main_sgm.AddHeaderColumn("WORK_UNIT", "단위", 60, true);
                main_sgm.AddHeaderColumn("PLAN_CNT", "예정수량", 90, true);
                main_sgm.AddHeaderColumn("WORK_CNT", "생산수량", 90, true); //사용자기능
                main_sgm.AddHeaderColumn("WORK_OK_CNT", "생산량\n(양품)", 90, true); //사용자기능
                main_sgm.AddHeaderColumn("WORK_START_DATE", "작업시작", 140, true);
                main_sgm.AddHeaderColumn("WORK_END_DATE", "작업완료", 140, true);
                main_sgm.AddHeaderColumn("CMD_BEGIN", " ", 90, true); //사용자기능
                main_sgm.AddHeaderColumn("CMD_END", " ", 90, true); //사용자기능
                main_sgm.AddHeaderColumn("WORK_STATE", "작업상태", 90, false); //

                main_sgm.AddHeaderColumn("WORK_STATE_NAME", "작업상태", 90, true);
                main_sgm.AddHeaderColumn("WORK_ETC", "기타", 90, true);

                //날짜형식
                main_sgm.ColumnFormatDateTime("WORK_START_DATE", "yyyy-MM-dd HH:mm");
                main_sgm.ColumnFormatDateTime("WORK_END_DATE", "yyyy-MM-dd HH:mm");

                //정렬
                for (int i = 0; i < main_sgm.GridView.Sheets[0].ColumnCount; i++)
                    main_sgm.ColumnAlignment(i, CellHorizontalAlignment.Center, CellHorizontalAlignment.Center);
                main_sgm.ColumnAlignment("WORK_NAME", CellHorizontalAlignment.Center, CellHorizontalAlignment.Left);

                //사용자정렬기능
                main_sgm.GridView.Sheets[0].SetColumnAllowAutoSort(main_sgm.GetIndexofColHeader("WORK_MNG_NUM"), main_sgm.GridView.Sheets[0].ColumnCount, true);
                //main_sgm.GridView.Sheets[0].SetColumnAllowAutoSort(main_sgm.GetIndexofColHeader("XXXXX"), 1, false);

                //진행율표시
                //main_sgm.ColumnFormatPrograss("XXXX", Color.DarkOrange, 0, 100);

                //생산수량
                main_sgm.GridView.Sheets[0].Columns["WORK_CNT"].Font = new Font("맑은 고딕", 11, FontStyle.Bold | FontStyle.Underline);
                main_sgm.GridView.Sheets[0].Columns["WORK_CNT"].ForeColor = Color.White;

                //생산량(양품)
                main_sgm.GridView.Sheets[0].Columns["WORK_OK_CNT"].Font = new Font("맑은 고딕", 11, FontStyle.Bold | FontStyle.Underline);
                main_sgm.GridView.Sheets[0].Columns["WORK_OK_CNT"].ForeColor = Color.White;

                //작업시작
                main_sgm.GridView.Sheets[0].Columns["CMD_BEGIN"].Font = new Font("맑은 고딕", 11, FontStyle.Bold | FontStyle.Underline);
                main_sgm.GridView.Sheets[0].Columns["CMD_BEGIN"].ForeColor = Color.White;

                //작업완료
                main_sgm.GridView.Sheets[0].Columns["CMD_END"].Font = new Font("맑은 고딕", 11, FontStyle.Bold | FontStyle.Underline);
                main_sgm.GridView.Sheets[0].Columns["CMD_END"].ForeColor = Color.White;

            }
            #endregion
        }

        //그리드 조회표시
        private void DataGridView_Display()
        {
            Hashtable param_ht = new Hashtable();



            #region 생산목록

            {

                //새로고침 후 스크롤 원위치

                int iTopRow = fpSpread1.GetViewportTopRow(0);

                int iActiveRowIndex = main_sgm.GridSheetView.ActiveRowIndex;



                DataSet ds = sqlQuery.SelectMES_TD3_420_이미터사출검사_생산목록(param_ht);

                main_sgm.GridSheetView.Rows.Clear();

                if (ds != null && ds.Tables.Count > 0 && ds.Tables[0].Rows.Count > 0)

                {

                    DataGridView_Display(main_sgm, ds.Tables[0]);

                }



                //새로고침 후 스크롤 원위치

                fpSpread1.SetViewportTopRow(0, iTopRow);



                //색상처리

                Common.DataGridView_ColorState(main_sgm);

                DataGridView_Color(main_sgm);



                //상세표시

                if (main_sgm.GridSheetView.RowCount > 0)

                {

                    //줄선택

                    main_sgm.GridSheetView.OperationMode = OperationMode.RowMode;

                    //새로고침 후 스크롤 원위치

                    main_sgm.GridSheetView.ActiveRowIndex = iActiveRowIndex;



                    //상세정보표시

                    DataGridView_DisplaySub(iActiveRowIndex);



                }

            }

            #endregion



        }
```