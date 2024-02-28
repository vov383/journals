---
title: 콤보박스 항목 sql로 가져오기
created: 2024-02-28 10:09
alias:
tags:
---
```csharp
private List<string> getCboxItems(string item)
{
    using (MySqlConnection conn = new MySqlConnection(_connectionAddress))
    {
        string queryStr = $"SELECT DISTINCT {item} FROM employee_list"; // 쿼리에 Parameters.AddWithValue(); 방식은 컬럼명이나 테이블명에 사용 불가
        conn.Open();
        MySqlDataAdapter adapter = new MySqlDataAdapter();
        
        MySqlCommand cmd = new MySqlCommand(queryStr, conn);
        adapter.SelectCommand = cmd;

        DataSet ds = new DataSet();
        adapter.Fill(ds, "employee_list");

        List<string> cobxItems = new List<string>();

        foreach (DataRow row in ds.Tables["employee_list"].Rows)
        {
            cobxItems.Add(row[item].ToString());
        }
        conn.Close();
        return cobxItems;
    }
        
}
```
![[sql 쿼리 파라미터|sql 쿼리 파라미터]]

폼이 로드될 때
```csharp
private void InsertForm_Load(object sender, EventArgs e)
{
    List<string> itemList = new List<string>() { "department", "rank_position" }; // 가져올 목록의 컬럼명

    string[] deptListItem = getCboxItems(itemList[0]).ToArray();
    Trace.WriteLine("부서목록 : " + deptListItem);
    string[] rankListItem = getCboxItems(itemList[1]).ToArray();
    cboxDept.Items.AddRange(deptListItem); // 부서 목록을 cbox에 담기
    cboxRank.Items.AddRange(rankListItem); // 직급 목록을 cbox에 담기
}
```


