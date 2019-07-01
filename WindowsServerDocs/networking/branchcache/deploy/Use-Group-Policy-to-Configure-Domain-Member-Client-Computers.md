---
title: 그룹 정책을 사용 하 여 도메인 구성원 클라이언트 컴퓨터를 구성 합니다.
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 911c1538-f79d-42e9-ba38-f4618f87b008
ms.author: pashort
author: shortpatti
ms.date: 06/02/2018
ms.openlocfilehash: 8e82d3e0ee7a84fbd6e2916d0f22472a8c117688
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855084"
---
# <a name="use-group-policy-to-configure-domain-member-client-computers"></a>그룹 정책을 사용 하 여 도메인 구성원 클라이언트 컴퓨터를 구성 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 섹션에서는 모든 컴퓨터에 대 한 그룹 정책 개체에서 조직, 분산된 캐시 모드를 사용 하 여 도메인 구성원 클라이언트 컴퓨터를 구성 또는 호스트 캐시 모드 만들고 BranchCache를 허용 하도록 고급 보안이 포함 된 Windows 방화벽 구성 트래픽입니다.  
  
이 섹션에는 다음 절차가 포함 됩니다.  
  
1.  [그룹 정책 개체를 만들고 BranchCache 모드를 구성 하려면](#bkmk_gp)  
  
2.  [고급 보안 인바운드 트래픽 규칙을 사용 하 여 Windows 방화벽을 구성 하려면](#bkmk_inbound)  
  
3.  [고급 보안 아웃 바운드 트래픽 규칙을 사용 하 여 Windows 방화벽을 구성 하려면](#bkmk_outbound)  
  
> [!TIP]  
> 하지만 다음 절차에서는 기본 도메인 정책에 그룹 정책 개체를 만들려고 라는 메시지가 표시 되, 배포에 적절 한 다른 컨테이너 또는 조직 구성 단위 (OU)에 개체를 만들 수 있습니다.  
  
멤버 여야 **Domain Admins**, 또는 이러한 절차를 수행 하려면 해당 합니다.  
  
## <a name="bkmk_gp"></a>그룹 정책 개체를 만들고 BranchCache 모드를 구성 하려면  
  
1.  있는 Active Directory 도메인 서비스 서버 역할 설치 된 컴퓨터, 서버 관리자에서 클릭 **도구**, 를 클릭 하 고 **그룹 정책 관리**합니다. 그룹 정책 관리 콘솔을 엽니다.  
  
2.  그룹 정책 관리 콘솔에서 다음 경로 확장: **포리스트:** *example.com*, **도메인**를 *example.com*하십시오 **그룹 정책 개체**여기서  *example.com* 구성할는 BranchCache 클라이언트 컴퓨터 계정이 있는 도메인의 이름입니다.  
  
3.  마우스 오른쪽 단추로 클릭 **그룹 정책 개체**, 를 클릭 하 고 **새로**합니다. **새 GPO** 대화 상자가 열립니다. **이름**, 에 대 한 새 그룹 정책 개체 (GPO) 이름을 입력 합니다. 예를 들어 개체 BranchCache 클라이언트 컴퓨터의 이름을 하려는 입력 **BranchCache 클라이언트 컴퓨터**합니다. **확인**을 클릭합니다.  
  
4.  그룹 정책 관리 콘솔에서 **그룹 정책 개체** 을 선택 하 고 세부 정보 창에서 방금 만든 GPO를 마우스 오른쪽 단추로 클릭 합니다. 예를 들어 GPO BranchCache 클라이언트 컴퓨터를 이름을 마우스 오른쪽 단추로 클릭 **BranchCache 클라이언트 컴퓨터**합니다. 클릭 **편집**합니다. 그룹 정책 관리 편집기 콘솔을 엽니다.  
  
5.  그룹 정책 관리 편집기 콘솔에서 다음 경로 확장: **컴퓨터 구성**하십시오 **정책을**, **관리 템플릿: 로컬 컴퓨터에서 정책 정의 (ADMX 파일)를 검색할**, **네트워크**합니다 **BranchCache**합니다.  
  
6.  클릭 **BranchCache**, 세부 정보 창에서 두 번 클릭 하 고 **BranchCache 설정**합니다. 정책 설정 대화 상자가 열립니다.  
  
7.  에 **BranchCache 설정** 대화 상자, 클릭 **Enabled**, 클릭 하 고 **확인**합니다.  
  
8.  세부 정보 창에서 BranchCache 분산된 캐시 모드를 사용 하도록 설정 하려면 두 번 클릭 **설정 BranchCache 분산 캐시 모드**합니다. 정책 설정 대화 상자가 열립니다.  
  
9. 에 **설정 BranchCache 분산 캐시 모드** 대화 상자를 클릭 **Enabled**, 클릭 하 고 **확인**합니다.  
  
10. 여기서 호스트 캐시 모드로 BranchCache를 배포 하는 하 고 배포한 호스트 캐시 서버 해당 사무실에 하나 이상의 지점이 있는 경우, 두 번 클릭 **자동 호스트 캐시 검색 사용 서비스 연결 지점에**합니다. 정책 설정 대화 상자가 열립니다.  
  
11. 에 **자동 호스트 캐시 검색 사용 서비스 연결 지점에** 대화 상자를 클릭 **Enabled**, 클릭 하 고 **확인**합니다.  
  
    > [!NOTE]  
    > 둘 다 사용 하는 경우는 **설정 BranchCache 분산 캐시 모드** 및 **자동 호스트 캐시 검색 사용 서비스 연결 지점에** 정책 설정, 지점의 호스트 캐시 모드에서 작동 지점도 호스트 캐시 서버를 찾을 것 하지 않는 한 클라이언트 컴퓨터 BranchCache 분산된 캐시 모드에서 작동 합니다.  
  
12. 그룹 정책을 사용 하 여 클라이언트 컴퓨터에서 방화벽 설정을 구성 하려면 다음 절차를 사용 합니다.  
  
## <a name="bkmk_inbound"></a>고급 보안 인바운드 트래픽 규칙을 사용 하 여 Windows 방화벽을 구성 하려면  
  
1.  그룹 정책 관리 콘솔에서 다음 경로 확장: **포리스트:** *example.com*, **도메인**를 *example.com*하십시오 **그룹 정책 개체**여기서  *example.com* 구성할는 BranchCache 클라이언트 컴퓨터 계정이 있는 도메인의 이름입니다.  
  
2.  그룹 정책 관리 콘솔에서 **그룹 정책 개체** 을 선택 하 고 세부 정보 창에서 BranchCache 클라이언트 컴퓨터 이전에 만든 GPO를 마우스 오른쪽 단추로 클릭 합니다. 예를 들어 GPO BranchCache 클라이언트 컴퓨터를 이름을 마우스 오른쪽 단추로 클릭 **BranchCache 클라이언트 컴퓨터**합니다. 클릭 **편집**합니다. 그룹 정책 관리 편집기 콘솔을 엽니다.  
  
3.  그룹 정책 관리 편집기 콘솔에서 다음 경로 확장: **컴퓨터 구성**, **정책을**를 **Windows 설정**를 **보안 설정**, **고급보안이포함된Windows방화벽**, **With Advanced Security-LDAP Windows 방화벽**합니다 **인바운드 규칙**합니다.  
  
4.  **인바운드 규칙**을 마우스 오른쪽 단추로 클릭한 다음 **새 규칙**을 클릭합니다. 새 인바운드 규칙 마법사가 열립니다.  
  
5.  **규칙 유형**, 클릭 **미리 정의 된**, 선택 항목의 목록을 확장 하 고 클릭 한 다음 **BranchCache-콘텐츠 검색 (사용 하 여 HTTP)** 합니다. **다음**을 클릭합니다.  
  
6.  **미리 정의 된 규칙**, 클릭 **다음**합니다.  
  
7.  **작업**, 되도록 **연결을 허용** 을 선택한 다음 클릭 **마침**합니다.  
  
    > [!IMPORTANT]  
    > 선택 해야 **연결을 허용** 이 포트에서 트래픽을 받을 수 있으려면 BranchCache 클라이언트에 대 한 합니다.  
  
8.  Ws-discovery 방화벽 예외를 만들려면 다시 마우스 오른쪽 단추로 클릭 **인바운드 규칙**, 를 클릭 하 고 **새 규칙**합니다. 새 인바운드 규칙 마법사가 열립니다.  
  
9. **규칙 유형**, 클릭 **미리 정의 된**, 선택 항목의 목록을 확장 하 고 클릭 한 다음 **BranchCache-피어 검색 (사용 하 여 WSD)** 합니다. **다음**을 클릭합니다.  
  
10. **미리 정의 된 규칙**, 클릭 **다음**합니다.  
  
11. **작업**, 되도록 **연결을 허용** 을 선택한 다음 클릭 **마침**합니다.  
  
    > [!IMPORTANT]  
    > 선택 해야 **연결을 허용** 이 포트에서 트래픽을 받을 수 있으려면 BranchCache 클라이언트에 대 한 합니다.  
  
## <a name="bkmk_outbound"></a>고급 보안 아웃 바운드 트래픽 규칙을 사용 하 여 Windows 방화벽을 구성 하려면  
  
1.  그룹 정책 관리 편집기 콘솔에서 마우스 오른쪽 단추로 클릭 **아웃 바운드 규칙**, 를 클릭 하 고 **새 규칙**합니다. 새 아웃 바운드 규칙 마법사가 열립니다.  
  
2.  **규칙 유형**, 클릭 **미리 정의 된**, 선택 항목의 목록을 확장 하 고 클릭 한 다음 **BranchCache-콘텐츠 검색 (사용 하 여 HTTP)** 합니다. **다음**을 클릭합니다.  
  
3.  **미리 정의 된 규칙**, 클릭 **다음**합니다.  
  
4.  **작업**, 되도록 **연결을 허용** 을 선택한 다음 클릭 **마침**합니다.  
  
    > [!IMPORTANT]  
    > 선택 해야 **연결을 허용** BranchCache 클라이언트가이 포트에서 트래픽을 보낼 수 있습니다.  
  
5.  Ws-discovery 방화벽 예외를 만들려면 다시 마우스 오른쪽 단추로 클릭 **아웃 바운드 규칙**, 를 클릭 하 고 **새 규칙**합니다. 새 아웃 바운드 규칙 마법사가 열립니다.  
  
6.  **규칙 유형**, 클릭 **미리 정의 된**, 선택 항목의 목록을 확장 하 고 클릭 한 다음 **BranchCache-피어 검색 (사용 하 여 WSD)** 합니다. **다음**을 클릭합니다.  
  
7.  **미리 정의 된 규칙**, 클릭 **다음**합니다.  
  
8.  **작업**, 되도록 **연결을 허용** 을 선택한 다음 클릭 **마침**합니다.  
  
    > [!IMPORTANT]  
    > 선택 해야 **연결을 허용** BranchCache 클라이언트가이 포트에서 트래픽을 보낼 수 있습니다.  
  

