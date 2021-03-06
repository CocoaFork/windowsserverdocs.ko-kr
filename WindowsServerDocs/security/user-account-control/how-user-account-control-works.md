---
title: 사용자 계정 컨트롤 작동 방식
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-tpm
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da83ddb2-6182-417c-aa8e-0b47b2e17d13
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: f12a690c06a37a6e1c01674bcdb96d0a9010a245
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403333"
---
# <a name="how-user-account-control-works"></a>사용자 계정 컨트롤 작동 방식

>적용 대상: Windows Server(반기 채널), Windows Server 2016

UAC(사용자 계정 컨트롤)는 악성 프로그램(맬웨어라고도 함)이 컴퓨터를 손상시키지 않도록 하고 조직이 관리하기 쉬운 데스크톱을 배포할 수 있도록 해 줍니다. UAC를 사용하면 관리자가 특별히 시스템에 대한 관리자 수준 액세스 권한을 부여하지 않은 경우 응용 프로그램과 작업은 항상 관리자가 아닌 계정의 보안 컨텍스트에서 실행됩니다. UAC는 권한 없는 응용 프로그램의 자동 설치를 차단하고 시스템 설정을 실수로 변경하지 않도록 방지할 수 있습니다.

## <a name="uac-process-and-interactions"></a>UAC 프로세스 및 상호 작용
관리자 액세스 토큰이 필요한 각 응용 프로그램은 관리자에게 동의를 요청해야 합니다. 한 가지 예외는 부모 프로세스와 자식 프로세스 사이의 관계입니다. 자식 프로세스는 부모 프로세스에서 사용자 액세스 토큰을 상속합니다. 그러나 부모 프로세스와 자식 프로세스의 무결성 수준은 같아야 합니다. Windows Server 2012는 무결성 수준을 표시 하 여 프로세스를 보호 합니다. 무결성 수준은 신뢰의 측정 결과입니다. 무결성이 "높은" 응용 프로그램은 시스템 데이터를 수정하는 작업을 수행하는 응용 프로그램(예: 디스크 분할 응용 프로그램)이고, 무결성이 "낮은" 응용 프로그램은 운영 체제를 손상시킬 수 있는 작업을 수행하는 응용 프로그램(예: 웹 브라우저)입니다. 무결성 수준이 낮은 응용 프로그램은 무결성 수준이 높은 응용 프로그램의 데이터를 수정할 수 없습니다. 표준 사용자가 관리자 액세스 토큰이 필요한 응용 프로그램을 실행하려고 하면 UAC는 사용자에게 유효한 관리자 자격 증명을 제공하도록 요청합니다.

이 프로세스의 수행 방법을 더 잘 이해 하려면 Windows Server 2012 로그온 프로세스의 세부 정보를 검토 하는 것이 중요 합니다.

### <a name="windows-server-2012-logon-process"></a>Windows Server 2012 Logon Process
다음 그림에서는 관리자의 로그온 프로세스가 표준 사용자의 로그온 프로세스와 어떻게 다른지 보여줍니다.

![관리자의 로그온 프로세스가 표준 사용자에 대 한 로그온 프로세스와 어떻게 다른 지 보여 주는 그림](../media/How-User-Account-Control-Works/UACWindowsLogonProcess.gif)

기본적으로 표준 사용자와 관리자는 표준 사용자의 보안 컨텍스트에서 리소스에 액세스하고 응용 프로그램을 실행합니다. 사용자가 컴퓨터에 로그온하면 해당 사용자의 액세스 토큰이 만들어집니다. 액세스 토큰에는 특정 SID(보안 식별자) 및 Windows 권한을 비롯하여 사용자에게 부여된 액세스 수준에 대한 정보가 포함됩니다.

관리자가 로그온하면 해당 사용자에 대해 표준 사용자 액세스 토큰과 관리자 액세스 토큰이라는 두 개의 개별 액세스 토큰이 만들어집니다. 표준 사용자 액세스 토큰에는 관리자 액세스 토큰과 동일한 사용자별 정보가 있지만 Windows 관리 권한 및 SID는 제거됩니다. 표준 사용자 액세스 토큰은 관리 작업을 수행하지 않는 응용 프로그램(표준 사용자 응용 프로그램)을 시작하는 데 사용됩니다. 그런 다음 표준 사용자 액세스 토큰은 데스크톱(Explorer.exe)을 표시하는 데 사용됩니다. Explorer.exe는 사용자가 시작하는 다른 모든 프로세스가 해당 액세스 토큰을 상속하는 부모 프로세스입니다. 따라서 사용자가 전체 관리 액세스 토큰을 사용하도록 응용 프로그램을 승인하는 동의 또는 자격 증명을 제공하지 않을 경우 모든 응용 프로그램이 표준 사용자로 실행됩니다.

Administrators 그룹의 구성원 인 사용자는 표준 사용자 액세스 토큰을 사용 하 여 로그온 하 고 웹을 찾아보고 전자 메일을 읽을 수 있습니다. 관리자가 관리자 액세스 토큰을 요구 하는 작업을 수행 해야 하는 경우 Windows Server 2012에서 사용자에 게 승인 하 라는 메시지를 자동으로 표시 합니다. 이 프롬프트를 권한 상승 프롬프트라고 하며, 로컬 보안 정책 스냅인(Secpol.msc) 또는 그룹 정책을 사용하여 이러한 프롬프트의 동작을 구성할 수 있습니다.

> [!NOTE]
> "권한 상승" 이라는 용어는 전체 관리자 액세스 토큰을 사용 하기 위해 사용자에 게 동의 또는 자격 증명을 묻는 메시지를 표시 하는 Windows Server 2012의 프로세스를 참조 하는 데 사용 됩니다.

### <a name="the-uac-user-experience"></a>UAC 사용자 환경
UAC를 사용하면 표준 사용자의 사용자 환경이 관리자 승인 모드에 있는 관리자의 사용자 환경과 다릅니다. Windows Server 2012를 가장 안전 하 게 실행 하는 방법은 기본 사용자 계정을 표준 사용자 계정으로 만드는 것입니다. 표준 사용자로 실행하면 관리되는 환경의 보안을 최대화하는 데 도움이 됩니다. 기본 제공 UAC 권한 상승 구성 요소를 사용하면 표준 사용자가 로컬 관리자 계정에 대한 유효한 자격 증명을 입력하여 관리 작업을 손쉽게 수행할 수 있습니다. 표준 사용자에 대한 기본 제공 UAC 권한 상승 구성 요소는 자격 증명 프롬프트입니다.

표준 사용자로 실행하는 또 다른 방법은 관리자 승인 모드에서 관리자로 실행하는 것입니다. 기본 제공 UAC 권한 상승 구성 요소를 사용 하는 경우 로컬 관리자 그룹의 구성원은 승인을 제공 하 여 관리 작업을 쉽게 수행할 수 있습니다. 관리자 승인 모드에 있는 관리자 계정에 대한 기본 제공 UAC 권한 상승 구성 요소를 동의 확인 프롬프트라고 하며, 로컬 보안 정책 스냅인(Secpol.msc) 또는 그룹 정책을 사용하여 이러한 프롬프트의 동작을 구성할 수 있습니다.

**동의 및 자격 증명 프롬프트**

UAC를 사용 하는 경우 Windows Server 2012은 전체 관리자 액세스 토큰이 필요한 프로그램이 나 작업을 시작 하기 전에 유효한 로컬 관리자 계정의 자격 증명을 묻는 메시지를 표시 하거나 동의를 요청 합니다. 이 프롬프트는 악성 프로그램이 자동으로 설치되는 것을 방지합니다.

**동의 확인 프롬프트**

사용자가 사용자의 관리 액세스 토큰이 필요한 작업을 수행하려고 하면 동의 확인 프롬프트가 표시됩니다. 다음은 UAC 동의 확인 프롬프트의 스크린샷입니다.

![UAC 동의 확인 프롬프트의 스크린샷](../media/How-User-Account-Control-Works/UACConsentPrompt.gif)

**자격 증명 프롬프트**

표준 사용자가 사용자의 관리 액세스 토큰이 필요한 작업을 수행하려고 하면 자격 증명 프롬프트가 표시됩니다. 이 표준 사용자 기본 프롬프트 동작은 로컬 보안 정책 스냅인(Secpol.msc) 또는 그룹 정책을 사용하여 구성할 수 있습니다. 관리자는 사용자 계정 컨트롤: 관리자 승인 모드에서 관리자에 대 한 권한 상승 확인 방법 정책 설정 값을 자격 증명 프롬프트로 설정 하 여 자격 증명을 제공 해야 할 수도 있습니다.

다음 스크린샷은 UAC 자격 증명 프롬프트의 예입니다.

![UAC 자격 증명 프롬프트의 예를 보여 주는 스크린샷](../media/How-User-Account-Control-Works/UACCredentialPrompt.gif)

**UAC 권한 상승 프롬프트**

UAC 권한 상승 프롬프트는 응용 프로그램의 잠재적인 보안 위험을 즉시 식별할 수 있도록 응용 프로그램별로 색상으로 구분됩니다. 응용 프로그램이 관리자의 모든 액세스 토큰을 사용 하 여 실행 되려고 하는 경우 Windows Server 2012는 먼저 실행 파일을 분석 하 여 해당 게시자를 확인 합니다. 응용 프로그램은 먼저 실행 파일의 게시자를 기반으로 하 여 Windows Server 2012, 게시자 확인 (서명 됨) 및 게시자 확인 되지 않음 (서명 되지 않음)을 기반으로 하는 세 가지 범주로 구분 됩니다. 다음 다이어그램에서는 Windows Server 2012에서 사용자에 게 제공할 색 상승 프롬프트를 결정 하는 방법을 보여 줍니다.

권한 상승 프롬프트는 색상에 따라 다음과 같이 구분됩니다,

-   빨간색 방패 아이콘과 빨간색 배경: 응용 프로그램이 그룹 정책에 의해 차단되고 차단된 게시자에 의해 게시되었습니다.

-   파랑 및 금색 방패 아이콘을 사용한 파랑 배경: 응용 프로그램은 제어판 항목과 같은 Windows Server 2012 관리 응용 프로그램입니다.

-   파란색 방패 아이콘과 파란색 배경: 응용 프로그램이 Authenticode를 사용하여 서명되었고 로컬 컴퓨터에 의해 신뢰되었습니다.

-   노란색 방패 아이콘과 노란색 배경: 응용 프로그램이 서명되지 않거나 서명되었지만 로컬 컴퓨터에 의해 신뢰되지 않았습니다.

**방패 아이콘**

**날짜 및 시간 속성**과 같은 일부 제어판 항목에는 관리자 작업과 표준 사용자 작업의 조합이 포함되어 있습니다. 표준 사용자는 시계를 보고 표준 시간대를 변경할 수 있지만 로컬 시스템 시간을 변경하려면 전체 관리자 액세스 토큰이 필요합니다. 다음은 **날짜 및 시간 속성** 제어판 항목의 스크린샷입니다.

![\* * 날짜 및 시간 속성 * * 제어판 항목을 보여 주는 스크린샷](../media/How-User-Account-Control-Works/UACShieldIcon.gif)

**날짜 및 시간 변경** 단추의 방패 아이콘은 프로세스가 전체 관리자 액세스 토큰을 필요로 하고 UAC 권한 상승 프롬프트를 표시함을 나타냅니다.

**권한 상승 프롬프트 보안**

권한 상승 프로세스는 프롬프트를 보안된 데스크톱으로 리디렉션하여 추가로 보호할 수 있습니다. 동의 및 자격 증명 프롬프트는 기본적으로 Windows Server 2012에 보안 된 데스크톱에 표시 됩니다. Windows 프로세스만 보안된 데스크톱에 액세스할 수 있습니다. 더 높은 보안 수준을 위해 **사용자 계정 컨트롤: 권한 상승 요청 시 보안 데스크톱으로 전환** 정책 설정을 설정된 상태로 유지하는 것이 좋습니다.

실행 파일이 권한 상승을 요청하면 사용자 데스크톱이라고도 하는 대화형 데스크톱이 보안된 데스크톱으로 전환됩니다. 보안된 데스크톱은 사용자 데스크톱을 희미하게 표시하고 계속하기 전에 응답해야 하는 권한 상승 프롬프트를 표시합니다. 사용자가 예 또는 아니요를 클릭 하면 데스크톱이 사용자 데스크톱으로 다시 전환 됩니다.

맬웨어는 보안 된 데스크톱의 모조을 제공할 수 있지만, 사용자 계정 컨트롤: 관리자 승인 모드에서 관리자에 대 한 권한 상승 확인 방법 정책 설정이 동의 확인으로 설정 되어 있는 경우 사용자가 예를 클릭 하면 맬웨어가 상승 되지 않습니다. 모조. 자격 증명을 묻는 메시지를 표시 하도록 정책 설정을 설정 하면 맬웨어가 자격 증명 프롬프트를 모방 사용자 로부터 자격 증명을 수집할 수 있습니다. 그러나 맬웨어는 상승된 권한을 얻지 못하고 시스템은 다른 방법으로 맬웨어가 수집된 암호를 사용하여 사용자 인터페이스를 제어하는 것을 방지할 수 있습니다.

맬웨어는 보안된 데스크톱의 모조 데스크톱을 제공할 수 있지만 사용자가 이전에 컴퓨터에 맬웨어를 설치하지 않은 경우 이 문제가 발생할 수 없습니다. UAC가 사용하도록 설정된 경우 관리자 액세스 토큰을 필요로 하는 프로세스가 자동으로 설치할 수 없으므로 사용자는 **예**를 클릭하거나 관리자 자격 증명을 제공하여 동의를 명시적으로 제공해야 합니다. UAC 권한 상승 프롬프트의 특정 동작은 그룹 정책에 의해 결정됩니다.

## <a name="uac-architecture"></a>UAC 아키텍처
다음 다이어그램은 UAC 아키텍처를 자세히 보여줍니다.

![UAC 아키텍처를 자세히 설명 하는 다이어그램](../media/How-User-Account-Control-Works/UACArchitecture.gif)

각 구성 요소를 보다 잘 이해 하려면 아래 표를 검토 하십시오.

|구성 요소|설명|
|-------|--------|
|**사용자**||
|사용자가 권한이 필요한 작업 수행|이 작업에 의해 파일 시스템이나 레지스트리가 변경되면 가상화가 호출됩니다. 다른 모든 작업은 ShellExecute를 호출합니다.|
|ShellExecute|ShellExecute는 CreateProcess를 호출합니다. ShellExecute는 CreateProcess에서 ERROR_ELEVATION_REQUIRED 오류를 검색합니다. 오류가 검색되면 ShellExecute는 응용 프로그램 정보 서비스를 호출하여 관리자 권한 프롬프트로 요청된 작업을 수행하려고 시도합니다.|
|CreateProcess|응용 프로그램에 권한 상승이 필요한 경우 CreateProcess는 ERROR_ELEVATION_REQUIRED로 호출을 거부합니다.|
|**컴퓨터**||
|응용 프로그램 정보 서비스|실행하려면 하나 이상의 상승된 권한 또는 사용자 권한이 필요한 응용 프로그램(예: 로컬 관리 작업) 및 더 높은 무결성 수준이 필요한 응용 프로그램을 시작하도록 도와주는 시스템 서비스입니다. 응용 프로그램 정보 서비스는 권한 상승이 필요하고 그룹 정책에 따라 사용자가 권한 상승에 동의한 경우 관리 사용자의 모든 권한 액세스 토큰으로 응용 프로그램에 대한 새 프로세스를 만들어 이러한 응용 프로그램을 시작하는 것을 도와줍니다.|
|ActiveX 설치 권한 상승|ActiveX가 설치되지 않은 경우 시스템은 UAC 슬라이더 수준을 확인합니다. ActiveX가 설치된 경우 시스템은 **사용자 계정 컨트롤: 권한 상승 요청 시 보안 데스크톱으로 전환** 그룹 정책 설정을 확인합니다.|
|UAC 슬라이더 수준 확인|이제 UAC에는 다음과 같은 네 개의 알림 수준과 이러한 알림 수준을 선택하는 데 사용할 수 있는 슬라이더가 있습니다.<br /><br /><ul><li>높음<br /><br />    슬라이더가 **항상 알림**으로 설정된 경우 시스템은 보안된 데스크톱을 사용할 수 있는지 여부를 확인합니다.</li><li>보통<br /><br />    슬라이더가 **기본값 - 프로그램에서 사용자 모르게 컴퓨터를 변경하려는 경우에만 알림**으로 설정된 경우 시스템은 **사용자 계정 컨트롤: 서명되고 유효성이 확인된 실행 파일만 권한 상승** 정책 설정을 확인합니다.<br /><br /><ul><li>이 정책 설정을 사용하면 지정된 실행 파일의 실행을 허용하기 전에 해당 실행 파일에 대해 PKI(공개 키 인프라) 인증 경로 유효성 검사가 적용됩니다.</li><li>이 정책 설정을 사용하지 않으면(기본값) 지정된 실행 파일의 실행을 허용하기 전에 해당 실행 파일에 대해 PKI 인증 경로 유효성 검사가 적용되지 않습니다. **사용자 계정 컨트롤: 권한 상승 요청 시 보안 데스크톱으로 전환** 그룹 정책 설정이 확인됩니다.</li></ul></li><li>낮음<br /><br />    슬라이더가 **프로그램에서 사용자 모르게 컴퓨터를 변경하려는 경우에만 알림(바탕 화면을 흐리게 표시하지 않음)** 으로 설정된 경우 CreateProcess가 호출됩니다.</li><li>알리지 않음<br /><br />    슬라이더가 자동으로 **알리지 않음**으로 설정 된 경우에는 프로그램에서 컴퓨터를 설치 하거나 변경 하려고 할 때 UAC 프롬프트가 알리지 않습니다. **중요:**     이 설정은 권장 되지 않습니다. 이 설정은 사용자 계정 컨트롤을 설정 하는 것과 같습니다 **. 관리자 승인 모드에서 관리자에 대 한 권한 상승 확인** 방법 정책 설정은 메시지를 표시 **하지 않고 상승**합니다.</li></ul>|
|보안된 데스크톱 사용|**사용자 계정 컨트롤: 권한 상승 요청 시 보안 데스크톱으로 전환** 정책 설정이 확인됩니다.<br /><br />-보안 된 데스크톱이 사용 하도록 설정 된 경우 관리자 및 표준 사용자에 대 한 프롬프트 동작 정책 설정에 관계 없이 모든 권한 상승 요청이 보안 된 데스크톱으로 이동 합니다.<br />-보안 데스크톱이 사용 하도록 설정 되어 있지 않으면 모든 권한 상승 요청이 대화형 사용자의 데스크톱으로 이동 하 고 관리자 및 표준 사용자에 대 한 사용자별 설정이 사용 됩니다.|
|CreateProcess|CreateProcess는 AppCompat, 퓨전 및 설치 관리자 검색을 호출하여 응용 프로그램에 권한 상승이 필요한지 여부를 확인합니다. 그런 다음 실행 파일을 검사하여 실행 파일의 응용 프로그램 매니페스트에 저장된 요청된 실행 수준을 확인합니다. 매니페스트에 지정된 요청된 실행 수준이 액세스 토큰과 일치하지 않고 ShellExecute에 오류(ERROR_ELEVATION_REQUIRED)가 반환되면 CreateProcess가 실패합니다. |
|AppCompat|AppCompat 데이터베이스는 응용 프로그램에 대한 응용 프로그램 호환성 수정 항목에 정보를 저장합니다.|
|퓨전|퓨전 데이터베이스는 응용 프로그램을 설명하는 응용 프로그램 매니페스트의 정보를 저장합니다. 매니페스트 스키마는 새 요청된 실행 수준 필드를 추가하도록 업데이트됩니다.|
|설치 관리자 검색|설치 관리자 검색은 설치 실행 파일을 검색하여 설치가 사용자 동의 없이 몰래 실행되지 않도록 합니다.|
|**커널**||
|가상화|가상화 기술은 호환되지 않는 응용 프로그램이 자동으로 또는 원인을 알 수 없는 방식으로 실행되지 않는 문제가 발생하지 않도록 합니다. 또한 UAC는 보호된 영역에 쓰는 응용 프로그램에 대한 파일 및 레지스트리 가상화와 로깅을 제공합니다.|
|파일 시스템 및 레지스트리|사용자별 파일 및 레지스트리 가상화는 컴퓨터별 레지스트리 및 파일 쓰기 요청을 해당 사용자별 위치로 리디렉션합니다. 읽기 요청은 먼저 가상화된 사용자별 위치로 리디렉션되고 그 다음에 컴퓨터별 위치로 리디렉션됩니다.|

이전 Windows 버전의 Windows Server 2012 UAC에 대 한 변경 내용이 있습니다. 새 슬라이더는 UAC를 완전히 해제 하지 않습니다. 새 설정에는 다음이 수행 됩니다.

-   UAC 서비스를 계속 실행 합니다.

-   관리자가 시작한 모든 권한 상승 요청이 UAC 프롬프트를 표시 하지 않고 자동 승인 되도록 합니다.

-   표준 사용자에 대 한 모든 권한 상승 요청을 자동으로 거부 합니다.

> [!IMPORTANT]
> UAC를 완전히 사용 하지 않도록 설정 하려면 정책 **사용자 계정 컨트롤: 관리자 승인 모드에서 모든 관리자 실행**을 사용 하지 않도록 설정 해야 합니다.

> [!WARNING]
> UAC를 사용 하지 않도록 설정한 경우에는 Windows Server 2012에서 맞춤식 응용 프로그램이 작동 하지 않습니다.

### <a name="virtualization"></a>가상화
엔터프라이즈 환경에서는 시스템 관리자에 의해 시스템이 보호되기 때문에 많은 LOB(기간 업무) 응용 프로그램이 표준 사용자 액세스 토크만 사용하도록 설계되었습니다. 따라서 IT 관리자는 UAC를 사용 하는 Windows Server 2012를 실행할 때 대부분의 응용 프로그램을 교체할 필요가 없습니다.

 Windows Server 2012에는 UAC 규격이 아니고 관리자의 액세스 토큰이 올바르게 실행 되어야 하는 응용 프로그램에 대 한 파일 및 레지스트리 가상화 기술이 포함 되어 있습니다. 가상화는 UAC 규격이 아닌 응용 프로그램도 Windows Server 2012와 호환 되도록 합니다. UAC 규격이 아닌 응용 프로그램이 Program Files 등의 보호되는 디렉터리에 쓰려고 시도하는 경우 UAC는 응용 프로그램이 변경하려는 리소스의 고유한 가상화된 보기를 응용 프로그램에 제공합니다. 가상화된 복사본은 사용자의 프로필에 유지 관리됩니다. 이 전략에 따라 비규격 응용 프로그램을 실행하는 사용자마다 가상화된 파일의 복사본이 하나씩 만들어집니다.

가상화 기능을 사용하면 대부분의 응용 프로그램 작업이 올바르게 작동합니다. 가상화를 사용하여 대부분의 응용 프로그램을 실행할 수 있지만, 이는 단기적인 수정일 뿐 장기적인 해결 방법이 아닙니다. 응용 프로그램 개발자는 파일, 폴더 및 레지스트리 가상화에 의존 하지 않고 가능한 한 빨리 Windows Server 2012 로고 프로그램을 준수 하도록 응용 프로그램을 수정 해야 합니다.

다음과 같은 시나리오에서는 가상화가 옵션으로 제공되지 않습니다.

1.  가상화는 권한이 상승되고 모든 관리 액세스 권한 토큰을 사용하여 실행되는 응용 프로그램에 적용되지 않습니다.

2.  가상화는 32비트 응용 프로그램만 지원합니다. 일반 권한의 64비트 응용 프로그램은 Windows 개체에 대한 핸들(고유 식별자)을 가져오려고 시도할 때 액세스 거부 메시지만 수신합니다. 기본 Windows 64비트 응용 프로그램은 반드시 UAC와 호환되고 올바른 위치에 데이터를 써야 합니다.

3.  요청된 실행 수준 특성이 있는 응용 프로그램 매니페스트가 포함된 응용 프로그램의 경우에는 UAC 가상화가 사용되지 않도록 설정됩니다.

### <a name="request-execution-levels"></a>요청 실행 수준
애플리케이션 매니페스트는 런타임에 애플리케이션이 바인딩해야 하는 공유 및 프라이빗 병렬 어셈블리를 설명하고 식별하는 XML 파일입니다. Windows Server 2012에서는 응용 프로그램 매니페스트에 UAC 응용 프로그램 호환성을 위한 항목이 포함 되어 있습니다. 응용 프로그램 매니페스트의 항목을 포함하는 관리 응용 프로그램은 사용자에게 사용자의 액세스 토큰에 액세스할 수 있는 권한을 요청합니다. 대부분의 관리 응용 프로그램은 응용 프로그램 매니페스트의 항목이 부족해도 응용 프로그램 호환성 수정을 사용하여 수정하지 않고도 실행할 수 있습니다. 응용 프로그램 호환성 픽스는 UAC 규격이 아닌 응용 프로그램이 Windows Server 2012에서 제대로 작동 하는 데 사용할 수 있는 데이터베이스 항목입니다.

모든 UAC 규격 응용 프로그램에는 응용 프로그램 매니페스트에 추가된 요청된 실행 수준이 있어야 합니다. 응용 프로그램에 시스템에 대한 관리 액세스 권한이 필요한 경우 응용 프로그램의 요청된 실행 수준을 "관리자 권한 필요"로 표시하면 시스템이 이 프로그램을 관리 응용 프로그램으로 식별하고 필요한 권한 상승 단계를 수행합니다. 요청된 실행 수준은 응용 프로그램에 필요한 권한을 지정합니다.

### <a name="installer-detection-technology"></a>설치 관리자 검색 기술
설치 프로그램은 소프트웨어를 배포하기 위해 설계된 응용 프로그램입니다. 대부분의 설치 프로그램은 시스템 디렉터리 및 레지스트리 키에 씁니다. 일반적으로 설치 관리자 검색 기술의 관리자만 이러한 보호된 시스템 위치에 쓸 수 있습니다. 즉, 표준 사용자는 프로그램을 설치할 수 있는 충분한 권한이 없습니다. Windows Server 2012 발견적는 설치 프로그램을 검색 하 고 관리자 자격 증명을 요청 하거나 관리자가 액세스 권한으로 실행 하기 위해 관리자에 게 승인을 요청 합니다. 또한 Windows Server 2012는 응용 프로그램을 제거 하는 업데이트 및 프로그램을 발견적 검색 합니다. UAC의 설계 목적 중 하나는 설치 프로그램이 파일 시스템 및 레지스트리의 보호된 영역에 쓰기 때문에 설치가 사용자 동의 없이 몰래 실행되는 것을 방지하는 것입니다.

설치 관리자 검색은 다음에만 적용됩니다.

-   32비트 실행 파일

-   요청된 실행 수준 특성이 없는 응용 프로그램

-   UAC를 사용하도록 설정한 상태에서 표준 사용자로 실행되는 대화형 프로세스

32비트 프로세스를 만들기 전에 다음 특성을 검사하여 해당 프로세스가 설치 관리자인지 여부를 확인합니다.

-   파일 이름에 "install," "setup" 또는 "update"와 같은 키워드가 포함되어 있습니다.

-   버전 관리 리소스 필드에 공급업체, 회사 이름, 제품 이름, 파일 설명, 원래 파일 이름, 내부 이름, 내보내기 이름 등의 키워드가 포함되어 있습니다.

-   병렬 매니페스트의 키워드가 실행 파일에 포함되어 있습니다.

-   특정 StringTable 항목의 키워드가 실행 파일에서 링크됩니다.

-   리소스 스크립트 데이터의 키 특성이 실행 파일에서 링크됩니다.

-   실행 파일 내에 바이트의 대상 시퀀스가 있습니다.

> [!NOTE]
> 바이트의 키워드 및 시퀀스는 다양한 설치 관리자 기술에 있는 공통 특성에서 파생되었습니다.

> [!NOTE]
> 설치 프로그램을 검색 하려면 설치 프로그램 검색에 대 한 사용자 계정 컨트롤: 응용 프로그램 설치 및 권한 상승 확인 정책 설정을 사용 하도록 설정 해야 합니다. 이 설정은 기본적으로 사용하도록 설정되며 로컬 보안 정책 스냅인(Secpol.msc)을 사용하여 로컬로 구성하거나 그룹 정책(Gpedit.msc)을 사용하여 도메인, OU 또는 특정 그룹에 대해 구성할 수 있습니다.


