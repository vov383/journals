---
title: viewCompareSpread() 에서 범위를 어떻게
created: 2024-04-15 12:55
alias:
tags:
---
스케쥴의 시작일부터 
즉 어제부터 오늘에서 6일 더한 날짜까지 7일이 변수

경우의수 DT START , DT END
DT START가 S 미만 DT END 가 S 미만 안보임
DT START가 S 미만 DT END 가 S 이상  DT END가 E 이하 보임
DT START가 S 미만 DT END 가 S 이상  DT END가 E 초과 보임
DT START가 S 이상 DT END 가 E 이하 보임
DT START가 S 이상 DT END 가 E 초과 보임
DT START가 E 초과 안보임

1A부터 시작 중간 끝
1A시작 7B 끝

중간 시작 중간 끝
중간 시작 7B 끝



e보다 뒤에 끝나더라도 dt_start가 e보다 작으면 가져오고


