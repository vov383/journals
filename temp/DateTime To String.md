---
title: DateTime To String
created: 2024-03-14 09:35
alias:
tags:
---
C#을 사용하여 Windows Forms 애플리케이션에서 날짜를 나타내는 문자열을 `DateTime` 개체로 변환하려면 일반적으로 `DateTime.Parse` 또는 `DateTime.TryParse` 메서드를 사용합니다
```cs
string dateString = "2024-03-14"; // Example date
DateTime dateTime = DateTime.Parse(dateString);
Console.WriteLine(dateTime.ToString("yyyy-MM-dd"));

string dateString = "2024-03-14"; // Example date DateTime dateTime; bool success = DateTime.TryParse(dateString, out dateTime); if (success) { Console.WriteLine(dateTime.ToString("yyyy-MM-dd")); } else { Console.WriteLine("Invalid date format."); }

```


