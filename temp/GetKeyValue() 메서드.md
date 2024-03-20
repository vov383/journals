---
title: GetKeyValue() 메서드
created: 2024-03-20 02:02
alias:
tags:
---
ds, 키컬럼, 밸류컬럼
dgv, 키, 벨류
```cs
public static Hashtable GetKeyValue(DataSet ds, string keyColumn, string valueColumn)
{
    Hashtable ht = new Hashtable();

    if (ds != null && ds.Tables.Count > 0 && ds.Tables[0].Rows.Count > 0)
    {
        if (ds.Tables[0].Columns.Contains(keyColumn) && ds.Tables[0].Columns.Contains(valueColumn))
        {
            foreach (DataRow dr in ds.Tables[0].Rows)
            {
                string key = Convert.ToString(dr[keyColumn]);
                string value = Convert.ToString(dr[valueColumn]);
                ht[key] = value;
            }
        }
    }

    return ht;
}
public static Hashtable GetKeyValue(DataSet ds, string filterExpression)
{
    Hashtable ht = new Hashtable();

    if (ds != null && ds.Tables.Count > 0 && ds.Tables[0].Rows.Count > 0)
    {
        DataRow[] rows = ds.Tables[0].Select(filterExpression);
        if (rows != null && rows.Length > 0)
        {
            foreach (DataRow dr in rows)
            {
                foreach (DataColumn dc in ds.Tables[0].Columns)
                {
                    string key = dc.ColumnName;
                    string value = Convert.ToString(dr[dc.ColumnName]);
                    ht[key] = value;
                }
            }
        }
    }

    return ht;
}
public static Hashtable GetKeyValue(DataSet ds, int rowIndex)
{
    Hashtable ht = new Hashtable();

    if (ds != null && ds.Tables.Count > 0 && ds.Tables[0].Rows.Count > 0)
    {
        if (rowIndex >=0 && rowIndex < ds.Tables[0].Rows.Count)
        {
            foreach (DataColumn dc in ds.Tables[0].Columns)
            {
                string key = dc.ColumnName;
                string value = Convert.ToString(ds.Tables[0].Rows[rowIndex][dc.ColumnName]);
                ht[key] = value;
            }
        }
    }

    return ht;
}

/// <summary>
/// DataGridView에서 Hashtable[key=value]을 반환합니다.
/// </summary>
public static Hashtable GetKeyValue(DataGridView dgv, string keyColumn, string valueColumn)
{
    Hashtable ht = new Hashtable();

    if (dgv.Rows.Count > 0)
    {
        if (dgv.Columns.Contains(keyColumn) && dgv.Columns.Contains(valueColumn))
        {
            foreach (DataGridViewRow row in dgv.Rows)
            {
                string key = Convert.ToString(row.Cells[keyColumn].Value);
                string value = Convert.ToString(row.Cells[valueColumn].Value);
                ht[key] = value;
            }
        }
    }

    return ht;
}
```


