---
title: 보호된 사용자 보안 그룹
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b0b5180-f65a-43ac-8ef3-66014116f296
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: bd6b53c0febdfb2d344136097a9654c981405568
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862364"
---
# <a name="protected-users-security-group"></a>보호된 사용자 보안 그룹

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IT 전문가를 위한 이 항목에서는 Active Directory 보안 그룹인 보호된 사용자에 대해 알아보고 작동 방식을 설명합니다. 이 그룹은 Windows Server 2012 R2 도메인 컨트롤러에서 도입 되었습니다.

## <a name="BKMK_ProtectedUsers"></a>개요

이 보안 그룹은 엔터프라이즈 내에서 자격 증명 노출 관리 전략의 일환으로 설계 되었습니다. 이 그룹의 구성원 계정에는 구성할 수 없는 보호가 자동으로 적용됩니다. 보호된 그룹의 구성원은 기본적으로 사전에 엄격하게 보호됩니다. 계정에 대한 이러한 보호를 수정하려면 보안 그룹에서 해당 계정을 제거하는 방법밖에 없습니다.

> [!WARNING]
> 서비스 및 컴퓨터 계정은 보호 된 사용자 그룹의 멤버를 되어서는 안 됩니다. 이 그룹 암호 또는 인증서는 항상 호스트에서 사용할 수 있으므로 그래도 불완전 한 보호를 제공 됩니다. 오류가 발생 하 여 인증 하지 못합니다 \"사용자 이름 또는 암호가 올바르지 않습니다.\" 서비스 또는 보호 된 사용자 그룹에 추가 되는 컴퓨터에 대 한 합니다.

이 도메인 관련 글로벌 그룹은 Windows Server 2012 R2를 실행 하는 주 도메인 컨트롤러를 사용 하 여 장치 및 Windows Server 2012 R2 및 Windows 8.1 실행 하는 호스트 컴퓨터 또는 도메인의 사용자를 위해 나중에 구성할 수 없는 보호를 트리거합니다. 이 경우 사용자가 로그인 이러한 보호 기능을 사용 하 여 컴퓨터에 자격 증명의 기본 메모리 사용 공간이 크게 절감 됩니다.

자세한 내용은 [어떻게 보호 된 사용자 그룹 작동](#BKMK_HowItWorks) 이 항목의 합니다.



## <a name="BKMK_Requirements"></a>보호 된 사용자 그룹 요구 사항
다음과 같은 보호 된 사용자 그룹의 멤버에 대 한 장치 보호 기능을 제공 하기 위한 요구 사항

- 보호된 사용자 글로벌 보안 그룹이 계정 도메인의 모든 도메인 컨트롤러에 복제되어야 합니다.

- Windows 8.1 및 Windows Server 2012 R2에는 기본적으로 지원 추가. [Microsoft 보안 공지 2871997](https://technet.microsoft.com/library/security/2871997) Windows 7, Windows Server 2008 R2 및 Windows Server 2012에 지원을 추가 합니다.

보호된 사용자 그룹의 구성원에게 도메인 컨트롤러 보호를 제공하기 위한 요구 사항은 다음과 같습니다.

- Windows Server 2012 R2 또는 더 높은 도메인 기능 수준에 있는 도메인 사용자 여야 합니다.

### <a name="adding-protected-user-global-security-group-to-down-level-domains"></a>하위 수준 도메인을 보호 된 사용자 글로벌 보안 그룹 추가

Windows Server 2012 R2 이전의 운영 체제를 실행 하는 도메인 컨트롤러는 새 보호 된 사용자 보안 그룹에 추가 멤버를 지원할 수 있습니다. 이 도메인을 업그레이드 하기 전에 장치 보호 기능을 활용할 수 있습니다. 

> [!Note]
> 도메인 컨트롤러는 도메인 보호를 지원 하지 않습니다. 

보호 된 사용자 그룹을 만들 수 있습니다 [주 도메인 컨트롤러 (PDC) 에뮬레이터 역할을 전송](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx) Windows Server 2012 R2를 실행 하는 도메인 컨트롤러에 있습니다. 해당 그룹 개체를 다른 도메인 컨트롤러에 복제한 후 이전 버전의 Windows Server를 실행하는 도메인 컨트롤러에서 PDC 에뮬레이터 역할을 호스트할 수 있습니다.

### <a name="BKMK_ADgroup"></a>보호 된 사용자가 AD 그룹 속성

다음 표에는 보호된 사용자 그룹의 속성이 나와 있습니다.

|attribute|값|
|-------|-----|
|잘 알려진 SID/RID|S-1-5-21-<domain>-525|
|형식|도메인 전역|
|기본 컨테이너|CN=Users, DC=<domain>, DC=|
|기본 멤버|없음|
|기본 소속|없음|
|ADMINSDHOLDER에 의해 보호됨?|아니오|
|기본 컨테이너에서 안전하게 이동?|예|
|이 그룹의 관리를 서비스 관리자가 아닌 관리자에게 안전하게 위임?|아니요|
|기본 사용자 권한|기본 사용자 권한 없음|

## <a name="BKMK_HowItWorks"></a>보호 된 사용자 그룹의 작동 방식
이 섹션에서는 다음과 같은 경우 보호된 사용자 그룹의 작동 방식에 대해 설명합니다.

-   Windows 장치에 로그인

-   Windows Server 2012 R2 또는 더 높은 도메인 기능 수준에는 사용자 계정 도메인

### <a name="device-protections-for-signed-in-protected-users"></a>장치 보호에 대 한 보호 된 사용자 로그인
로그인된 한 사용자가 보호 된 사용자 그룹의 멤버인 경우에 다음 보호가 적용 됩니다.

-   캐시가 아닌 경우에 사용자의 일반 텍스트 자격 증명 위임 (CredSSP)는 자격 증명을 **기본 자격 증명 위임 허용** 그룹 정책 설정을 사용 합니다.

-   Windows 8.1 및 Windows Server 2012 R2 부터는 Windows 다이제스트 캐시 하지 않습니다 사용자의 일반 텍스트 자격 증명 Windows 다이제스트를 사용 하는 경우에 합니다.

> [!Note]
> 설치한 후 [Microsoft 보안 공지 2871997](https://technet.microsoft.com/library/security/2871997) Windows 다이제스트 자격 증명을 캐시 레지스트리 키를 구성할 때까지 계속 됩니다. 참조 [Microsoft 보안 권고: 자격 증명 보호 및 관리를 개선 하기 위해 업데이트: 2014 년 5 월 13 일](https://support.microsoft.com/en-us/help/2871997/microsoft-security-advisory-update-to-improve-credentials-protection-a) 지침에 대 한 합니다.

-   NTLM은 사용자의 일반 텍스트 자격 증명 또는 NT 단방향 함수의 (NTOWF)를 캐시 하지 않습니다.

-   더 이상 Kerberos DES 또는 RC4 키를 만듭니다. 또한이 캐시 하지 않습니다 사용자의 일반 텍스트 자격 증명 또는 장기 키 후 초기 TGT를 가져옵니다.

-   캐시 된 검증 도구를 로그인 시 만들어지지 않습니다 또는 잠금 해제, 오프 라인 로그인 더 이상이 지원 됩니다.

사용자 계정 보호 된 사용자 그룹에 추가 된 후 보호는 사용자가 장치에 로그인 할 때 시작 됩니다.

### <a name="domain-controller-protections-for-protected-users"></a>보호 된 사용자에 대 한 도메인 컨트롤러 보호
Windows Server 2012 R2 도메인에 인증 하는 보호 된 사용자 그룹의 구성원 인 계정 수 없는 합니다.

-   NTLM 인증을 통한 인증

-   Kerberos 사전 인증에서 DES 또는 RC4 암호화 종류 사용

-   제한 없는 위임 또는 제한된 위임을 사용한 위임

-   초기 4시간의 수명이 지난 후 Kerberos 갱신

보호된 사용자 그룹의 모든 계정에 구성할 수 없는 TGT 만료 설정이 지정됩니다. 일반적으로 도메인 컨트롤러는 **사용자 티켓 최대 수명** 및 **사용자 티켓 갱신 최대 수명** 도메인 정책에 따라 TGT 수명 및 갱신을 설정합니다. 보호된 사용자 그룹의 경우 이러한 도메인 정책에 대해 600분이 설정됩니다.

자세한 내용은 [보호된 계정을 구성하는 방법](how-to-configure-protected-accounts.md)을 참조하세요.

## <a name="troubleshooting"></a>문제 해결
보호된 사용자와 관련된 이벤트 문제를 해결하는 데 도움이 되는 두 가지 작업 관리 로그가 있습니다. 이러한 새 로그는 이벤트 뷰어에서 볼 수 있으며, 기본적으로 사용하지 않도록 설정되고 **Applications and Services Logs\Microsoft\Windows\Microsoft\Authentication**에 저장됩니다.

|이벤트 ID 및 로그|설명|
|----------|--------|
|104<br /><br />**ProtectedUser-Client**|이유: 클라이언트의 보안 패키지에 자격 증명이 없습니다.<br /><br />이 오류는 계정이 보호된 사용자 보안 그룹의 구성원인 경우 클라이언트 컴퓨터에 기록됩니다. 이 이벤트는 보안 패키지가 서버의 인증을 받는 데 필요한 자격 증명을 캐시하지 않음을 나타냅니다.<br /><br />패키지 이름, 사용자 이름, 도메인 이름 및 서버 이름을 표시합니다.|
|304<br /><br />**ProtectedUser-Client**|이유: 보안 패키지가 보호 된 사용자의 자격 증명을 저장 하지 않습니다.<br /><br />정보 이벤트는 보안 패키지가 사용자의 로그인 자격 증명을 캐시 하지 않습니다 나타내기 위해 클라이언트에 기록 됩니다. 다이제스트(WDigest), 자격 증명 위임(CredSSP) 및 NTLM은 보호된 사용자에 대한 로그온 자격 증명을 유지하지 못합니다. 자격 증명을 묻는 메시지가 나타나는 경우에도 응용 프로그램을 실행할 수 있습니다.<br /><br />패키지 이름, 사용자 이름 및 도메인 이름을 표시합니다.|
|100<br /><br />**ProtectedUserFailures-DomainController**|이유: 보호된 사용자 보안 그룹에 속한 계정에서 NTLM 로그인 실패가 발생합니다.<br /><br />계정이 보호된 사용자 보안 그룹의 구성원이기 때문에 NTLM 인증에 실패했음을 나타내는 오류가 도메인 컨트롤러에 기록됩니다.<br /><br />계정 이름 및 장치 이름을 표시합니다.|
|104<br /><br />**ProtectedUserFailures-DomainController**|이유: DES 또는 RC4 암호화 종류는 Kerberos 인증에 사용되므로 보호된 사용자 보안 그룹의 사용자에 대해서는 로그인 실패가 발생합니다.<br /><br />계정이 보호된 사용자 보안 그룹의 구성원인 경우에는 DES 또는 RC4 암호화 종류를 사용할 수 없으므로 Kerberos 사전 인증에 실패했습니다.<br /><br />(AES는 허용됩니다.)|
|303<br /><br />**ProtectedUserSuccesses-DomainController**|이유: 보호된 사용자 그룹의 구성원에게 Kerberos TGT(허용 티켓)가 성공적으로 발급되었습니다.|



## <a name="additional-resources"></a>추가 자료

-   [자격 증명 보호 및 관리](credentials-protection-and-management.md)

-   [인증 정책 및 인증 정책 사일로](authentication-policies-and-authentication-policy-silos.md)

-   [보호 된 계정을 구성 하는 방법](how-to-configure-protected-accounts.md)

