---
title: 드래그한 셀의 정보를 `_dragedShipCellDict에` 저장하는 기능
created: 2024-04-11 04:42
alias:
tags:
---
```cs
private void saveDragedShipCellData(SheetView sheet , Dictionary<string, object> item)
{
    int rIdx = 0;
    int cIdx = 0;
    int cIdxFrom = 0;
    int cIdxTo = 0;

    string keyRow = $"{item["MW_CD"]}";
    if (_rIdxBerth.Contains(keyRow))
        rIdx = Convert.ToInt32(_rIdxBerth[keyRow]);
    string keyFrom = $"{item["DT_START"]}_{item["SHIFT_START"]}";
    string keyTo = $"{item["DT_END"]}_{item["SHIFT_END"]}";

    if (_cIdxTimeBase.Contains(keyFrom))
        cIdxFrom = Convert.ToInt32(_cIdxTimeBase[keyFrom]);
    else
        cIdxFrom = _comSpread.GetColumnIndex("1A");

    if (_cIdxTimeBase.Contains(keyTo))
        cIdxTo = Convert.ToInt32(_cIdxTimeBase[keyTo]);
    else
        cIdxTo = _comSpread.GetColumnIndex("7B");

    // _dragedShipCellDict에 셀 정보를 저장
    _dragedShipCellDict = new Dictionary<int, Cell>();
    for (int i = 0; i <= cIdxTo-cIdxFrom; i++)
    {   
        _dragedShipCellDict.Add(i, sheet.Cells[rIdx, cIdxFrom + i]);
    }
    
}
```


