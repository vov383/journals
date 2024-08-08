---
title: COALESCE() in MySQL
created: 2024-08-08 09:32
alias:
tags:
---
`COALESCE` 함수는 
주어진 인자 중 첫 번째로 `NULL`이 아닌 값을 반환합니다. 만약 모든 인자가 `NULL`이라면, 마지막 인자를 반환합니다. 즉, `COALESCE(a, b)`는 `a`가 `NULL`이 아니면 `a`를 반환하고, `a`가 `NULL`이면 `b`를 반환합니다.
