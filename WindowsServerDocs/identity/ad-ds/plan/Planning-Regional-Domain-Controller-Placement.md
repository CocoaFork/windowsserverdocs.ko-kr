---
ms.assetid: eb600904-24b8-4488-a278-c1c971dc2f2d
title: 지역 도메인 컨트롤러 배치 계획
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 2508476f35462516f32877365cb15be919b5b6df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408730"
---
# <a name="planning-regional-domain-controller-placement"></a>지역 도메인 컨트롤러 배치 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

비용 효율성을 보장 하기 위해 가능한 한 많은 지역 도메인 컨트롤러를 계획 합니다. 먼저 [네트워크 정보 수집](../../ad-ds/plan/Collecting-Network-Information.md) 에 사용 되는 "지리적 위치 및 통신 링크" (DSSTOPO_1) 워크시트를 검토 하 여 위치가 허브 인지 여부를 확인 합니다.  
  
각 허브 위치에 표시 되는 각 도메인에 대해 지역 도메인 컨트롤러를 배치 하도록 계획 합니다. 모든 허브 위치에 지역 도메인 컨트롤러를 배치한 후 위성 위치에 지역 도메인 컨트롤러를 배치 해야 하는 필요성을 평가 합니다. 위성 위치에서 불필요 한 지역 도메인 컨트롤러를 제거 하면 원격 서버 인프라를 유지 관리 하는 데 필요한 지원 비용이 절감 됩니다.  
  
또한 허브와 위성 위치의 도메인 컨트롤러에 대 한 물리적 보안을 보장 하 여 권한 없는 담당자가 액세스할 수 없도록 합니다. 도메인 컨트롤러의 물리적 보안을 보장할 수 없는 허브 및 위성 위치에 쓰기 가능한 도메인 컨트롤러를 두지 마십시오. 쓰기 가능한 도메인 컨트롤러에 대 한 물리적 액세스 권한이 있는 사용자는 다음을 수행 하 여 시스템을 공격할 수 있습니다.  
  
- 도메인 컨트롤러에서 대체 운영 체제를 시작 하 여 실제 디스크 액세스  
- 도메인 컨트롤러에서 실제 디스크를 제거 하 고 교체 하 고 있습니다.  
- 도메인 컨트롤러 시스템 상태 백업의 복사본 가져오기 및 조작  
  
쓰기 가능한 지역 도메인 컨트롤러를 물리적 보안을 보장할 수 있는 위치에만 추가 합니다.  
  
물리적 보안이 부적절 한 위치에서는 RODC (읽기 전용 도메인 컨트롤러)를 배포 하는 것이 좋습니다. 계정 암호를 제외 하 고, RODC는 쓰기 가능한 도메인 컨트롤러에서 보유 하는 모든 Active Directory 개체 및 특성을 보유 합니다. 그러나 RODC에 저장 된 데이터베이스는 변경할 수 없습니다. 쓰기 가능한 도메인 컨트롤러에 대 한 변경 내용을 적용 한 다음 RODC에 다시 복제 해야 합니다.  
  
클라이언트 로그온 및 로컬 파일 서버에 대 한 액세스를 인증 하기 위해 대부분의 조직에서는 지정 된 위치에 표시 되는 모든 지역 도메인에 대해 지역 도메인 컨트롤러를 배치 합니다. 그러나 비즈니스 위치에서 클라이언트가 로컬 인증을 사용 해야 하는지 아니면 클라이언트가 인증을 사용 하 고 WAN (광역 네트워크) 링크를 통해 쿼리할 수 있는지를 평가할 때 많은 변수를 고려해 야 합니다. 다음 그림에서는 도메인 컨트롤러를 위성 위치에 배치할지 여부를 결정 하는 방법을 보여 줍니다.  
  
![지역 dc 배치 계획](media/Planning-Regional-Domain-Controller-Placement/49892c8c-2c99-4aab-92ba-808dbc8048e2.gif)  
  
## <a name="onsite-technical-expertise-availability"></a>온사이트 기술 전문 가용성

여러 가지 이유로 도메인 컨트롤러를 지속적으로 관리 해야 합니다. 도메인 컨트롤러를 관리할 수 있는 직원을 포함 하는 위치에만 지역 도메인 컨트롤러를 배치 하거나 도메인 컨트롤러를 원격으로 관리할 수 있어야 합니다.  
  
일반적으로 낮은 정보 기술 지식이 있는 물리적 보안 및 인력이 낮은 지점 환경에서는 RODC를 배포 하는 것이 좋습니다. RODC에 대 한 로컬 관리자 권한은 해당 사용자에 게 도메인 또는 다른 도메인 컨트롤러에 대 한 사용자 권한을 부여 하지 않고도 모든 도메인 사용자에 게 위임할 수 있습니다. 이렇게 하면 로컬 분기 사용자가 RODC에 로그온 하 여 서버에서 드라이버를 업그레이드 하는 등의 유지 관리 작업을 수행할 수 있습니다. 그러나 분기 사용자는 다른 도메인 컨트롤러에 로그온 하거나 도메인의 다른 관리 작업을 수행할 수 없습니다. 이러한 방식으로 분기 사용자는 도메인 또는 포리스트의 나머지 부분에 대 한 보안을 손상 시 키 지 않고 지점에서 RODC를 효과적으로 관리 하는 기능을 위임할 수 있습니다.  
  
## <a name="wan-link-availability"></a>WAN 링크 가용성

자주 중단 되는 WAN 링크를 통해 사용자를 인증할 수 있는 도메인 컨트롤러가 위치에 포함 되지 않은 경우 사용자에 게 심각한 생산성 손실이 발생할 수 있습니다. WAN 링크 가용성이 100%가 아니고 원격 사이트에서 서비스 중단을 허용할 수 없는 경우 WAN 링크가 다운 되 면 사용자가 로그온 하거나 exchange server에 액세스할 수 있어야 하는 위치에 지역 도메인 컨트롤러를 저장 합니다.  
  
## <a name="authentication-availability"></a>인증 가용성

은행 등의 특정 조직은 항상 사용자를 인증 해야 합니다. WAN 연결 가용성이 100%가 아닌 사용자가 항상 인증을 요구 하는 위치에 지역 도메인 컨트롤러를 배치 합니다.  
  
## <a name="logon-performance-over-wan-links"></a>WAN 링크를 통한 로그온 성능

WAN 링크 가용성이 매우 안정적 이면 WAN 링크를 통한 로그온 성능 요구 사항에 따라 위치에 도메인 컨트롤러를 배치 해야 합니다. WAN을 통한 로그온 성능에 영향을 주는 요인에는 링크 속도와 사용 가능한 대역폭, 사용자 및 사용 프로필 수, 로그온 네트워크 트래픽 양 및 복제 트래픽이 포함 됩니다.  
  
### <a name="wan-link-speed-and-bandwidth-utilization"></a>WAN 링크 속도 및 대역폭 사용률

단일 사용자의 활동은 저속 WAN 링크를 congest 수 있습니다. WAN 링크를 통한 로그온 성능이 허용 되지 않는 경우 위치에 도메인 컨트롤러를 배치 합니다.  
  
대역폭 사용률의 평균 백분율은 네트워크 링크의 정체를 나타냅니다. 네트워크 링크의 평균 대역폭 사용률이 허용 되는 값 보다 큰 경우 해당 위치에 도메인 컨트롤러를 배치 합니다.  
  
### <a name="number-of-users-and-usage-profiles"></a>사용자 및 사용 프로필 수

지정 된 위치의 사용자 수와 해당 사용 프로필은 지역 도메인 컨트롤러를 해당 위치에 배치 해야 하는지 여부를 결정 하는 데 도움이 될 수 있습니다. WAN 연결이 실패할 경우 생산성 손실을 방지 하려면 100 명 이상의 사용자가 있는 위치에 지역 도메인 컨트롤러를 배치 합니다.  
  
사용 프로필은 사용자가 네트워크 리소스를 사용 하는 방법을 표시 합니다. 네트워크 리소스에 자주 액세스 하지 않는 소수의 사용자만 포함 된 위치에 도메인 컨트롤러를 배치 하지 않아도 됩니다.  
  
### <a name="logon-network-traffic-vs-replication-traffic"></a>로그온 네트워크 트래픽 및 복제 트래픽 비교

Active Directory 클라이언트와 동일한 위치에서 도메인 컨트롤러를 사용할 수 없는 경우 클라이언트는 네트워크에서 로그온 트래픽을 만듭니다. 실제 네트워크에 생성 되는 로그온 네트워크 트래픽 양은 그룹 멤버 자격을 비롯 한 여러 가지 요인의 영향을 받습니다. 그룹 정책 개체 (Gpo) 수 및 크기 로그온 스크립트 오프 라인 폴더, 폴더 리디렉션 및 로밍 프로필과 같은 기능을 제공 합니다.  
  
반면, 지정 된 위치에 배치 된 도메인 컨트롤러는 네트워크에서 복제 트래픽을 생성 합니다. 도메인 컨트롤러에서 호스팅되는 파티션에서 수행 된 업데이트의 빈도 및 양은 네트워크에서 생성 된 복제 트래픽 양에 영향을 줍니다. 도메인 컨트롤러에서 호스팅되는 파티션에 대해 수행할 수 있는 다양 한 유형의 업데이트에는 사용자 및 사용자 특성 추가 또는 변경, 암호 변경, 글로벌 그룹, 프린터 또는 볼륨 추가 또는 변경 등이 있습니다.  
  
지역 도메인 컨트롤러를 위치에 배치 해야 하는지 여부를 확인 하려면 도메인 컨트롤러 없이 위치에 의해 생성 된 로그온 트래픽 비용과 도메인 컨트롤러를 위치에 배치 하 여 만든 복제 트래픽 비용을 비교 합니다.  
  
예를 들어 본사에 대 한 저속 링크를 통해 연결 된 지점 및 도메인 컨트롤러를 쉽게 추가할 수 있는 네트워크를 가정해 보겠습니다. 소수의 원격 사이트 사용자의 일일 로그온 및 디렉터리 조회 트래픽이 모든 회사 데이터를 분기로 복제 하는 것 보다 더 많은 네트워크 트래픽을 발생 시키는 경우 도메인 컨트롤러를 분기에 추가 하는 것이 좋습니다.  
  
도메인 컨트롤러를 유지 관리 하는 비용을 줄이는 것이 네트워크 트래픽 보다 중요 한 경우 해당 도메인에 대 한 도메인 컨트롤러를 중앙 집중화 하 고 지역 도메인 컨트롤러를 위치에 배치 하거나 Rodc를 위치에 배치 하는 것이 좋습니다.  
  
지역별 도메인 컨트롤러의 배치와 각 위치에 표시 되는 각 도메인에 대 한 사용자 수를 문서화 하는 데 도움이 되는 워크시트의 경우 [Windows Server 2003 배포 키트의 작업 지원](https://go.microsoft.com/fwlink/?LinkID=102558), 다운로드 Job_Aids_Designing_and_를 참조 하세요. Deploying_Directory_and_Security_Services를 열고 "도메인 컨트롤러 배치" (DSSTOPO_4)를 엽니다.  
  
지역 도메인을 배포할 때 지역 도메인 컨트롤러를 배치 해야 하는 위치에 대 한 정보를 참조 해야 합니다. 지역 도메인 배포 하는 방법에 대 한 자세한 내용은 참조 [배포 Windows Server 2008 지역 도메인](https://technet.microsoft.com/library/cc755118.aspx)합니다.  
