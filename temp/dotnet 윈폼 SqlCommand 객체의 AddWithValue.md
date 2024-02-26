---
title: dotnet 윈폼 SqlCommand 객체의 AddWithValue
created: 2024-02-26 02:04
alias:
tags:
---
```CSharp
string insertQuery = "INSERT INTO employee_list (" +
                "emp_name, gender, age, home_address, department, rank_position" +
                ", com_call_num, phone_num, mail_address, join_date) " +
            "VALUES (" +
                "@name, @gender, @age, @address, @dept, @rank, @com, @phone, @email, NOW());";
using(MySqlConnection mySqlConn = new MySqlConnection(_connectionAddress))
{

    try
    {
        mySqlConn.Open();

        MySqlCommand cmd = new MySqlCommand(insertQuery, mySqlConn);
        cmd.Parameters.AddWithValue("@name", textBoxName.Text);
        cmd.Parameters.AddWithValue("@gender", comboBoxGender.Text);
```

