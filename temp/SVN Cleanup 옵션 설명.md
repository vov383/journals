---
title: SVN Cleanup 옵션 설명
created: 2024-07-25 10:29
alias:
tags:
---
TortoiseSVN에서 Cleanup 명령을 실행할 때 사용할 수 있는 여러 옵션이 있습니다. 이 옵션들은 SVN 작업 디렉토리를 정리하고 잠금을 해제하는 데 도움이 됩니다.

#### TortoiseSVN Cleanup 옵션

1. **Break Locks (잠금 해제)**
   - 다른 사용자가 걸어놓은 잠금을 강제로 해제합니다. 이 옵션은 잠금을 강제 해제해야 할 경우 사용합니다.
1. **Fix Time Stamps (타임스탬프 수정)**
   - 파일 시스템의 타임스탬프를 수정하여 SVN과 파일 시스템 간의 시간 동기화를 맞춥니다.

3. **Revert all changes recursively (재귀적으로 모든 변경 사항 되돌리기)**
   - 작업 디렉토리 내 모든 변경 사항을 원래 상태로 되돌립니다. 재귀적으로 하위 디렉토리까지 적용됩니다.

4. **Delete unversioned files and folders (버전 관리되지 않은 파일 및 폴더 삭제)**
   - 버전 관리되지 않은 파일 및 폴더를 삭제합니다. 이 옵션을 사용하면 클린업 과정에서 필요 없는 파일이 제거됩니다.

5. **Include externals (외부 항목 포함)**
   - 외부 참조된 리포지토리의 항목도 클린업에 포함합니다.

#### TortoiseSVN Cleanup 실행 방법

1. **TortoiseSVN Cleanup 옵션 선택:**
   - 파일 탐색기에서 문제가 발생한 폴더로 이동합니다.
   - 해당 폴더를 마우스 오른쪽 버튼으로 클릭합니다.
   - 팝업 메뉴에서 `TortoiseSVN` > `Cleanup`을 선택합니다.
   - Cleanup 창이 나타나면 다음과 같은 옵션을 선택할 수 있습니다.
     - `Break Locks`
     - `Fix Time Stamps`
     - `Revert all changes recursively`
     - `Delete unversioned files and folders`
     - `Include externals`
   - 필요한 옵션을 선택한 후 `OK` 버튼을 클릭하여 Cleanup을 실행합니다.

#### 권장 옵션 사용 예시

- **권한 문제가 있을 때:**
  - `Break Locks` 옵션을 선택하여 잠금을 해제합니다.
  
- **타임스탬프 문제로 인해 충돌이 발생할 때:**
  - `Fix Time Stamps` 옵션을 선택하여 시간 동기화를 맞춥니다.

- **불필요한 파일을 제거하고 작업 디렉토리를 정리할 때:**
  - `Delete unversioned files and folders` 옵션을 선택합니다.

Q1: Cleanup 옵션 중에서 가장 많이 사용하는 옵션은 무엇인가요?
Q2: Cleanup 옵션을 사용한 후에도 문제가 해결되지 않는다면 어떻게 해야 하나요?

#### 요약

1. 여러 Cleanup 옵션을 통해 작업 디렉토리를 정리하고 잠금을 해제할 수 있습니다.
2. `Break Locks`, `Fix Time Stamps`, `Revert all changes recursively` 등의 옵션 사용 가능.
3. 파일 탐색기에서 Cleanup 옵션 선택 가능.
4. 권한 문제, 타임스탬프 문제 해결에 유용한 옵션 제공.
5. 필요에 따라 불필요한 파일 및 폴더를 제거할 수 있습니다.
6. 외부 항목 포함 옵션도 선택 가능.

Q1, Q2. 이 질문들은 SVN Cleanup 옵션의 실용성과 추가 문제 해결 방법에 대해 더 깊이 이해할 수 있도록 합니다.



![[../../noGitSync/Attachments/Pasted image 20250324171449.png]]
- **Vacuum pristine copies**  
    .svn 폴더 내부에는 “pristine copy”라는 작업 전/후 상태의 파일들이 별도로 저장됩니다. 이 항목에 체크하면 사용하지 않는 pristine 파일을 정리하여 .svn 폴더 용량을 줄일 수 있습니다.
    
- **Clean up working copy status**  
    작업 복사본 상태를 정리하면서 .svn 내부 메타데이터에 문제(잠금, 충돌 정보 등)가 있으면 해소할 수 있으므로 간접적으로 용량에 영향을 줄 수 있습니다.
