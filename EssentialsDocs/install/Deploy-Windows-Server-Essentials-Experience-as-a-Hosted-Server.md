---
title: Windows Server Essentials Experienc를 호스트된 서버로 배포
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a455c6b4-b29f-4f76-8c6b-1578b6537717
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 94d4040b65a63fe64e5d49d55f82c4deead5a121
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433580"
---
# <a name="deploy-windows-server-essentials-experience-as-a-hosted-server"></a>Windows Server Essentials Experienc를 호스트된 서버로 배포

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 문서는 랩에서 설치 (Windows Server Essentials 라고 문서의 나머지 부분에서는) Windows Server Essentials Experience 역할을 사용 하 여 Microsoft Windows Server 16을 배포 하려는 호스팅 서비스 공급자에 관련 된 정보를 포함 하 고 Windows Server Essentials Experience를 고객에 게 서비스로 제공 하 려 합니다. 이 문서에는 다음과 같은 섹션이 포함되어 있습니다.  
  

-   [Windows Server Essentials Experience 개요](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)  
  
-   [Windows Server Essentials Experience 호스팅의 이점](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)  
  
-   [지원 되는 배포 옵션](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)  
  
-   [지원 되는 네트워크 토폴로지](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)  
  
-   [Windows Server Essentials Experience 역할 이미지 사용자 지정](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)  
  
-   [Windows Server Essentials Experience의 배포를 자동화](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)  
  
-   [Windows Server Essentials Experience를 Windows Small Business Server에서 데이터 마이그레이션](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)  
  
-   [Windows PowerShell을 사용 하 여 일반적인 작업을 수행 합니다.](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)  
  
-   [Windows Server Essentials를 사용 하 여 전자 메일 통합](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)  
  
-   [네이티브 도구를 사용 하 여 모니터링 및 관리](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)  
  
-   [테스트 시나리오](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)  
  
-   [지원 정보](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)  

-   [Windows Server Essentials Experience 개요](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)  
  
-   [Windows Server Essentials Experience 호스팅의 이점](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)  
  
-   [지원 되는 배포 옵션](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)  
  
-   [지원 되는 네트워크 토폴로지](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)  
  
-   [Windows Server Essentials Experience 역할 이미지 사용자 지정](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)  
  
-   [Windows Server Essentials Experience의 배포를 자동화](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)  
  
-   [Windows Server Essentials Experience를 Windows Small Business Server에서 데이터 마이그레이션](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)  
  
-   [Windows PowerShell을 사용 하 여 일반적인 작업을 수행 합니다.](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)  
  
-   [Windows Server Essentials를 사용 하 여 전자 메일 통합](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)  
  
-   [네이티브 도구를 사용 하 여 모니터링 및 관리](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)  
  
-   [테스트 시나리오](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)  
  
-   [지원 정보](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)  

  
##  <a name="BKMK_WSEEOverview"></a> Windows Server Essentials Experience 개요  
 Windows Server Essentials Experience 서버 역할 Windows Server 2012 R2 Standard 및 Windows Server 2012 R2 Datacenter에서 사용할 수 있는 경우 Windows Server 2012 R2를 실행 하는 서버에서 Windows Server Essentials Experience 역할이 설치 될 때 고객은 잠금 및 제한 없이 Windows Server Essentials에서 사용할 수 있는 모든 기능을 활용을 걸릴 수 있습니다. Windows Server Essentials Experience 소규모 및 중간 규모 기업에 대 한 다음 크로스-프레미스 솔루션을 수 있습니다.  
  
-   **데이터 저장소 및 보호** 고객을 저장할 수 있습니다 "중앙된 위치에 있습니다의 데이터 및 서버 및 네트워크 내에서 클라이언트 컴퓨터 (75 대 미만)를 백업 하 여 서버 및 클라이언트 데이터를 보호 합니다.  
  
-   **사용자 관리** 단순화된 서버 대시보드를 통해 사용자 및 그룹을 관리할 수 있습니다. 또한 Microsoft Azure Active Directory (Azure AD)와 통합 데이터에 쉽게 액세스할을 수 Microsoft 온라인 서비스 (예를 들어 Office 365, Exchange Online 및 SharePoint Online)에 대 한 사용자에 대 한 해당 도메인 자격 증명을 사용 하 여 있습니다.  
  
-   **통합 서비스** Microsoft 온라인 서비스 (예: Office 365, SharePoint Online 및 Microsoft Azure Backup)를 사용 하 여 서버를 통합할 수 있습니다. 또한 서버를 사용자의 서비스 또는 타사 공급자가 제공하는 서비스와 통합할 수 있습니다.  
  
-   **원격 액세스** 고객은 인터넷에 연결되어 있는 경우 거의 모든 곳에서 거의 모든 장치를 사용하여 서버, 네트워크 컴퓨터 및 데이터에 액세스할 수 있습니다. 고객은 원격 웹 액세스를 사용하여 간소화된 터치 지원 브라우저 환경을 통해 응용 프로그램 및 데이터에 액세스할 수 있습니다. My Server 앱을 사용 하면 Windows Phone 또는 Microsoft Store 앱에서 데이터에 액세스할 수 있도록 합니다.  
  
-   **미디어 스트리밍** 최종 고객 사용 하도록 설정 하는 Windows Server Essentials Experience를 사용 하 여 서버에 미디어 패키지를 설치 하는 경우 공유 폴더에 음악, 비디오 및 사진을 저장 다음 네트워크에 연결 된 컴퓨터에서 이러한 미디어 파일에 액세스할 수 또는 원격 웹 액세스 합니다.  
  
-   **상태 모니터링** 네트워크 상태를 모니터링하고 사용자 지정된 상태 보고서를 얻을 수 있습니다.  
  
##  <a name="BKMK_Benefits"></a> Windows Server Essentials Experience 호스팅의 이점  
  Windows Server Essentials Experience Windows Server에서 역할 이므로 기존 배포 및 배포 하 고 Windows Server Essentials Experience 역할을 구성 하려면 Windows Server 관리 프레임 워크를 다시 사용할 수 있습니다. Windows Server Essentials Experience 역할을 호스팅하는 다음과 같은 이점이 있습니다.  
  
-   **간소화 된 배포** 단순히 Windows Server Essentials Experience 역할을 켜면, 가장 일반적으로 사용 되는 일부 역할 및 기능이 설정 되 고 중소기업을 위한 모범 사례를 사용 하 여 구성 합니다. Windows Server Essentials 기능을 사용자 지정하거나 몇 가지 온-프레미스 기능을 숨길 수 있습니다. Windows Azure 팩을 사용 하는 경우 Windows Server 2012 R2에서 Windows Server Essentials Experience에 대 한 갤러리 템플릿을 다운로드할 수 있습니다.  
  
-   **단순화된 대시보드** Windows Server Essentials Dashboard는 서버 폴더, 서버 저장소, 백업 및 복원, 사용자 또는 그룹 계정, 장치, 원격 액세스 및 전자 메일 관리와 같은 일반적인 작업을 단순화합니다. 중소기업 고객은 지원 센터에 기술 지원을 요청하는 대신 매일 관리 작업을 수행할 수 있습니다.  
  
-   **확장성** Windows Server Essentials Dashboard 및 Windows Server Essentials Connector 소프트웨어는 확장할 수 있습니다. 고객이 해당 서버 및 서비스의 모든 항목에 대한 하나의 진입점을 갖도록 사용자 고유의 브랜딩 및 서비스 통합을 추가할 수 있습니다.  
  
-   **모니터링** Windows Server Essentials를 실행하는 여러 서버를 모니터링 및 관리하는 데 사용할 수 있는 System Center 모니터링 팩의 새 버전을 사용할 수 있습니다. 관리 팩을 다운로드 하려면 [System Center 관리 팩에 대 한 Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809)합니다.  
  
##  <a name="BKMK_SupportedDeployment"></a> 지원 되는 배포 옵션  
  Windows Server Essentials Experience는 도메인 컨트롤러로 새 Active Directory 환경에 배포할 수 있습니다. 또는 기존 Active Directory 환경에 도메인 구성원으로 배포할 수 있습니다.  
  
 먼저 Windows Server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter, 배포 후 Windows Server Essentials Experience 역할을 설치 하는 것이 좋습니다. 이 배포 메서드를 사용 하 여 잠금 및 제한 없이 Windows Server Essentials 버전의 모든 기능을 가져옵니다.  
  

 Windows Server Essentials Experience 역할을 사용 하 여 Windows Server 2012 R2를 설치 하는 방법에 대 한 자세한 내용은 참조 하세요. [설치 및 Windows Server Essentials 구성](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)합니다.  


  
##  <a name="BKMK_SupportedToplogy"></a> 지원 되는 네트워크 토폴로지  
 로밍 클라이언트에서 Windows Server Essentials Experience를 사용 하려면 VPN 설정 되어야 합니다. 로밍 클라이언트에서 서버로 원격 액세스를 할 수 있으려면 서버에서 포트 443 및 포트 80을 열어야 합니다.  
  
 다음은 일반적인 서버 쪽 네트워킹 토폴로지 두 가지와 VPN 및 원격 웹 액세스를 구성하는 방법입니다.  
  
- **토폴로지 1** (기본 설정 토폴로지로서, 모든 서버와 VPN IP 범위를 동일한 서브넷에 배치함):  
  
  -   서버를 NAT(Network Address Translation) 장치에서 별도의 가상 네트워크에 설정합니다.  
  
  -   가상 네트워크에서 DHCP 서비스를 사용하도록 설정하거나 서버에 고정 IP 주소를 할당합니다.  
  
  -   라우터에서 공용 IP 포트 443을 서버의 로컬 네트워크 주소에 전달합니다.  
  
  -   포트 443에 대해 VPN 통과를 허용합니다.  
  
  -   서버 주소와 동일한 서브넷 범위에 VPN IPv4 주소 풀을 설정합니다.  
  
  -   두 번째 서버에 동일한 서브넷 내에 있지만 VPN 주소 풀 외부에 있는 고정 IP 주소를 할당합니다.  
  
- **토폴로지 2**:  
  
  -   서버에 개인 IP 주소를 할당합니다.  
  
  -   서버의 포트 443이 공용 포트 443 IP 주소에 도달하도록 합니다.  
  
  -   포트 443에 대해 VPN 통과를 허용합니다.  
  
  -   VPN IPv4 주소 풀 및 서버 주소에 대해 서로 다른 범위를 할당합니다.  
  
  토폴로지 2의 경우 동일한 도메인에 다른 서버를 추가할 수 없으므로 두 번째 서버 시나리오가 지원되지 않습니다.  
  
  Windows PowerShell 스크립트를 사용하여 무인 배포 중에 VPN을 사용하도록 설정하거나, 초기 구성 후 마법사를 사용하여 VPN을 구성할 수 있습니다.  
  
  Windows PowerShell을 사용하여 VPN을 사용하도록 설정하려면 Windows Server Essentials를 실행하는 서버에서 관리자 권한으로 다음 명령을 실행하고 필요한 모든 정보를 제공합니다.  
  
```  
##  
## To configure external domain and SSL certificate (if not yet done in unattended Initial Configuration).  
##  
  
$myExternalDomainName = 'remote.contoso.com';   ## corresponds to A or AAAA DNS record(s) that can be resolved on Internet and routed to the server  
$mySslCertificateFile = 'C:\ssl.pfx';   ## full path to SSL certificate file  
$mySslCertificatePassword = ConvertTo-SecureString  œAsPlainText  œForce '******';   ## password for private key of the SSL certificate  
$skipCertificateVerification = $true;   ## whether or not, skip verification for the SSL certificate  
  
Set-WssDomainNameConfiguration  œDomainName $myExternalDomainName  œCertificatePath $mySslCertificateFile  œCertificateFilePassword $mySslCertificatePassword  œNoCertificateVerification  
##  
## To install VPN with static IPv4 pool (and allow all existing users to establish VPN).  
##  
  
Install-WssVpnServer -IPv4AddressRange ('192.168.0.160','192.168.0.240') -ApplyToExistingUsers;  
  
```  
  
> [!NOTE]
>  고객이 서버를 소유하기 전에 VPN 연결을 제공할 수 없는 경우 고객이 원격 데스크톱 프로토콜을 사용하여 서버에 연결하고 서버를 구성할 수 있도록 인터넷을 통해 서버 포트 3389에 연결할 수 있는지 확인합니다.  
  
##  <a name="BKMK_CustomizeImage"></a> Windows Server Essentials Experience 역할 이미지 사용자 지정  
 Windows Server 필수 패키지 환경 역할을 구성하기 전에 이미지를 사용자 지정할 수 있습니다. 표준 Windows Server Sysprep 프로세스에 대한 자세한 내용은 [Windows 평가 및 배포 키트](https://msdn.microsoft.com/library/hh825420.aspx)를 참조하세요. Sysprep을 사용하여 이미지를 준비한 후 이미지를 사용하거나 새 배포를 위해 Install.wim으로 다시 봉인할 수 있습니다.  
  
 가상 컴퓨터 관리자를 사용하는 경우 실행 중인 인스턴스를 사용하여 템플릿을 만들 수 있습니다. 이 프로세스에서는 Sysprep을 사용하여 인스턴스를 준비하고 컴퓨터를 종료합니다. 라이브러리에 템플릿을 저장한 후 개별적으로 사용할 수 있습니다.  
  
 Windows Server Essentials Experience 역할을 설치한 후 Windows Server Essentials의 기능을 사용자 지정할 수 있습니다. 가장 중요한 사용자 지정 중 하나는 **IsHosted** 레지스트리 키 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\Deployment\IsHosted**입니다.  
  
 이 키가 0x1로 설정된 경우 온-프레미스 기능 중 일부가 동작을 변경합니다. 이러한 기능 변경은 다음과 같습니다.  
  
- **클라이언트 백업** 새로 가입된 클라이언트 컴퓨터에 대해서는 기본적으로 클라이언트 백업이 해제됩니다.  
  
- **클라이언트 복원 서비스** 클라이언트 복원 서비스가 사용하지 않도록 설정되며, UI가 대시보드에서 숨겨집니다.  
  
- **파일 히스토리** 새로 만들어진 사용자 계정에 대한 파일 히스토리 설정은 서버에 의해 자동으로 관리되지 않습니다.  
  
- **서버 백업** 서버 백업 서비스는 사용하지 않도록 설정되며, 서버 백업 UI가 대시보드에서 숨겨집니다.  
  
- **저장소 공간** 저장소 공간을 만들거나 관리하기 위한 UI가 대시보드에서 숨겨집니다.  
  
- **원격 액세스** 원격 액세스 설정 마법사를 실행할 때 라우터 및 VPN 구성은 기본적으로 건너뜁니다.  
  
  나열된 각 기능의 동작을 제어하려면 각 기능의 해당 레지스트리 키를 설정하면 됩니다. 레지스트리 키를 설정하는 방법에 대한 자세한 내용은 [Windows Server 2012 R2에서 Windows Server Essentials 사용자 지정 및 배포](https://technet.microsoft.com/library/dn293241.aspx)를 참조하세요.  
  
##  <a name="BKMK_AutomateDeployment"></a> Windows Server Essentials Experience의 배포를 자동화  
 배포를 자동화 하려면 먼저 운영 체제를 배포 하 고 다음 Windows Server Essentials Experience 역할을 설치 해야 합니다.  
  
-   Windows Server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter를 자동으로 배포 하려면의 지침을 따릅니다 [Windows Assessment and Deployment Kit](https://msdn.microsoft.com/library/hh825420.aspx)합니다.  
  
-   Windows PowerShell을 사용 하 여 Windows Server Essentials Experience 역할을 설치 하는 방법에 알아보려면 참조 [설치 및 Windows Server Essentials 구성](https://technet.microsoft.com/library/dn281793.aspx)합니다.  
  
> [!NOTE]
>  호스트 가상 머신 및 Windows Server Essentials Experience의 표준 시간대 설정이 동일한 지 확인 합니다. 그렇지 않으면 여러 오류가 발생할 수 있습니다. 여기에 포함 됩니다: 서버의 초기 구성에 성공 하지 않을 인증서 관련된 작업, 몇 시간 후 장치 정보 업데이트 되지 것입니다 및 Windows Server Essentials Experience 역할이 설치 되어 작동 하지 않거나 인증서 올바르게 합니다.  
  
 배포 후 Windows PowerShell cmdlet **Get-WssConfigurationStatus**를 사용하여 초기 구성에 성공했는지 확인합니다. 반환된 상태는 **Notstarted**, **FinishedWithWarning**, **Running**, **Finished**, **Failed** 또는 **PendingReboot** 중 하나여야 합니다.  
  
 초기 구성 중에 서버가 다시 시작됩니다. 이러한 자동 다시 시작을 방지해야 하는 경우 초기 구성을 시작하기 전에 다음 명령을 사용하여 레지스트리 키를 추가하면 됩니다.  
  
```  
New-ItemProperty "HKLM:\Software\Microsoft\Windows Server\Setup"Ã‚Â  -Name "WaitForReboot" -Value 1 -PropertyType "DWord" -Force -Confirm:$false  
  
```  
  
 초기 구성이 시작된 후 **Get-WssConfigurationStatus**를 사용하여 초기 구성 상태를 확인할 수 있으며, 상태가 **PendingReboot**이면 서버를 다시 시작할 수 있습니다.  
  
##  <a name="BKMK_Migrate"></a> Windows Server Essentials Experience를 Windows Small Business Server에서 데이터 마이그레이션  
 Windows Server Essentials를 실행 하는 서버에 Windows Small Business Server 2011, Windows Small Business Server 2008, Windows Small Business Server 2003 또는 Windows Server Essentials를 실행 하는 서버에서 데이터를 마이그레이션할 수 있습니다. 검토 합니다 [Windows Server Essentials로 마이그레이션](../migrate/Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md) 마이그레이션 온-프레미스 2 마이그레이션에 대 한 가이드 및 호스팅 환경에 따라 필요한 사용자 지정을 수행 합니다.  
  
> [!NOTE]
>  원본 서버와 대상 서버를 동일한 서브넷에 배치하는 것이 좋습니다. 이것이 불가능한 경우 다음을 확인해야 합니다.  
> 
> - 원본 서버와 대상 서버가 서로 액세스할 수 있는 "™ s 내부 DNS 이름입니다.  
>   -   필요한 모든 포트가 열려 있습니다.  
  
 마이그레이션 후 라이선스를 업그레이드하여 잠금 및 제한을 제거할 수 있습니다. 자세한 내용은 [Windows Server Essentials에서 Windows Server 2012 Standard 전환](https://technet.microsoft.com/library/jj247582.aspx)합니다.  
  
##  <a name="BKMK_PowerShell"></a> Windows PowerShell을 사용 하 여 일반적인 작업을 수행 합니다.  
 이 섹션에서는 Windows PowerShell을 사용하여 수행할 수 있는 일반적인 작업 몇 가지를 설명합니다.  
  
### <a name="enable-remote-web-access"></a>원격 웹 액세스 사용  
 **구문**:  
  
 Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]  
  
 **예**:  
  
 $Enable-WssRemoteWebAccess  œDenyAccessByDefault  œApplyToExistingUsers  
  
 이 명령은 라우터를 자동으로 구성하여 원격 웹 액세스를 사용하도록 설정하며 모든 기존 사용자의 기본 액세스 권한을 변경합니다.  
  
### <a name="add-user"></a>사용자 추가  
 **구문**:  
  
 추가 WssUser [-Name] < 문자열\> [-암호] < securestring\> [-AccessLevel < 문자열\> {0} 사용자 &#124; 관리자}] [-FirstName < 문자열\>] [-LastName < 문자열\>] [- AllowRemoteAccess] [-AllowVpnAccess] [< CommonParameters\>]  
  
 **예**:  
  
 $password Convertto-securestring "passw0rd!""= -asplaintext œforce$ Add-wssuser-이름 user2test"-암호 $password-Accesslevel 관리자-FirstName LastName User2 테스트  
  
 이 명령은 Passw0rd 암호로 user2test"라는 관리자로 추가 되었습니다.  
  
### <a name="add-server-folder"></a>서버 폴더 추가  
 **구문**:  
  
 Add-WssFolder [-Name] <string\> [-Path] <string\> [[-Description] <string\>] [-KeepPermissions] [<CommonParameters\>]  
  
 **예**:  
  
 $Add-WssFolder -Name "MyTestFolder" -Path "C:\ServerFolders\MyTestFolder"  
  
 이 명령은 지정 된 위치의 MyTestFolder 라는 서버 폴더를 추가 합니다.  
  
##  <a name="BKMK_EmailIntegration"></a> Windows Server Essentials를 사용 하 여 전자 메일 통합  
 Exchange Server를 호스트 하거나 Office 365를 사용 하 여 Windows Server Essentials Experience를 통합할 수 있습니다. 고객이 호스트된 메일을 사용하도록 하려면 Windows Server 필수 패키지 환경을 호스트된 메일 솔루션과 통합하기 위한 추가 기능을 개발해야 합니다. 자세한 내용은 [Windows Server Essentials SDK](https://msdn.microsoft.com/library/gg513877.aspx)를 참조하세요.  
  
##  <a name="BKMK_Monitoring"></a> 네이티브 도구를 사용 하 여 모니터링 및 관리  
 이 섹션에서는 Windows Server 2012 R2 모니터링 및 관리 서버를 사용할 수 있는 네이티브 도구를 설명 합니다.  
  
### <a name="group-policy"></a>그룹 정책  
  Windows Server Essentials Experience는 Windows Server 2012 R2의 기본 그룹 정책 지원을 활용 하 고 폴더 리디렉션 및 보안 설정을 구성 하기 위한 사용자 인터페이스를 제공 합니다.  
  
> [!NOTE]
>  호스트된 환경에서 사용자 프로필에 대해 폴더 리디렉션을 사용하도록 설정한 경우 데이터 크기가 크면 최종 사용자가 로그인하는 데 시간이 오래 걸릴 수 있습니다.  
  
### <a name="system-center-monitoring-pack"></a>System Center 모니터링 팩  
 System Center 모니터링 팩은 상태 경고 시스템 다 수의 Windows Server Essentials를 실행 하는 서버를 관리할 수 있도록 하 여 중소기업 전용 Windows Server Essentials Experience 모니터에 대 한 합니다. 자세한 내용은 [System Center 관리 팩에 대 한 Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809)합니다.  
  
### <a name="backup-and-restore"></a>Backup 및 Restore 메서드  
  Windows Server Essentials Experience와 함께 Windows Server 2012 R2를 사용 하면 서버 및 네트워크의 클라이언트 컴퓨터를 백업할 수 있습니다.  
  
#### <a name="server-backup"></a>서버 백업  
 Windows Server Essentials는 서버를 백업하는 두 가지 방법 즉, 온-프레미스 백업 및 오프-프레미스 백업을 지원합니다. 사용자 고유의 서버 백업 솔루션을 배포하려는 경우 이러한 옵션을 사용자 지정하면 됩니다.  
  
-   **온-프레미스 백업** 정기적으로 별도의 디스크에 블록 수준 증분 백업을 수행할 수 있습니다. 호스팅 서비스 공급자는 Windows Server Essentials를 실행하는 가상 컴퓨터에 가상 하드 디스크를 연결한 후 이 가상 하드 디스크에 백업하도록 서버를 구성할 수 있습니다. 가상 하드 디스크는 Windows Server Essentials를 실행하는 가상 컴퓨터와 다른 실제 디스크에 있어야 합니다.  
  
    > [!NOTE]
    >  가상 컴퓨터에 대한 다른 백업 솔루션이 있으며 사용자에게 Windows Server Essentials 기본 서버 백업 기능이 표시되지 않기를 원하는 경우 이 기능을 끄고 대시보드에서 관련 사용자 인터페이스를 제거할 수 있습니다. 자세한 내용은 [Windows Server 2012 R2에서 Windows Server Essentials 사용자 지정 및 배포](https://technet.microsoft.com/library/dn293413.aspx) 의 [서버 백업 사용자 지정](https://technet.microsoft.com/library/dn293241.aspx)섹션을 참조하세요.  
  
-   **오프-프레미스 백업** 주기적으로 클라우드 기반 서비스에 서버 데이터를 백업할 수 있습니다. 다운로드 하 고 Microsoft Azure Backup 통합 모듈에 대 한 Windows Server Essentials Microsoft에서 제공 하는 Azure Backup을 활용 하 여 설치할 수 있습니다.  
  
     자세한 내용은 통합 Windows Azure Backup에서 Windows Server Essentials 섹션을 참조 하세요 [Manage Server Backup](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md)합니다.  
  
     관리자 또는 사용자가 다른 클라우드 서비스를 선호하는 경우 다음을 고려해야 합니다.  
  
    -   기본 Azure Backup 대신 원하는 클라우드 서비스에 연결 되도록 대시보드의 사용자 인터페이스를 업데이트 합니다.  
  
    -   (선택 사항) 클라우드 기반 백업 서비스를 구성 및 관리하기 위한 대시보드용 추가 기능을 개발합니다.  
  
#### <a name="client-computer-backup"></a>클라이언트 컴퓨터 백업  
 Windows Server 필수 패키지 환경은 두 종류의 클라이언트 데이터 백업 즉, 전체 클라이언트 백업과 파일 히스토리를 지원합니다.  
  
> [!NOTE]
>  클라이언트 백업은 VPN을 통해 클라이언트에서 서버로 데이터를 전송해야 하므로 성능에 영향을 줄 수 있습니다.  
  
##### <a name="full-client-backup"></a>전체 클라이언트 백업  
 전체 클라이언트 백업은 기본적으로 Windows Server Essentials 네트워크에 연결된 모든 클라이언트 장치에 대해 설정되어 있습니다. 전체 클라이언트 백업은 클라이언트의 시스템 정보와 데이터를 완벽하게 백업하고 데이터 중복 제거를 지원합니다. 백업 데이터를 Windows Server Essentials를 실행 하는 서버에 저장 됩니다. 따라서 실패한 클라이언트가 이전 백업 지점에서 데이터를 검색할 수 있습니다.  
  
 전체 클라이언트 컴퓨터 백업에 대한 몇 가지 고려 사항은 다음과 같습니다.  
  
-   **성능** 초기 클라이언트 백업은 업로드할 데이터 양 때문에 시간이 많이 걸릴 수 있습니다.  
  
-   **안정성** 클라이언트 쪽 인터넷 연결이 안정적이지 않은 경우가 있습니다. 클라이언트 백업은 자동으로 다시 시작 하도록 설계 되었으며와 클라이언트 백업 데이터베이스는 40GB의 데이터가 백업 될 때마다 검사점을 만듭니다. 인터넷 연결이 불안정할 것으로 예상되는 경우 이 값을 더 작은 숫자로 변경할 수 있습니다.  
  
    -   검사점 작업을 사용하려면: 서버에서 레지스트리 키 **HKLM\Software\Microsoft\Windows Server\Backup\GetCheckPointJobs**를 1로 설정합니다.  
  
    -   검사점 임계값을 변경하려면: 클라이언트에서 변경할 **HKLM\Software\Microsoft\Windows Server\Backup\CheckPointThreshold** 기본값 40gb에서.  
  
-   **클라이언트 완전 복구** Windows 사전 설치 환경은 VPN 연결을 지원하지 않으므로 클라이언트 완전 복구는 지원되지 않습니다. [Windows Server 2012 R2에서 Windows Server Essentials 사용자 지정 및 배포](https://technet.microsoft.com/library/dn293241.aspx)의 단계에 따라 클라이언트 복원 서비스 작업을 숨겨야 합니다.  
  
##### <a name="file-history"></a>파일 기록  
 파일 히스토리는 프로필 데이터(라이브러리, 데스크톱, 연락처, 즐겨찾기)를 네트워크 공유에 백업하는 Windows 8.1 및 Windows 8 기능입니다. Windows Server Essentials 네트워크에 가입된, Windows 8.1 또는 Windows 8을 실행하는 모든 컴퓨터의 파일 히스토리 설정을 중앙에서 관리할 수 있습니다. 백업 데이터는 Windows Server Essentials를 실행하는 서버에 저장됩니다. [Windows Server 2012 R2에서 Windows Server Essentials 사용자 지정 및 배포](https://technet.microsoft.com/library/dn293241.aspx)의 단계에 따라 클라이언트 복원 서비스 작업을 숨겨야 합니다.  
  
### <a name="storage-management"></a>저장소 관리  
 저장소 공간을 사용하면 개별 하드 드라이브의 실제 저장소 용량을 집계하고, 하드 드라이브를 동적으로 추가하며, 지정된 복원력 수준으로 데이터 볼륨을 만들 수 있습니다. 호스트 또는 가상 컴퓨터에서 이렇게 할 수 있습니다. Windows Server Essentials를 실행하는 가상 컴퓨터에서 이 기능을 숨기려면 [Windows Server 2012 R2에서 Windows Server Essentials 사용자 지정 및 배포](https://technet.microsoft.com/library/dn293241.aspx)의 지침에 따르세요.  
  
##  <a name="BKMK_Scenarios"></a> 테스트 시나리오  
 호스팅 관점에서 다음과 같은 시나리오를 테스트하는 것이 좋습니다.  
  

-   [서버 배포](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerDeploy)  
  
-   [서버 구성](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerConfig2)  
  
-   [서버 관리](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerManage)  
  
-   [클라이언트 환경](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ClientXP)  

  
###  <a name="BKMK_ServerDeploy"></a> 서버 배포  
 다음과 같은 서버 배포 시나리오를 테스트할 수 있습니다.  
  
-   랩 환경에서 도메인 컨트롤러로 Windows Server 2012 R2를 실행 하는 서버를 배포 하 고 Windows Server Essentials Experience 역할을 설치 합니다.  
  
-   랩 환경에서 Windows Server 2012 R2를 실행 하는 서버를 배포 하 고이 서버를 기존 도메인에 가입 후 Windows Server Essentials Experience 역할을 설치 합니다.  
  
-   필요한 경우 Windows Server Essentials 이미지를 사용자 지정합니다.  
  
-   무인 파일 및 Windows PowerShell을 사용하여 Windows Server Essentials 배포를 자동화합니다.  
  
-   Windows Small Business Server를 실행하는 온-프레미스 서버를 Windows Server Essentials를 실행하는 호스트된 서버로 마이그레이션합니다.  
  
###  <a name="BKMK_ServerConfig2"></a> 서버 구성  
 다음과 같은 서버 구성 시나리오를 테스트할 수 있습니다.  
  
-   원격 액세스(가상 사설망, 원격 웹 액세스 및 DirectAccess)를 구성합니다.  
  
-   저장소 및 서버 폴더를 구성합니다.  
  
-   BranchCache를 설정합니다.  
  
-   (해당하는 경우) 서버 백업, 온라인 백업, 클라이언트 백업 및 파일 히스토리를 구성합니다.  
  
-   (해당하는 경우) 저장소 공간을 구성하고 관리합니다.  
  
-   (해당하는 경우) 전자 메일 솔루션 통합(Office 365 및 호스트된 Exchange Server)을 구성합니다.  
  
-   (해당하는 경우) 다른 Microsoft 온라인 서비스와의 통합을 구성합니다.  
  
-   (해당하는 경우) 미디어 서버를 구성합니다.  
  
###  <a name="BKMK_ServerManage"></a> 서버 관리  
 다음과 같은 서버 관리 시나리오를 테스트할 수 있습니다.  
  
-   사용자 및 그룹을 관리합니다.  
  
-   경고 메일 알림을 구성하고 수신합니다.  
  
-   모범 사례 분석기를 실행하여 오류 또는 경고 메시지가 있는지 확인합니다.  
  
-   System Center Operations Manager 팩을 구성합니다.  
  
-   운영 체제가 손상될 경우를 대비하여 서버 복구를 구성합니다.  
  
###  <a name="BKMK_ClientXP"></a> 클라이언트 환경  
 다음과 같은 최종 사용자 시나리오를 테스트할 수 있습니다.  
  
-   인터넷을 통해 클라이언트를 배포합니다(PC 또는 Mac 운영 체제).  
  
-   클라이언트에서 실행 패드를 사용하여 공유 폴더에 액세스합니다.  
  
-   다양한 장치(PC, 휴대폰 및 태블릿)에서 원격 웹 액세스를 통해 서버 자산에 액세스합니다.  
  
-   Windows Phone용 내 서버 앱에 액세스합니다.  
  
-   (해당하는 경우) 파일 히스토리, 클라이언트 백업 및 복원과 폴더 리디렉션에 액세스합니다.  
  
-   (해당하는 경우) 메일 통합 환경을 확인합니다.  
  
##  <a name="BKMK_Support"></a> 지원 정보  
 Windows Server Essentials 소프트웨어 개발 키트 (SDK) Windows Server Essentials 평가 및 배포 키트 (ADK)를 다운로드할 수 있습니다.  
  
-   [Windows Server Essentials 소프트웨어 개발 키트](https://msdn.microsoft.com/library/gg513877.aspx)SDK  
  
-   [사용자 지정 및 Windows Server 2012 R2에서 Windows Server Essentials를 배포 합니다.](https://technet.microsoft.com/library/dn293241.aspx)  
  
## <a name="see-also"></a>참조  
  
-   [Windows Server Essentials의 새로운 기능](../get-started/what-s-new.md)  

-   [Windows Server Essentials 설치](Install-Windows-Server-Essentials.md)  

-   [Windows Server Essentials 시작](../get-started/get-started.md)
