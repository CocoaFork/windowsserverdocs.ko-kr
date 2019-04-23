---
title: AD FS 문제 해결-Idp 시작 로그온
description: 이 문서에는 AD FS 로그인 페이지에서 문제를 해결 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 61e9adc708e95a6ab4a82550280737b2f4bad0a1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844944"
---
# <a name="ad-fs-troubleshooting---idp-initiated-sign-on"></a>AD FS 문제 해결-Idp 시작 로그온
인증이 작동 하는지 여부를 테스트 하려면 AD FS 로그인 페이지를 사용할 수 있습니다.  페이지로 이동 하 고 로그인 하면 됩니다.  또한 모든 SAML 2.0 신뢰 당사자 나열 되어 있는지 확인 하려면 로그인 페이지를 사용할 수 있습니다.

## <a name="enable-the-idp-intiated-sign-on-page"></a>Idp를 시작한 사람에 대 한 로그온 페이지를 사용 하도록 설정
기본적으로 Windows 2016에서 AD FS 되지 않은 기호를 사용 하도록 설정 하는 페이지입니다.  사용 하도록 설정 하려면 Set-adfsproperties PowerShell 명령을 사용할 수 있습니다.  페이지를 사용 하도록 설정 하려면 다음 절차를 따르십시오.

1.  열린 Windows PowerShell
2.  입력: `Get-AdfsProperties` 하 고 enter 키를 누릅니다
3.  확인 **EnableIdpInitiatedSignonPage** false로 설정 된 ![False](media/ad-fs-tshoot-initiatedsignon/idp2.png)
4.  PowerShell에서 다음을 입력 합니다.  `Set-AdfsProperties -EnableIdpInitiatedSignonPage $true`
5.  확인 하므로 Get-adfsproperties를 다시 입력 하 고 확인 표시 되지 것입니다 **EnableIdpInitatedSignonPage** 설정을 true로 합니다.
![True](media/ad-fs-tshoot-initiatedsignon/idp4.png)

## <a name="test-authentication"></a>인증 테스트
Idp-Initiated 로그온 페이지를 사용 하 여 AD FS 인증을 테스트 하려면 다음 절차를 따르십시오.

1.  웹 브라우저를 열고 Idp에 대 한 로그온 페이지로 이동 합니다.  예:  https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
2.  에 로그인 하 라는 메시지가 표시 됩니다.  자격 증명을 입력 합니다.
![Sign-on](media/ad-fs-tshoot-initiatedsignon/idp5.png)
3.  이 성공한 경우에 로그인 해야 합니다.


## <a name="test-authentication-using-a-seamless-logon-experience"></a>원활 하 게 로그온 환경을 사용 하 여 인증 테스트
AD FS 서버에 대 한 URL 인터넷 옵션의 로컬 인트라넷 영역에 추가 되어 있는지 확인 하 여 원활 하 게 로그온 환경을 테스트할 수 있습니다.  다음 절차를 따르십시오.

1.  Windows 10 클라이언트에서 시작을 클릭 하 고 인터넷 옵션 입력 인터넷 옵션을 선택 합니다.
2.   보안 탭을 클릭, 로컬 인트라넷에서 클릭 하 고 사이트 단추를 클릭 합니다.
![원활 하 게](media/ad-fs-tshoot-initiatedsignon/idp8.png)
1.  고급을 클릭합니다.
2.  Url을 입력 하 고 추가 클릭 합니다.  닫기를 클릭 합니다.
![Url 추가](media/ad-fs-tshoot-initiatedsignon/idp9.png)
1.  확인을 클릭 합니다.  확인을 클릭 합니다.  이 인터넷 옵션 닫아야 합니다.
2.  웹 브라우저를 열고 Idp에 대 한 로그온 페이지로 이동 합니다.  예:  https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
3.  로그인 단추를 클릭 합니다.  자동으로 로그인 해야 하 고 자격 증명을 묻는 메시지가 나타나지 않습니다.
![원활 하 게](media/ad-fs-tshoot-initiatedsignon/idp6.png)

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)