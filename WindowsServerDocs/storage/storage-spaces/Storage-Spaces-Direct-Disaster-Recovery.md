---
title: 하이퍼 수렴 형 인프라에 대 한 재해 복구 시나리오
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: johnmarlin-msft
ms.date: 03/29/2018
description: 이 문서에서는 Microsoft HCI (저장소 공간 다이렉트)의 재해 복구를 위해 현재 제공 되는 시나리오를 설명합니다.
ms.localizationpriority: medium
ms.openlocfilehash: c844c56c3a1717658bcdb970e78d45b5cdda861c
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453126"
---
# <a name="disaster-recovery-with-storage-spaces-direct"></a>저장소 공간 다이렉트를 사용 하 여 재해 복구

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 재해 복구를 위해 어떻게 하이퍼 수렴 형 인프라 (HCI) 시나리오를 구성할 수 있습니다.

많은 회사에서 하이퍼 수렴 형 솔루션 실행 및 재해 대비 계획 수를 유지 하거나 다시 프로덕션으로 신속 하 게 재해가 발생 하는 경우. 재해 복구를 위한 HCI를 구성 하는 방법은 여러 가지가 있습니다.이 문서에서는 현재 사용할 수 있는 옵션을 설명 하며

경우 토론 재해가 발생할 경우 가용성을 복원 하는 복구 시간 목표 (RTO)로 알려진 중심으로 합니다. 이것이 비즈니스에 사용할 수 없는 결과가 발생 하지 않도록 하려면 서비스 해야 복원할 대상으로 하는 기간입니다. 경우에 따라이 프로세스는 거의 즉시 복원 하는 프로덕션을 사용 하 여 자동으로 발생할 수 있습니다. 다른 경우에 서비스를 복원 하려면 관리자가 수동으로 조작 수행 되어야 합니다.

하이퍼 수렴 형 된 재해 복구 옵션을 현재 다음과 같습니다.

1. 여러 클러스터 활용 하 여 저장소 복제본
2. Hyper-v 복제본 클러스터 간에
3. Backup 및 Restore 메서드

## <a name="multiple-clusters-utilizing-storage-replica"></a>여러 클러스터 활용 하 여 저장소 복제본

[저장소 복제본](../storage-replica/storage-replica-overview.md) 볼륨의 복제를 사용 하도록 설정 하 고 동기 및 비동기 복제를 지원 합니다. 동기 또는 비동기 복제를 사용할지를 선택할 때 복구 지점 목표 (RPO)를 고려해 야 합니다. 복구 지점 목표는 의향이 없다면 주요 손실 간주 되기 전에 발생 가능한 데이터 손실의 양입니다. 동기 복제를 사용 하 여 이동 하면 동시에 양쪽에 쓸 순차적으로 됩니다. 으로 전환 하면 사용 하 여 비동기 쓰기는 매우 빠른 복제 되지만 여전히 손실 될 수 있습니다. 가장 잘 작동 하는 수에 대 한 참조를 응용 프로그램 또는 파일 사용을 고려해 야 합니다.

저장소 복제본은 파일 수준 및 블록 수준 복사 메커니즘 즉, 중요 하지 않습니다 복제 되는 데이터의 종류입니다. 따라서이 하이퍼 수렴 형 인프라에 대 한 인기 있는 옵션입니다. 저장소 복제본도 활용할 수 있습니다 다른 종류의 드라이브 하나 HCI에 모두 형식 저장소를 포함 하므로, 복제 파트너 간의 이며 다른 형식 저장소를 다른 아무 문제 없습니다. 

하나의 중요 한 저장소 복제본의 기능은 온-프레미스 뿐만 아니라 Azure에서 실행할 수 있습니다. 온-프레미스에서 온-프레미스, Azure에서 Azure 또는 온-프레미스에서 Azure로 (또는 그 반대로)를 설정할 수 있습니다.

이 시나리오에서는 두 개의 별도 독립적인 클러스터가 있습니다. HCI 간에 저장소 복제본을 구성 하려면의 단계를 따르면 [클러스터와 클러스터 간 저장소 복제](../storage-replica/cluster-to-cluster-storage-replication.md)합니다.

![저장소 복제 다이어그램](media/storage-spaces-direct-disaster-recovery/Disaster-Recovery-Figure1.png)

다음 고려 사항에는 저장소 복제본을 배포할 때 적용 됩니다. 

1.  복제를 구성 합니다. 장애 조치 클러스터링 외부에서 수행 됩니다. 
2.  복제 방법 선택 네트워크 대기 시간 및 RPO 요구 사항에 따라 좌우 됩니다. 동기 오류 시 데이터가 손실 되지 않도록 하려면 크래시 일관성을 사용 하 여 지연율이 낮은 네트워크에서 데이터를 복제 합니다. 비동기 복제 대기 시간이 높기 있지만 각 사이트를 사용 하 여 네트워크를 통해 데이터를 동일한 복사본 실패 시에 없을 수 있습니다. 
3.  재해 시 클러스터 간의 장애 조치 자동 없는 하 고 저장소 복제본 PowerShell cmdlet을 통해 수동으로 오케스트레이션 수 해야 합니다. 위의 다이어그램에서 자가용은 주 서버이 고 ClusterB은 보조 합니다. 자가용 다운 되 면 리소스를 가져올 수 있습니다 전에를 주 ClusterB를 수동으로 설정 해야 합니다. 자가용 백업 되 면 보조 복제본을 확인 해야 합니다. 모든 데이터를 동기화 된, 변경 후 다시 원래 설정 된 방식으로 역할을 교환 합니다.
4.  저장소 복제본은 데이터를 복제만 있으므로 새 가상 컴퓨터나 Scale Out 파일 서버 (SOFS)이이 데이터를 활용 하 여 장애 조치 클러스터 관리자 내에서 복제 파트너에 생성 해야 합니다.

가상 머신 또는 SOFS 클러스터에서 실행 해야 하는 경우 저장소 복제본을 사용할 수 있습니다. HCI 복제본의 리소스를 온라인 상태로 전환 수동 또는 자동화 된 PowerShell 스크립트를 사용 하 여 가능 합니다.

## <a name="hyper-v-replica"></a>Hyper-V 복제본

[Hyper-v 복제본](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/set-up-hyper-v-replica) 하이퍼 수렴 형 인프라에서 재해 복구를 위한 가상 머신 수준 복제를 제공 합니다. 가상 머신을 가져오고 (복제본) Azure 또는 보조 사이트에 복제 하는 Hyper-v 복제본에서 수행할 수 있는 작업입니다. 그런 다음 보조 사이트에서 Hyper-v 복제본 수 가상 머신을 복제 세 번째 (확장 된 복제본).

![Hyper-v 복제 다이어그램](media/storage-spaces-direct-disaster-recovery/Disaster-Recovery-Figure2.png)

Hyper-v 복제본을 사용 하 여 복제를 알아서 Hyper-v에서. 복제에 대 한 가상 컴퓨터를 먼저 사용 하도록 설정한 경우 해당 복제본 클러스터를 전송할 수 있도록 하려는 초기 복사본에 대 한 세 가지 선택 사항이 있습니다.

1.  네트워크를 통해 초기 복사본 보내기
2.  서버에 수동으로 복사할 수 있도록 외부 미디어 초기 복사본 보내기
3.  복제본 호스트에 이미 만들어진 기존 가상 컴퓨터를 사용 합니다.

이 초기 복제가 수행 될 때에 대 한 다른 옵션이입니다.

1.  복제를 즉시 시작
2.  초기 복제를 수행 하면 시간을 예약 합니다. 

해야 하는 다른 고려 사항은 다음과 같습니다.

- 어떤 VHD/VHDX의 복제 하려고 합니다. 모두 또는 둘 중 하나만 복제 하도록 선택할 수 있습니다.
- 저장 하려는 복구 지점의 수입니다. 있는 복원 하려는 시점에 대 한 몇 가지 옵션이 하려는 경우 사용자가 원하는 지정 하려는 것입니다. 복원 지점 하나를 원하는 경우에도 선택할 수 있습니다.
- 얼마나 자주 볼륨 섀도 복사본 서비스 (vss) 증분 섀도 복사본을 복제 하려고 합니다.
- 빈도 (30 초, 5 분, 15 분) 변경 내용을 복제 합니다.

HCI Hyper-v 복제본에 참여할 때 있어야 합니다 [Hyper-v 복제본 브로커](https://blogs.technet.microsoft.com/virtualization/2012/03/27/why-is-the-hyper-v-replica-broker-required/) 각 클러스터에서 생성 된 리소스입니다. 이 리소스는 몇 가지를 수행합니다.

1.  제공 단일 네임 스페이스에 연결 하는 Hyper-v 복제본에 대 한 각 클러스터에 대 한 합니다.
2.  먼저 복사본을 받으면 복제본 (또는 확장 된 복제본)에 저장 됩니다 하는 클러스터 내의 노드를 결정 합니다.
3.  가상 머신을 다른 노드로 이동 하는 경우 복제본 (또는 확장 된 복제본) 소유 하는 노드 계속 추적 합니다. 적절 한 노드 정보를 보낼 수 있습니다 복제 수행 될 때 되도록이 이벤트를 추적 해야 합니다.

## <a name="backup-and-restore"></a>Backup 및 Restore 메서드

거의 없는 이야기 하지만 중요 한 기존 재해 복구 옵션은 전체 클러스터 또는 클러스터의 노드 실패 합니다. 이 시나리오를 사용 하 여 두 옵션 중 하나는 Windows NT 백업을 사용 합니다. 

것이 항상 하이퍼 수렴 형 인프라의 정기적으로 백업 하도록 권장 합니다. 클러스터 서비스가 실행 되는 동안, 시스템 상태 백업을 사용 하는 경우, 클러스터 레지스트리 데이터베이스는 해당 백업의 일부가 것입니다. 클러스터 또는 데이터베이스 복원에 (비-신뢰할 수 있음 및 신뢰할 수 있음)는 두 가지 방법이 있습니다.

### <a name="non-authoritative"></a>권한 없는

권한 없는 복원 Windows NT 백업을 사용 하 여 수행할 수 있으며 해당 클러스터 노드 자체의 전체 복원 하는 것과 같습니다. 클러스터 노드 (및 클러스터 레지스트리 데이터베이스)를 복원 해야 하는 경우 및 모든 현재 클러스터 정보 좋은 사용 하 여 신뢰할 수 없는 복원할 수 있습니다. 권한 없는 복원 WBADMIN 명령줄 이나 Windows NT 백업 인터페이스를 통해 수행할 수 있습니다. EXE 수 있습니다.

노드를 복원한 후 클러스터에 가입 하도록 합니다. 어떻게 되나요는 기존 실행 중인 클러스터로 이동 하 고 현재를 사용 하 여 모든 해당 정보를 업데이트 됩니다.

### <a name="authoritative"></a>신뢰할 수 있는

반면에 클러스터 구성의 정식 복원을 다시에서 클러스터 구성을 사용합니다. 자체 클러스터 정보 손실 되어 복원 해야 하는 경우에이 유형의 복원 작업 수행. 예를 들어 누군가가 실수로 1천 개가 넘는 공유를 포함 하는 파일 서버를 삭제 하 고 다시 필요 합니다. 클러스터의 정식 복원을 완료 백업 명령줄에서 실행 하는 것이 필요 합니다.

신뢰할 수 있는 복원 하는 경우 클러스터 노드에서 시작 되 면 클러스터 보기에서 다른 모든 노드에서 클러스터 서비스가 중지 되 고 클러스터 구성 고정 된 합니다. 이 때문에 복원 된 실행 하는 노드에서 클러스터 서비스가 클러스터 구성의 새 복사본을 사용 하 여 클러스터 형식이 있으므로 먼저 시작할 중요 한 것입니다.

정식 복원을 통해를 실행 하려면 다음 단계를 수행할 수 있습니다.

1.  WBADMIN을 실행 합니다. 설치 및 시스템 상태 구성 요소 중 하나 인지 확인 하려는 백업의 최신 버전을 가져오려면 관리자 명령 프롬프트에서 EXE 복원할 수 있습니다.

    ```powershell
    Wbadmin get versions
    ```

2.  경우 있는 버전 백업에는 클러스터에 레지스트리 정보 구성 요소로 결정 합니다. 이 명령은, 버전 및 3 단계에서에서 사용 하기 위해 응용 프로그램/구성 요소에서 해야 하는 몇 가지 항목이 있습니다. 버전의 경우 예를 들어 백업 2018 년 1 월 3 일 오전 2 시 04 구현 되었으며이 필요한 복원 합니다.

    ```powershell
    wbadmin get items -backuptarget:\\backupserver\location
    ```

3.  필요한 클러스터 레지스트리 버전만 복구할 정식 복원을 시작 합니다. 

    ```powershell
    wbadmin start recovery -version:01/03/2018-02:04 -itemtype:app -items:cluster
    ```

복원이 수행 되 면이 노드는 클러스터 서비스를 처음 시작 하 고 클러스터에 있는 이어야 합니다. 다른 모든 노드의 시작 하 고 클러스터에 가입 해야 다음 합니다.

## <a name="summary"></a>요약 

이 모든 합 하이퍼 수렴 형 재해 복구를 신중 하 게 아웃 계획 해야 하는 것입니다. 사용자의 요구에 가장 적합 한 수 고 철저히 테스트 해야 하는 몇 가지 시나리오가 있습니다. 에 하나의 항목 인 경우 친숙 한 장애 조치 클러스터를 사용 하 여 이전에 확장 클러스터 되었는지 년간 매우 인기 있는 옵션은입니다. 약간의 하이퍼 수렴 형 솔루션을 사용 하 여 디자인 변경 되었으며 기반 복원 력으로 합니다. 하이퍼 수렴 형 클러스터의 두 노드를 손실 된 경우 전체 클러스터 이동 합니다. 이는 하이퍼 수렴 형 환경의 경우 스트레치 시나리오는 지원 되지 않습니다.

