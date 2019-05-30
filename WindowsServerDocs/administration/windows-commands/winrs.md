---
title: winrs
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c370de31-5651-400a-872d-ef229aae2309
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c54a747f4dde1113fa735c1408f48dbfaf2e74dc
ms.sourcegitcommit: 39ab8041d166e6817a95417d6aa30bc7abeeef54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66260268"
---
# <a name="winrs"></a>winrs

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 원격 관리를 사용 하면 관리 하 고 프로그램을 원격으로 실행할 수 있습니다.   
## <a name="syntax"></a>구문  
```  
winrs [/<parameter>[:<value>]] <command>  
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|/remote:\<endpoint>|NetBIOS 이름이 나 표준 연결을 사용 하 여 대상 끝점을 지정 합니다.<br /><br />-   <url>: [\<transport>://]\<target>[:\<port>]<br /><br />지정 하지 않으면 **/r:localhost** 사용 됩니다.|  
|/unencrypted|원격 셸에 메시지 암호화 되지 않았음을 지정 합니다. 이 네트워크 트래픽을 이미 사용 하 여 암호화 하는 경우 나 문제 해결에 유용 **ipsec**, 또는 물리적 보안이 적용 되는 시점입니다.<br /><br />기본적으로 Kerberos 또는 NTLM 키를 사용 하 여 메시지를 암호화 합니다.<br /><br />이 명령줄 옵션에는 HTTPS 전송을 선택한 경우 무시 됩니다.|  
|/username:\<username>|명령줄에서 사용자 이름을 지정 합니다.<br /><br />지정 하지 않으면 도구 이름에 대 한 프롬프트 또는 협상 인증 사용 합니다.<br /><br />하는 경우 **/username** 를 지정 하면 **/password** 도 지정 해야 합니다.|  
|/password:\<password>|명령줄에서 암호를 지정합니다.<br /><br />하는 경우 **/password** 지정 하지 않으면 하지만 **/username** 되 면 도구는 암호에 대 한 라는 메시지가 표시 됩니다.<br /><br />하는 경우 **/password** 를 지정 하면 **/username** 도 지정 해야 합니다.|  
|/timeout:\<seconds>|이 옵션을 사용 하는 사용 되지 않습니다.|  
|/directory:\<path>|원격 셸에 대 한 시작 디렉터리를 지정합니다.<br /><br />지정 하지 않으면 원격 셸 환경 변수로 정의 된 사용자의 홈 디렉터리에서 시작 됩니다 **% USERPROFILE %** 합니다.|  
|/environment:\<문자열 > =<value>|셸 시작 되 면 기본 환경에 대 한 변경 허용 셸 설정 해야 하는 단일 환경 변수를 지정 합니다.<br /><br />여러 환경 변수를 지정 하려면이 스위치를 여러 번 사용 되어야 합니다.|  
|/noecho|해당 에코 하지 않도록 지정 합니다. 이 원격 프롬프트에 사용자의 답변 로컬로 표시 되지 않는지 확인 해야 할 수도 있습니다.<br /><br />기본 echo "on"입니다.|  
|/noprofile|사용자의 프로필을 로드 하지 않아야 지정 합니다.<br /><br />기본적으로는 서버는 사용자 프로필을 로드 하려고 합니다.<br /><br />원격 사용자 대상 시스템에서 로컬 관리자가 아닌 경우이 옵션을 필요한 수 (기본값 오류가 발생 합니다).|  
|/allowdelegate|사용자의 자격 증명 사용할 수 있도록 원격 공유에 액세스 하는 대상 끝점 보다 다른 컴퓨터에서 찾을 수를 지정 합니다.|  
|/compression|압축을 사용 합니다.  원격 컴퓨터에서 이전 설치는 기본적으로 해제 되어 있으므로 압축을 지원 하지 않습니다.<br /><br />기본 설정은 꺼져 원격 컴퓨터에 설치 된 이전 압축을 지원 하지 않을 수 있습니다.|  
|/usessl|원격 끝점을 사용 하는 경우 SSL 연결을 사용 합니다.  이 전송 하는 대신 지정 **https:** 기본값이 사용 됩니다 **WinRM** 기본 포트입니다.|  
|/?|명령 프롬프트에 도움말을 표시합니다.|  

## <a name="remarks"></a>설명  
-   모든 명령줄 옵션 약식 표현 또는 긴 형식에 적용 합니다. 예를 들어 모두 **/r** 및 **/원격** 유효 합니다.  
-   종료 합니다 **/원격** 명령을 입력할 수 있습니다 **Ctrl + C** 또는 **ctrl-break**, 원격 셸에 전송 됩니다. 두 번째 **Ctrl + C** 를 강제로 종료 **winrs.exe**합니다.  
-   활성 원격 셸 또는 winrs 구성을 관리 하려면 WinRM 도구를 사용 합니다.  URI 활성 셸을 관리 하기 별칭은 **셸/cmd**합니다.  별칭 winrs 구성에 대 한 URI가 **winrm/config/winrs**합니다.  

## <a name="BKMK_Examples"></a>예제  
```  
winrs /r:https://contoso.com command  
```  
```  
winrs /r:contoso.com /usessl command  
```  
```  
winrs /r:myserver command  
```  
```  
winrs /r:http://127.0.0.1 command  
```  
```  
winrs /r:http://169.51.2.101:80 /unencrypted command  
```  
```  
winrs /r:https://[::FFFF:129.144.52.38] command  
```  
```  
winrs /r:http://[1080:0:0:0:8:800:200C:417A]:80 command  
```  
```  
winrs /r:https://contoso.com /t:600 /u:administrator /p:$%fgh7 ipconfig  
```  
```  
winrs /r:myserver /env:path=^%path^%;c:\tools /env:TEMP=d:\temp config.cmd  
```  
```  
winrs /r:myserver netdom join myserver /domain:testdomain /userd:johns /passwordd:$%fgh789  
```  
```  
winrs /r:myserver /ad /u:administrator /p:$%fgh7 dir \\anotherserver\share  
```  

## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
  
