---
title: 1 단계 DirectAccess 인프라 구성
description: 이 항목은 Windows Server 2016에 대 한 기존 원격 액세스 (VPN) 배포에 DirectAccess 추가 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5dc529f7-7bc3-48dd-b83d-92a09e4055c4
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4437101c6cde25ebb370fe54a2f8ef821997f15d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388773"
---
# <a name="step-1-configure-the-directaccess-infrastructure"></a>1 단계 DirectAccess 인프라 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 기존 VPN 배포에서 DirectAccess를 사용하는 데 필요한 인프라를 구성하는 방법에 대해 설명합니다. 에 설명 된 계획 단계를 완료 한 확인 배포 단계를 시작 하기 전에 [1 단계: DirectAccess 인프라 계획](Step-1-Plan-DirectAccess-Infrastructure.md)합니다.  
  
|태스크|설명|  
|----|--------|  
|서버 네트워크 설정 구성|원격 액세스 서버에서 서버 네트워크 설정을 구성합니다.|  
|회사 네트워크의 라우팅을 구성합니다.|트래픽이 적절히 라우팅되도록 회사 네트워크의 라우팅을 구성합니다.|  
|방화벽 구성|필요한 경우 추가 방화벽을 구성합니다.|  
|CA 및 인증서 구성|DirectAccess 사용 마법사는 사용자 이름 및 암호를 사용하여 인증하는 기본 제공 Kerberos 프록시를 구성합니다. 또한 원격 액세스 서버에서 IP-HTTPS 인증서를 구성합니다.|  
|DNS 서버 구성|원격 액세스 서버에 대한 DNS 설정을 구성합니다.|  
|Active Directory 구성|클라이언트 컴퓨터를 Active Directory 도메인에 가입시킵니다.|  
|GPO 구성|필요한 경우 배포에 사용되는 GPO를 구성합니다.|  
|보안 그룹 구성|DirectAccess 클라이언트 컴퓨터를 포함할 보안 그룹 및 배포에 필요한 기타 보안 그룹을 구성합니다.|  
|네트워크 위치 서버 구성|DirectAccess 사용 마법사는 DirectAccess 서버에서 네트워크 위치 서버를 구성합니다.|  
  
## <a name="ConfigNetworkSettings"></a>서버 네트워크 설정 구성  
IPv4 및 IPv6을 사용하는 환경에 단일 서버를 배포하려면 다음 네트워크 인터페이스 설정이 필요합니다. 모든 IP 주소를 사용 하 여 구성 된 **어댑터 설정 변경** 에 **Windows 네트워크 및 공유 센터**합니다.  
  
-   에지 토폴로지  
  
    -   하나의 인터넷 연결 공용 고정 IPv4 또는 IPv6 주소  
  
    -   단일 내부 고정 IPv4 또는 IPv6 주소  
  
-   NAT 장치 뒤(네트워크 어댑터 2개)  
  
    -   단일 내부 네트워크 연결 고정 IPv4 또는 IPv6 주소  
  
-   NAT 장치 뒤(네트워크 어댑터 1개)  
  
    -   단일 고정 IPv4 또는 IPv6 주소  
  
> [!NOTE]  
> 원격 액세스 서버에 두 개의 네트워크 어댑터(하나는 도메인 프로필에서 분류되고 다른 하나는 공용/프라이빗 프로필에서 분류됨)가 있지만 단일 NIC 토폴로지를 사용하려는 경우 권장 사항은 다음과 같습니다.  
>   
> 1.  두 번째 NIC도 도메인 프로필에서 분류되어야 합니다(권장).  
> 2.  두 번째 NIC를 도메인 프로필용으로 구성할 수 없는 경우 다음 Windows PowerShell 명령을 사용하여 DirectAccess IPsec 정책의 범위를 모든 프로필로 수동으로 지정해야 합니다.  
>   
>     ```  
>     $gposession = Open-NetGPO -PolicyStore <Name of the server GPO>  
>     Set-NetIPsecRule -DisplayName <Name of the IPsec policy> -GPOSession $gposession -Profile Any  
>     Save-NetGPO -GPOSession $gposession  
>     ```  
  
## <a name="ConfigRouting"></a>회사 네트워크에서 라우팅 구성  
다음과 같이 회사 네트워크의 라우팅을 구성합니다.  
  
-   조직에 기본 IPv6이 배포된 경우 내부 네트워크의 라우터가 원격 액세스 서버를 통해 IPv6 트래픽을 다시 라우팅할 수 있도록 경로를 추가합니다.  
  
-   원격 액세스 서버에서 조직의 IPv4 및 IPv6 경로를 수동으로 구성합니다. 조직(/48) IPv6 접두사가 있는 모든 트래픽이 내부 네트워크로 전달되도록 게시된 경로를 추가합니다. 또한 IPv4 트래픽의 경우 내부 네트워크로 IPv4 트래픽이 전달되도록 명시적인 경로를 추가합니다.  
  
## <a name="ConfigFirewalls"></a>방화벽 구성  
배포에서 추가 방화벽을 사용하는 경우 원격 액세스 서버가 IPv4 인터넷에 있으면 원격 액세스 트래픽에 대해 다음 인터넷 연결 방화벽 예외를 적용합니다.  
  
-   6to4 트래픽-IP 프로토콜 41 인바운드 및 아웃 바운드입니다.  
  
-   IP HTTPS 전송 제어 프로토콜 (TCP) 대상 포트 443 및 TCP 포트 443 아웃 바운드 원본입니다. 원격 액세스 서버에 단일 네트워크 어댑터가 포함되고 네트워크 위치 서버가 원격 액세서 서버에 있는 경우 TCP 포트 62000도 필요합니다.  
  
추가 방화벽을 사용하는 경우 원격 액세스 서버가 IPv6 인터넷에 있으면 원격 액세스 트래픽에 대해 다음 인터넷 연결 방화벽 예외를 적용합니다.  
  
-   IP 프로토콜 50  
  
-   UDP 대상 포트 500 인바운드, UDP 원본 포트 500 아웃바운드  
  
추가 방화벽을 사용하는 경우 원격 액세스 트래픽에 대해 다음 내부 네트워크 방화벽 예외를 적용합니다.  
  
-   ISATAP 프로토콜 41 인바운드 및 아웃 바운드  
  
-   TCP/UDP - 모든 IPv4/IPv6 트래픽  
  
## <a name="ConfigCAs"></a>Ca 및 인증서 구성  
DirectAccess 사용 마법사는 사용자 이름 및 암호를 사용하여 인증하는 기본 제공 Kerberos 프록시를 구성합니다. 또한 원격 액세스 서버에서 IP-HTTPS 인증서를 구성합니다.  
  
### <a name="ConfigCertTemp"></a>인증서 템플릿 구성  
내부 CA를 사용하여 인증서를 발급하는 경우 IP-HTTPS 인증서 및 네트워크 위치 서버 웹 사이트 인증서용 인증서 템플릿을 구성해야 합니다.  
  
##### <a name="to-configure-a-certificate-template"></a>인증서 템플릿을 구성하려면  
  
1.  내부 CA에서 인증서 템플릿을에 설명 된 대로 만듭니다 [인증서 템플릿 만들기](https://technet.microsoft.com/library/cc731705.aspx)합니다.  
  
2.  에 설명 된 대로 인증서 템플릿을 배포 [인증서 템플릿 배포](https://technet.microsoft.com/library/cc770794.aspx)합니다.  
  
### <a name="configure-the-ip-https-certificate"></a>IP-HTTPS 인증서 구성  
원격 액세스에는 원격 액세스 서버에 대한 IP-HTTPS 연결을 인증할 IP-HTTPS 인증서가 필요합니다. IP-HTTPS 인증서에 대한 인증서 옵션에는 다음 세 가지가 있습니다.  
  
-   **공용**-타사에서 제공 합니다.  
  
    IP-HTTPS 인증에 사용되는 인증서. 인증서 주체 이름이 와일드카드가 아닌 경우에는 원격 액세스 서버 IP-HTTPS 연결에만 사용되는 외부에서 확인 가능한 FQDN URL이어야 합니다.  
  
-   **개인**-아직 존재 하지 않는 경우에 다음이 필요 합니다.  
  
    -   IP-HTTPS 인증에 사용되는 웹 사이트 인증서. 인증서 주체는 인터넷에서 연결할 수 있는 외부에서 확인 가능한 FQDN(정규화된 도메인 이름)이어야 합니다.  
  
    -   공개적으로 확인 가능한 FQDN에서 연결할 수 있는 CRL(인증서 해지 목록) 배포 지점  
  
-   **자체 서명**-아직 존재 하지 않는 경우에 다음이 필요 합니다.  
  
    > [!NOTE]  
    > 멀티 사이트 배포에는 자체 서명된 인증서를 사용할 수 없습니다.  
  
    -   IP-HTTPS 인증에 사용되는 웹 사이트 인증서. 인증서 주체는 인터넷에서 연결할 수 있는 외부에서 확인 가능한 FQDN이어야 합니다.  
  
    -   공개적으로 확인 가능한 FQDN(정규화된 도메인 이름)에서 연결할 수 있는 CRL 배포 지점  
  
IP-HTTPS 인증에 사용되는 웹 사이트 인증서는 다음 요구 사항을 충족해야 합니다.  
  
-   인증서의 일반 이름이 IP-HTTPS 사이트의 이름과 일치해야 합니다.  
  
-   주체 필드에 원격 액세스 서버 외부 연결 어댑터의 IPv4 주소 또는 IP-HTTPS URL의 FQDN을 지정합니다.  
  
-   확장된 키 사용 필드의 경우 서버 인증 OID(개체 식별자)를 사용합니다.  
  
-   CRL 배포 지점 필드의 경우 인터넷에 연결된 DirectAccess 클라이언트에서 액세스할 수 있는 CRL 배포 지점을 지정합니다.  
  
-   IP-HTTPS 인증서에 프라이빗 키가 있어야 합니다.  
  
-   IP-HTTPS 인증서를 개인 저장소로 직접 가져와야 합니다.  
  
-   IP-HTTPS 인증서 이름에 와일드카드를 사용할 수 있습니다.  
  
##### <a name="to-install-the-ip-https-certificate-from-an-internal-ca"></a>내부 CA의 IP-HTTPS 인증서를 설치하려면  
  
1.  원격 액세스 서버에서:에 **시작** 화면에서 입력**mmc.exe**, 한 다음 ENTER를 누릅니다.  
  
2.  MMC 콘솔의 **파일** 메뉴에서 **스냅인 추가/제거**를 클릭합니다.  
  
3.  에 **추가 / 제거 스냅인** 대화 상자를 클릭 **인증서**, 클릭 **추가**, 클릭 **컴퓨터 계정**, 클릭 **다음**, 클릭 **로컬 컴퓨터**, 클릭 **마침**, 클릭 하 고 **확인**합니다.  
  
4.  인증서 스냅인의 콘솔 트리에서 **인증서(로컬 컴퓨터)\개인\인증서**를 엽니다.  
  
5.  **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 가리킨 다음 **새 인증서 요청**을 클릭합니다.  
  
6.  **다음** 을 두 번 클릭합니다.  
  
7.  에 **인증서 요청** 페이지 인증서 템플릿에 대 한 확인란을 선택 하 고 필요한 경우 클릭 **이 인증서를 등록 하려면 추가 정보가 필요**합니다.  
  
8.  **인증서 속성** 대화 상자의 **주체** 탭에 있는 **주체 이름** 영역 내 **유형**에서 **일반 이름**을 선택합니다.  
  
9. **값**, 원격 액세스 서버 외부 연결 어댑터의 IPv4 주소 또는 IP-HTTPS URL의 FQDN을 지정 하 고 클릭 한 다음 **추가**합니다.  
  
10. 에 **대체 이름** 영역에서 **형식**, 선택, **DNS**합니다.  
  
11. **값**, 원격 액세스 서버 외부 연결 어댑터의 IPv4 주소 또는 IP-HTTPS URL의 FQDN을 지정 하 고 클릭 한 다음 **추가**합니다.  
  
12. **일반** 탭의 **이름**에 인증서를 식별하는 데 도움이 되는 이름을 입력할 수 있습니다.  
  
13. 에 **확장** 탭 옆에 **확장 키 용도**, 화살표를 클릭 하 고 서버 인증에 있는지 확인 하십시오는 **선택한 옵션** 목록입니다.  
  
14. 클릭 **확인**, 클릭 **등록**, 를 클릭 하 고 **마침**합니다.  
  
15. 인증서 스냅인의 세부 정보 창에서 새 인증서가 서버 인증 용도로 등록되었는지 확인합니다.  
  
## <a name="ConfigDNS"></a>DNS 서버 구성  
배포의 내부 네트워크에 대한 네트워크 위치 서버 웹 사이트의 DNS 항목을 수동으로 구성해야 합니다.  
  
### <a name="NLS_DNS"></a>네트워크 위치 서버 및 웹 프로브 DNS 레코드를 만들려면  
  
1.  내부 네트워크 DNS 서버: **시작** 화면에서 * * dnsmgmt.msc * *를 입력 한 다음 enter 키를 누릅니다.  
  
2.  **DNS 관리자** 콘솔의 왼쪽 창에서 도메인에 대한 정방향 조회 영역을 확장합니다. 도메인을 마우스 오른쪽 단추로 클릭하고 **새 호스트(A 또는 AAAA)** 를 클릭합니다.  
  
3.  에 **새 호스트** 대화 상자는 **이름 (부모 도메인 이름 사용 비어 있는 경우)** 상자에 네트워크 위치 서버 웹 사이트 (이 이름은 DirectAccess 클라이언트는 네트워크 위치 서버에 연결 하는 데 사용)에 대 한 DNS 이름을 입력 합니다. 에 **IP 주소** 상자에 네트워크 위치 서버의 IPv4 주소를 입력 한 다음 클릭 **호스트 추가할**합니다. 에 **DNS** 대화 상자를 클릭 하 여 **확인**합니다.  
  
4.  **새 호스트** 대화 상자의 **이름(입력하지 않으면 부모 도메인 이름 사용)** 상자에 웹 검색의 DNS 이름(기본 웹 검색의 이름은 directaccess-webprobehost)을 입력합니다. **IP 주소** 상자에 웹 검색의 IPv4 주소를 입력하고 **호스트 추가**를 클릭합니다. directaccess-corpconnectivityhost 및 수동으로 만든 모든 연결 검증 도구에 대해 이 프로세스를 반복합니다. 에 **DNS** 대화 상자를 클릭 하 여 **확인**합니다.  
  
5.  **완료**를 클릭합니다.  

![Windows PowerShell](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure_3/PowerShellLogoSmall.gif)***<em>windows powershell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
Add-DnsServerResourceRecordA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv4Address <network_location_server_IPv4_address>  
Add-DnsServerResourceRecordAAAA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv6Address <network_location_server_IPv6_address>  
```  
  
다음에 대한 DNS 항목도 구성해야 합니다.  
  
-   **IP-HTTPS 서버**-DirectAccess 클라이언트는 인터넷에서 원격 액세스 서버의 DNS 이름을 확인할 수 있어야 합니다.  
  
-   **CRL 해지 확인**-DirectAccess에서는 DirectAccess 클라이언트 및 원격 액세스 서버 간의 IP-HTTPS 연결 및 DirectAccess 클라이언트와 네트워크 위치 서버 간의 HTTPS 기반 연결에 대 한 인증서 해지를 확인 합니다. 두 경우 모두 DirectAccess 클라이언트에서 CRL 배포 지점 위치를 확인하고 액세스할 수 있어야 합니다.  
  
## <a name="ConfigAD"></a>Active Directory 구성  
원격 액세스 서버와 모든 DirectAccess 클라이언트 컴퓨터는 Active Directory 도메인에 가입되어 있어야 합니다. DirectAccess 클라이언트 컴퓨터에는 다음 도메인 유형 중 하나의 구성원이어야 합니다.  
  
-   원격 액세스 서버와 동일한 포리스트에 속한 도메인  
  
-   원격 액세스 서버 포리스트와 양방향 트러스트 관계에 있는 포리스트에 속한 도메인  
  
-   원격 액세스 서버 도메인과 양방향 트러스트 관계에 있는 도메인  
  
#### <a name="to-join-client-computers-to-the-domain"></a>도메인에 클라이언트 컴퓨터를 가입시키려면  
  
1.  에 **시작** 화면에서 입력 **explorer.exe**, 한 다음 ENTER를 누릅니다.  
  
2.  컴퓨터 아이콘을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **속성**합니다.  
  
3.  **시스템** 페이지에서 **고급 시스템 설정**을 클릭합니다.  
  
4.  **시스템 속성** 대화 상자의 **컴퓨터 이름** 탭에서 **변경**을 클릭합니다.  
  
5.  **컴퓨터 이름**, 서버를 도메인에 가입 하는 경우에 컴퓨터 이름을 변경 하려는 경우 컴퓨터의 이름을 입력 합니다. **소속 그룹**에서 **도메인**을 클릭하고 서버를 가입시킬 도메인 이름(예: corp.contoso.com)을 입력한 다음 **확인**을 클릭합니다.  
  
6.  사용자 이름 및 암호를 묻는 메시지가 나타나면 컴퓨터를 도메인에 가입시킬 권한이 있는 사용자의 사용자 이름 및 암호를 입력한 다음 **확인**을 클릭합니다.  
  
7.  도메인을 시작한다는 내용의 대화 상자가 표시되면 **확인**을 클릭합니다.  
  
8.  컴퓨터를 다시 시작해야 한다는 메시지가 표시되면 **확인**을 클릭합니다.  
  
9. 에 **시스템 속성** 대화 상자에서 닫기를 클릭 합니다. 클릭 **지금 다시 시작** 메시지가 표시 되 면 합니다.  
  
![Windows PowerShell](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure_3/PowerShellLogoSmall.gif)***<em>windows powershell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
아래의 Add-Computer 명령을 입력한 후 도메인 자격 증명을 제공해야 합니다.  
  
```  
Add-Computer -DomainName <domain_name>  
Restart-Computer  
```  
  
## <a name="ConfigGPOs"></a>Gpo 구성  
원격 액세스를 배포 하려면 최소 두 개의 그룹 정책 개체의 필요한: DirectAccess 클라이언트 컴퓨터에 대 한 설정을 포함 하 고 하나의 그룹 정책 개체에는 원격 액세스 서버에 대 한 설정이 포함 되어 있습니다. 원격 액세스를 구성 하는 경우 마법사는 자동으로 필요한 그룹 정책 개체를 만듭니다. 그러나 조직에서 명명 규칙을 적용 또는 만들기 또는 그룹 정책 개체를 편집 하는 데 필요한 권한이 없는 경우 원격 액세스를 구성 하기 전에 만들 수 있어야 합니다.  
  
그룹 정책 개체를 만들려면 참조 [만들고 그룹 정책 개체 편집](https://technet.microsoft.com/library/cc754740.aspx)합니다.  
  
> [!IMPORTANT]  
> 관리자는 다음이 단계를 사용 하 여 조직 구성 단위에 DirectAccess 그룹 정책 개체를 수동으로 연결할 수 있습니다.  
>   
> 1.  DirectAccess를 구성하기 전에, 만든 GPO를 각 조직 구성 단위에 연결합니다.  
> 2.  클라이언트 컴퓨터의 보안 그룹을 지정하여 DirectAccess를 구성합니다.  
> 3.  원격 액세스 관리자 수도 도메인 그룹 정책 개체에 연결 하는 권한이 없을 수도 있습니다. 두 경우 모두의 그룹 정책 개체를 자동으로 구성 됩니다. GPO가 OU에 이미 연결되어 있는 경우에는 연결이 제거되지 않으며 GPO가 도메인에 연결되지 않습니다. 서버 GPO의 경우 OU에 서버 컴퓨터 개체가 있어야 하며, 그렇지 않으면 GPO가 도메인의 루트에 연결됩니다.  
> 4.  DirectAccess 마법사를 실행 하기 전에 OU에 연결 수행 하지 않은 하는 경우 다음 구성을 완료 한 후 도메인 관리자에 연결할 수 DirectAccess 그룹 정책 개체 필요한 조직 구성 단위. 이 도메인 연결은 제거할 수 있습니다. 조직 구성 단위에 그룹 정책 개체에 연결을 확인할 수 있습니다 단계 [여기](https://technet.microsoft.com/library/cc732979.aspx)합니다.  
  
> [!NOTE]  
> 그룹 정책 개체를 수동으로 만든 경우 그룹 정책 개체는 사용할 수 없는 DirectAccess 구성 중 불가능 해제 합니다. 그룹 정책 개체 관리 컴퓨터에 가장 가까운 도메인 컨트롤러에 복제 되지 않을 수 있습니다. 이 경우 관리자는 복제가 완료될 때까지 기다리거나 복제를 강제로 실행할 수 있습니다.  
  
## <a name="ConfigSGs"></a>보안 그룹 구성  
클라이언트 컴퓨터 그룹 정책 개체에에서 포함 된 DirectAccess 설정은 원격 액세스를 구성할 때 지정 하는 보안 그룹의 구성원 인 컴퓨터에만 적용 됩니다. 또한 보안 그룹을 사용하여 응용 프로그램 서버를 관리하는 경우 이러한 서버의 보안 그룹을 만듭니다.  
  
### <a name="Sec_Group"></a>DirectAccess 클라이언트에 대 한 보안 그룹을 만들려면  
  
1.  에 **시작** 화면에서 입력**dsa.msc**, 한 다음 ENTER를 누릅니다. 에 **Active Directory 사용자 및 컴퓨터** 보안 그룹에 포함 되 면 마우스 오른쪽 단추로 클릭 하는 도메인을 확장 하는 콘솔의 왼쪽된 창에서 **사용자**, 가리킨 **새로**, 클릭 하 고 **그룹**합니다.  
  
2.  에 **새 개체-그룹** 대화 상자의 **그룹 이름**, 보안 그룹의 이름을 입력 합니다.  
  
3.  아래에서 **그룹 범위**, 클릭 **Global**, 아래에서 **그룹 종류**, 클릭 **보안**, 를 클릭 하 고 **확인**합니다.  
  
4.  DirectAccess 클라이언트 컴퓨터 보안 그룹을 두 번 클릭 하 고 속성 대화 상자에서 클릭 된 **멤버** 탭 합니다.  
  
5.  **구성원** 탭에서 **추가**를 클릭합니다.  
  
6.  에 **사용자 선택, 연락처, 컴퓨터 또는 서비스 계정** 대화 상자에서 클라이언트 컴퓨터를 DirectAccess에 사용 하도록 설정 하 고 클릭 하 고 선택 **확인**합니다.  
  
![Windows PowerShell](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure_3/PowerShellLogoSmall.gif)**Windows powershell 해당 명령**  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
New-ADGroup -GroupScope global -Name <DirectAccess_clients_group_name>  
Add-ADGroupMember -Identity DirectAccess_clients_group_name -Members <computer_name>  
```  
  
## <a name="ConfigNLS"></a>네트워크 위치 서버 구성  
네트워크 위치 서버는 항상 사용 가능한 서버여야 하며, DirectAccess 클라이언트에서 신뢰할 수 있는 유효한 SSL 인증서가 있어야 합니다. 네트워크 위치 서버 인증서에 대한 인증서 옵션에는 다음 두 가지가 있습니다.  
  
-   **개인**-아직 존재 하지 않는 경우에 다음이 필요 합니다.  
  
    -   네트워크 위치 서버에 사용되는 웹 사이트 인증서. 인증서 주체는 네트워크 위치 서버의 URL이어야 합니다.   
  
    -   내부 네트워크에서 항상 사용할 수 있는 CRL 배포 지점  
  
-   **자체 서명**-아직 존재 하지 않는 경우에 다음이 필요 합니다.  
  
    > [!NOTE]  
    > 멀티 사이트 배포에는 자체 서명된 인증서를 사용할 수 없습니다.  
  
    -   네트워크 위치 서버에 사용되는 웹 사이트 인증서. 인증서 주체는 네트워크 위치 서버의 URL이어야 합니다.  
  
> [!NOTE]  
> 네트워크 위치 서버가 원격 액세스 서버에 있는 경우에는 제공한 서버 인증서에 바인딩되는 원격 액세스를 구성할 때 웹 사이트가 자동으로 만들어집니다.  
  
#### <a name="to-install-the-network-location-server-certificate-from-an-internal-ca"></a>내부 CA의 네트워크 위치 서버 인증서를 설치하려면  
  
1.  네트워크 위치 서버 웹 사이트를 호스팅하는 서버에서:에 **시작** 화면에서 입력**mmc.exe**, 한 다음 ENTER를 누릅니다.  
  
2.  MMC 콘솔의 **파일** 메뉴에서 **스냅인 추가/제거**를 클릭합니다.  
  
3.  에 **추가 / 제거 스냅인** 대화 상자를 클릭 **인증서**, 클릭 **추가**, 클릭 **컴퓨터 계정**, 클릭 **다음**, 클릭 **로컬 컴퓨터**, 클릭 **마침**, 클릭 하 고 **확인**합니다.  
  
4.  인증서 스냅인의 콘솔 트리에서 **인증서(로컬 컴퓨터)\개인\인증서**를 엽니다.  
  
5.  **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 가리킨 다음 **새 인증서 요청**을 클릭합니다.  
  
6.  **다음** 을 두 번 클릭합니다.  
  
7.  에 **인증서 요청** 페이지 인증서 템플릿에 대 한 확인란을 선택 하 고 필요한 경우 클릭 **이 인증서를 등록 하려면 추가 정보가 필요**합니다.  
  
8.  **인증서 속성** 대화 상자의 **주체** 탭에 있는 **주체 이름** 영역 내 **유형**에서 **일반 이름**을 선택합니다.  
  
9. **값**, 네트워크 위치 서버 웹 사이트의 FQDN을 입력 하 고 클릭 한 다음 **추가**합니다.  
  
10. 에 **대체 이름** 영역에서 **형식**, 선택, **DNS**합니다.  
  
11. **값**, 네트워크 위치 서버 웹 사이트의 FQDN을 입력 하 고 클릭 한 다음 **추가**합니다.  
  
12. **일반** 탭의 **이름**에 인증서를 식별하는 데 도움이 되는 이름을 입력할 수 있습니다.  
  
13. 클릭 **확인**, 클릭 **등록**, 를 클릭 하 고 **마침**합니다.  
  
14. 인증서 스냅인의 세부 정보 창에서 새 인증서가 서버 인증 용도로 등록되었는지 확인합니다.  
  

  


