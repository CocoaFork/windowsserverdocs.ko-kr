---
title: Configure a Multi-Forest Deployment
description: 이 항목은 Windows Server 2016에서 다중 포리스트 환경에서 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c8feff2-cae1-4376-9dfa-21ad3e4d5d99
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bf9222293dfd22b6f32cf00021f34b44c555e340
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281101"
---
# <a name="configure-a-multi-forest-deployment"></a>Configure a Multi-Forest Deployment

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 여러 가능한 시나리오에서 원격 액세스 다중 포리스트 배포를 구성하는 방법에 대해 설명합니다. 모든 시나리오에서는 현재 DirectAccess가 이름이 Forest1인 단일 포리스트에 배포되어 있으며 DirectAccess를 이름이 Forest2인 새로운 포리스트에서 사용할 수 있도록 구성한다고 가정합니다.  
  
## <a name="AccessForest2"></a>Forest2에서 리소스에 액세스  
이 시나리오에서는 DirectAccess가 이미 Forest1에 배포되었으며 Forest1의 클라이언트가 회사 네트워크에 액세스하도록 구성되었다고 가정합니다. 기본적으로 DirectAccess를 통해 연결되어 있는 클라이언트는 Forest1의 리소스에만 액세스할 수 있으며 Forest2의 서버에는 액세스할 수 없습니다.  
  
#### <a name="to-enable-directaccess-clients-to-access-resources-from-forest2"></a>DirectAccess 클라이언트가 Forest2의 리소스에 액세스할 수 있도록 설정하려면  
  
1.  Forest2의 DNS 접미사가 Forest1의 DNS 접미사의 일부가 아니라면 Forest2의 도메인 접미사에 NRPT 규칙을 추가하고 선택적으로 Forest2의 도메인 접미사를 DNS 접미사 검색 목록에 추가합니다.  
  
2.  IPv6가 내부 네트워크에 배포된 경우에는 Forest2의 관련된 내부 IPv6 접두사를 추가하세요.  
  
## <a name="EnableForest2DA"></a>Forest2의 클라이언트가 DirectAccess를 통해 연결 하도록 설정  
이 시나리오에서는 Forest2의 클라이언트가 회사 네트워크에 액세스하도록 원격 액세스 배포를 구성합니다. Forest2의 클라이언트 컴퓨터에 필요한 보안 그룹을 생성했다고 가정합니다.   
  
#### <a name="to-allow-clients-from-forest2-to-access-the-corporate-network"></a>Forest2의 클라이언트가 회사 네트워크에 액세스할 수 있도록 허용하려면  
  
1.  Forest2 클라이언트의 보안 그룹을 추가합니다.  
  
2.  Forest2의 DNS 접미사가 Forest1의 DNS 접미사의 일부가 없는 경우 인증에 대 한 도메인 컨트롤러에 대 한 액세스를 사용 하도록 설정 하려면 Forest2의 클라이언트의 도메인 접미사를 사용 하 여 NRPT 규칙을 추가 하 고 선택적으로 Forest2의 도메인 접미사를 DNS suf에 추가 검색 목록을 수정 합니다. 
  
3.  Forest2에 내부 IPv6 접두사를 추가하여 인증을 위해 DirectAccess에서 도메인 컨트롤러로의 IPsec 터널을 생성하도록 설정합니다.  
  
4.  관리 서버 목록을 새로 고칩니다.  
  
## <a name="AddEPForest2"></a>Forest2에서 진입점 추가  
이 시나리오에서는 DirectAccess가 Forest1에서 멀티 사이트 구성으로 배포되어 있고 이름이 DA2인 원격 액세스 서버를 Forest2에서 기존 DirectAccess 멀티 사이트 배포로 진입점으로서 추가하고자 한다고 가정합니다.  
  
#### <a name="to-add-a-remote-access-server-from-forest2-as-an-entry-point"></a>Forest2의 원격 액세스 서버를 진입점으로 추가하려면  
  
1.  원격 액세스 관리자가 DA2의 도메인에서 GPO를 작성할 권한이 있으며 원격 액세스 관리자가 DA2의 로컬 관리자인지 확인합니다.  
  
2.  DA2를 진입점으로 추가합니다.   
  
3.  Forest2의 도메인 접미사에 NRPT 규칙을 추가하여 인증을 위해 도메인 컨트롤러에 액세스하도록 설정하고, 선택적으로 Forest2의 도메인 접미사를 DNS 접미사 검색 목록에 추가합니다.  
  
4.  필요한 경우 Forest2의 관련한 내부 IPv6 접두사를 추가하여 원격 액세스에서 회사 리소스로의 IPsec 터널을 설정하도록 하고 NCSI 검색이 제대로 작동하도록 합니다.  
  
5.  관리 서버 목록을 새로 고칩니다.  
  
## <a name="OTPMultiForest"></a>다중 포리스트 배포에서 OTP를 구성 합니다.  
OTP를 다중 포리스트 배포로 구성할 때에는 다음 용어를 참조합니다.  
  
-   루트 CA는 포리스트의 주 PKI 트리 CA입니다.  
  
-   엔터프라이즈 CA 모두 다른 Ca입니다.  
  
-   리소스 포리스트에 포리스트 루트 CA를 포함 하는 '관리 포리스트이며' 것으로 간주 됩니다.  
  
-   계정 포리스트의 모든 토폴로지에서 다른 포리스트의 합니다.  
  
이 절차에는 PowerShell 스크립트인 PKISync.ps1이 필요합니다. 참조 [AD CS: 크로스 포리스트 인증서 등록을 위한 PKISync.ps1 스크립트](https://technet.microsoft.com/library/ff961506.aspx)합니다.  
  
> [!NOTE]  
> 이 항목에는 설명한 절차의 일부를 자동화하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 참조 [Cmdlet를 사용 하 여](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
### <a name="BKMK_CertPub"></a>Ca 인증서 게시자로 구성  
  
1.  관리자 권한 명령 프롬프트에서 다음 명령을 실행하여 모든 포리스트의 전체 엔터프라이즈 CA에 대해 LDAP 조회 지원을 사용합니다.  
  
    ```  
    certutil -setreg Policy\EditFlags +EDITF_ENABLELDAPREFERRALS  
    ```  
  
2.  각 계정 포리스트에서 모든 엔터프라이즈 CA 컴퓨터 계정을 Active Directory Cert Publishers 보안 그룹에 추가합니다.  
  
3.  관리자 권한 명령 프롬프트에서 다음 명령을 실행하여 모든 포리스트의 전체 CA 컴퓨터에서 모든 certsvc 서비스를 다시 시작합니다.  
  
    ```  
    net stop certsvc && net start certsvc  
    ```  
  
4.  관리자 권한 명령 프롬프트에서 다음 명령을 실행하여 루트 CA 인증서를 추출합니다.  
  
    ```  
    certutil -config <Computer-Name>\<Root-CA-Name> -ca.cert <root-ca-cert-filename.cer>  
    ```  
  
    (루트 CA에서 명령을 실행 하는 경우에 연결 정보 인-config < 컴퓨터 이름 >을 생략할 수 있습니다\\< 루트-CA-이름 >)  
  
    1.  관리자 권한 명령 프롬프트에서 다음 명령을 실행하여 계정 포리스트 CA의 이전 단계에서 루트 CA 인증서를 가져옵니다.  
  
        ```  
        certutil -dspublish -f <root-ca-cert-filename.cer> RootCA  
        ```  
  
    2.  권한 부여 리소스 포리스트 인증서 템플릿 읽기/쓰기 권한을 합니다 \<계정 포리스트\>\\< 관리자 계정\>합니다.  
  
    3.  관리자 권한 명령 프롬프트에서 다음 명령을 실행하여 모든 리소스 포리스트 엔터프라이즈 CA 인증서를 추출합니다.  
  
        ```  
        certutil -config <Computer-Name>\<Enterprise-CA-Name> -ca.cert <enterprise-ca-cert-filename.cer>  
        ```  
  
        (루트 CA에서 명령을 실행 하는 경우에 연결 정보 인-config < 컴퓨터 이름 >을 생략할 수 있습니다\\< 루트-CA-이름 >)  
  
    4.  관리자 권한 명령 프롬프트에서 다음 명령을 실행하여 계정 포리스트 CA의 이전 단계에서 엔터프라이즈 CA 인증서를 가져옵니다.  
  
        ```  
        certutil -dspublish -f <enterprise-ca-cert-filename.cer> NTAuthCA  
        certutil -dspublish -f <enterprise-ca-cert-filename.cer> SubCA  
        ```  
  
    5.  발급된 인증서 템플릿 목록에서 계정 포리스트 OTP 인증서 템플릿을 제거합니다.  
  
### <a name="BKMK_DelImp"></a>삭제 하 고 OTP 인증서 템플릿 가져오기  
  
1.  OTP 인증서 템플릿을 계정 포리스트, 즉 Forest2에서 삭제합니다.  
  
2.  다음 PowerShell 명령을 사용하여 리소스 포리스트의 인증서 템플릿 및 Oid 개체를 각 계정 포리스트로 복사합니다.  
  
    ```  
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type Template -cn <DA OTP registration authority template common name>.  
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type Template -cn <Secure DA OTP logon certificate template common name>.  
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type Oid -f  
    ```  
  
### <a name="BKMK_Publish"></a>OTP 인증서 템플릿 게시  
  
-   새로 가져온 인증서 템플릿을 모든 계정 프리스트 CA에서 발급합니다.  
  
### <a name="BKMK_Extract"></a>압축을 풀고 CA를 동기화 합니다.  
  
1.  관리자 권한 명령 프롬프트에서 다음 명령을 실행하여 계정 포리스트에서 모든 엔터프라이즈 CA 인증서를 추출합니다.  
  
    ```  
    certutil -config <Computer-Name>\<Enterprise-CA-Name> -ca.cert <enterprise-ca-cert-filename.cer>  
    ```  
  
2.  다음 PowerShell 명령을 사용하여 CA를 계정 포리스트에서 리소스 포리스트로 전체 포리스트에 걸쳐 동기화합니다.  
  
    ```  
    .\PKISync.ps1 -sourceforest <account forest DNS> -targetforest <resource forest DNS> -type CA -cn <enterprise CA sanitized name> -f  
    ```  
  
3.  다음 PowerShell 명령을 사용하여 CA를 리소스 포리스트에서 계정 포리스트로 전체 포리스트에 걸쳐 동기화합니다.  
  
    ```  
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type CA -cn <enterprise CA sanitized name> -f  
    ```  
  
## <a name="configuration-procedures"></a>구성 절차  
다음 섹션에는 상기 시나리오 배포를 위한 구성 절차가 포함되어 있습니다. 절차를 완료한 후에는 시나리오로 돌아가 남은 단계를 계속 진행하세요.  
  
### <a name="NRPT_DNSSearchSuffix"></a>NRPT 규칙 및 DNS 접미사를 추가 합니다.  
DirectAccess를 통해 회사 네트워크에 연결하는 클라이언트는 NRPT(이름 확인 정책 테이블)를 사용하여 다른 리소스 주소를 확인하는 데 어떤 DNS 서버를 사용해야 하는지 결정합니다. 이렇게 하면 클라이언트가 회사 리소스 주소를 확인하여 DirectAccess의 지속적인 작동에 필요한 적절한 사내/사외 분류를 더욱 편리하게 유지할 수 있습니다. DirectAccess 구성 도구는 Forest1의 루트 DNS 접미사를 자동으로 감지하여 NRPT 테이블에 추가합니다. 그러나 Forest2의 FQDN 접미사는 NRPT 테이블에 자동으로 추가되지 않기 때문에 원격 액세스 관리자가 수동으로 추가해야 합니다.  
  
DNS 접미사 검색 목록을 사용하면 클라이언트가 FQDN 대신 짧은 레이블 이름을 사용할 수 있습니다. 원격 액세스 구성 도구를 사용하면 Forest1의 모든 도메인을 DNS 접미사 검색 목록에 자동으로 추가할 수 있습니다. 클라이언트가 Forest2 리소스에 대해 짧은 레이블 이름을 사용하도록 하려면 해당 이름을 수동으로 추가해야 합니다.  
  
##### <a name="to-add-a-dns-suffix-to-the-nrpt-table-and-domain-suffixes-to-the-dns-suffix-search-list"></a>DNS 접미사를 NRPT 테이블에 추가하고 도메인 접미사를 DNS 접미사 검색 목록에 추가하려면  
  
1.  원격 액세스 관리 콘솔 중간 창의 **3단계 인프라 서버** 영역에서 **편집**을 클릭합니다.  
  
2.  **네트워크 위치 서버** 페이지에서 **다음**을 클릭합니다.  
  
3.  **DNS** 페이지에 표시된 테이블에 Forest 2의 회사 네트워크 중 일부인 추가 이름 접미사를 입력합니다. **DNS 서버 주소**에 서버 주소를 수동으로 입력하거나 **감지**를 클릭합니다. 주소를 입력 하지 않으면, 새 항목 내용이 NRPT 예외로 적용 됩니다. 그리고 **다음**을 클릭합니다.  
  
4.  선택 사항: **DNS 접미사 검색 목록** 페이지에서 **새 접미사** 상자에 기타 다른 DNS 접미사를 추가하고 **추가**를 클릭합니다. 그리고 **다음**을 클릭합니다.  
  
5.  **관리** 페이지에서 **마침**을 클릭합니다.  
  
6.  원격 액세스 관리 콘솔의 중간 창에서 **마침**을 클릭합니다.  
  
7.  **원격 액세스 검토** 대화 상자에서 **적용**을 클릭합니다.  
  
8.  **원격 액세스 설정 마법사 설정 적용** 대화 상자에서 **닫기**를 클릭합니다.  
  
### <a name="IPv6Prefix"></a>내부 IPv6 접두사 추가  
  
> [!NOTE]  
> 내부 IPv6 접두사 추가는 IPv6가 내부 네트워크에 배포되어 있는 경우에만 의미가 있습니다.  
  
원격 액세스는 회사 리소스의 IPv6 접두사 목록을 관리합니다. DirectAccess를 통해 연결하는 클라이언트는 이와 같은 IPv6 접두사가 있는 리소스에만 액세스할 수 있습니다. 원격 액세스 관리 콘솔 및 Windows PowerShell 명령을 자동으로 Forest1의 IPv6 접두사를 추가 하 고 다른 포리스트의 접두사는 추가 되지 않을 수 때문에 Forest2의 접두사 중 누락 된을 수동으로 추가 해야 합니다.  
  
##### <a name="to-add-an-ipv6-prefix"></a>IPv6 접두사를 추가하려면  
  
1.  원격 액세스 관리 콘솔 중간 창의 **2단계 원격 액세스 서버** 영역에서 **편집**을 클릭합니다.  
  
2.  원격 액세스 설정 마법사에서 **접두사 구성**을 클릭합니다.  
  
3.  **접두사 구성** 페이지의 **내부 네트워크 IPv6 접두사**에 세미콜론으로 구분된 기타 다른 IPv6 접두사를 추가합니다. 예를 들면 2001:db8:1::/64;2001:db8:2::/64와 같습니다. 그리고 **다음**을 클릭합니다.  
  
4.  **인증** 페이지에서 **마침**을 클릭합니다.  
  
5.  원격 액세스 관리 콘솔의 중간 창에서 **마침**을 클릭합니다.  
  
6.  **원격 액세스 검토** 대화 상자에서 **적용**을 클릭합니다.  
  
7.  **원격 액세스 설정 마법사 설정 적용** 대화 상자에서 **닫기**를 클릭합니다.  
  
### <a name="SGs"></a>클라이언트 보안 그룹 추가  
DirectAccess를 통해 리소스에 액세스 하는 Forest2의 Windows 8 클라이언트 컴퓨터를 사용 하려면 원격 액세스 배포에 Forest2의 보안 그룹을 추가 해야 합니다.  
  
##### <a name="to-add-windows-8-client-security-groups"></a>Windows 8 클라이언트 보안 그룹을 추가하려면  
  
1.  원격 액세스 관리 콘솔 중간 창의 **1단계 원격 클라이언트** 영역에서 **편집**을 클릭합니다.  
  
2.  DirectAccess 클라이언트 설정 마법사에서 **그룹 선택**을 클릭한 다음 **그룹 선택** 페이지에서 **추가**를 클릭합니다.  
  
3.  **그룹 선택** 대화 상자에서 DirectAccess 클라이언트 컴퓨터를 포함한 보안 그룹을 선택합니다. 그리고 **다음**을 클릭합니다.  
  
4.  **네트워크 연결 길잡이** 페이지에서 **마침**을 클릭합니다.  
  
5.  원격 액세스 관리 콘솔의 중간 창에서 **마침**을 클릭합니다.  
  
6.  **원격 액세스 검토** 대화 상자에서 **적용**을 클릭합니다.  
  
7.  **원격 액세스 설정 마법사 설정 적용** 대화 상자에서 **닫기**를 클릭합니다.  
  
Forest2의 클라이언트 컴퓨터를 리소스에 액세스할 때 멀티 사이트 DirectAccess 통해 사용 하도록 설정 하는 Windows 7을 사용 하려면 각 진입점에 대 한 원격 액세스 배포에 Forest2의 보안 그룹을 추가 해야 합니다. Windows 7 보안 그룹을 추가 하는 것에 대 한 자세한 설명을 참조 합니다 **클라이언트 지원** 3.6에는 페이지입니다. 멀티 사이트 배포를 사용 하도록 설정 합니다.  
  
### <a name="RefreshMgmtServers"></a>관리 서버 목록 새로 고침  
원격 액세스는 DirectAccess 구성 GPO를 포함하는 모든 포리스트에서 인프라 서버를 자동으로 검색합니다. DirectAccess를 Forest1의 서버에 배포했다면 서버 GPO가 Forest1의 해당 도메인에 작성됩니다. Forest2의 클라이언트가 DirectAccess에 액세스할 수 있도록 설정한 경우 Forest2의 도메인에 클라이언트 GPO가 작성됩니다.  
  
DirectAccess를 통해 도메인 컨트롤러 및 System Center Configuration Manager에 액세스하도록 설정하려면 인프라 서버의 자동 검색 프로세스가 필요합니다. 검색 프로세스는 수동으로 시작해야 합니다.  
  
##### <a name="to-refresh-the-management-servers-list"></a>관리 서버 목록을 새로 고치려면  
  
1.  원격 액세스 관리 콘솔에서 **구성**을 클릭하고 **작업** 창에서 **관리 서버 새로 고침**을 클릭합니다.  
  
2.  **관리 서버를 새로 고치는 중** 대화 상자에서 **닫기**를 클릭합니다.  
  

