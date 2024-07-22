---
title: MySQL에서 날짜 및 시간 관련 함수들
created: 2024-07-22 01:52
alias:
tags:
---
#### MySQL 날짜 및 시간 관련 함수들
1. **CURDATE()**:
   - **용도**: 현재 날짜를 반환합니다.
   - **예제**: `SELECT CURDATE();` -> '2024-07-22'

2. **CURTIME()**:
   - **용도**: 현재 시간을 반환합니다.
   - **예제**: `SELECT CURTIME();` -> '14:30:15'

3. **NOW()**:
   - **용도**: 현재 날짜와 시간을 반환합니다.
   - **예제**: `SELECT NOW();` -> '2024-07-22 14:30:15'

4. **DATE_FORMAT(date, format)**:
   - **용도**: 날짜를 지정된 형식으로 변환합니다.
   - **예제**: `SELECT DATE_FORMAT(NOW(), '%Y-%m-%d');` -> '2024-07-22'

5. **DATE_ADD(date, INTERVAL value unit)**:
   - **용도**: 날짜에 지정된 간격을 더합니다.
   - **예제**: `SELECT DATE_ADD('2024-07-22', INTERVAL 1 DAY);` -> '2024-07-23'

6. **DATE_SUB(date, INTERVAL value unit)**:
   - **용도**: 날짜에서 지정된 간격을 뺍니다.
   - **예제**: `SELECT DATE_SUB('2024-07-22', INTERVAL 1 DAY);` -> '2024-07-21'

7. **DATEDIFF(date1, date2)**:
   - **용도**: 두 날짜 사이의 일 수 차이를 계산합니다.
   - **예제**: `SELECT DATEDIFF('2024-07-22', '2024-07-20');` -> 2

8. **TIMESTAMPDIFF(unit, datetime_expr1, datetime_expr2)**:
   - **용도**: 두 날짜 및 시간 값 사이의 차이를 지정된 단위로 반환합니다.
   - **예제**: `SELECT TIMESTAMPDIFF(HOUR, '2024-07-22 14:30:15', '2024-07-22 15:30:15');` -> 1


