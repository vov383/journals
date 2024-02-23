---
title: 입력 값 검증 및 오류 처리 구현
created: 2024-02-22 01:33
alias:
tags:
---
1. **입력 값 검증**: "age" 필드에 대한 입력 값이 정수인지 확인합니다. 또한, 다른 필드에 대해서도 유효성 검사를 수행할 수 있습니다(예: 필수 필드가 비어 있지 않은지 확인).

2. **사용자 피드백 제공**: 유효하지 않은 입력에 대해 사용자에게 메시지 박스를 통해 알립니다.

3. **올바른 데이터만 데이터베이스에 삽입**: 모든 입력 값이 유효한 경우에만 데이터베이스에 삽입 작업을 수행합니다.

# 예제 코드

```csharp
private void btnInsert_Click(object sender, EventArgs e)
{
    // 'age' 필드의 입력 값을 검증합니다.
    if (!int.TryParse(textBoxAge.Text, out int age))
    {
        MessageBox.Show("Age must be an integer.", "Invalid Input", MessageBoxButtons.OK, MessageBoxIcon.Error);
        return; // 메서드를 더 이상 진행하지 않고 종료합니다.
    }
    
    // 다른 필드에 대한 검증도 여기서 수행할 수 있습니다.

    try
    {
        using (MySqlConnection conn = new MySqlConnection(_connectionAddress))
        {
            conn.Open();
            string insertQuery = $"INSERT INTO employee_list (emp_name, gender, age, home_address, department, rank_position, com_call_num, phone_num, mail_address, join_date) VALUES ('{textBoxName.Text}', '{comboBoxGender.SelectedValue}', {age}, '{textBoxAddress.Text}', '{textBoxDept.Text}', '{textBoxPositionRank.Text}', '{textBoxComNum.Text}', '{textBoxHpNum.Text}', '{textBoxEmail.Text}', NOW());";
            
            MySqlCommand command = new MySqlCommand(insertQuery, conn);

            if (command.ExecuteNonQuery() != 1)
            {
                MessageBox.Show("Fail to insert data");
            }
            else
            {
                MessageBox.Show("Data inserted successfully");
                // 필드를 초기화하는 로직을 여기에 추가할 수 있습니다.
            }
        }
    }
    catch (Exception exc)
    {
        MessageBox.Show(exc.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
    }
}
```

이 코드는 "age" 필드에 대한 사용자 입력이 정수인지 확인합니다. `int.TryParse` 메서드는 입력 문자열을 정수로 변환할 수 있으면 `true`를 반환하고 변환된 정수를 `out` 파라미터로 반환합니다. 변환할 수 없으면 `false`를 반환하고, 이 경우 사용자에게 오류 메시지를 표시한 후 메서드 실행을 중단합니다. 이런 방식으로 입력 값 검증을 추가하면 사용자가 입력한 데이터의 유효성을 보장하고, 데이터베이스 관련 오류를 방지할 수 있습니다.

