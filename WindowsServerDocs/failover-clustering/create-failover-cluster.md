---
title: 장애 조치(failover) 클러스터 만들기
description: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016 및 Windows Server 2019에 대 한 장애 조치 클러스터를 만드는 방법입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: b36f707edc08a4a8b2bc55a87c9db168e19a5487
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810973"
---
# <a name="create-a-failover-cluster"></a>장애 조치(failover) 클러스터 만들기

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012

이 항목에서는 장애 조치(failover) 클러스터 관리자 스냅인 또는 Windows PowerShell을 사용하여 장애 조치(failover) 클러스터를 만드는 방법을 보여 줍니다. AD DS(Active Directory 도메인 서비스)에서 클러스터의 컴퓨터 개체와 관련 클러스터된 역할을 만드는 일반적인 배포에 대해 다룹니다. 저장소 공간 다이렉트 클러스터에 배포 하는 경우 참조 대신 [저장소 공간 다이렉트 배포](../storage/storage-spaces/deploy-storage-spaces-direct.md)합니다.

또한 Active Directory 분리 클러스터를 배포할 수 있습니다. 이 배포 방법을 사용하면 AD DS에서 컴퓨터 개체를 만들 수 있는 권한 없이 또는 컴퓨터 개체가 AD DS에서 사전 준비되도록 요청하지 않고도 장애 조치(failover) 클러스터를 만들 수 있습니다. 이 옵션은 Windows PowerShell을 통해서만 사용할 수 있으며 특정 시나리오에만 권장됩니다. 자세한 내용은 [Active Directory 분리 클러스터 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))를 참조하십시오.

#### <a name="checklist-create-a-failover-cluster"></a>검사 목록: 장애 조치(failover) 클러스터 만들기

| 상태 | 태스크 | 참조 |
| ---    | ---  | ---       |
| ☐    | 필수 구성 요소 확인 | [필수 구성 요소를 확인 합니다.](#verify-the-prerequisites) |
| ☐    | 클러스터 노드로 추가할 모든 서버에 장애 조치(failover) 클러스터링 기능 설치 | [장애 조치 클러스터링 기능 설치](#install-the-failover-clustering-feature) |
| ☐    | 클러스터 유효성 검사 마법사를 실행하여 구성 유효성 검사 | [구성 유효성 검사](#validate-the-configuration) |
| ☐ | 클러스터 만들기 마법사를 실행하여 장애 조치(failover) 클러스터 만들기 | [장애 조치 클러스터 만들기](#create-the-failover-cluster) |
| ☐ | 클러스터 작업을 호스트할 클러스터된 역할 만들기 | [클러스터 된 역할 만들기](#create-clustered-roles) |

## <a name="verify-the-prerequisites"></a>필수 구성 요소 확인

시작하기 전에 다음 필수 구성 요소를 확인합니다.

- 클러스터 노드로 추가할 모든 서버가 동일한 버전의 Windows Server를 실행하고 있는지 확인합니다.
- 하드웨어 요구 사항을 검토하여 사용자의 구성이 지원되는지 확인합니다. 자세한 내용은 [장애 조치(failover) 클러스터링 하드웨어 요구 사항 및 저장소 옵션](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj612869(v%3dws.11))을 참조하세요. 저장소 공간 다이렉트 클러스터를 만드는 경우 참조 [저장소 공간 다이렉트 하드웨어 요구 사항](../storage/storage-spaces/storage-spaces-direct-hardware-requirements.md)합니다.
- 클러스터를 만드는 동안 클러스터 된 저장소를 추가할 모든 서버 저장소에 액세스할 수 있는지를 확인 합니다. 클러스터를 만든 후 클러스터된 저장소를 추가할 수도 있습니다.
- 클러스터 노드로 추가할 모든 서버가 동일한 Active Directory 도메인에 가입되어 있는지 확인합니다.
- (선택 사항) OU(조직 구성 단위)를 만들고 클러스터 노드로 추가할 서버의 컴퓨터 계정을 OU로 이동합니다. AD DS의 고유한 OU에 장애 조치(failover) 클러스터를 배치하는 것이 좋습니다. 이렇게 하면 클러스터 노드에 영향을 주는 그룹 정책 설정 또는 보안 템플릿 설정을 보다 효율적으로 제어할 수 있습니다. 클러스터를 고유한 OU에 격리하면 클러스터 컴퓨터 개체가 실수로 삭제되는 것을 방지하는 데에도 도움이 됩니다.

또한 다음 계정 요구 사항을 확인합니다.

- 클러스터를 만드는 데 사용할 계정이 클러스터 노드로 추가할 모든 서버에서 관리자 권한이 있는 도메인 사용자인지 확인합니다.
- 다음 중 하나에 해당하는지 확인합니다.
    - 클러스터를 만드는 사용자에게 클러스터를 구성할 서버가 있는 컨테이너 또는 OU에 대한 **컴퓨터 개체 만들기** 권한이 있습니다.
    - 사용자에게 **컴퓨터 개체 만들기** 권한이 없는 경우 도메인 관리자에게 클러스터에 대한 클러스터 컴퓨터 개체를 사전 준비하도록 요청합니다. 자세한 내용은 [Active Directory 도메인 서비스에서 클러스터 컴퓨터 개체 사전 준비](prestage-cluster-adds.md)를 참조하세요.

> [!NOTE]
> Windows Server 2012 R2에서 Active Directory 분리 클러스터를 만들려는 경우에이 요구 사항은 적용 되지 않습니다. 자세한 내용은 [Active Directory 분리 클러스터 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))를 참조하십시오.

## <a name="install-the-failover-clustering-feature"></a>장애 조치(failover) 클러스터링 기능 설치

장애 조치 클러스터 노드로 추가할 모든 서버에 장애 조치 클러스터링 기능을 설치 해야 합니다.

### <a name="install-the-failover-clustering-feature"></a>장애 조치(failover) 클러스터링 기능 설치

1. 서버 관리자를 시작합니다.
2. 에 **관리** 메뉴에서 **역할 및 기능 추가**합니다.
3. 에 **시작 하기 전에** 페이지에서 **다음**합니다.
4. 에 **설치 유형 선택** 페이지에서 선택 **역할 기반 또는 기능 기반 설치**를 선택한 후 **다음**합니다.
5. 에 **대상 서버 선택** 페이지에서 기능을 설치 하 고 클릭 하려는 서버를 선택 **다음**합니다.
6. 에 **서버 역할 선택** 페이지에서 선택 **다음**합니다.
7. **기능 선택** 페이지에서 **장애 조치(failover) 클러스터링** 확인란을 선택합니다.
8. 장애 조치 클러스터 관리 도구를 설치 하려면 **기능 추가**를 선택한 후 **다음**합니다.
9. 에 **설치 선택 확인** 페이지에서 **설치**합니다.
<br>장애 조치(failover) 클러스터링 기능에는 서버를 다시 시작할 필요가 없습니다.

10. 설치가 완료 되 면 선택 **닫기**합니다.
11. 클러스터 노드로 추가할 모든 서버에 장애 조치(failover) 클러스터링 기능 설치

> [!NOTE]
> 장애 조치(failover) 클러스터링 기능을 설치한 후에는 Windows 업데이트에서 최신 업데이트를 적용하는 것이 좋습니다. 또한 Windows Server 2012 기반 장애 조치 클러스터에 대 한 검토를 [의 권장 핫픽스 및 Windows Server 2012 기반 장애 조치 클러스터에 대 한 업데이트](https://support.microsoft.com/help/2784261/recommended-hotfixes-and-updates-for-windows-server-2012-based-failove) Microsoft 지원 문서를 적용 되는 업데이트를 설치 합니다.

## <a name="validate-the-configuration"></a>구성 유효성 검사

장애 조치(failover) 클러스터를 만들기 전에 구성의 유효성을 검사하여 하드웨어 및 하드웨어 설정이 장애 조치(failover) 클러스터링과 호환되는지 확인하는 것이 좋습니다. Microsoft는 전체 구성이 모든 유효성 검사를 통과하고 모든 하드웨어가 클러스터 노드에서 실행하는 Windows Server 버전에 대해 인증된 경우에만 클러스터 솔루션을 지원합니다.

> [!NOTE]
> 모든 테스트를 실행하려면 두 개 이상의 노드가 있어야 합니다. 노드가 하나만 있으면 중요한 저장소 테스트가 대부분 실행되지 않습니다.

### <a name="run-cluster-validation-tests"></a>클러스터 유효성 검사 테스트를 실행 합니다.

1. 원격 서버 관리 도구에서 장애 조치(failover) 클러스터 관리 도구를 설치한 컴퓨터 또는 장애 조치(failover) 클러스터링 기능을 설치한 서버에서 장애 조치(failover) 클러스터 관리자를 시작합니다. 서버에서이 작업을 수행 하려면 서버 관리자를 시작 한 후 합니다 **도구** 메뉴에서 **장애 조치 클러스터 관리자**합니다.
2. 에 **장애 조치 클러스터 관리자** 창 아래에 있는 **관리**를 선택 **구성 유효성 검사**합니다.
3. 에 **시작 하기 전에** 페이지에서 **다음**합니다.
4. 에 **서버 선택 또는 클러스터** 페이지의 **이름 입력** , 상자 하 고, NetBIOS 이름 또는 장애 조치 클러스터 노드로 추가 하려는 서버의 정규화 된 도메인 이름을 입력 하 고, 선택한 다음 **추가**합니다. 추가하려는 각 서버에 대해 이 단계를 반복합니다. 여러 서버를 동시에 추가하려면 쉼표 또는 세미콜론으로 이름을 구분합니다. 예를 들어 이름을 형식으로 입력 `server1.contoso.com, server2.contoso.com`합니다. 작업을 완료 하는 경우 선택할 **다음**합니다.
5. 에 **테스트 옵션** 페이지에서 **(권장) 모든 테스트를 실행**를 선택한 후 **다음**합니다.
6. 에 **확인** 페이지에서 **다음**합니다.

    유효성 검사 중 페이지에 실행 중인 테스트의 상태가 표시됩니다.
7. **요약** 페이지에서 다음 중 하나를 수행합니다.
    
      - 결과 테스트가 성공적으로 완료 되 고 구성이 클러스터링에 적합 하 즉시 클러스터를 만들려는 경우를 확인 합니다 **유효성이 검사 된 노드를 사용 하 여 클러스터를 만들** 확인 상자는 선택 및 선택 **완료**합니다. 그런 다음 [장애 조치(failover) 클러스터 만들기](#create-the-failover-cluster) 절차의 4단계를 계속 진행합니다.
      - 결과 경고 또는 오류가 발생 했음을 나타낼 경우 선택 **보고서 보기** 를 세부 정보를 보고 해결 해야 하는 문제를 확인 합니다. 특정 유효성 검사 테스트에 대한 경고에서는 장애 조치(failover) 클러스터의 해당 측면이 지원될 수 있지만 권장 모범 사례에는 맞지 않을 수 있음을 나타냅니다.
        
        > [!NOTE]
        > 저장소 공간 영구 예약 유효성 검사 테스트에 대한 경고를 받은 경우 자세한 내용은 블로그 게시물 [Windows 장애 조치(failover) 클러스터 유효성 검사에서 디스크가 저장소 공간에 대한 영구 예약을 지원하지 않음을 나타내는 경고가 표시됨](https://blogs.msdn.microsoft.com/clustering/2013/05/24/validate-storage-spaces-persistent-reservation-test-results-with-warning/) 을 참조하세요.

하드웨어 유효성 검사 테스트에 대한 자세한 내용은 [Validate Hardware for a Failover Cluster](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>)를 참조하세요.

## <a name="create-the-failover-cluster"></a>장애 조치(failover) 클러스터 만들기

이 단계를 완료하려면 로그온한 사용자 계정이 이 항목의 [필수 구성 요소 확인](#verify-the-prerequisites) 섹션에 설명된 요구 사항을 충족해야 합니다.

1. 서버 관리자를 시작합니다.
2. 에 **도구** 메뉴에서 **장애 조치 클러스터 관리자**합니다.
3. 에 **장애 조치 클러스터 관리자** 창 아래에 있는 **관리**를 선택 **클러스터 만들기**합니다.
    
    클러스터 만들기 마법사가 열립니다.
4. 에 **시작 하기 전에** 페이지에서 **다음**합니다.
5. 경우는 **서버 선택** 페이지의 **이름 입력** , 상자 하 고, NetBIOS 이름 또는 장애 조치 클러스터 노드로 추가 하려는 서버의 정규화 된 도메인 이름을 입력 하 고, 선택한 다음 **추가**합니다. 추가하려는 각 서버에 대해 이 단계를 반복합니다. 여러 서버를 동시에 추가하려면 쉼표 또는 세미콜론으로 이름을 구분합니다. 예를 들어 *server1.contoso.com, server2.contoso.com*형식으로 이름을 입력합니다. 작업을 완료 하는 경우 선택할 **다음**합니다.
    
    > [!NOTE]
    > 유효성 검사를 실행 한 즉시 클러스터를 만들도록 선택한 경우는 [절차의 유효성을 검사 하는 구성](#validate-the-configuration)에 표시 되지 것입니다는 **서버 선택** 페이지. 유효성을 검사한 노드는 클러스터 만들기 마법사에 자동으로 추가되므로 다시 입력할 필요가 없습니다.
6. 앞에서 유효성 검사를 건너뛴 경우 **유효성 검사 경고** 페이지가 나타납니다. 클러스터 유효성 검사를 실행하는 것이 좋습니다. Microsoft에서는 모든 유효성 검사 테스트를 통과한 클러스터만 지원합니다. 유효성 검사 테스트를 실행 하려면 **Yes**를 선택한 후 **다음**합니다. 에 설명 된 대로 유효성 검사 구성 마법사를 완료 [구성 유효성 검사](#validate-the-configuration)합니다.
7. **클러스터 관리 액세스 지점** 페이지에서 다음을 수행합니다.
    
    1. **클러스터 이름** 상자에 클러스터를 관리하는 데 사용할 이름을 입력합니다. 그 전에 먼저 다음 정보를 검토합니다.
        
          - 클러스터를 만드는 동안 이 이름이 AD DS에 클러스터 컴퓨터 개체( *클러스터 이름 개체* 또는 *CNO*라고도 함)로 등록됩니다. 클러스터의 NetBIOS 이름을 지정한 경우 클러스터 노드의 컴퓨터 개체가 있는 곳과 동일한 위치에 CNO가 만들어집니다. 이는 기본 컴퓨터 컨테이너 또는 OU일 수 있습니다.
          - CNO의 다른 위치를 지정하려면 **클러스터 이름** 상자에 OU의 고유 이름을 입력하면 됩니다. 예를 들어 다음과 같은 가치를 제공해야 합니다. *CN=ClusterName, OU=Clusters, DC=Contoso, DC=com*
          - 도메인 관리자가 클러스터 노드에 있는 것과 다른 OU에서 CNO를 사전 준비한 경우 도메인 관리자가 제공하는 고유 이름을 지정합니다.
    2. 서버에 DHCP를 사용하도록 구성된 네트워크 어댑터가 없는 경우 장애 조치(failover) 클러스터의 고정 IP 주소를 하나 이상 구성해야 합니다. 클러스터 관리에 사용할 각 네트워크 옆의 확인란을 선택합니다. 선택 된 **주소** 선택한 네트워크 옆의 필드 및 다음 클러스터에 할당 하려는 IP 주소를 입력 합니다. 이 IP 주소는 DNS(Domain Name System)에서 클러스터 이름에 연결됩니다.
    3. 작업을 완료 하는 경우 선택할 **다음**합니다.
8. **확인** 페이지에서 설정을 검토합니다. 기본적으로 **클러스터에 사용할 수 있는 모든 저장소를 추가하세요.** 확인란이 선택되어 있습니다. 다음 중 하나를 수행하려면 이 확인란의 선택을 취소합니다.
    
      - 나중에 저장소를 구성하려는 경우
      - 파일 및 저장소 서비스에서 저장소 공간을 아직 만들지 않았으며, 장애 조치(failover) 클러스터 관리자 또는 장애 조치(failover) 클러스터링 Windows PowerShell cmdlet을 통해 클러스터된 저장소 공간을 만들려는 경우 자세한 내용은 [클러스터된 저장소 공간 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>)를 참조하세요.
9. 선택 **다음** 장애 조치 클러스터를 만듭니다.
10. **요약** 페이지에서 장애 조치(failover) 클러스터가 성공적으로 만들어졌는지 확인합니다. 경고 또는 오류 경우 요약 출력 보거나 선택 **보고서 보기** 전체 보고서를 볼 수 있습니다. 선택 **완료**합니다.
11. 클러스터가 만들어졌는지 확인하려면 탐색 트리의 **장애 조치(failover) 클러스터 관리자** 아래에 클러스터 이름이 있는지 확인합니다. 클러스터 이름을 확장 하 고를 선택한 다음 아래에 있는 항목 **노드**, **저장소** 또는 **네트워크** 관련된 리소스를 보고 합니다.
    
    DNS에서 클러스터 이름을 복제하는 데 약간의 시간일 걸릴 수 있습니다. DNS 등록 및 복제가 완료를 선택 하는 경우 이후에 **모든 서버** 서버 관리자에서 클러스터 이름이 인 서버로 나열 되어 있어야를 **관리 효율성** 상태의 **온라인** .

클러스터를 만든 후 클러스터 쿼럼 구성을 확인하고 필요에 따라 CSV(클러스터 공유 볼륨)를 만드는 등의 작업을 수행할 수 있습니다. 자세한 내용은 [저장소 공간 다이렉트에서 이해 쿼럼](../storage/storage-spaces/understand-quorum.md) 하 고 [장애 조치 클러스터에서 사용 하 여 클러스터 공유 볼륨](failover-cluster-csvs.md)합니다.

## <a name="create-clustered-roles"></a>클러스터된 역할 만들기

장애 조치(failover) 클러스터를 만든 후 클러스터 작업을 호스트할 클러스터된 역할을 만들 수 있습니다.

>[!NOTE]
>클라이언트 액세스 지점이 필요한 클러스터된 역할의 경우 AD DS에 VCO(가상 컴퓨터 개체)가 만들어집니다. 기본적으로 클러스터의 모든 VCO는 CNO와 동일한 컨테이너 또는 OU에 만들어집니다. 클러스터를 만든 후 CNO를 원하는 OU로 이동할 수 있습니다.

클러스터 된 역할을 만드는 방법은 다음과 같습니다.

1. 서버 관리자 또는 Windows PowerShell을 사용하여 클러스터된 역할에 필요한 기능 또는 역할을 각 장애 조치(failover) 클러스터 노드에 설치합니다. 예를 들어 클러스터된 파일 서버를 만들려면 모든 클러스터 노드에 파일 서버 역할을 설치합니다.
    
    다음 표에서는 고가용성 마법사에서 구성할 수 있는 클러스터된 역할 및 필수 구성 요소로 설치해야 하는 관련 서버 역할 또는 기능을 보여 줍니다.

   | 클러스터된 역할  | 역할 또는 기능 필수 구성 요소  |
   | ---------       | ---------                    |
   | Namespace 서버     |   네임 스페이스 (파일 서버 역할의 일부)       |
   | DFS 네임스페이스 서버     |  DHCP 서버 역할       |
   | DTC(Distributed Transaction Coordinator)     | 없음        |
   | 파일 서버     |  파일 서버 역할       |
   | 일반 응용 프로그램     |  해당 사항 없음       |
   | 일반 스크립트     |   해당 사항 없음      |
   | 일반 서비스     |   해당 사항 없음      |
   | Hyper-V 복제본 브로커     |   Hyper-V 역할      |
   | iSCSI 대상 서버     |    iSCSI 대상 서버(파일 서버 역할의 일부)     |
   | iSNS 서버     |  iSNS 서버 서비스 기능       |
   | 메시지 큐     |  메시지 큐 서비스 기능       |
   | 기타 서버     |  없음       |
   | 가상 컴퓨터     |  Hyper-V 역할       |
   | WINS 서버     |   WINS 서버 기능      |

2. 장애 조치 클러스터 관리자에서 클러스터 이름을 확장 하 고 마우스 오른쪽 단추로 클릭 **역할**를 선택한 후 **역할 구성**합니다.
3. 고가용성 마법사의 단계에 따라 클러스터된 역할을 만듭니다.
4. 클러스터된 역할이 만들어졌는지 확인하려면 **역할** 창에서 역할의 상태가 **실행 중**인지 확인합니다. 역할 창에는 소유자 노드로 표시됩니다. 장애 조치를 테스트 하려면 역할을 마우스 오른쪽 단추로 클릭, 가리킨 **이동**를 선택한 후 **노드 선택**합니다. 에 **클러스터 된 역할 이동** 대화 상자에서 원하는 클러스터 노드를 선택한 후 **확인**합니다. **소유자 노드** 열에서 소유자 노드가 변경되었는지 확인합니다.

## <a name="create-a-failover-cluster-by-using-windows-powershell"></a>Windows PowerShell을 사용하여 장애 조치(failover) 클러스터 만들기

다음 Windows PowerShell cmdlet이이 항목의 이전 절차와 동일한 기능을 수행 합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

> [!NOTE]
> Windows Server 2012 R2에서 Active Directory 분리 클러스터를 만드는 Windows PowerShell을 사용 해야 합니다. 구문에 대한 자세한 내용은 [Deploy an Active Directory-Detached Cluster](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))를 참조하세요.

다음 예제에서는 장애 조치(failover) 클러스터링 기능을 설치합니다.

```PowerShell
Install-WindowsFeature –Name Failover-Clustering –IncludeManagementTools
```

다음 예제에서는 *Server1* 및 *Server2*컴퓨터에서 모든 클러스터 유효성 검사 테스트를 실행합니다.

```PowerShell
Test-Cluster –Node Server1, Server2
```

> [!NOTE]
> 합니다 **Test-cluster** cmdlet은 현재 작업 디렉터리에서 로그 파일에 결과 출력 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다. C:\Users\<username>\AppData\Local\Temp.

다음 예제에서는 *Server1* 및 *Server2* 노드가 있는 *MyCluster*라는 장애 조치(failover) 클러스터를 만들고, 고정 IP 주소 *192.168.1.12*를 할당하며, 사용 가능한 모든 저장소를 장애 조치(failover) 클러스터에 추가합니다.

```PowerShell
New-Cluster –Name MyCluster –Node Server1, Server2 –StaticAddress 192.168.1.12
```

다음 예제에서는 이전 예제와 동일한 장애 조치(failover) 클러스터를 만들지만 사용 가능한 저장소를 장애 조치(failover) 클러스터에 추가하지 않습니다.

```PowerShell
New-Cluster –Name MyCluster –Node Server1, Server2 –StaticAddress 192.168.1.12 -NoStorage
```

다음 예제에서는 *Contoso.com* 도메인의 *Cluster* OU에 *MyCluster*라는 클러스터를 만듭니다.

```PowerShell
New-Cluster -Name CN=MyCluster,OU=Cluster,DC=Contoso,DC=com -Node Server1, Server2
```

클러스터된 역할을 추가하는 방법의 예는 [Add-ClusterFileServerRole](https://docs.microsoft.com/powershell/module/failoverclusters/add-clusterfileserverrole?view=win10-ps) 및 [Add-ClusterGenericApplicationRole](https://docs.microsoft.com/powershell/module/failoverclusters/add-clustergenericapplicationrole?view=win10-ps)과 같은 항목을 참조하세요.

## <a name="more-information"></a>자세한 정보

  - [장애 조치(failover) 클러스터링](failover-clustering.md)
  - [Hyper-v 클러스터 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj863389(v%3dws.11)>)
  - [응용 프로그램 데이터용 스케일 아웃 파일 서버](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831349(v%3dws.11)>)
  - [Active Directory 분리 클러스터 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))
  - [고가용성을 위한 게스트 클러스터링을 사용 하 여](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn440540(v%3dws.11)>)
  - [클러스터 인식 업데이트](cluster-aware-updating.md)
  - [New-Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/new-cluster?view=win10-ps)
  - [Test-Cluster](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps)
