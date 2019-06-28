---
title: ktpass
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47087676-311e-41f1-8414-199740d01444
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ae7508aaefd136a91bd19e547b407020293ca484
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437925"
---
# <a name="ktpass"></a>ktpass

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active directory Domain Services (AD DS)에서 호스트 또는 서비스에 대 한 서버 주체 이름을 구성 하 고 서비스의 공유 비밀 키를 포함 하는 t a b 파일을 생성 합니다. .keytab 파일은 MIT(매사추세츠 공과대학교)의 Kerberos 인증 프로토콜 구현을 기반으로 합니다. Ktpass 명령줄 도구에는 Kerberos 키 배포 센터 (KDC) 서비스에서 제공 하는 상호 운용성 기능을 사용 하려면 Kerberos 인증을 지 원하는 Windows가 아닌 서비스 수 있습니다. 이 항목에 지정 된 운영 체제 버전에 적용 됩니다는 **에 적용 됩니다.** 목록 항목의 시작 부분에 있습니다.  

## <a name="syntax"></a>구문  
```  
ktpass  
[/out <FileName>]   
[/princ <PrincipalName>]   
[/mapuser <UserAccount>]   
[/mapop {add|set}] [{-|+}desonly] [/in <FileName>]  
[/pass {Password|*|{-|+}rndpass}]  
[/minpass]  
[/maxpass]  
[/crypto {DES-CBC-CRC|DES-CBC-MD5|RC4-HMAC-NT|AES256-SHA1|AES128-SHA1|All}]  
[/itercount]  
[/ptype {KRB5_NT_PRINCIPAL|KRB5_NT_SRV_INST|KRB5_NT_SRV_HST}]  
[/kvno <KeyversionNum>]  
[/answer {-|+}]  
[/target]  
[/rawsalt] [{-|+}dumpsalt] [{-|+}setupn] [{-|+}setpass <Password>]  [/?|/h|/help]  
```  
## <a name="parameters"></a>매개 변수  

|                                             매개 변수                                              |                                                                                                                                                                                                                                                                                                      설명                                                                                                                                                                                                                                                                                                       |
|----------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                          /out <FileName>                                           |                                                                                                                                                                        생성할 Kerberos 버전 5.keytab 파일의 이름을 지정 합니다. **참고:** 기존.keytab 파일로/etc/krb5.keytab Windows 운영 체제를 실행 하지 않는 컴퓨터에 전송 하 고 다음 대체 하거나 병합.keytab 파일입니다.                                                                                                                                                                        |
|                                       /princ <PrincipalName>                                       |                                                                                                                                                                                                                   보안 주체 이름 형식 지정 host/computer.contoso.com@CONTOSO.COM합니다. **경고:** 이 매개 변수는 대/소문자 구분 합니다. 참조 [주의](#BKMK_remarks) 자세한 내용은 합니다.                                                                                                                                                                                                                    |
|                                       /mapuser <UserAccount>                                       |                                                                                                                                                                                                                                                지정 된 Kerberos 사용자 이름을 매핑하는 **princ** 매개 변수를 지정 된 도메인 계정.                                                                                                                                                                                                                                                |
|                                       /mapop {추가&#124;설정}                                        |                                                                                                                                                                             매핑 특성을 설정 하는 방법을 지정 합니다.<br /><br />-   **추가** 지정 된 로컬 사용자 이름의 값을 추가 합니다. 기본값입니다.<br />-   **설정** 설정 값에 대 한 표준 DES (데이터 암호화)-지정 된 로컬 사용자 이름에 대 한 암호화만 합니다.                                                                                                                                                                             |
|                                         {-&#124; +} desonly                                          |                                                                                                                                                            DES 전용 암호화는 기본적으로 설정 됩니다.<br /><br />-    **+** DES 전용 암호화에 대 한 계정을 설정합니다.<br />-    **-** DES 전용 암호화에 대 한 계정에 대 한 제한을 해제합니다. **중요:** Windows 7 및 Windows Server 2008 R2 부터는 Windows에서는 DES 기본적으로 지원 하지.                                                                                                                                                            |
|                                           /in <FileName>                                           |                                                                                                                                                                                                                                                       Windows 운영 체제를 실행 하지 않는 호스트 컴퓨터에서 읽을.keytab 파일을 지정 합니다.                                                                                                                                                                                                                                                        |
|                          /pass {Password&#124;\*&#124;{-&#124;+}rndpass}                           |                                                                                                                                                                                                                                           로 지정 된 주 사용자 이름에 대 한 암호를 지정 된 **princ** 매개 변수입니다. 사용 하 여 "\*" 암호를 입력 합니다.                                                                                                                                                                                                                                            |
|                                              /minpass                                              |                                                                                                                                                                                                                                                                            15 자로 임의의 암호의 최소 길이 설정합니다.                                                                                                                                                                                                                                                                            |
|                                              /maxpass                                              |                                                                                                                                                                                                                                                                           임의의 암호의 최대 길이 256 자로 설정합니다.                                                                                                                                                                                                                                                                            |
| 암호화 / {DES-CBC-CRC &#124; DES-CBC-m d 5 &#124; RC4-HMAC-NT &#124; AES256 SHA1 &#124; AES128 SHA1 &#124; 모든} | 키 파일에서 생성 되는 키를 지정 합니다.<br /><br />-   **DES-CBC-CRC** 호환성을 위해 사용 됩니다.<br />-   **DES-CBC-MD5** MIT 구현과 더욱 긴밀 하 게 준수 하 고 호환성을 위해 사용 됩니다.<br />-   **RC4-HMAC-NT** 128 비트 암호화를 사용 합니다.<br />-   **AES256 SHA1** AES256-CTS-HMAC-h a 1-96 암호화를 사용 합니다.<br />-   **AES128 SHA1** AES128 CTS-HMAC-h a 1-96 암호화를 사용 합니다.<br />-   **모든** 상태는 지원 되는 모든 암호화 종류를 사용할 수 있습니다. **참고:** 기본 설정은 이전 MIT 버전을 기반으로 합니다. 따라서 `/crypto` 항상 지정 해야 합니다. |
|                                             /itercount                                             |                                                                                                                                                                                                                        AES 암호화에 사용 되는 반복 횟수를 지정 합니다. 기본값은 **itercount** -AES 암호화에 대 한 무시 되 고 AES 암호화를 위해 4, 096에서 설정 됩니다.                                                                                                                                                                                                                         |
|               /ptype {KRB5_NT_PRINCIPAL &#124; KRB5_NT_SRV_INST &#124; KRB5_NT_SRV_HST}                |                                                                                                                                                                                         보안 주체 유형을 지정합니다.<br /><br />-   **KRB5_NT_PRINCIPAL** 는 일반적인 보안 주체 유형 (권장).<br />-   **KRB5_NT_SRV_INST** 사용자 서비스 인스턴스입니다.<br />-   **KRB5_NT_SRV_HST** 호스트 서비스 인스턴스입니다.                                                                                                                                                                                         |
|                                       /kvno <KeyversionNum>                                        |                                                                                                                                                                                                                                                                               키 버전 번호를 지정합니다. 기본값은 1입니다.                                                                                                                                                                                                                                                                                |
|                                         대답 / {-&#124; +}                                         |                                                                                                                                                                                                                    배경 응답 모드를 설정합니다.<br /><br />**-** 대답에는 아니요. 자동으로 암호 프롬프트가 다시 설정<br /><br />**+** 답변 예에 자동으로 암호 프롬프트가 다시 설정합니다.                                                                                                                                                                                                                     |
|                                              /target                                               |                                                                                                                                                                                           도메인 컨트롤러를 사용 하도록 설정 합니다. 기본값은 검색, 보안 주체 이름을 기반으로 하는 도메인 컨트롤러입니다. 도메인 컨트롤러 이름을 해결 되지 않으면 유효한 도메인 컨트롤러에 대 한 대화 상자를 묻습니다.                                                                                                                                                                                           |
|                                              /rawsalt                                              |                                                                                                                                                                                                                                                           키를 생성할 때 rawsalt 알고리즘을 사용 하 여 ktpass가 되도록 합니다. 이 매개 변수가 필요 하지 않습니다.                                                                                                                                                                                                                                                            |
|                                         {-&#124; +} dumpsalt                                         |                                                                                                                                                                                                                                                           이 매개 변수는 출력 키를 생성 하는 데 사용 되는 MIT salt 알고리즘을 보여 줍니다.                                                                                                                                                                                                                                                            |
|                                          {-&#124; +} setupn                                          |                                                                                                                                                                                                                                          서비스 사용자 이름 (SPN) 외에도 사용자 보안 주체 이름 (UPN)을 설정합니다. 기본값은.keytab 파일에서 모두 설정 하는 것입니다.                                                                                                                                                                                                                                           |
|                                    {0}-&#124;+} setpass <Password>                                    |                                                                                                                                                                                                                                                          제공 되는 경우 사용자의 암호를 설정 합니다. Rndpass 사용 되는 경우에 임의의 암호를 대신 생성 됩니다.                                                                                                                                                                                                                                                           |
|                                       /? &#124;/h&#124;/h                                        |                                                                                                                                                                                                                                                                                         Ktpass에 대 한 도움말을 명령줄 표시 합니다.                                                                                                                                                                                                                                                                                         |

## <a name="BKMK_remarks"></a>remarks  
Active directory Domain Services에서 서비스 인스턴스 계정으로 Windows 운영 체제를 실행 하지 않는 시스템에서 실행 되는 서비스를 구성할 수 있습니다. 따라서 모든 Kerberos 클라이언트 Windows Kdc를 사용 하 여 Windows 운영 체제를 실행 하지 않는 서비스에 인증할 수 있습니다.  
/Princ 매개 변수는 ktpass에서 평가 되지 않습니다 하 고 제공 된 대로 사용 됩니다. 점검이 없음을 매개 변수가의 정확한 대/소문자와 일치 하는 경우에 **userPrincipalName** 키 파일을 생성할 때 특성 값입니다. 이 키 파일을 사용 하 여 대/소문자 구분 Kerberos 분포 때 정확한 사례 일치 하는 데 문제가 있을 수 및 사전 인증 하는 동안 실패할 수 있습니다. 확인 하 고 올바른 검색 **userPrincipalName** LDifDE 내보내기 파일에서 특성 값입니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
```  
ldifde /f keytab_user.ldf /d "CN=Keytab User,OU=UserAccounts,DC=contoso,DC=corp,DC=microsoft,DC=com" /p base /l samaccountname,userprincipalname  
```  
## <a name="BKMK_examples"></a>예제  
다음 예제에서는 Sample1 사용자에 대 한 현재 디렉터리에 machine.keytab, Kerberos.keytab 파일을 만드는 방법을 보여 줍니다. (Windows 운영 체제를 실행 하지 않는 호스트 컴퓨터에서 Krb5.keytab 파일과이 파일을 병합 됩니다.) 일반 보안 주체 유형에 대 한 모든 지원 되는 암호화 유형에 대 한 Kerberos.keytab 파일이 생성 됩니다.  
Windows 운영 체제를 실행 하지 않는 호스트 컴퓨터에 대 한.keytab 파일을 생성 하려면 다음 단계를 사용 하 여 주 서버는 계정에 매핑되고 호스트 사용자 암호를 설정 하려면:  
1.  Active directory 사용자 및 컴퓨터 스냅인에서 Windows 운영 체제를 실행 하지 않는 컴퓨터를 서비스에 대 한 사용자 계정을 만들려면 사용 합니다. 예를 들어 Sample1 이름으로 계정을 만듭니다.  
2.  Ktpass를 사용 하 여 명령 프롬프트에서 다음을 입력 하 여 사용자 계정에 대 한 id 매핑을 설정 하려면:  
    ```  
    ktpass /princ host/Sample1.contoso.com@CONTOSO.COM /mapuser Sample1 /pass MyPas$w0rd /out Sample1.keytab /crypto all /ptype KRB5_NT_PRINCIPAL /mapop set   
    ```  

    > [!NOTE]  
    > 동일한 사용자 계정에 여러 서비스 인스턴스를 매핑할 수 없습니다.  

3.  Windows 운영 체제를 실행 하지 않는 호스트 컴퓨터에서 /Etc/Krb5.keytab 파일과.keytab 파일을 병합 합니다. 

#### <a name="additional-references"></a>추가 참조  
[명령줄 구문 키](command-line-syntax-key.md)  
