---
title: Git 브랜치 전략
created: 2024-02-28 08:10
aliases: 
tags:
---
visual studio 터미널에 git bash 추가
옵션 > 환경 > 터미널 > 추가 > 이름 `Git bash` > 셀 위치 `C:\Program Files\Git\bin\bash.exe` > 인수 `--login -i`
![[4. Archive/attachment/Pasted image 20240228081526.png]]
터미널 단축키는 Ctrl + T, M

파워셸을 깃 배쉬 터미널로 변경
![[4. Archive/attachment/Pasted image 20240228081757.png]]

###### 브랜치 조회
git branch
현재 로컬에 존재하는 브랜치 조회

git branch -a 
현재 로컬의 모든 브랜치 + 리모트 브랜치 조회

###### 브랜치 생성
git branch <브랜치 이름>

###### 브랜치 이동
git switch <브랜치 이름>

git checkout <브랜치이름> 도 동일한 기능을 하지만 checkout은 다른 기능도 많이 담고있어서 switch를 사용하길 권장함

새 브랜치에서 visual studio에서 push하면 remote에서도 새 브랜치에 push됨

###### 브랜치 생성과 동시에 이동
git switch -c <브랜치 이름>

###### 브랜치 삭제
git branch -d <브랜치 이름>

git branch -D it <브랜치 이름>
삭제 명령어는 매우 간단한데, 특이한 점은 소문자와 대문자에 따라 다르다
`git branch -d` 옵션을 사용해서 branch를 지울 경우 해당 브랜치가 만약 **문제가 있는 브랜치**다(정상적인 머지 상태가 아니거나 충돌이 해결되지 않은 브랜치) **라고 판단될 경우 git에서 에러를 발생하며 명령어가 실행되지 않는다.**

`git branch -D` 옵션의 경우에는 대문자로 만들어놓은 것처럼 **그냥 다 무시하고 삭제**하라 라는 의미이다.

안전하게 삭제할 때는 -d 사용한다. 

###### 브랜치 병합
git merge

