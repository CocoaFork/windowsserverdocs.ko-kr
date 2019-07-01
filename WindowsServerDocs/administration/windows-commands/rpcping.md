---
title: rpcping
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7382aa0d-90fc-47c0-84b3-15f52dd656d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a32f9c16c8c077942459599f2099a2d7e85a1397
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441697"
---
# <a name="rpcping"></a>rpcping

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Microsoft Exchange Server 및 지원 되는 Microsoft Exchange 클라이언트 워크스테이션의 네트워크에서 실행 중인 컴퓨터 간의 RPC 연결을 확인 합니다. 네트워크를 통해 클라이언트 워크스테이션에서 Microsoft Exchange Server 서비스 RPC 요청에 응답 하는지 확인 하려면이 유틸리티를 사용할 수 있습니다. 

## <a name="syntax"></a>구문
```
rpcping [/t <protseq>] [/s <server_addr>] [/e <endpoint>
        |/f <interface UUID>[,Majorver]] [/O <Interface Object UUID]
        [/i <#_iterations>] [/u <security_package_id>] [/a <authn_level>]
        [/N <server_princ_name>] [/I <auth_identity>] [/C <capabilities>]
        [/T <identity_tracking>] [/M <impersonation_type>]
        [/S <server_sid>] [/P <proxy_auth_identity>] [/F <RPCHTTP_flags>]
        [/H <RPC/HTTP_authn_schemes>] [/o <binding_options>]
        [/B <server_certificate_subject>] [/b] [/E] [/q] [/c]
        [/A <http_proxy_auth_identity>] [/U <HTTP_proxy_authn_schemes>]
        [/r <report_results_interval>] [/v <verbose_level>] [/d]
```

### <a name="parameters"></a>매개 변수

|            매개 변수             |                                                                                                                                                                                                                                                                                                                                               설명                                                                                                                                                                                                                                                                                                                                               |
|----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          /t \<protseq>           |                                                                                                                                                                                                                                                  프로토콜 시퀀스를 사용 하 여 지정 합니다. 예를 들어 표준 RPC 프로토콜 시퀀스 중 하나일 수 있습니다: ncacn_ip_tcp, ncacn_np 또는 ncacn_http 합니다.<br /><br />지정 하지 않으면 기본값은 ncacn_ip_tcp입니다.                                                                                                                                                                                                                                                   |
|        /s \<server_addr>         |                                                                                                                                                                                                                                                                                                            서버 주소를 지정 합니다. 지정 하지 않으면 로컬 컴퓨터를 ping 할 됩니다.                                                                                                                                                                                                                                                                                                            |
|          /e \<endpoint>          |                                                                                                                                                                                                                                                    Ping에 끝점을 지정 합니다. 지정 되지 않은 경우 대상 컴퓨터에 끝점 매퍼 ping 수행할 수 있습니다.<br /><br />이 옵션은 인터페이스와 함께 사용할 수 없습니다 ( **/f**) 옵션입니다.                                                                                                                                                                                                                                                     |
|      /o \<binding_options>       |                                                                                                                                                                                                                                                                                                                             RPC ping에 대 한 바인딩 옵션을 지정합니다.                                                                                                                                                                                                                                                                                                                             |
| /f \<interface UUID>[,Majorver]  |                                                                                                            Ping 하는 인터페이스를 지정 합니다. 이 옵션은 끝점 옵션을 함께 사용할 수 없습니다. 인터페이스는 UUID로 지정 됩니다.<br /><br />경우는 *Majorver* 지정 하지 않으면 인터페이스의 버전 1을 검색 합니다.<br /><br />인터페이스를 지정 하는 경우 **rpcping** 지정된 된 인터페이스에 대 한 끝점을 검색 하는 대상 컴퓨터에 끝점 매퍼를 쿼리 합니다. 명령줄에 지정 된 옵션을 사용 하 여 끝점 매퍼를 쿼리할 수 됩니다.                                                                                                             |
|        /O \<UUID 개체 >         |                                                                                                                                                                                                                                                                                                                       인터페이스를 등록 한 경우에 UUID 개체를 지정 합니다.                                                                                                                                                                                                                                                                                                                        |
|        /i \<#_iterations>        |                                                                                                                                                                                                                                                                          확인에 대 한 호출 수를 지정 합니다. 기본값은 1입니다. 이 옵션은 여러 차례 반복을 지정 하는 연결 대기 시간을 측정 하는 데 유용 합니다.                                                                                                                                                                                                                                                                          |
|    /u \<security_package_id>     | (보안 공급자) 보안 패키지 지정 RPC 호출에 사용 합니다. 보안 패키지는 숫자 또는 이름으로 식별 됩니다. 번호를 사용 하는 경우 RpcBindingSetAuthInfoEx API와 같이 동일한 수입니다. 아래 목록 이름 및 번호를 보여 줍니다. 이름은 대 소문자를 구분 하지 않습니다.<br /><br />협상 / 9 또는 하나의 협상, snego의 또는 협상<br />-NTLM / 10 또는 NTLM<br />-SChannel 14 / 또는 SChannel<br />Kerberos / 16 또는 Kerberos<br />커널 / 20 또는 커널<br />    이 옵션을 지정 하는 경우 "없음" 이외의 인증 수준을 지정 해야 합니다. 이 옵션에 대 한 기본값이 없습니다. 지정 되지 않은 경우에 RPC는 ping에 대 한 보안을 사용 하지 않습니다. |
|        /a \<authn_level>         |                                                                                                                                                               사용할 인증 수준을 지정 합니다. 가능한 값은<br /><br />-연결<br />-호출<br />-pkt<br />-무결성<br />-개인 정보 보호<br /><br />이 옵션을 지정 하는 경우 보안 패키지 ID (/ u)도 지정 해야 합니다. 이 옵션에 대 한 기본값이 없습니다.<br /><br />이 옵션을 지정 하지 않으면 하는 경우에 RPC는 ping에 대 한 보안을 사용 하지 않습니다.                                                                                                                                                               |
|     /N \<server_princ_name>      |                                                                                                                                                                                                                                                                                 서버 보안 주체 이름을 지정합니다.<br /><br />이 필드는만 사용할 수 있습니다 인증 수준 및 보안 패키지를 선택 하는 경우.                                                                                                                                                                                                                                                                                  |
|       /I \<auth_identity>        |                                                         서버에 연결 하는 대체 id를 지정할 수 있습니다. 양식 사용자, 도메인, 암호의 id가입니다. 사용자 이름, 도메인 또는 암호 셸에서 해석 될 수 있는 특수 문자가 있으면 id를 큰따옴표로 묶습니다. 지정할 수 있습니다 **\\** \* 암호 및 RPC 대신 묻는을 화면에 출력 하지 않고 암호를 입력 합니다. 이 필드를 지정 하지 않으면 로그온된 한 사용자의 id는 사용 됩니다.<br /><br />이 필드는만 사용할 수 있습니다 인증 수준 및 보안 패키지를 선택 하는 경우.                                                         |
|        /C \<기능 >        |                                                                                                                                                                                                                                                                                   플래그의 비트 16 진수 마스크를 지정합니다. 이 필드는만 사용할 수 있습니다 인증 수준 및 보안 패키지를 선택 하는 경우.                                                                                                                                                                                                                                                                                    |
|     /T \<identity_tracking>      |                                                                                                                                                                                                                                                               정적 또는 동적를 지정합니다. 그렇지 않은 경우 지정 된, 동적 값이 기본값입니다.<br /><br />이 필드는만 사용할 수 있습니다 인증 수준 및 보안 패키지를 선택 하는 경우.                                                                                                                                                                                                                                                                |
|     /M \<impersonation_type>     |                                                                                                                                                                                                                                                           익명으로 지정 식별, 가장 또는 위임 합니다. 기본 가장 됩니다.<br /><br />이 필드는만 사용할 수 있습니다 인증 수준 및 보안 패키지를 선택 하는 경우.                                                                                                                                                                                                                                                           |
|         /S \<server_sid>         |                                                                                                                                                                                                                                                                              서버의 예상된 SID를 지정합니다.<br /><br />이 필드는만 사용할 수 있습니다 인증 수준 및 보안 패키지를 선택 하는 경우.                                                                                                                                                                                                                                                                              |
|    /P \<proxy_auth_identity>     |                                                                                                                                                                                                                              RPC/HTTP 프록시에 인증 하는 데 id를 지정 합니다. /I 옵션의 경우와 형식이 동일 합니다. 보안 패키지를 지정 해야 합니다 (/ u), 인증 수준 (/ a), 및 인증 체계 (/ H) 하려면이 옵션을 사용 합니다.                                                                                                                                                                                                                               |
|       /F \<RPCHTTP_flags>        |                                                                                                                                                                RPC/HTTP 프런트 엔드 인증을 위해 전달할 플래그를 지정 합니다. 숫자 또는 현재 인식 된 플래그는 이름으로 플래그를 지정할 수 있습니다.<br /><br />--SSL을 사용 하는 중 1 / ssl 또는 use_ssl 또는<br />첫 번째 인증 체계를 사용할 수 있는 / 2 또는 첫 번째 또는 use_first<br /><br />보안 패키지를 지정 해야 합니다 (/ u) 및 인증 수준 (/) 하려면이 옵션을 사용 합니다.                                                                                                                                                                 |
|   /H \<RPC/HTTP_authn_schemes>   |                                                                                                                           RPC/HTTP 프런트 엔드 인증에 사용할 인증 체계를 지정 합니다. 이 옵션은 숫자 값 또는 쉼표로 구분 된 이름 목록입니다. 예: 기본, NTLM입니다. 인식 되는 값은 (이름은 대 소문자를 구분 하지 않습니다.):<br /><br />-기본적인 / 1 또는 기본<br />-NTLM / 2 또는 NTLM<br />-인증서 65536 / 인증서 또는<br /><br />보안 패키지를 지정 해야 합니다 (/ u) 및 인증 수준 (/) 하려면이 옵션을 사용 합니다.                                                                                                                            |
| /B \<server_certificate_subject> |                                                                                                                                                                                                                                                    서버 인증서 주체를 지정합니다. 이 옵션에 대 한 SSL을 사용 해야 작동 합니다.<br /><br />보안 패키지를 지정 해야 합니다 (/ u) 및 인증 수준 (/) 하려면이 옵션을 사용 합니다.                                                                                                                                                                                                                                                     |
|                /b                |                                                                                                                                                                                      서버에서 보낸 인증서에서 서버 인증서 주체를 검색 하 고 화면 또는 로그 파일에 출력 합니다. 프록시 에코만 옵션 하는 경우에 유효 (/ E) 사용 하 여 SSL 옵션을 지정 합니다.<br /><br />보안 패키지를 지정 해야 합니다 (/ u) 및 인증 수준 (/) 하려면이 옵션을 사용 합니다.                                                                                                                                                                                      |
|                /R                |                                                                                                                                                               HTTP 프록시를 지정합니다. 경우 *none*, RPC 프록시를 사용 합니다. 값 *기본* IE 설정을 클라이언트 컴퓨터에서 사용 하 여 것을 의미 합니다. 다른 모든 값은 명시적 HTTP 프록시로 간주 합니다. 이 플래그를 지정 하지 않으면 기본값 가정 면, IE 설정이 확인 됩니다. 이 플래그는 경우에만 유효 합니다 **/E** (에코만 해당) 플래그를 설정 합니다.                                                                                                                                                                |
|                /E                |                                                                                                                                                     RPC/HTTP 프록시를 사용할 경우에에 ping을 제한합니다. Ping 서버에 도달 하지 않습니다. RPC/HTTP 프록시를 연결할 수 있는지 여부를 설정 하려는 경우에 유용 합니다. HTTP 프록시를 지정 하려면 /R 플래그를 사용 합니다. HTTP 프록시 /o 플래그에 지정 된 경우이 옵션이 무시 됩니다.<br /><br />보안 패키지를 지정 해야 합니다 (/ u) 및 인증 수준 (/) 하려면이 옵션을 사용 합니다.                                                                                                                                                      |
|                /q                |                                                                                                                                                                                                                                                                                 자동 모드를 지정합니다. 암호를 제외 하 고 프롬프트 발생 하지 않습니다. 가정 *Y* 모든 쿼리에 응답 합니다. 이 옵션을 사용 하 여 주의 해야 합니다.                                                                                                                                                                                                                                                                                  |
|                /c                |                                                                                                                                                                                                                                                                                                               스마트 카드 인증서를 사용 합니다. rpcping은 스마트 카드를 선택 하는 사용자 라는 메시지가 나타납니다.                                                                                                                                                                                                                                                                                                                |
|                / A                |                                                                                                                                                                                                                        HTTP 프록시에 인증을 사용 하 여 id를 지정 합니다. /I 옵션의 경우와 형식이 동일 합니다.<br /><br />인증 체계를 지정 해야 합니다 (/ U), 보안 패키지 (/ u) 및 인증 수준 (/) 하려면이 옵션을 사용 합니다.                                                                                                                                                                                                                         |
|                /U                |                                                                                                                                                  HTTP 프록시 인증에 사용할 인증 체계를 지정 합니다. 이 옵션은 숫자 값 또는 쉼표로 구분 된 이름 목록입니다. 예: 기본, NTLM입니다. 인식 되는 값은 (이름은 대 소문자를 구분 하지 않습니다.):<br /><br />-기본적인 / 1 또는 기본<br />-NTLM / 2 또는 NTLM<br /><br />보안 패키지를 지정 해야 합니다 (/ u) 및 인증 수준 (/) 하려면이 옵션을 사용 합니다.                                                                                                                                                  |
|                /r                |                                                                                                                                                                                                                                             이 옵션을 해 여러 차례 반복을 지정 하는 경우 **rpcping** 표시 현재 실행 통계 주기적으로 대신 마지막으로 호출한 후입니다. 보고 간격은 초 단위로 제공 됩니다. 기본값은 15입니다.                                                                                                                                                                                                                                              |
|                /v                |                                                                                                                                                                                                                                                                                           지시 **rpcping** 세부 수준을 지정 하 고 출력을 합니다. 기본값은 1입니다. 2와 3 단계에서 더 많은 출력을 제공 합니다. **rpcping**합니다.                                                                                                                                                                                                                                                                                           |
|                /d                |                                                                                                                                                                                                                                                                                                                                   RPC가 실행 한 다음 네트워크 진단 UI입니다.                                                                                                                                                                                                                                                                                                                                   |
|                /p                |                                                                                                                                                                                                                                                                                                                      인증에 실패 하는 경우 자격 증명을 요청 하도록 지정 합니다.                                                                                                                                                                                                                                                                                                                       |
|                /?                |                                                                                                                                                                                                                                                                                                                                  명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                                                                                                                                                                                   |

## <a name="BKMK_Examples"></a>예제
RPC/HTTP를 통해 연결 하는 Exchange 서버는 액세스할 수 있는지를 확인 하려면 다음을 입력 합니다.
```
rpcping /t ncacn_http /s exchange_server /o RpcProxy=front_end_proxy /P "username,domain,*" /H Basic /u NTLM /a connect /F 3
```

## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)