---
title: 윈도우 파워쉘 ssl 인증키 생성
created: 2025-08-01 04:31
alias:
tags:
---
```powershell
  # RSA 4096비트 개인키 생성
openssl genrsa -out C:\ssl\ca-key.pem 4096
  # 자체 서명된 루트 CA 인증서 발급 (CN=rootCA)
openssl req -x509 -new -nodes `
  -key C:\ssl\ca-key.pem `
  -days 3650 `
  -out C:\ssl\ca.pem `
  -subj "/CN=rootCA"

# 서버용 개인키 및 CSR 생성 (CN=serverCA)
openssl genrsa -out C:\ssl\server-key.pem 2048
openssl req -new -key C:\ssl\server-key.pem `
  -out C:\ssl\server-req.pem `
  -subj "/CN=192.168.0.184,OU=serverCA"

# 루트 CA로 서버 CSR 서명
openssl x509 -req `
  -in C:\ssl\server-req.pem `
  -CA C:\ssl\ca.pem `
  -CAkey C:\ssl\ca-key.pem `
  -CAcreateserial `
  -out C:\ssl\server-cert.pem `
  -days 365

# 클라이언트용 개인키 및 CSR 생성 (CN=dbclient,OU=clientCA)
openssl genrsa -out C:\ssl\client-key.pem 2048
openssl req -new -key C:\ssl\client-key.pem `
  -out C:\ssl\client-req.pem `
  -subj "/CN=dbclient,OU=clientCA"

# 루트 CA로 클라이언트 CSR 서명
openssl x509 -req `
  -in C:\ssl\client-req.pem `
  -CA C:\ssl\ca.pem `
  -CAkey C:\ssl\ca-key.pem `
  -CAcreateserial `
  -out C:\ssl\client-cert.pem `
  -days 365
```


##### 파워쉘에서 했던 거
```
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

새로운 기능 및 개선 사항에 대 한 최신 PowerShell을 설치 하세요! https://aka.ms/PSWindows

PS C:\WINDOWS\system32> winget search openssl
이름                 장치 ID                      버전  일치             원본
-------------------------------------------------------------------------------
OpenSSL              ShiningLight.OpenSSL.Dev     3.5.1                  winget
FireDaemon OpenSSL 3 FireDaemon.OpenSSL           3.5.1 Command: openssl winget
OpenSSL Light        ShiningLight.OpenSSL.Light   3.5.1 Command: openssl winget
FireDaemon Lozenge   FireDaemon.FireDaemonLozenge 3.0.4 Tag: openssl     winget
Stunnel              MichalTrojnara.Stunnel       5.75  Tag: openssl     winget
PS C:\WINDOWS\system32> winget install --id=ShiningLight.OpenSSL.Light
찾음 OpenSSL Light [ShiningLight.OpenSSL.Light] 버전 3.5.1
이 응용 프로그램의 라이선스는 그 소유자가 사용자에게 부여했습니다.
Microsoft는 타사 패키지에 대한 책임을 지지 않고 라이선스를 부여하지도 않습니다.
이 패키지에는 다음 종속성이 필요합니다.
  - 패키지
      Microsoft.VCRedist.2015+.x64
다운로드 중 https://slproweb.com/download/Win64OpenSSL_Light-3_5_1.msi
  ██████████████████████████████  5.75 MB / 5.75 MB
설치 관리자 해시를 확인했습니다.
패키지 설치를 시작하는 중...
설치 성공
PS C:\WINDOWS\system32> openssl version
OpenSSL 3.5.1 1 Jul 2025 (Library: OpenSSL 3.5.1 1 Jul 2025)
PS C:\WINDOWS\system32> cd c:/
PS C:\> mkdir ssl
mkdir : 지정한 이름(C:\ssl)의 항목이 이미 있습니다.
위치 줄:1 문자:1
+ mkdir ssl
+ ~~~~~~~~~
    + CategoryInfo          : ResourceExists: (C:\ssl:String) [New-Item], IOException
    + FullyQualifiedErrorId : DirectoryExist,Microsoft.PowerShell.Commands.NewItemCommand

PS C:\>  # RSA 4096비트 개인키 생성
>> openssl genrsa -out C:\ssl\ca-key.pem 4096
>>   # 자체 서명된 루트 CA 인증서 발급 (CN=rootCA)
>> openssl req -x509 -new -nodes `
>>   -key C:\ssl\ca-key.pem `
>>   -days 3650 `
>>   -out C:\ssl\ca.pem `
>>   -subj "/CN=rootCA"
PS C:\> # 서버용 개인키 및 CSR 생성 (CN=serverCA)
>> openssl genrsa -out C:\ssl\server-key.pem 2048
>> openssl req -new -key C:\ssl\server-key.pem `
>>   -out C:\ssl\server-req.pem `
>>   -subj "/CN=serverCA"
>>
>> # 루트 CA로 서버 CSR 서명
>> openssl x509 -req `
>>   -in C:\ssl\server-req.pem `
>>   -CA C:\ssl\ca.pem `
>>   -CAkey C:\ssl\ca-key.pem `
>>   -CAcreateserial `
>>   -out C:\ssl\server-cert.pem `
>>   -days 365
Certificate request self-signature ok
subject=CN=serverCA
PS C:\> # 클라이언트용 개인키 및 CSR 생성 (CN=dbclient,OU=clientCA)
>> openssl genrsa -out C:\ssl\client-key.pem 2048
>> openssl req -new -key C:\ssl\client-key.pem `
>>   -out C:\ssl\client-req.pem `
>>   -subj "/CN=dbclient,OU=clientCA"
>>
>> # 루트 CA로 클라이언트 CSR 서명
>> openssl x509 -req `
>>   -in C:\ssl\client-req.pem `
>>   -CA C:\ssl\ca.pem `
>>   -CAkey C:\ssl\ca-key.pem `
>>   -CAcreateserial `
>>   -out C:\ssl\client-cert.pem `
>>   -days 365
Certificate request self-signature ok
subject=CN=dbclient,OU=clientCA
PS C:\>

```


