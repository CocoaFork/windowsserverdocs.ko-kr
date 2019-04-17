---
title: "Windows Server Essentials 대상 서버 마이그레이션 Windows SBS 2003 설정 및 데이터 이동"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67087ccb-d820-4642-8ca2-7d2d38714014
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 74375d65845a7a5e9c2d6752bdee49993b8cc791
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="move-windows-sbs-2003-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Windows Server Essentials 대상 서버 마이그레이션 Windows SBS 2003 설정 및 데이터 이동

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

다음과 같이 대상 서버 설정 및 데이터 이동 합니다.

1.  [대상 서버에 데이터를 복사](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)  
  
2.  [사용자 계정 Active Directory (선택 사항) Windows Server Essentials 대시보드를 가져오기](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_ImportADaccounts)  
  
3.  [(옵션) 이전 로그온 스크립트 제거](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_RemoveScripts)  
  
4.  [제거 레거시 Active Directory 그룹 정책 개체 (선택 사항)](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_RemoveLegacyADGPO)  
  
5.  [네트워크를 구성](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Configure)  
  
6.  [사용자 계정에 허용 된 컴퓨터 지도](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)  
 
##  <a name="BKMK_CopyData"></a>대상 서버에 데이터를 복사  
 대상 서버에 데이터 소스 서버에서 복사 하기 전에 다음과 같은 작업을 수행 합니다.  
  
-   각 폴더에 대 한 권한을 포함 하 여 원본 서버의 공유 폴더 목록을 검토 합니다. 만들거나 폴더 원본 서버에서 마이그레이션하는 폴더 구조 일치 하도록 대상 서버에 사용자 지정 합니다.  
  
-   각 폴더의 크기를 검토 하 고 대상 서버에 충분 한 공간이 있는지 확인 합니다.  
  
-   확인 원본 서버의 공유 폴더 읽기 전용 모든 사용자에 대해 대상 서버에 파일을 복사 하는 동안 없이 쓰기 드라이브에 장소를 될 수 있도록 합니다.  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>원본 서버에서 대상 서버에 데이터를 복사 하려면  
  
1.  대상 서버 도메인 관리자 권한으로 로그온 합니다.  
  
2.  클릭 **시작**, 입력 **cmd** 다음 enter 키를 차례로 검색 상자에 있습니다.  
  
3.  명령 프롬프트에서 다음 명령을 입력 하 고 enter 다음과 같습니다.  
  
    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`  
  
     위치:
     - \ < SourceServerName\ >은 원본 서버의 이름입니다.
     - \ < SharedSourceFolderName\ >은 원본 서버에서 공유 된 폴더의 이름입니다.
     - \ < DestinationServerName\ >는 대상 폴더의 이름
     - \ < SharedDestinationFolderName\ >는 공유 폴더 대상 서버의 데이터 복사할 수 있습니다.  
 
4.  원본 서버에서 마이그레이션하는 각 공유 폴더를 이전 단계를 반복 합니다.  
  
##  <a name="BKMK_ImportADaccounts"></a>사용자 계정 Active Directory (선택 사항) Windows Server Essentials 대시보드를 가져오기  
 기본적으로 원본 서버의 만든 모든 사용자 계정에서 Windows Server Essentials 대시보드도 이동 자동으로 않습니다. 그러나 일부 속성 마이그레이션 요구 사항을 충족 하지 않는 경우 Active Directory 사용자 계정의 자동 마이그레이션 실패 합니다. 사용자 Active Directory를 가져오려면 다음 Windows PowerShell cmdlet에 사용할 수 있습니다.  
  
#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>Windows Server Essentials 대시보드 Active Directory 사용자 계정 가져오려면  
  
1.  대상 서버 도메인 관리자 권한으로 로그온 합니다.  
  
2.  Windows PowerShell을 관리자 권한으로 엽니다.  
  
3.  다음 cmdlet 실행 여기서 `[AD username]` 가져올 Active Directory 사용자 계정 이름입니다.  
  
     `Import-WssUser SamAccountName [AD username]`  
  
##  <a name="BKMK_RemoveScripts"></a>(옵션) 이전 로그온 스크립트 제거  
 Windows SBS 2003 로그온 스크립트 소프트웨어를 설치 하 고 바탕 화면을 사용자 지정 등의 작업에 대 한 사용 합니다.  Windows Server Essentials 로그온 스크립트 그룹 정책 개체의 조합으로 나만의 Windows SBS 2003 로그온 스크립트를 바꿉니다.  
  
> [!NOTE]
>  Windows SBS 2003 로그온 스크립트를 수정 하는 경우 사용자 지정을 유지 하기 위해 스크립트 이름을 바꿔야 합니다.  
  
> [!NOTE]
>  Windows SBS 2003 로그온 스크립트를 사용 하 여 추가 된 사용자 계정에만 적용는 **새 사용자에 게 추가 마법사**합니다.  
  
#### <a name="to-remove-the-windows-sbs-2003-logon-scripts"></a>Windows SBS 2003 로그온 스크립트 제거 하려면  
  
1.  클릭 **시작**를 가리킨 **관리 도구**을 차례로 클릭 하 고 **Active Directory 사용자와 컴퓨터**합니다.  
  
2.  **Active Directory 사용자와 컴퓨터**, 네트워크를 차례로 클릭 한 다음 **사용자**합니다.  
  
3.  사용자 이름을 마우스 오른쪽 단추로 클릭, **속성**을 차례로 클릭 하 고 있는 **프로필** 탭 합니다.  
  
4.  내용을 삭제는 **로그온 스크립트** 텍스트 상자와 클릭 한 다음 **확인**합니다.  
  
5.  각 사용자에 대해 3-4 단계를 반복 합니다.  
  
##  <a name="BKMK_RemoveLegacyADGPO"></a>제거 레거시 Active Directory 그룹 정책 개체 (선택 사항)  
 그룹 정책 개체 (Gpo) Windows Server Essentials에 대 한 업데이트 됩니다. Windows SBS 2003 gpo 상위 됩니다. Windows Server Essentials에 대 한 다양 한 SBS 2003 Gpo Windows와 Windows WMI (Management Instrumentation) 필터 WMI 및 Windows Server Essentials Gpo 필터 충돌을 방지 하기 위해 수동으로 삭제 합니다.  
  
> [!NOTE]
>  원본 Windows SBS 2003 그룹 정책 개체, 수정 하는 경우에 중 복사본 다른 위치에 저장 하 고 Windows SBS 2003에서 삭제 해야 합니다.  
  
#### <a name="to-remove-old-group-policy-objects-from-windows-sbs-2003"></a>그룹 정책 개체 이전 Windows SBS 2003에서 제거 하려면  
  
1.  관리자 계정 사용 하 여 원본 서버에 로그온 합니다.  
  
2.  클릭 **시작**을 차례로 클릭 하 고 **서버 관리**합니다.  
  
3.  탐색 창에서 클릭 **고급 관리**, 클릭 **그룹 정책 관리**을 차례로 클릭 하 고 **숲:***< YourDomainName\ >*합니다.  
  
4.  클릭 **도메인**, 클릭 *< YourDomainName\ >*을 차례로 클릭 하 고 **그룹 정책 개체**합니다.  
  
5.  마우스 오른쪽 단추로 클릭 **소규모 기업 서버 감사 정책**, 클릭 **삭제**을 차례로 클릭 하 고 **확인**합니다.  
  
6.  네트워크에 적용 되는 다음과 같은 Gpo 삭제 5 단계를 반복 합니다.  
  
    -   소규모 기업 서버 클라이언트 컴퓨터  
  
    -   소규모 기업 서버 도메인 암호 정책  
  
         강력한 암호를 Windows Server Essentials의 암호 정책을 구성 하는 것이 좋습니다. 암호 정책을 구성 하려면 구성을 기본 도메인 정책에 쓰는 대시보드를 사용 합니다. Windows SBS 2003에 같은 암호 정책 구성 작은 Business Server 도메인 암호 정책 개체, 기록 되지 않습니다.  
  
    -   소규모 기업 서버 인터넷 연결이 방화벽  
  
    -   소규모 기업 서버 잠금 정책  
  
    -   소규모 기업 서버 원격 지원 정책  
  
    -   소규모 기업 서버 Windows 방화벽  
  
    -   소규모 기업 서버 업데이트 서비스 클라이언트 컴퓨터 정책  
  
         이 GPO Windows SBS 2003 R2에서 마이그레이션하는 하는 경우 표시 됩니다.  
  
    -   소규모 기업 서버 업데이트 서비스 일반적인 설정 정책  
  
         이 GPO Windows SBS 2003 R2에서 마이그레이션하는 하는 경우 표시 됩니다.  
  
    -   소규모 기업 서버 업데이트 서비스 서버 컴퓨터 정책  
  
         이 GPO Windows SBS 2003 R2에서 마이그레이션하는 하는 경우 표시 됩니다.  
  
7.  확인 Gpo 모두 삭제 됩니다.  
  
#### <a name="to-remove-wmi-filters-from-windows-sbs-2003"></a>Windows SBS 2003에서 WMI 필터 제거 하려면  
  
1.  관리자 계정 사용 하 여 원본 서버에 로그온 합니다.  
  
2.  클릭 **시작**을 차례로 클릭 하 고 **서버 관리**합니다.  
  
3.  탐색 창에서 클릭 **고급 관리**, 클릭 **그룹 정책 관리**을 차례로 클릭 하 고 **숲:***< YourNetworkDomainName\ >*  
  
4.  클릭 **도메인**, 클릭 *< YourNetworkDomainName\ >*을 차례로 클릭 하 고 **WMI 필터**합니다.  
  
5.  마우스 오른쪽 단추로 클릭 **PostSP2**, 클릭 **삭제**을 차례로 클릭 하 고 **예**합니다.  
  
6.  마우스 오른쪽 단추로 클릭 **PreSP2**, 클릭 **삭제**을 차례로 클릭 하 고 **예**합니다.  
  
7.  이러한 3 WMI 필터 삭제 됩니다 확인 합니다.  
  
##  <a name="BKMK_Configure"></a>네트워크를 구성  
  
#### <a name="to-configure-the-network"></a>네트워크를 구성  
  
1.  대상 서버의 대시보드를 엽니다.  
  
2.  대시보드에서 **홈** 페이지, 클릭 **설치**, 클릭 **어디서 나 액세스를 설정**, 다음 선택 하 고는 **구성 원하는 위치에 액세스 하려면 클릭** 옵션 합니다.  
  
3.  지침에 따라는 **어디서 나 액세스를 설정** 마법사를 구성 라우터와 도메인 이름입니다.  
  
 라우터 UPnP framework를 지원 하지 않는 경우 또는 UPnP 프레임 워크를 사용 하지 않는 경우 라우터에 이름 옆에 노란색 경고 아이콘이 나타날 수 있습니다. 다음 포트 열기 되며 대상 서버의 IP 주소를 전달 하는 것이 있는지 확인 합니다.  
  
-   포트 80: HTTP 웹 교통량  
  
-   HTTPS 웹 교통 포트 443:  
  
> [!NOTE]
>  를 두 번째 서버에는 온-프레미스 Exchange server를 설정 하는 경우 (SMTP)에 대 한 포트 25 공개 되며 온-프레미스 Exchange server의 IP 주소 리디렉션됩니다 확인 해야 합니다.  
  
##  <a name="BKMK_MapPermittedComputers"></a>사용자 계정에 허용 된 컴퓨터 지도  
 Windows SBS 2003 원격 웹 액세스 하는 사용자가 연결 하는 경우 네트워크에 있는 모든 컴퓨터 표시 됩니다. 이 컴퓨터 사용자에 액세스할 수 있는 권한이 없는 포함 될 수 있습니다. Windows Server Essentials의 사용자를 웹에 대 한 원격 액세스에 표시 하는 컴퓨터에 명시적으로 할당 합니다. 각 사용자 계정에서 Windows SBS 2003 마이그레이션에 하나 이상의 컴퓨터에 매핑됩니다 해야 합니다.  
  
#### <a name="to-map-user-accounts-to-computers"></a>컴퓨터에 사용자 계정이 지도로  
  
1.  대상 서버, Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 클릭 **사용자**합니다.  
  
3.  사용자 계정의 목록에서 사용자 계정 마우스 클릭 한 다음 **계정 속성 보기**합니다.  
  
4.  클릭 하 고 **원하는 위치에 액세스** 탭을 클릭 한 다음 **웹 원격 액세스 허용와 웹 서비스 응용 프로그램에 대 한 액세스 합니다. **.  
  
5.  클릭 **공유 폴더**, 클릭 **컴퓨터**, 클릭 **홈페이지 링크**을 차례로 클릭 하 고 **적용**합니다.  
  
6.  클릭는 **컴퓨터 액세스** 탭 하 고 액세스할 수 있도록 하려면 컴퓨터의 이름을 클릭 합니다.  
  
7.  각 사용자 계정에 대 한 3, 4, 5, 6 단계를 반복 합니다.  
  
> [!NOTE]
>  클라이언트 컴퓨터 구성 변경할 필요가 없습니다. 자동으로 구성 되어 있습니다.  
  
> [!NOTE]
>  대상 서버에서 첫 번째 새 사용자 계정을 만들 때 문제가 발생 하는 경우 마이그레이션을 완료 한 후 사용자 계정이 추가한 제거한 다음 다시 만들어야 합니다.
