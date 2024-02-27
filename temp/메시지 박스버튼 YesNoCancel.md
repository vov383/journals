---
title: 메시지 박스버튼 YesNoCancel
created: 2024-02-27 08:42
alias:
tags:
---
```CSharp 
DialogResult result = MessageBox.Show("해당 직원의 데이터를 삭제하시겠습니까?", "작업확인", MessageBoxButtons.YesNoCancel, MessageBoxIcon.Question);

if (result == DialogResult.Yes)
{
    int id = 0;
    using (MySqlConnection conn = new MySqlConnection(_connectionAddress))
    {

        try
        {
            conn.Open();
            string delQuery = "DELETE FROM employee_list WHERE id = @id;";
            MySqlCommand cmd = new MySqlCommand(delQuery, conn);
            cmd.Parameters.AddWithValue("@id", listItem[0]);

            conn.Close();
        }
        catch (Exception exc)
        {
            MessageBox.Show(exc.Message);
        }
    }
    MessageBox.Show("데이터가 삭제되었습니다.");
} else
{
    MessageBox.Show("데이터가 삭제되지 않았습니다.");
}
```


