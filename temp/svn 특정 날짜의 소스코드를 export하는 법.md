---
title: svn 특정 날짜의 소스코드를 export하는 법
created: 2025-07-25 02:03
alias:
tags:
---
log 명령으로 원하는 commit 버전을 찾고
export 명령으로 소스를 내려받음.
```
svn log -r {"<날짜 from>"}:{"<날짜 To>"} <url>

svn export -r <리비전넘버> <url>
```

###### 실제 명령 실행 예시
![[../../noGitSync/cd/실제 svn export 명령 실행 예시]]
