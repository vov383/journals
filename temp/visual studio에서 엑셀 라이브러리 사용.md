---
title: visual studio에서 엑셀 라이브러리 사용
created: 2024-03-04 03:57
alias:
tags:
---
`Microsoft.Office.Interop.Excel` 라이브러리를 사용하려면, 프로젝트에 해당 어셈블리 참조를 추가해야 합니다. 
Visual Studio에서 프로젝트 우클릭 -> 참조 추가 -> COM 탭 -> `Microsoft Excel Object Library` 검색 후 추가합니다. 
Excel 애플리케이션 인스턴스를 생성하고, 워크북과 워크시트를 만든 다음, DataGridView의 데이터를 순회하며 Excel 워크시트에 데이터를 채웁니다. 데이터 입력 후, Excel 파일을 저장합니다.


