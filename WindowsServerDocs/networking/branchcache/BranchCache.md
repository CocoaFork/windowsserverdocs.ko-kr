---
title: BranchCache
description: 이 항목에서는 BranchCache Windows Server 2016에 대 한 개요
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-bc
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4587cff-c086-49f1-a0bf-cd74b8a44440
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5540d89827b80a21bf23f6a2aa8f54f09dfde67a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="branchcache"></a>BranchCache

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 내용은 IT 전문가 위한 BranchCache 모드, 기능, 기능 및 다양 한 운영 체제에 사용할 수 있는 BranchCache 기능을 포함 하 여 BranchCache에 대 한 개요 정보를 제공 합니다.

> [!NOTE]
> 이 항목 외에 다음과 같은 BranchCache 문서를 사용할 수 있습니다.
> 
> - [네트워크 BranchCache 셸 및 Windows PowerShell 명령](../branchcache/BranchCache-Network-Shell-and-Windows-PowerShell-Commands.md)
> -   [BranchCache 배포 가이드](../branchcache/deploy/BranchCache-Deployment-Guide.md)

**사용자는 관심이 BranchCache 되나요?**

시스템 관리자가, 네트워크 또는 저장소 솔루션 설계자 또는 기타 IT 전문가 인 경우 BranchCache 다음과 같은 경우 관심 될 수 있습니다.

- 디자인 또는 IT 인프라 본사를 지점에서 두 개 이상의 실제 위치 및 다양 한 영역 (네트워크) 연결을가 조직에 대 한 지원 합니다.

- 디자인 또는 클라우드 기술에 배포 하는 조직의 IT 인프라를 지원 하 고 데이터에 액세스 하 고 원격 위치의 응용 프로그램에는 직원 WAN 연결을 사용 합니다.

- 네트워크 교통 지점 사이의 본사 양을 줄여 WAN 대역폭 사용을 최적화 하려고 합니다.

- 배포한 또는 배포 주 사무실이 항목에 설명 된 구성와 일치 하는 콘텐츠 서버에 계획입니다.

- Windows 10, Windows 8.1, Windows 8 또는 Windows 7 클라이언트 컴퓨터 지점에서 실행 됩니다.

이 항목 다음 섹션에 포함 됩니다.

-   [BranchCache은 무엇 인가요?](#bkmk_what)

-   [BranchCache 모드](#BKMK_2)
  
-   [콘텐츠 서버 BranchCache 사용](#BKMK_3)
  
-   [BranchCache 하 고 구름](#BKMK_3a)
  
-   [콘텐츠 정보 버전](#bkmk_version)  
  
-   [파일의 콘텐츠 업데이트가 제공 BranchCache 처리 하는 방법](#bkmk_handles)  
  
-   [BranchCache 설치 가이드](#BKMK_4)  
  
-   [운영 체제 버전 BranchCache에 대 한](#bkmk_os)  
  
-   [BranchCache 보안](#bkmk_security)  
  
-   [콘텐츠 흐름과 프로세스](#bkmk_flow)  
  
-   [캐시 보안](#bkmk_cache)  
  
## <a name="bkmk_what"></a>BranchCache은 무엇 인가요?

BranchCache 일부 버전의 Windows Server 2016 및 Windows 10 운영 체제 및 Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2 및 Windows 7의 일부 버전에 포함 되어 있는 다양 한 영역 네트워크 (WAN) 대역폭 최적화 기술을입니다. 사용자가 원격 서버에 콘텐츠에 액세스 하는 때를 WAN 대역폭 최적화 하려면 BranchCache 주 사무실에서 콘텐츠를 가져오는 또는 클라우드 콘텐츠 서버 호스트 고 캐시 지점 위치에 있는 항목 클라이언트 wan가 대신 로컬 콘텐츠에 액세스 하는 지점에 컴퓨터를 허용 합니다.
  
분기 사무실에서 콘텐츠 호스트 캐시에 또는 Windows 10, Windows 8.1, Windows 8 또는 Windows 7을 실행 하는 클라이언트 컴퓨터에서 지점에 없는 서버를 사용할 수 있는 때 구성 하는 서버에 저장 됩니다. 클라이언트 컴퓨터를 요청 하 고 본사에서 콘텐츠를 받는 지점에서 캐시 된 콘텐츠를 후 같은 지점에서 다른 컴퓨터 WAN 링크를 통해 콘텐츠 서버에서 콘텐츠를 다운로드 하는 것이 아니라 로컬 콘텐츠를 얻을 수 있습니다.

클라이언트 다운로드 클라이언트 컴퓨터에서 동일한 콘텐츠에 대 한 후속 요청 하면 *정보 내용* 실제 콘텐츠는 대신 서버에서 합니다. 콘텐츠 정보 원래 콘텐츠 청크를 사용 하 여 계산 된이 데이터에는 내용에 비해 매우 작은 해시 구성 되어 있습니다. 클라이언트 컴퓨터 사용 하 여 콘텐츠 정보는 지점에 캐시에서 콘텐츠를 찾는 클라이언트 컴퓨터 또는 서버에 있는 캐시 인지. 컴퓨터 클라이언트 및 서버 캐시 된 콘텐츠 무단으로 액세스할 수 없는 보호를 위해 콘텐츠 정보를 사용할 수도 있습니다.

BranchCache 최종 사용자의 생산성 향상 클라이언트 및 서버 지점에서에 대 한 콘텐츠 쿼리에 응답 시간을 개선 하 고 교통 WAN 링크를 통해 줄여 네트워크 성능 개선에 도움이 될 수 있습니다.

## <a name="BKMK_2"></a>BranchCache 모드
BranchCache 작업의 두 가지 모드는: 캐시 모드와 호스트 캐시 모드를 배포 합니다.

분산된 캐시 모드로 BranchCache 배포 하는 경우는 지점에 콘텐츠 캐시 클라이언트 컴퓨터 간에 배포 됩니다.

호스트 캐시 모드로 BranchCache 배포 하는 경우 콘텐츠 캐시를 지점은 하나 또는 라고 하는 많은 서버 컴퓨터 호스팅 캐시 서버 합니다.

> [!NOTE]
> 그러나 하나만 모드는 지점에 따라 사용할 수 두 가지 모드를 사용 하 여 BranchCache 배포할 수 있습니다. 예를 들어, 두 지점, 서버에 및, 하지 않는 경우에 클라이언트 컴퓨터 포함 된 사무실에서 분산된 캐시 모드로 BranchCache 배포 하는 동안 서버를 포함 하는 office 호스트 캐시 모드로 BranchCache 배포할 수 있습니다.

다음 그림에서는 BranchCache 두 모드에서 배포 됩니다.  

![BranchCache 모드](../media/BranchCache/bc_modes.jpg)

분산된 캐시 모드는 로컬 서버 호스트 캐시 서버도 사용 하기 위해 포함 되어 있지 않은 작은 지점에 가장 적합 합니다. 분산된 캐시 모드 지점에 추가 되지 하드웨어 BranchCache 배포할 수 있습니다.

배포 BranchCache 하려는 지점 다른 작업을 실행 하는 하나 이상의 서버 같은 추가 인프라 포함 되어 있는 경우 호스트 캐시 모드로 BranchCache 배포 유용 이유는 다음과 같습니다.

### <a name="increased-cache-availability"></a>향상 된 캐시 공급 일

캐시 된 데이터를 원래 요청 하는 클라이언트 오프 라인 상태인 경우에 콘텐츠를 사용할 수 있으므로 호스트 캐시 모드 캐시 효율성을 높여 줍니다. 호스트 캐시 서버를 사용할 수 있는 항상 때문에 더 많은 콘텐츠 캐시 된 큰 WAN 대역폭 절약 제공 하 고 BranchCache 효율성을 개선 합니다.

### <a name="centralized-caching-for-multiple-subnet-branch-offices"></a>여러 서브넷 지점에 대 한 캐시 중앙 집중식


분산된 캐시 모드 단일 서브넷에서 작동합니다. 여러 서브넷 지점 분산된 캐시 모드에 대 한 구성에서 다른 서브넷 클라이언트 컴퓨터와 한 서브넷에 다운로드 한 파일을 공유할 수 없습니다. 

이 인해는 파일 이미 다운로드를 검색할 수 없습니다 다른 서브넷 클라이언트가 파일을 가져올 본사 콘텐츠 서버에서 WAN 대역폭 프로세스에 사용 하 여.

그러나 호스트 캐시 모드 배포 하는 경우의 경우 이것이-여러 서브넷 지점에 모든 클라이언트 클라이언트 다른에 있는 경우에 호스트 캐시 서버에 저장 되는 하나의 캐시를에 액세스할 수 있습니다. 또한 BranchCache Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012에서 둘 이상의 호스트 캐시 서버 지점 별로 배포 하는 기능을 제공 합니다.

> [!CAUTION]
> 파일 및 폴더의 SMB 캐싱 BranchCache을 사용 하면 오프 라인 파일 해제 하지 마십시오. 오프 라인 파일을 해제 하면 캐시 BranchCache SMB 제대로 작동 하지 않습니다.

## <a name="BKMK_3"></a>콘텐츠 서버 BranchCache 사용

BranchCache 배포할 때 소스 콘텐츠 주 사무실에 또는 클라우드 데이터 센터에 BranchCache 가능 콘텐츠 서버에 저장 됩니다. 다음과 같은 유형의 콘텐츠 서버 BranchCache에서 지원 됩니다.

> [!NOTE]
> 만 소스 콘텐츠, 즉 클라이언트 컴퓨터가 BranchCache 가능 콘텐츠 서버-에서 가져올 처음 콘텐츠 BranchCache 하면 빨라집니다 됩니다. 인터넷 또는 Windows 업데이트의 웹 서버와 같은 다른 소스에서 직접 클라이언트 컴퓨터 획득 하는 클라이언트 컴퓨터에서 캐시 되지 않습니다 또는 캐시 서버 호스트 콘텐츠와 지사에서 다른 컴퓨터와 공유 합니다. 하지만 Windows 업데이트 콘텐츠를 더욱 빠르게 이용할 하려는 경우 수 설치 본사 또는 클라우드 데이터 센터에는 Windows Server Update Services (WSUS) 응용 프로그램이 서버 하 BranchCache 콘텐츠 서버도 구성 되어 있습니다.

### <a name="web-servers"></a>웹 서버

지원 되는 웹 서버 실행 중인 컴퓨터 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 r 2를 설치 하는 웹 서버 IIS () 서버 역할 있고 하이퍼텍스트 전송 (HTTP 프로토콜) 또는 HTTP 보안 (HTTPS)를 사용 하는 포함 됩니다.

또한 웹 서버 BranchCache 기능이 설치 되어 있어야 합니다.

### <a name="file-servers"></a>파일 서버

지원 되는 파일 서버 실행 중인 컴퓨터에 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2 서비스 파일 서버 역할을 설치 하는 네트워크 파일 역할 서비스에 대 한 BranchCache 있는 포함 됩니다. 

이러한 파일 서버 메시지 블록 SMB (서버)를 사용 하 여 컴퓨터 간에 정보를 교환 하려면 연락처. 파일 서버의 설치를 완료 한 후 폴더를 공유 해야 및 BranchCache 사용 하도록 설정 하려면 그룹 정책 또는 컴퓨터 정책을 로컬를 사용 하 여 해시 생성 공유 폴더를 사용 해야 합니다.

### <a name="application-servers"></a>응용 프로그램 서버

지원 되는 응용 프로그램 서버 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012를 실행 하는 컴퓨터에 포함 되어 또는 Windows Server 2008 r 2와 배경 지능형 서비스 BITS (전송) 설치 되어 사용 하도록 설정 합니다. 

또한, 응용 프로그램 서버 BranchCache 기능이 설치 되어 있어야 합니다. 예를 들어 서버 응용 프로그램의 Microsoft Windows Server Update Services (WSUS) 및 Microsoft 시스템 Center Configuration Manager 분기 배포 지점 서버 BranchCache 콘텐츠 서버로 배포할 수 있습니다.

## <a name="BKMK_3a"></a>BranchCache 하 고 구름

클라우드 작동 비용을 절감 및 배율 새로운 수준 거 대 한 발생할 수 있음을 하지만 네트워킹 비용을 향상 하 고 생산성 영향을 미칠 수 이동 하는 사람에 따라 달라 멀리 작업입니다. 사용자가 고성능 될 것으로 기대 하 고 응용 프로그램과 데이터 호스트 되 상관 하지 않는 합니다. 

BranchCache는 네트워크에 연결 된 응용 프로그램의 성능을 향상 하 고 데이터 공유 캐시 된 대역폭 소모를 줄일 수 있습니다.  지사 및 작업자 클라우드에서 배포 되는 서버를 사용 중인 본사 생산성을 개선 합니다.

새 하드웨어 또는 네트워크 토폴로지 변경 BranchCache 필요 하지 않으므로, 위치 및 공공와 개인 구름 간 통신 개선 하기 위한 뛰어난 솔루션입니다.

> [!NOTE]
> 일부 웹 프록시 사용할 수 없는 콘텐츠 인코딩 머리글 처리할 수 없습니다을 하기 때문에 Hyper 텍스트 전송 프로토콜 Secure (HTTPS)와 하지 HTTP BranchCache을 사용 하는 것이 좋습니다.
  
=== 클라우드 기술 Windows Server 2016에 대 한 자세한 내용은 참조 [소프트웨어 네트워킹 정의 & #40; SDN & #41; ](../sdn/Software-Defined-Networking--SDN-.md).
  
## <a name="bkmk_version"></a>콘텐츠 정보 버전

콘텐츠 정보의 버전을 두 가지가 있습니다.

- Windows Server 2008 R2 및 Windows 7을 실행 하는 컴퓨터에 호환 되는 콘텐츠 정보 1, 버전 또는 V1 라고 합니다. V1 BranchCache 파일 조각화 된 파일 V2 보다 큰 선분과의 크기는 합니다. 큰 고정된 세그먼트 크기 때문에 파일 길이 수정 하는 경우 변경 하면 해당 사용자를 변경 세그먼트 무효화 뿐만 아니라 모든 파일의 끝으로 세그먼트 무효화 됩니다. 따라서 다음 전화 지사에서 다른 사용자가 변경된 된 파일에 대 한 변경된 내용 및 변경 된 후 모든 콘텐츠 WAN 링크를 통해 전송 되기 때문에 감소 WAN 대역폭에 발생 합니다.

- Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012 및 Windows 8을 실행 하는 컴퓨터에 호환 되는 콘텐츠 정보 2, 버전 또는 V2 라고 합니다. 콘텐츠 정보 V2 파일에 변경 내용을 더 많은 허용 하는 더 작은, 가변 세그먼트 사용 합니다. 이 증가 사용자가 콘텐츠 서버에서 파일의 변경된 부분만 검색을 하 고 WAN 대역폭 적게 사용 하 여 업데이트 된 버전에 액세스할 때 가능성 나누어에서 이전 버전의 파일을 다시 사용할 수 있습니다.

다음 표에서 클라이언트를 콘텐츠 서버에 따라 사용 되는 콘텐츠 정보 버전에 대해 설명 하 고 BranchCache 배포에서 사용 하는 캐시 서버 운영 체제 호스트 합니다.

> [!NOTE]
> 아래 표에서 "OS" 약어 운영 체제를 의미합니다.

|클라이언트 운영 체제|서버 운영 체제 콘텐츠|호스트 캐시 서버 운영 체제|콘텐츠 정보 버전|
|-------------|---------------------|--------------------------|-------------------------------|
|Windows Server 2008 R2 및 Windows 7 |Windows Server 2012 이상|Windows Server 2012 또는 이후입니다. 분산된 캐시 모드에 대 한 없음|V1|
|Windows Server 2012 또는 이후입니다. Windows 8 이상|Windows Server 2008 R2 |Windows Server 2012 또는 이후입니다. 분산된 캐시 모드에 대 한 없음|V1|
|Windows Server 2012 또는 이후입니다. Windows 8 이상| Windows Server 2012 이상| Windows Server 2008 R2 |V1|
|Windows Server 2012 또는 이후입니다. Windows 8 이상|Windows Server 2012 이상|Windows Server 2012 또는 이후입니다. 분산된 캐시 모드에 대 한 없음|V 2|

서버 콘텐츠를 호스트 캐시 서버 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012를 실행 하는 사용 하 여 정보를 요청 하는 BranchCache 클라이언트의 운영 체제에 따라 적절 한 되는 콘텐츠 정보 버전 합니다. 

콘텐츠 및 호스팅된 캐시 서버 V2 콘텐츠 정보; 사용 하 여 Windows Server 2012와 Windows 8 또는 이상 운영 체제를 실행 하는 컴퓨터에서 콘텐츠를 요청 하는 경우 Windows Server 2008 R2 및 Windows 7을 실행 하는 컴퓨터에서 콘텐츠를 요청 및 호스팅된 콘텐츠 캐시 서버 V1 콘텐츠 정보를 사용 합니다.

>[!IMPORTANT]
>분산된 캐시 모드로 BranchCache 배포 하는 경우 다른 콘텐츠 정보 버전을 사용 하는 클라이언트는 콘텐츠를 서로 공유 하지 않습니다. 예를 들어, Windows 7을 실행 하는 클라이언트 컴퓨터와 동일한 지점에 설치 되어 있는 Windows 10을 실행 하는 클라이언트 컴퓨터 서로 된 콘텐츠를 공유 하지 않습니다.
  
## <a name="bkmk_handles"></a>파일의 콘텐츠 업데이트가 제공 BranchCache 처리 하는 방법

지점 사용자를 수정 하거나 문서의 내용을 업데이트할 때 변경 직접 BranchCache의 참여 하지 않고 본사 콘텐츠 서버에 기록 됩니다. 사용자의 콘텐츠 서버에서 문서를 다운로드 하거나 지점에 호스팅된 또는 분산 캐시 중 하나에서 얻은 여부 마찬가지입니다.

수정된 된 파일을 다른 클라이언트 지점에서 요청 하면 새 부분의 파일 본사 서버에서 다운로드 하 고 분산 또는 호스트 된 캐시 해당 분기에 추가 됩니다. 이 인해 지점 사용자가 항상 최신 버전의 캐시 된 콘텐츠를 받습니다.

## <a name="BKMK_4"></a>BranchCache 설치 가이드

설치 BranchCache 기능 또는 서비스 파일 서버 역할의 네트워크 파일 역할 서비스에 대 한 BranchCache 서버 관리자 Windows Server 2016에 사용할 수 있습니다. 다음 표에서 역할 서비스 또는 기능을 설치할지 여부를 결정을 사용할 수 있습니다.

|기능|컴퓨터 위치|이 BranchCache 요소를 설치 합니다.|
|-----------------|---------------------|------------------------------------|
|콘텐츠 서버 \ (비트 기반 응용 프로그램이 server\)|주 office 스토어 또는 클라우드 데이터 센터|BranchCache 기능|
|콘텐츠 서버 \(Web server\)|주 office 스토어 또는 클라우드 데이터 센터|BranchCache 기능|
|콘텐츠 서버 \ (SMB protocol\를 사용 하 여 파일 서버)|주 office 스토어 또는 클라우드 데이터 센터|네트워크 파일 서버 역할 파일 서비스의 역할 서비스에 대 한 BranchCache|
|호스트 캐시 서버|지점|호스트 캐시 서버 모드를 사용 BranchCache 기능|
|컴퓨터 BranchCache 사용 하는 클라이언트|지점|없음 설치 사용할 수 있습니다. 방금 BranchCache 및 BranchCache 모드를 사용 하도록 설정 \(distributed or hosted\) 클라이언트|

역할 서비스 또는 기능을 설치 하려면 관리자 서버 열고 BranchCache 기능을 활성화 하려면 컴퓨터를 선택 합니다. 서버 관리자 클릭 **관리**을 차례로 클릭 하 고 **역할 추가 및 기능**합니다. **역할 추가 및 기능** 마법사가 열립니다. 마법사를 실행 하면 다음과 같은 선택 항목을 확인 합니다.

- 마법사 페이지 **설치 유형을 선택**선택 **역할 또는 기능 기반 설치**합니다.

- 마법사 페이지에서 **서버 역할 선택**BranchCache 사용 파일 서버, 설치 하는 경우, 확장 **파일 및 저장소 서비스** 및 **파일과 iSCSI 서비스**를 선택한 다음 **BranchCache 네트워크 파일에 대 한**합니다.  디스크 공간을 절약 하기 선택할 수도 있습니다는 **데이터 중복 제거** 역할 서비스를 하 고 설치를 완료 마법사를 통해 계속 합니다. BranchCache 사용 파일 서버를 설치 하려는 경우 네트워크 파일 역할 서비스에 대 한 BranchCache 된 파일 및 저장소 서비스 역할을 설치 하지 마십시오.

- 마법사 페이지 **기능을 선택**선택 호스트 캐시 서버, 설치 하는 파일 서버 되지 않는 콘텐츠 서버를 설치 하는 경우 **BranchCache**, 다음 마법사를 완료 하 고 설치를 진행 합니다. 호스트 캐시 서버 또는 파일 서버 콘텐츠 서버를 설치 하려면 BranchCache 기능을 설치 하지 않습니다.
  
## <a name="bkmk_os"></a>운영 체제 버전 BranchCache에 대 한

다음과 같은 여러 형식의 BranchCache 기능을 지 원하는 운영 체제의 목록입니다.

### <a name="operating-systems-for-branchcache-client-computer-functionality"></a>운영 체제 BranchCache 클라이언트 컴퓨터 기능에 대 한

다음 운영 체제 BranchCache 배경 지능형 서비스 BITS (전송), Hyper 텍스트 전송 (HTTP 프로토콜)를 및 블록 SMB (서버 메시지)에 대 한 지원을 제공합니다.

- Windows 10 Enterprise

- Windows 10 Education

- Windows 8.1 Enterprise

- Windows 8 Enterprise

- Windows 7 Enterprise

- Windows 7 Ultimate

다음 운영 체제 BranchCache HTTP 및 SMB 기능을 지원 하지 않는 하지만 BranchCache 비트 기능을 지원 합니다.

-   Windows 10 Pro로 비트만 지원

-   Windows 8.1 Pro 비트만 지원

-   Windows 8 Pro 비트만 지원

-   Windows 7 Pro 비트만 지원

> [!NOTE]
> BranchCache는 기본적으로 Windows Server 2008 또는 Windows Vista의 운영 체제에 사용할 수 없는 경우 그러나 이러한 운영 체제에서 다운로드 하 고 관리 프레임 워크 Windows 업데이트를 설치 하는 경우 BranchCache 기능은 배경 지능형 서비스 BITS (전송) 프로토콜에만 사용할 수 있습니다. 표시 되는 자세한 정보 및 Windows Management Framework 다운로드 [Windows Management Framework (Windows PowerShell 2.0, WinRM 2.0 및 비트 4.0)](https://go.microsoft.com/fwlink/?LinkId=188677) 에 https://go.microsoft.com/fwlink/?LinkId=188677합니다.
  
### <a name="operating-systems-for-branchcache-content-server-functionality"></a>운영 체제에 대 한 BranchCache 콘텐츠 서버 기능

BranchCache 콘텐츠 서버와 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012 제품군 운영 체제에 사용할 수 있습니다.

또한 Windows Server 2008 R2 가족의 운영 체제는 다음과 같은 차이점이 BranchCache 콘텐츠 서버도 사용할 수 있습니다.

- Hyper-v와 Windows Server 2008 R2 Enterprise의 서버 Core 설치 BranchCache 수 없습니다.

- Hyper-v와 Windows Server 2008 R2 Datacenter Server Core 설치 BranchCache 수 없습니다.

### <a name="operating-systems-for-branchcache-hosted-cache-server-functionality"></a>운영 체제 BranchCache에 대 한 캐시 서버 기능 호스트

BranchCache 캐시 서버 호스트 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012 제품군 운영 체제에 사용할 수 있습니다.

또한 다음과 같은 Windows Server 2008 R2 운영 체제 BranchCache 캐시 서버 호스트으로 사용할 수 있습니다.

- Windows Server 2008 R2 Enterprise

- Hyper-v와 Windows Server 2008 R2 Enterprise

- Windows Server 2008 R2 Enterprise 서버 Core 설치

- Windows Server 2008 R2 Enterprise 서버 Core 설치 Hyper V와

- Itanium 기반 시스템용 Windows Server 2008 R2

- Windows Server 2008 R2 Datacenter

- Hyper-v와 Windows Server 2008 R2 Datacenter

- Windows Server 2008 R2 Datacenter Server Core 설치 Hyper V와

## <a name="bkmk_security"></a>BranchCache 보안

BranchCache 하면 기존 네트워크 보안 아키텍처를 않고도 추가 장치 또는 구성을 복잡 한 추가 보안에 대 한와 함께 원활 하 게 작동 하는 보안 디자인 방식을 구현 합니다.
  
BranchCache 침해 하지 이며 Windows 인증 또는 인증 프로세스를 변경 하지 않습니다. BranchCache를 배포한 후 아직 인증할 도메인 자격 증명 하 고 있는 승인 액세스 제어 (Acl 목록)와 기능을 변경 하는 방법은 사용 하 여 합니다. 또한 다른 구성 계속 이전과 BranchCache 배포 하는 것 처럼 작동 합니다.

BranchCache 보안 모델 메타 데이터를는 일련의 해시 형식으로 작성을 기반으로 합니다. 이러한 해시 콘텐츠 정보를 라고도 합니다.

콘텐츠 정보를 만든 후 실제 데이터를 대신 BranchCache 메시지 거래소에 사용 되 고 지원된 (HTTP, HTTPS 및 SMB) 프로토콜을 사용 하 여 교환 합니다.

캐시 된 데이터가 암호화 된 유지 되 고 원본에서 콘텐츠에 액세스할 수 있는 권한이 없는 하는 클라이언트에서 액세스할 수 없습니다.  클라이언트 인증 하 고 콘텐츠 메타 데이터를 검색할 수 있는 콘텐츠 메타 데이터를 액세스 로컬 사무실에 캐시 있어야만 전에 콘텐츠 원본 하 여 권한을 부여 해야 합니다.

### <a name="how-branchcache-generates-content-information"></a>BranchCache 콘텐츠 정보를 생성 하는 방법

여러 요소 로부터 콘텐츠 정보를 만든 콘텐츠 정보의 값은 고유한 항상 합니다. 이러한 요소는 다음과 같습니다.

- 실제 콘텐츠 (예: 웹 페이지 또는 파일 공유) 해시 만들어집니다.  

- 구성 매개 해시 알고리즘 및 차단 크기와 같은 합니다. 콘텐츠 정보를 생성 하려면 콘텐츠 서버를 단위로 콘텐츠 나누고 블록으로 세그먼트 다음 세분 합니다. BranchCache 암호화 해시 안전 하 게 식별 하 고 SHA256 hash algorithm 지원 각 차단 및 세그먼트 확인할 사용 합니다.

- 서버 암호입니다. 모든 콘텐츠 서버 서버 비밀 임의의 길이 이진 값으로 설정 해야 합니다.

> [!NOTE]
> 서버 암호를 사용 하 않도록 클라이언트 컴퓨터가 자체 콘텐츠 정보를 생성할 수 없는 수 있습니다. 이 악의적인 사용자를가 컴퓨터 BranchCache 사용 하는 클라이언트와 공격을 사용 하 여 클라이언트 이전 버전에 액세스 했던 하지만 현재 버전에 액세스할 수 없는 경우에는 버전 간 사소한 변경 내용에 추측 수 없습니다.

### <a name="content-information-details"></a>세부 정보 콘텐츠

BranchCache 관련 콘텐츠 해시 공인된 클라이언트로 전송 된 정보를 추출 하기 위해 서버 비밀 키를 사용 합니다. 이 해시를 생성 해시 알고리즘을 결합 된 서버 암호 및 데이터 해시 적용 합니다.

이 해시 세그먼트 시크릿을 라고 합니다. BranchCache는 세그먼트 비밀 커뮤니케이션 보호를 위해 사용 합니다. 또한 BranchCache 해시 데이터 블록 목록은 차단 해시 목록 및 해시의 데이터를 해시 차단 해시 목록에서 생성 되는 만듭니다.

콘텐츠 정보는 다음과 같습니다.

- 차단 해시 목록은 다음과 같습니다.

    `BlockHashi = Hash(dataBlocki)   1<=i<=n`

- 데이터 (HoD) 해시:

    `HoD = Hash(BlockHashList)`

- 세그먼트 시크릿 (Kp):

    `Kp = HMAC(Ks, HoD)`

BranchCache 보안 캐싱 및 콘텐츠 캐시 간에 데이터의 검색을 확인 하는 프로세스를 구현 하 여 피어 콘텐츠 캐싱 및 검색 프레임 워크 프로토콜을 사용 합니다.

또한 BranchCache 핸들 동일한 수준의 자체 실제 콘텐츠를 전송 하 고 처리 하는 때 사용 하는 보안 정보를 내용입니다.

## <a name="bkmk_flow"></a>콘텐츠 흐름과 프로세스

콘텐츠 정보 및 실제 콘텐츠 흐름 4 단계도 구분 됩니다.

1.  [BranchCache 프로세스: 콘텐츠를 요청](#BKMK_8)

2.  [BranchCache 프로세스: 콘텐츠를 찾습니다.](#BKMK_9)

3.  [BranchCache 프로세스: 콘텐츠를 검색](#BKMK_10)

4.  [BranchCache 프로세스: 콘텐츠를 캐시 합니다.](#BKMK_11)

다음 섹션에서는 다음이 단계에 설명 합니다.

## <a name="BKMK_8"></a>BranchCache 프로세스: 콘텐츠를 요청

첫 번째 단계는 지점에 클라이언트 컴퓨터 주 office 등의 원격 위치에 있는 콘텐츠 서버에서 파일 또는 웹 페이지 등의 콘텐츠를 요청합니다. 콘텐츠 서버 클라이언트 컴퓨터 요청된 콘텐츠를 받을 수 있는 권한이 있는지 확인 합니다. 클라이언트 컴퓨터 권한이 부여 된 경우 콘텐츠 서버와 클라이언트는 BranchCache\ 활성화 콘텐츠 서버 콘텐츠 정보를 생성 합니다.

콘텐츠 서버 콘텐츠 정보 실제 콘텐츠에 사용 된 것과 동일한 프로토콜을 사용 하는 클라이언트 컴퓨터를 보냅니다. 

예를 들어 클라이언트 컴퓨터 요청 HTTP를 통해 웹 페이지 콘텐츠 서버 HTTP 사용 하 여 콘텐츠 정보를 보냅니다. 이 인해 유선 수준 보안 보증 콘텐츠 및 콘텐츠 정보는 동일 합니다.

(데이터 해시 + 세그먼트 시크릿) 콘텐츠 정보의 초기 부분을 받은 후 클라이언트 컴퓨터 다음과 같은 작업을 수행 합니다.

- 암호화 키 (Ke)로 세그먼트 시크릿 (Kp)를 사용합니다.

- HoD 및 Kp (HoHoDk) 세그먼트 ID를 생성 합니다.

    `HoHoDk = HMAC(Kp, HoD + C), where C is the ASCII string "MS_P2P_CACHING" with NUL terminator.`

이 계층 기본 위협 BranchCache 암호화 세그먼트 시크릿을 보호 하는 콘텐츠 데이터 블록 세그먼트 암호에 대 한 위험은. BranchCache 콘텐츠는 내 콘텐츠 블록은 선분의 세그먼트 시크릿에서 파생 암호화 키를 사용 하 여이 작업을 수행 합니다.

이 방법을 사용 하면 서버 시크릿 소유에서 하지 않은 엔터티의 데이터 블록의 실제 콘텐츠를 검색할 수 없습니다. 세그먼트 시크릿은 보안을 사용 하 여으로 처리 일반 텍스트 분할 자체에 해당 분야 세그먼트 시크릿의 기술 엔터티 세그먼트 동료에서 가져올 한 다음 암호를 해독를 사용 하기 때문에 합니다. 서버 비밀의 기술 즉시 모든 특정 일반 텍스트를 생성 하지 않습니다 하지만으로 이동한 다음 무작위 추측 공격에 데이터가 일부 부분적으로 알려진 노출 될 수 암호화 텍스트에서 특정 종류의 데이터를 추출 하는 데 사용 될 수 있습니다. 서버 시크릿 따라서 기밀로 유지 되어야 합니다.
  
## <a name="BKMK_9"></a>BranchCache 프로세스: 콘텐츠를 찾습니다.

컴퓨터에서 수신 하는 콘텐츠 정보, 후 클라이언트 세그먼트 ID를 사용 하 여을 해당 캐시 클라이언트 컴퓨터 간에 배포 또는 호스트 된 캐시 서버에 요청된 콘텐츠 로컬 지점 office 캐시에서 찾습니다.

클라이언트 컴퓨터 호스트 캐시 모드를 구성 된 경우 호스트 캐시 서버의 컴퓨터 이름을로 구성 하 고 있는 콘텐츠를 검색 하는 서버에 연결 합니다.

하지만 여러 캐시 지사에서 여러 대의 컴퓨터에 걸쳐 콘텐츠 저장 될 수 클라이언트 컴퓨터를 분산된 캐시 모드에 대 한 구성 합니다. 클라이언트 컴퓨터 콘텐츠 위치한 콘텐츠를 검색 하기 전에 검색 해야 합니다.

분산된 캐시 모드에 대 한 구성 클라이언트 컴퓨터 웹 서비스 동적 (WS 검색) 검색 프로토콜에 따라 검색 프로토콜을 사용 하 여 콘텐츠를 검색 합니다. 클라이언트 WS 검색 전송 콘텐츠를 검색할 수 캐시 된 네트워크를 통해 멀티 캐스트 검사 메시지. 검색 메시지가를 통해 요청된 콘텐츠 해당 캐시에 저장 된 콘텐츠가 일치 하는지 확인 하는 클라이언트 세그먼트 ID가 포함 됩니다. 세그먼트 ID 콘텐츠는 로컬 캐시를 일치 하는 경우 초기 검사 메시지 회신 유니캐스트 검사 일치 메시지를 사용 하 여 쿼리 클라이언트를 수신 하는 클라이언트 합니다.  

검색을 수행 하는 클라이언트가 요청 하는 콘텐츠에 대 한 콘텐츠 서버에서 제공 하는 올바른 콘텐츠 정보를 사실에 WS 검색 프로세스의 성공 여부에 따라 다릅니다.

요청 콘텐츠 단계 데이터에 대 한 기본 위협을 정보 공개 되므로 콘텐츠 정보에 대 한 액세스 권한이 부여 된 콘텐츠에 대 한 액세스 의미 합니다. 이 위험을 완화 하 고 검색 프로세스에서 찾을 수 없는 콘텐츠를 포함 하는 일반 세그먼트에 대해서는 세그먼트 ID 이외의 콘텐츠 정보를 표시 되지 않습니다.

또한 다른 클라이언트 컴퓨터에서 동일한 네트워크 서브넷 악의적인 사용자가 실행 라우터 통과 하 고 콘텐츠 원본에 BranchCache 검색 교통량을 확인할 수 있습니다.

요청한 콘텐츠를 찾지 지점에 클라이언트는 WAN 링크를 통해 콘텐츠 콘텐츠 서버에서 직접 요청 합니다.

콘텐츠를 받은 후에 로컬 캐시를 가지의 또는 호스트 된 캐시 서버에 추가 됩니다. 이 경우 콘텐츠 정보 클라이언트를 방지 하거나 캐시 서버 해시 일치 하지 않는 모든 콘텐츠는 로컬 캐시를 추가 하 여 호스팅된 합니다. 해시 비교 하 여 콘텐츠를 확인 하는 프로세스 유효한 콘텐츠가 캐시를에 추가 보호 되는 로컬 캐시 무결성 블 됩니다.

## <a name="BKMK_10"></a>BranchCache 프로세스: 콘텐츠를 검색

클라이언트 컴퓨터 호스트 캐시 서버 또는 분산된 캐시 모드 클라이언트 컴퓨터를 하는 콘텐츠 호스트에서 원하는 콘텐츠를 찾으면 클라이언트 컴퓨터 콘텐츠를 검색 하는 과정을 시작 합니다.

먼저 컴퓨터를 필요로 하는 첫 번째 블록에 대 한 콘텐츠 호스트 요청을 보냅니다. 원하는 콘텐츠를 식별 하는 세그먼트 ID 및 차단 범위를 포함 하는 요청 합니다. 하나만 블록 반환 되기 때문에 단일 블록만 차단 범위 내에 포함 되어 있습니다. (여러 블록에 대 한 요청은 현재 지원 되지 않습니다.) 클라이언트 요청 로컬 뛰어난 요청 목록에 저장 됩니다.  

유효한 요청 메시지 클라이언트에서 받으면 콘텐츠 호스트 요청에 지정 된 블록 콘텐츠 호스트 콘텐츠 캐시에 있는지 확인 합니다.

콘텐츠 호스트 콘텐츠 블록 소유에서 경우 콘텐츠 호스트 세그먼트 ID, 블록 ID, 암호화 된 데이터 차단 및 블록 암호화 하는 데 사용 하는 초기화 공격 포함 된 응답을 보냅니다.

콘텐츠 호스트 콘텐츠 블록 소유에 없는 경우 콘텐츠 호스트 빈 응답 메시지를 보냅니다. 콘텐츠 호스트 요청한 차단 되지 않았는지 클라이언트 컴퓨터 알립니다. 빈 응답 메시지 세그먼트 ID와 함께 크기가 0 데이터 블록 요청한 블록 차단 ID 포함 되어 있습니다.

클라이언트 컴퓨터 콘텐츠 호스트에서 응답 받으면 클라이언트는 메시지가 해당 요청 메시지의 뛰어난 요청 목록에 있는지 확인 합니다. (세그먼트 ID와 차단 색인 일치 해야 뛰어난 요청 합니다.)

이 인증 프로세스는 성공 클라이언트 컴퓨터 뛰어난 요청 목록에 해당 요청 메시지 없는 경우 컴퓨터에서 메시지를 삭제 합니다.

이 인증 프로세스 성공 하 고 클라이언트 컴퓨터 뛰어난 요청 목록에 해당 요청 메시지의 경우 컴퓨터 블록을 해독 합니다. 클라이언트의 적절 한 차단 해시 클라이언트 처음 원래 콘텐츠 서버에서 얻은 콘텐츠 정보를 비교 해독된 차단 다음 유효성을 검사 합니다.

블록 유효성 검사가 실패 하면 암호 해독된 블록 캐시에 저장 됩니다.

이 프로세스는 클라이언트 되는 모든 필요한 차단 될 때까지 반복 합니다.

> [!NOTE]
> 검색 프로토콜 검색 및 조합 소스에서 콘텐츠를 조립 전체 부분의 콘텐츠 한 컴퓨터에서 존재 하지 않는 경우: 일련의 캐시 모드 클라이언트 컴퓨터 호스트 캐시 서버, 배포 및-지점 캐시 하는 경우 전체 콘텐츠-본사에서 원래 콘텐츠 서버에 포함 되어 있지 않습니다.

BranchCache 콘텐츠 정보 또는 콘텐츠를 전송, 전에 데이터가 암호화 됩니다. BranchCache 암호화 응답 메시지를 차단 합니다. Windows 7에서 BranchCache 사용 하는 기본 암호화 알고리즘 aes-128, 암호화 키를 Ke, 이며 키 크기 128 bits 암호화 알고리즘 정의 된 대로 합니다. 

BranchCache는 암호화 알고리즘에 적합 한 암호화 키를 사용 하 여 블록 암호화 하는 초기화 vector를 생성 합니다. 그러면 BranchCache 메시지에 암호화 알고리즘 하 고 초기화 vector를 기록합니다. 

서버와 클라이언트 절대 교환, 공유 또는 암호화 키 간에 전송 합니다. 클라이언트 소스 콘텐츠를 호스트 하는 콘텐츠 서버에서 암호화 키를 받습니다. 블록 다음, 해독 서버에서 받은 암호화 하 고 초기화 알고리즘 vector를 사용 하 여 것입니다. 다른 명시적 인증 또는 다운로드 프로토콜에 기본 제공 되는 인증 않습니다.

### <a name="security-threats"></a>보안 위협

이 계층 기본 보안 위협 다음과 같습니다.

- 데이터와 변조 다음과 같습니다.

  *데이터와 데이터를 요청 자가에 대 한 서비스 클라이언트 유도할*합니다. BranchCache 보안 모델 해시 사용 하 여 확인도 아니고 클라이언트는 서버 데이터 변경 했습니다.  

- 정보 공개의 경우:  

    *BranchCache 적절 한 세그먼트 ID를 지정 하는 모든 클라이언트 암호화 된 콘텐츠를 보냅니다*합니다. 세그먼트 Id 공개, 되므로 클라이언트 암호화 된 콘텐츠를 받을 수 있습니다. 그러나 악의적인 사용자 암호화 된 콘텐츠를 얻고 콘텐츠를 암호화 하 암호화 키를 알고 있어야 있습니다. 위 계층 프로토콜 인증을 수행 하 고 인증 되 고 공인 클라이언트를 콘텐츠 정보를 제공 합니다. 콘텐츠 정보 보안 자체에 콘텐츠를 제공 하는 보안에 해당 이며 BranchCache 콘텐츠 정보를 제공 하지 않습니다.  

    *공격자가 있는 콘텐츠를 가져오는 유선*합니다.  BranchCache 암호화 클라이언트 AES128 비밀 키가 Ke, 유선에서 정보를 수집할 되 고에서 방지 데이터를 사용 하 여 모든 전송 합니다.  자체 데이터 했을 것 및 하는 경우 BranchCache 사용 하지 않은 전혀 보다 정보 공개의 따라서 보호 더 많거나 적을 콘텐츠 서버에서 다운로드 하는 콘텐츠 정보 동일한 방식으로 보호 됩니다.

-   서비스 거부가 다음과 같습니다.

    *클라이언트는 데이터에 대 한 요청에 당황*합니다. BranchCache 프로토콜 큐 관리 카운터 및 클라이언트 오버 되지 않도록 하려면 타이머를 통합 합니다.

## <a name="BKMK_11"></a>BranchCache 프로세스: 콘텐츠를 캐시 합니다.

분산된 캐시 모드 클라이언트 컴퓨터 및 분기 사무실에 있는 호스트 캐시 서버에서 콘텐츠 캐시 빌드됩니다 시간이 지남에 따라으로 WAN 링크를 통해 콘텐츠를 검색 합니다.

클라이언트 컴퓨터 호스트 캐시 모드도 구성 된 경우 자녀가 콘텐츠 자체 로컬 캐시를 추가 하 고 호스트 캐시 서버에 데이터를 제공 합니다. 호스트 캐시 프로토콜 서버에 알리는 호스트 캐시 콘텐츠 및 세그먼트 가용성에 대 한 클라이언트에 대 한 장치를 제공 합니다.

콘텐츠를 호스트 캐시 서버에 업로드 하는 클라이언트는 서버에 세그먼트 제공 되는 알립니다. 다음 호스트 캐시 서버 모두 콘텐츠 정보 제공 되는 세그먼트 연결 되어 있고 실제로 필요한 세그먼트 내 블록 다운로드를 검색 합니다. 이 프로세스는 클라이언트 세그먼트가 없이 더 호스트 캐시 서버 제공 될 때까지 반복 합니다.

호스트 캐시 프로토콜을 사용 하 여 호스팅된 캐시 서버를 업데이트 하려면 다음 요구 사항은 만족 해야 합니다.

- 클라이언트 컴퓨터 일련의 내에서 여 호스팅된 캐시 서버에 게 제공할 수 있는 세그먼트 블록이 필요 합니다. 클라이언트 제공 되는 세그먼트;에 대 한 콘텐츠 정보를 제공 해야 이 세그먼트 ID, 세그먼트 데이터 콘텐츠의 해시, 세그먼트 시크릿 및 세그먼트 포함 되도록 모든 블록 해시 목록이 구성 됩니다.

- 호스트 캐시 인증서와 관련 된 개인 키 호스트 캐시 서버, Windows Server 2008 R2 실행 하는 서버를 필요 하며 발급 된 인증서를 인증 기관 (캐나다)는 지점에 컴퓨터 클라이언트 신뢰할 수 있어야 합니다. 클라이언트 및 서버 성공적으로 HTTPS 서버 인증에 참여할 수 있게 합니다.

    > [!IMPORTANT]
    > Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 서버 호스트 캐시 호스트 캐시 서버 인증서와 관련 된 개인 키 필요 하지 않습니다.  

- 클라이언트 컴퓨터 호스트 캐시 서버와 있는 호스트 캐시 서버가 BranchCache 교통량 수신 전송 컨트롤 Protocol (TCP) 포트 번호의 컴퓨터 이름을으로 구성 됩니다. 호스트 캐시 서버의 인증서가이 포트에 연결 됩니다. 호스트 캐시 서버의 컴퓨터 이름을 호스트 캐시 서버가 도메인 구성원 컴퓨터 경우 정식된 도메인 이름 (FQDN) 될 수 있습니다. 또는 호스트 된 캐시 서버 도메인 구성원이 아닙니다 컴퓨터의 이름을 NetBIOS 될 수 있습니다.

- 들어오는 블록 요청에 대 한 클라이언트 컴퓨터 적극적으로 수신합니다. 듣고 있는 포트 호스트 캐시 서버에 혜택 메시지의 일환으로 클라이언트에서 전달 됩니다. 그러면 데이터 블록 구역 부분에서을 검색 하는 클라이언트 컴퓨터에 연결 하려면 BranchCache 프로토콜을 사용 하 여 호스팅된 캐시 서버 있습니다.

- 호스트 캐시 서버 초기화할 때 수신 HTTP 요청을 듣기 시작 합니다.

- 호스트 캐시 서버를 클라이언트 컴퓨터 인증을 요구 하도록 구성 된 경우 클라이언트 및 서버 호스트 캐시는 지원 HTTPS 인증 해야 합니다.

### <a name="hosted-cache-mode-cache-population"></a>호스트 캐시 모드 캐시 인구

Id. 세그먼트 포함 된 INITIAL_OFFER_MESSAGE 보내면 콘텐츠를 호스트 캐시 서버의 캐시 지점에 추가 하는 과정을 시작 호스트 캐시 서버의 블록 캐시에서 해당 세그먼트 데이터 콘텐츠의 해시, 블록 해시 목록 및 세그먼트 시크릿 검색 INITIAL_OFFER_MESSAGE 요청은 세그먼트 ID는 사용 합니다. 호스트 캐시 서버에 이미 특정 분야 콘텐츠 모든 정보는 INITIAL_OFFER_MESSAGE에 대 한 응답, 확인 됩니다 없이 다운로드 요청을 블록 발생 합니다.

호스트 캐시 서버에는에서 차단 해시와 관련 된 블록 제공 되는 데이터의 일부 없는 INITIAL_OFFER_MESSAGE에 대 한 응답 싶으세요 됩니다. 클라이언트 제공 되는 하나의 세그먼트 설명 하는 SEGMENT_INFO_MESSAGE 보냅니다. 호스트 캐시 서버가 확인 메시지에 응답 하 고는 제공에서 누락 된 블록 다운로드 시작 클라이언트 컴퓨터 합니다.

세그먼트 데이터 콘텐츠의 해시, 블록 해시 목록 및 세그먼트 시크릿은 콘텐츠를 다운로드 하는 하지 드라이버를 변조 했는지 되었거나 했거나 확인 하는 데 사용 됩니다. 다운로드 한 블록 호스트 캐시 서버의 블록 캐시에 추가 됩니다.

## <a name="bkmk_cache"></a>캐시 보안  
이 섹션 BranchCache 캐시 된 데이터는 클라이언트에서 및 호스트 캐시 서버에 고정 하는 방법에 대해 설명 합니다.

### <a name="client-computer-cache-security"></a>클라이언트 컴퓨터 캐시 보안
큰 위협은 BranchCache에 저장 된 데이터를 변조 됩니다. 공격자 캐시에 저장 된 콘텐츠 및 콘텐츠 정보로 조작 수, 경우 시도 하 고 공격 BranchCache 사용 하는 컴퓨터를 시작 하는 데 사용 수도 것입니다. 공격자 기타 데이터를 대신 악성 소프트웨어를 삽입 하 여 공격이 시작할 수 있습니다. BranchCache 블록 해시 콘텐츠 정보에 사용 하 여 모든 콘텐츠를 검사 하 여 이러한 위협 요소를 줄입니다. 시스템에 침투와이 데이터를 조작 하려고 삭제 되 고 원본에서 유효한 데이터로 바뀝니다.

보조 위협이 있는 BranchCache에 저장 된 데이터에는 정보 공개 합니다. 분산된 캐시 모드로 클라이언트 캐시만 자체; 요청한는 콘텐츠 그러나이 데이터 지우기 텍스트에 저장 되 고 위험에 노출 될 수 있습니다. 캐시 액세스만 BranchCache 서비스를 제한할 위해는 로컬 캐시는 ACL에 지정 된 파일 시스템 권한 보호 됩니다. 

ACL은 권한 없는 사용자나 캐시에 액세스 하지 못하도록 차단 효과적 이지만 취해도 관리자 권한이 있는 사용자가 수동으로에 지정 된 권한 변경 하 여 캐시에 액세스할 수 있습니다. BranchCache 관리자 계정 악의적인 사용 으로부터 보호 하지 않습니다.

콘텐츠 캐시에 저장 된 데이터를 암호화 되지 데이터 누수 제기 되는 문제를 암호화 기술을 BitLocker 등의 암호화 EFS (파일 시스템)를 사용할 수 있습니다. BranchCache에서 사용 되는 로컬 캐시; 지점에 컴퓨터에 통한 정보가 노출 위협 증가 하지 캐시 디스크 암호화 되지 않은 있는 파일의 복사본과만 포함 되어 있습니다. 

전체 디스크 암호화는 실제 클라이언트 보안이 보장 하기 어려운 인 환경 특히 중요 합니다. 예를 들어, 전체 디스크 암호화 지점 환경에서 제거 될 수 있는 모바일 컴퓨터에 중요 한 데이터를 보호 하는 데 도움이 됩니다.

### <a name="hosted-cache-server-cache-security"></a>호스트 캐시 서버 캐시 보안

호스트 캐시 모드에서 가장 큰 호스트 캐시 서버 보안 위협 정보 공개입니다. 캐시 된 데이터를 보호 하는 파일 시스템 권한이 있는 호스트 캐시 환경에서 BranchCache 분산된 캐시 모드로 유사한 방식으로 작동 합니다. 호스트 캐시 서버 모든 데이터 한 클라이언트를 요청 하는 것이 아니라 지점 모든 BranchCache 활성화 컴퓨터를 요청 하는 콘텐츠를 저장 하는 다릅니다. 훨씬 더 많은 데이터 위험에 노출 때문에이 캐시 무단 결과 심각한 훨씬 더 될 수 있습니다.  
  
호스트 캐시 서버 실행 되 고 있는 Windows Server 2008 R2 호스트 캐시 환경에서 BitLocker 또는 EFS 같은 암호화 기술을 사용 하는 중요 한 데이터 WAN 링크를 통해 액세스할 수 있는 지사에서 클라이언트의 경우이 좋습니다. 이기도 호스트 캐시에 물리적 액세스 하지 못하도록 하는 데 필요한 디스크 암호화만 때 컴퓨터 꺼져 공격자 물리적 액세스 하는 경우 작동 하기 때문입니다.  컴퓨터가 켜 지거나 절전 모드, 경우 디스크 암호화 작은 보호를 제공 합니다.

> [!NOTE]
> Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 호스트 캐시 서버 되므로 추가 암호화 기술 사용 필요 하지 않습니다. 기본적으로 캐시에 모든 데이터를 암호화 됩니다.

클라이언트 호스트 캐시 모드를 구성 된 경우에 캐시 데이터를 로컬로 여전히 및 호스트 캐시 서버의 캐시 뿐 아니라 로컬 캐시를 보호 하기 위한 조치를 수행 하는 것이 좋습니다.