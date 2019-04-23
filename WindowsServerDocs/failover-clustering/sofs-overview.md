---
title: 응용 프로그램 데이터를 위한 스케일 아웃 파일 서버 개요
description: Windows Server 201 R2, Windows Server 2012 및 Windows Server 2016에 대 한 스케일 아웃 파일 서버 기능의 개요를 설명 합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 04e25e9c69062611d9d14c220614f148ac5de770
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884774"
---
# <a name="scale-out-file-server-for-application-data-overview"></a>응용 프로그램 데이터를 위한 스케일 아웃 파일 서버 개요

>적용 대상: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

스케일 아웃 파일 서버는 파일 기반 서버 응용 프로그램 저장소에 계속 사용할 수 있는 스케일 아웃 파일 공유를 제공하도록 설계된 기능입니다. 스케일 아웃 파일 공유는 같은 클러스터의 여러 노드에서 동일한 폴더를 공유하는 기능을 제공합니다. 이 시나리오는 스케일 아웃 파일 서버를 계획 및 배포하는 방법에 중점을 둡니다.

다음 방법 중 하나를 사용하여 클러스터된 파일 서버를 배포 및 구성할 수 있습니다.

- **응용 프로그램 데이터용 스케일 아웃 파일 서버** 이 클러스터 된 파일 서버 기능은 Windows Server 2012에서 도입 되었으며 파일 공유에 Hyper-v 가상 컴퓨터 파일과 같은 서버 응용 프로그램 데이터를 저장 하며 비슷한 수준의 얻을 수 있습니다 안정성, 가용성, 관리 효율성 및 저장소 영역 네트워크에서 기대 되는 성능 우선 합니다. 모든 파일 공유는 모든 노드에서 동시에 온라인 상태입니다. 이런 종류의 클러스터된 파일 서버와 연결된 파일 공유는 스케일 아웃 파일 공유라고 불립니다. 이는 때에 따라 활성-활성이라고도 불립니다. SMB(서버 메시지 블록)를 통해 Hyper-V를 배포하거나 SMB를 통해 Microsoft SQL Server를 배포하는 경우에 권장되는 파일 서버 유형입니다.
- **일반 용도의 파일 서버** 이는 장애 조치(failover) 클러스터링이 도입된 이후 Windows Server에서 지원되는 클러스터된 파일 서버의 연장선 상에 있습니다. 이 종류의 클러스터된 파일 서버 및 클러스터된 파일 서버와 연결된 모든 공유는 한 번에 한 노드에서 온라인 상태입니다. 활성-수동 또는 이중-활성으로 불리는 경우도 있습니다. 이러한 종류의 클러스터된 파일 서버와 연결된 파일 공유는 클러스터된 파일 공유라 불립니다. 정보 근로자 시나리오를 배포하는 경우에 권장되는 파일 서버 유형입니다.

## <a name="scenario-description"></a>시나리오 설명

스케일 아웃 파일 공유를 사용하면 클러스터의 여러 노드에서 동일한 폴더를 공유할 수 있습니다. 예를 들어, 4 노드 파일 서버 클러스터 규모를 확장할 서버 메시지 블록 (SMB)를 사용 하는 경우 Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 컴퓨터는 4 개의 노드 중 어디 에서도 파일 공유를 액세스할 수 있습니다. 이는 새로운 Windows Server 장애 조치(failover) 클러스터링 기능 및 Windows 파일 서버 프로토콜, SMB 3.0의 기능을 활용하여 달성됩니다. 파일 서버 관리자는 스케일 아웃 파일 공유 및 지속적으로 사용할 수 있는 파일 서비스를 서버 응용 프로그램에 제공하여 더 많은 서버를 온라인 상태로 전환하는 방법을 통해 늘어나는 수요에 재빠르게 대응할 수 있습니다. 이 모든 과정이 프로덕션 환경에서 서버 응용 프로그램에 완전히 투명하게 실행됩니다.

스케일 아웃 파일 서버에서 제공하는 주요 이점은 다음과 같습니다.

- **활성-활성 파일 공유**합니다. 모든 클러스터 노드에 적용 하 고 SMB 클라이언트 요청을 처리할 수 있습니다. 모든 클러스터 노드를 통해 파일 공유 콘텐츠에 동시에 액세스할 수 있도록 만드는 방법으로 SMB 3.0 클러스터 및 클라이언트는 서비스 중단을 수반하는 예기치 않은 실패 및 계획된 유지 보수가 발생할 때 투명한 장애 조치(failover)를 대체 클러스터 노드에 제공할 수 있도록 협력합니다.
- **증가 한 대역폭**합니다. 최대 공유 대역폭은 모든 파일 서버 클러스터 노드의 총 대역폭입니다. Windows Server의 이전 버전과는 다르게 총 대역폭은 더 이상 단일 클러스터 노드의 대역폭으로 제한되지 않으며 오히려 지원 저장소 시스템의 기능이 제약 조건을 정의합니다. 노드를 추가하면 총 대역폭을 높일 수 있습니다.
- **CHKDSK 가동**합니다. Windows Server 2012의 CHKDSK은 파일 시스템은 복구에 대 한 오프 라인 시간을 대폭 줄이도록 크게 향상 되었습니다. CSV(클러스터된 공유 볼륨)는 오프라인 단계를 제거하여 이를 한 단계 더 발전시킵니다. CSVFS(CSV 파일 시스템)는 파일 시스템에서 열린 핸들로 응용 프로그램에 영향을 주지 않으면서 CHKDSK를 사용할 수 있습니다.
- **클러스터 된 공유 볼륨 캐시**합니다. Windows Server 2012의 Csv에 크게 성능을 개선할 수 있는 특정 시나리오에서와 같이 가상 데스크톱 인프라 (VDI)에 읽기 캐시 지원이 도입 되었습니다.
- **간편해 진 관리**합니다. 스케일 아웃 파일 서버를 사용 하 여 스케일 아웃 파일 서버를 만들고 필요한 Csv 및 파일 공유를 추가 합니다. 더 이상 클러스터 디스크가 따로 있는 클러스터된 파일 서버를 여러 개 만든 뒤 배치 정책을 세워서 각 클러스터 노드의 작업을 확인할 필요가 없습니다.
- **스케일 아웃 파일 서버 클라이언트 자동 리 밸런스**합니다. 확장성 및 관리 효율성 스케일 아웃 파일 서버에 대 한 Windows Server 2012 R2에서 개선 자동 리 밸런스 합니다. SMB 클라이언트 연결은 서버 단위가 아니라 파일 공유 단위로 추적되며, 클라이언트는 파일 공유에서 사용하는 볼륨에 대한 최상의 액세스를 제공하는 클러스터 노드로 리디렉션됩니다. 따라서 파일 서버 노드 간의 리디렉션 트래픽이 감소하므로 효율성이 향상됩니다. 클라이언트는 초기 연결 후 클러스터 저장소가 다시 구성된 경우에 리디렉션됩니다.

## <a name="in-this-scenario"></a>이 시나리오의 내용

다음 항목은 스케일 아웃 파일 서버를 배포하는 데 도움이 됩니다.

- [스케일 아웃 파일 서버에 대 한 계획](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134258(v%3dws.11)>)

  - [1단계: 스케일 아웃 파일 서버의 저장소 계획](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134181%28v%3dws.11%29>)
  - [2단계: 스케일 아웃 파일 서버의 네트워킹 계획](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134253%28v%3dws.11%29>)

- [스케일 아웃 파일 서버 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831359%28v%3dws.11%29>)

  - [1단계: 스케일 아웃 파일 서버의 필수 구성 요소를 설치 합니다.](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831478%28v%3dws.11%29>)
  - [2단계: 스케일 아웃 파일 서버 구성](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831718%28v%3dws.11%29>)
  - [3 단계: 스케일 아웃 파일 서버를 사용 하기 위해 Hyper-v 구성](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831463%28v%3dws.11%29>)
  - [4 단계: 스케일 아웃 파일 서버를 사용 하도록 Microsoft SQL Server 구성](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831815%28v%3dws.11%29>)

## <a name="when-to-use-scale-out-file-server"></a>스케일 아웃 파일 서버를 사용하는 경우

사용자의 작업 부하로 수많은 메타데이터 작업이 생성된다면 스케일 아웃 파일 서버를 사용해서는 안 됩니다. 이러한 메타데이터 작업에는 파일 여닫기, 새로운 파일 만들기, 기존 파일 이름 변경하기 등이 있습니다. 일반적인 정보 산업 근로자는 수많은 메타데이터 작업을 생성합니다. 스케일 아웃 파일 서버는 스케일 아웃 파일 서버가 제공하는 확장성과 간결성을 원하며 스케일 아웃 파일 서버로 지원되는 기술만 필요한 경우에 사용할 수 있습니다.

다음 표에서는 SMB 3.0, 일반적인 Windows 파일 시스템, 파일 서버 데이터 관리 기술 및 일반적인 작업의 기능을 보여 줍니다. 기술이 스케일 아웃 파일 서버로 지원되는지 여부 또는 기존의 클러스터된 파일 서버(일반 용도로 파일 서버라고도 함)가 필요한지 여부를 확인할 수 있습니다.

<table>
<thead>
<tr class="header">
<th>기술 영역</th>
<th>기능</th>
<th>일반 용도 파일 서버 클러스터</th>
<th>스케일 아웃 파일 서버</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>SMB</td>
<td>SMB 지속적인 가용성</td>
<td>예</td>
<td>예</td>
</tr>
<tr class="even">
<td>SMB</td>
<td>SMB 다중 채널</td>
<td>예</td>
<td>예</td>
</tr>
<tr class="odd">
<td>SMB</td>
<td>SMB 다이렉트</td>
<td>예</td>
<td>예</td>
</tr>
<tr class="even">
<td>SMB</td>
<td>SMB 암호화</td>
<td>예</td>
<td>예</td>
</tr>
<tr class="odd">
<td>SMB</td>
<td>SMB 투명 장애 조치(Failover)</td>
<td>예(지속적인 가용성을 사용할 수 있는 경우)</td>
<td>예</td>
</tr>
<tr class="even">
<td>파일 시스템</td>
<td>NTFS</td>
<td>예</td>
<td>NA</td>
</tr>
<tr class="odd">
<td>파일 시스템</td>
<td>복원 파일 시스템 (<a href="https://docs.microsoft.com/windows-server/storage/refs/refs-overview">ReFS</a>)</td>
<td>저장소를 사용 하 여 권장 되는 공간 다이렉트</td>
<td>저장소를 사용 하 여 권장 되는 공간 다이렉트</td>
</tr>
<tr class="even">
<td>파일 시스템</td>
<td>CSV(클러스터 공유 볼륨) 파일 시스템</td>
<td>NA</td>
<td>예</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>BranchCache</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>데이터 중복 제거(Windows Server 2012)</td>
<td>예</td>
<td>아니오</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>데이터 중복 제거(Windows Server 2012 R2)</td>
<td>예</td>
<td>예(VDI만 해당)</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>DFSN(DFS 네임스페이스) 루트 서버 루트</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>DFSN(DFS 네임스페이스) 폴더 대상 서버</td>
<td>예</td>
<td>예</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>DFSR(DFS 복제)</td>
<td>예</td>
<td>아니오</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>파일 서버 리소스 관리자(화면 및 할당량)</td>
<td>예</td>
<td>아니오</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>파일 분류 인프라</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>동적 Access Control(클레임 기반 액세스, CAP)</td>
<td>예</td>
<td>아니오</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>폴더 리디렉션</td>
<td>예</td>
<td>권장되지 않음*</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>오프라인 파일(클라이언트 쪽 캐싱)</td>
<td>예</td>
<td>권장되지 않음*</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>로밍 사용자 프로필</td>
<td>예</td>
<td>권장되지 않음*</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>홈 디렉터리</td>
<td>예</td>
<td>권장되지 않음*</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>클라우드 폴더</td>
<td>예</td>
<td>아니오</td>
</tr>
<tr class="odd">
<td>NFS</td>
<td>NFS 서버</td>
<td>예</td>
<td>아니오</td>
</tr>
<tr class="even">
<td>애플리케이션</td>
<td>Hyper-V</td>
<td>권장되지 않음</td>
<td>예</td>
</tr>
<tr class="odd">
<td>애플리케이션</td>
<td>Microsoft SQL Server</td>
<td>권장되지 않음</td>
<td>예</td>
</tr>
</tbody>
</table>

\* 폴더 리디렉션, 오프 라인 파일, 로밍 사용자 프로필 또는 홈 디렉터리에 기록 (버퍼링) 없이 디스크에 즉시 써야 하는 많은 생성 지속적으로 사용 가능한 파일 공유를 사용 하는 경우에 비교 했을 때 성능이 감소 일반 용도의 파일 공유 합니다. 또한 지속적으로 사용 가능한 파일 공유는 파일 서버 리소스 관리자 및 Windows XP를 실행하는 PC와 호환되지 않습니다. 이외에도, 사용자가 공유에 액세스할 수 없게 된 후 3-6분 동안 오프라인 파일이 오프라인 모드로 전환되지 않아 오프라인 파일의 항상 오프라인 모드를 사용하지 않는 사용자에게 불편을 줄 수 있습니다.

## <a name="practical-applications"></a>유용한 팁

스케일 아웃 파일 서버는 서버 응용 프로그램 저장소에 적합합니다. 스케일 아웃 파일 공유에 해당 데이터를 저장할 수 있는 서버 응용 프로그램의 몇 가지 예는 다음과 같습니다.

- IIS(인터넷 정보 서비스) 웹 서버는 스케일 아웃 파일 공유에 웹 사이트에 대한 구성 및 데이터를 저장할 수 있습니다. 자세한 내용은 [공유 구성](http://www.iis.net/learn/manage/managing-your-configuration-settings/shared-configuration_264)을 참조하세요.
- Hyper-V는 스케일 아웃 파일 공유에 구성 및 라이브 가상 디스크를 저장할 수 있습니다. 자세한 내용은 [SMB를 통한 Hyper-V 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)를 참조하세요.
- SQL Server는 스케일 아웃 파일 공유에 라이브 데이터베이스 파일을 저장할 수 있습니다. 자세한 내용은 [SMB 파일 공유와 함께 저장소로 SQL Server 설치 옵션](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option)을 참조하세요.
- VMM(Virtual Machine Manager)은 스케일 아웃 파일 공유에 가상 컴퓨터 템플릿 및 관련 파일을 포함하는 라이브러리 공유를 저장할 수 있습니다. 그러나 라이브러리 서버 자체는 스케일 아웃 파일 서버를 수 없습니다-독립 실행형 서버 또는 스케일 아웃 파일 서버 클러스터 역할을 사용 하지 않는 장애 조치 클러스터에 있어야 합니다.

스케일 아웃 파일 공유를 라이브러리 공유로 사용하는 경우 스케일 아웃 파일 서버와 호환되는 기술만 사용할 수 있습니다. 예를 들어 DFS 복제를 사용하여 스케일 아웃 파일 공유에 호스트된 라이브러리 공유를 복제할 수 없습니다. 또한 스케일 아웃 파일 서버에 최신 소프트웨어 업데이트가 설치되어 있어야 합니다.

스케일 아웃 파일 공유를 라이브러리 공유로 사용하려면 먼저 로컬 공유를 포함하거나 공유가 없는 라이브러리 서버(대체로 가상 컴퓨터)를 추가합니다. 그런 다음 라이브러리 공유를 추가할 때 스케일 아웃 파일 서버에 호스트된 파일 공유를 선택합니다. 이 공유는 VMM에서 관리되고 라이브러리 서버 전용으로 생성되어야 합니다. 또한 스케일 아웃 파일 서버에 최신 업데이트를 설치해야 합니다. VMM 라이브러리 서버 및 라이브러리 공유를 추가 하는 방법에 대 한 자세한 내용은 참조 하십시오 [VMM 라이브러리에 프로필 추가](https://docs.microsoft.com/system-center/vmm/library-profiles?view=sc-vmm-1801)합니다. 파일 및 저장소 서비스에 대해 현재 사용할 수 있는 핫픽스 목록은 [Microsoft 기술 자료 문서 2899011](https://support.microsoft.com/help/2899011/list-of-currently-available-hotfixes-for-the-file-services-technologie)을 참조하세요.

>[!NOTE]
>정보 근로자와 같은 일부 사용자의 작업은 성능에 더 큰 영향을 줍니다. 예를 들어 파일 열기 및 닫기, 새 파일 만들기, 기존 파일의 이름 바꾸기와 같은 작업은 여러 사용자가 수행할 경우 성능에 영향을 줍니다. 지속적인 가용성을 사용할 수 있는 파일 공유는 데이터 무결성을 제공하지만 전반적인 성능에 영향을 줍니다. 지속적인 가용성을 위해 디스크에 데이터 동시 쓰기를 수행하여 스케일 아웃 파일 서버에서 클러스터 노드 오류가 발생할 경우 무결성을 보장해야 합니다. 따라서 사용자가 지속적으로 사용 가능한 파일 공유에서 여러 개의 큰 파일을 파일 서버에 복사할 경우 성능이 훨씬 저하될 수 있습니다.

## <a name="features-included-in-this-scenario"></a>이 시나리오에 포함된 기능

다음 표에는 이 시나리오에 포함된 기능이 나열되어 있으며, 이 기능이 시나리오를 지원하는 방법에 대한 설명이 나와 있습니다.

<table>
<thead>
<tr class="header">
<th>기능</th>
<th>이 시나리오를 지원하는 방법</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="failover-clustering.md">장애 조치 클러스터링</a></td>
<td>장애 조치 클러스터 스케일 아웃 파일 서버를 지원 하도록 Windows Server 2012에는 다음 기능을 추가 했습니다. 분산된 네트워크 이름, 스케일 아웃 파일 서버 리소스 종류, 클러스터 공유 볼륨 (CSV) 2 및 스케일 아웃 파일 서버 고가용성 역할입니다. 이러한 기능에 대 한 자세한 내용은 참조 하세요. <a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)">What's New in Windows Server 2012 [리디렉션 됨]에서 장애 조치 클러스터링</a>합니다.</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831795(v%3dws.11)">서버 메시지 블록</a></td>
<td>SMB 3.0 스케일 아웃 파일 서버를 지원 하도록 Windows Server 2012에는 다음 기능을 추가 했습니다. SMB 투명 장애 조치(failover), SMB 다중 채널 및 SMB 다이렉트 기능이 추가되었습니다.<br />
<br />
Windows Server 2012 R2의 SMB에 대 한 새로운 기능과 변경 된 기능에 자세한 내용은 참조 <a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)">What's New in Windows Server에서 SMB</a>합니다.</td>
</tr>
</tbody>
</table>

## <a name="more-information"></a>자세한 정보

- [소프트웨어 정의 저장소 디자인 고려 사항 가이드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt243829(v%3dws.11)>)
- [서버, 저장소 및 네트워크 가용성 향상](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831437(v%3dws.11)>)
- [SMB를 통한 Hyper-v 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
- [서버 응용 프로그램에 대 한 빠르고 효율적인 파일 서버 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
- [규모를 확장하느냐 마느냐 그것이 문제다](https://blogs.technet.com/b/filecab/archive/2013/12/05/to-scale-out-or-not-to-scale-out-that-is-the-question.aspx) (블로그 게시물)
- [폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh848267(v%3dws.11)>)