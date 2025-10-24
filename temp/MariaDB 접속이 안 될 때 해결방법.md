---
title: MariaDB 접속이 안 될 때 해결방법
created: 2025-10-22 10:14
aliases: 
tags:
---
### MariaDB 서비스 실행중이 아님
20251022 발생
인터넷 정상. 마리아디비만 문제

1. db pc에 원격으로 접속
2. `win + r` -> `services.msc`에서 MariaDB 서비스가 '실행 중'이 아니어서, DB 서버 자체가 꺼져있는 상태
3. 서비스를 '실행'으로 변경하여 문제를 해결

원인 추측 **메모리 부족(Out of Memory):** PC의 메모리(RAM)가 부족하여 OS가 MariaDB 프로세스를 강제로 종료시켰을 가능성 있음
task 실행 중에 발생하였음.
