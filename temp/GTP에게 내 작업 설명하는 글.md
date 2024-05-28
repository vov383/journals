---
title: GTP에게 내 작업 설명하는 글
created: 2024-05-28 13:32
aliases: 
tags:
---
내 DB의 DOCK_ORDER2는 선석배정계획의 확정 데이터이고 DECISION 컬럼이 있어. 이게 1이면 확정이고 0이면 확정이 아니야. 그리고 DOCK_PLAN2는 선석배정계획의 임시 데이터이고 VIEW 컬럼이 있어. 이게 1이면 화면에 표시할거고 0이면 화면에 표시하지 않을거야. ORDER2와 PLAN2의 컬럼은 DECISION컬럼과 VIEW컬럼 유무의 차이 외에는 모두 동일해. 
이때 LEFTJOIN으로 PLAN2에서 ORDER2로 LEFTJOIN하면 모든 PLAN2 데이터를 가져오고 그 중에 DECISION이 1이거나 0인 데이터와 아직 ORDER2에 없는 데이터를 가져올 수 있겠지?