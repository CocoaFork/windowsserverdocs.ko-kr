---
title: 가상 네트워크 피어링
description: ''
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: aab4ec7c69ec5b52eae926cd1065d777415b1124
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446213"
---
# <a name="virtual-network-peering"></a>가상 네트워크 피어링

>적용 대상: Windows Server

가상 네트워크 피어 링을 통해 두 가상 네트워크에 원활 하 게 연결할 수 있습니다. 연결을 위해 피어 링 되 면 가상 네트워크를 하나로 표시 됩니다. 

가상 네트워크 피어 링을 사용 하는 이점은 다음과 같습니다.

-   피어 링 된 가상 네트워크의 가상 머신 간의 트래픽은 백본 인프라를 통해 라우팅됩니다 *개인* IP 주소를 통해서만 합니다. 가상 네트워크 간의 통신에는 공용 인터넷 또는 게이트웨이가 필요 하지 않습니다.

-   다른 가상 네트워크의 리소스 간에 짧은 대기 시간, 높은 대역폭 연결입니다.

-   다른 가상 네트워크의 리소스와 통신할 하나의 가상 네트워크의 리소스에 사용할 수 있습니다.

-   가동 중지 시간 없이 각 가상 네트워크 피어 링을 만들 때에 리소스입니다.

## <a name="requirements-and-constraints"></a>요구 사항 및 제약 조건

가상 네트워크 피어 링에 몇 가지 요구 사항 및 제약 조건이 있습니다.

- 피어 링 된 가상 네트워크는 다음 작업을 수행 해야합니다.

  -   겹치지 않는 IP 주소 공간을 가진

  -   동일한 네트워크 컨트롤러에서 관리

- 다른 가상 네트워크를 사용 하 여 가상 네트워크에 피어 링 되 면 추가 하거나 주소 공간에 주소 범위를 삭제할 수 없습니다.

  >[!TIP]
  >주소 범위를 추가 하는 경우:<ol><li>피어 링을 제거 합니다.</li><li>주소 공간을 추가 합니다.</li><li>피어 링을 다시 추가 합니다.</li></ol>

- 가상 네트워크 피어 링 하는 것은 두 가상 네트워크 간에, 이므로 파생 된 전이적 관계가 없습니다 피어 링을 통해입니다. 예를 들어 virtualNetworkA virtualNetworkB와 virtualNetworkC와 virtualNetworkB에 피어 링 하는 경우 다음 virtualNetworkA 않습니다 하지 가져오기 virtualNetworkC와 피어 링 합니다.

  [여기에 이미지]

## <a name="connectivity"></a>연결

가상 네트워크를 피어 링 할 후 각 가상 네트워크의 리소스는 피어 링 된 가상 네트워크의 리소스를 사용 하 여 직접 연결할 수 있습니다.

-   피어 링 된 가상 네트워크의 가상 머신 간의 네트워크 대기 시간이 단일 가상 네트워크 내의 대기 시간과 같습니다.

-   네트워크 처리량은 가상 머신에 대해 허용 되는 대역폭을 기반으로 합니다. 피어 링 내에서 대역폭에 대 한 추가 제한이 없습니다.

-   피어 링 된 가상 네트워크에서 가상 머신 간의 트래픽 또는 공용 인터넷을 통해서가 아니라 백본 인프라를 통해 직접 라우팅됩니다.

-   가상 네트워크의 가상 머신은 피어 링된 된 가상 네트워크에서 내부 load balancer를 액세스할 수 있습니다.

원하는 경우 다른 가상 네트워크 또는 서브넷에 대 한 액세스를 차단 하려면 각 가상 네트워크에 대 한 액세스 제어 목록 (Acl)을 적용할 수 있습니다. (기본 옵션 임) 피어 링 된 가상 네트워크 간의 전체 연결을 열 경우에 특정 서브넷 또는 가상 컴퓨터를 차단 하거나 특정 액세스를 거부할 Acl을 적용할 수 있습니다. Acl에 대 한 자세한 내용은 참조 하세요 [사용 하 여 액세스 제어 목록 (Acl) 데이터 센터 네트워크 트래픽 흐름을 관리 하려면](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-acls-for-traffic-flow)합니다.

## <a name="service-chaining"></a>서비스 체 이닝

서비스 체 이닝을 사용 하도록 설정 하려면 다음 홉 IP 주소와 피어 링 된 가상 네트워크에서 가상 머신을 가리키는 사용자 정의 경로 구성할 수 있습니다. 서비스 체 이닝 있도록 트래픽을 하나의 가상 네트워크에서 사용자 정의 경로 통해 피어 링된 된 가상 네트워크에서 가상 어플라이언스를 합니다.

허브 가상 네트워크는 네트워크 가상 어플라이언스와 같은 인프라 구성 요소를 호스트할 수 있는 허브 및 스포크 네트워크를 배포할 수 있습니다. 허브 가상 네트워크를 사용 하 여 모든 스포크 가상 네트워크 피어 링 합니다. 허브 가상 네트워크에서 네트워크 가상 어플라이언스를 통해 트래픽을 전달할 수 있습니다.

다음 홉이 피어 링된 된 가상 네트워크에서 가상 컴퓨터의 IP 주소에 대 한 사용자 정의 경로 사용 하면 가상 네트워크 피어 링 합니다. 사용자 정의 경로 대 한 자세한 내용은 참조 하세요 [가상 네트워크에서 사용 하 여 네트워크 가상 어플라이언스에](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-network-virtual-appliances-on-a-vn)합니다.

## <a name="gateways-and-on-premises-connectivity"></a>게이트웨이 및 온-프레미스 연결

각 가상 네트워크는 다른 가상 네트워크와 피어 링 하는 여부에 관계 없이 고유한 게이트웨이 온-프레미스 네트워크에 연결할 아직 수 있습니다. 가상 네트워크를 피어 링 할 때 온-프레미스 네트워크에 전송 지점으로 피어 링된 된 가상 네트워크에 게이트웨이도 구성할 수 있습니다. 이 경우 원격 게이트웨이 사용 하는 가상 네트워크는 고유한 게이트웨이 사용할 수 없습니다. 가상 네트워크 피어 링된 된 가상 네트워크) (에서 일 수 있습니다. 있는 게이트웨이 하나만 로컬 또는 원격 게이트웨이 사용할 수 있습니다.

## <a name="monitor"></a>모니터

두 가상 네트워크를 피어 링 할 때 각 가상 네트워크 피어 링의 피어 링을 구성 해야 합니다.

다음 상태 중 하나일 수 있는 피어 링 연결의 상태를 모니터링할 수 있습니다.

-   **시작:** 두 번째 가상 네트워크에 첫 번째 가상 네트워크에서 피어 링을 만들면 표시 합니다.

-   **연결:** 첫 번째 가상 네트워크에 두 번째 가상 네트워크에서 피어 링을 만든 후 표시 합니다. 첫 번째 가상 네트워크 피어 링 상태가 시작 됨에서 연결 됨으로 변경합니다. 두 가상 네트워크 피어 가상 네트워크 피어 링을 성공적으로 설정 하기 전에 연결의 상태를 있어야 합니다.

-   **연결 끊김.** 하나의 가상 네트워크의 다른 가상 네트워크 연결을 끊습니다 나와 있습니다.

[상태 인포 그래픽]

## <a name="next-steps"></a>다음 단계
[가상 네트워크 피어 링 구성](sdn-configure-vnet-peering.md): 이 절차를 사용 하 여 Windows PowerShell 찾기는 HNV 공급자 논리 네트워크, 두 가상 네트워크를 만들려면 하나의 서브넷이 있는 각 합니다. 또한 두 가상 네트워크 간에 피어 링을 구성 합니다.
