---
title: DataGridView 컬럼 헤더 텍스트 변경
created: 2024-02-27 09:43
alias:
tags:
---
```CSharp 
private void updateColumnHeaderText()
{
    dataGridView1.Columns["emp_name"].HeaderText = "이름";
    dataGridView1.Columns["gender"].HeaderText = "성별";
    dataGridView1.Columns["age"].HeaderText = "나이";
    dataGridView1.Columns["home_address"].HeaderText = "주소";
    dataGridView1.Columns["department"].HeaderText = "부서";
    dataGridView1.Columns["rank_position"].HeaderText = "직책";
    dataGridView1.Columns["com_call_num"].HeaderText = "회사번호";
    dataGridView1.Columns["phone_num"].HeaderText = "개인번호";
    dataGridView1.Columns["mail_address"].HeaderText = "이메일";
    dataGridView1.Columns["join_date"].HeaderText = "입사일";
}
```

[[../../dotnet DataGridView|dotnet DataGridView]]
