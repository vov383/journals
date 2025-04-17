---
title: shifting계획서_mes정보 관련
created: 2025-04-10 17:15
aliases: 
tags:
---
인터페이스에서 필요한 값

실제 접안시간
ship_alngsd_dt 

일반 접안
RMAT_MGT_SHIP_ALNGSD_PRNMT_DT_1
ALNGSD_PRNMT_BERTH_NO_1


이안접안
RMAT_MGT_SHIP_ALNGSD_PRNMT_DT_2
ALNGSD_PRNMT_BERTH_NO_2



5 재접안

ship_

원료관리선박접안예정일시1~8
접안예정선석번호1~8

![[../../noGitSync/Attachments/Pasted image 20250410174141.png]]


독오더에 넣는건 취소

DOCK_SHIFT 테이블을 조회해서
접안 날짜 있고 선석 있고 접안~LT END 까지 FROM TO 로 표현

이안일시1 있으면 
접안~이안일시1를 SLICE1, 이안일시1~LT END를 SLICE2로 FROM TO로 표현.

###### dock_shift의 선석접안 계획 관련 항목 8개. 정리
1. 예정접안 선석, 일시
2. 이안1 선석, 일시
3. 이안2 선석, 일시
4. 출항 선석, 일시
5. 외항대기 일시
6. 재접안 선석, 일시
7. 재접안 후 이안1 선석, 일시
8. 재접안 후 이안2 선석, 일시

###### dock_shift의 선석접안 실적 관련 항목
MW_CD,
DT_SH_ENTRY (입항) ? (입항예정)
DT_SH_DOCK (접안)
DT_SH_END (완료(출항))

DT_LT_START 
DT_LT_END

