---
title: Visual studio 오류(HRESULT 0x8000FFFF(E_UNEXPECTED))
created: 2024-02-27 09:12
alias:
tags:
---
![[4. Archive/attachment/Pasted image 20240227085719.png]]
# 원인:
Windows 캐시가 가득 차있거나 차단되었습니다.
# 해결 방법:
이 동작을 방지하려면 다음을 수행할 수 있습니다.
Vault 클라이언트를 닫습니다.
Vault 클라이언트를 시작합니다.
파일의 이름을 바꾸거나 설계를 복사하려고 다시 시도합니다.
# 문제를 방지하기 위한 예방 조치:
Vault 클라이언트 워크스테이션에서 다음 폴더를 비웁니다.
C:\Windows\temp\
C:\Temp\
%TEMP%
%APPDATA%\Autodesk\VaultCommon\
Inventor 초기 정보 문서를 비웁니다.


