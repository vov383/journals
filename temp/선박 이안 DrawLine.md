---
title: 선박 이안 DrawLine
created: 2024-04-02 09:54
aliases: 
tags:
---
선박의 이안정보 표시 계속(03.29~
이안정보 표시를 위한 drawLine
1. 현재 셀 + 1컬럼의 점의 좌표값을 알고 있음.
2. 그 좌표값에서 셀 height의 절반만큼 아래의 포인트 좌표 구하기
3. drawLine
4. 그 좌표값에서 2칸정도 셀의 width만큼 옆의 좌표 구하기 
5. 그 좌표값에서 셀 width의 절반만큼
6. drawLine
선박 이안정보 표시 drawLine은 나중에 수정하기로