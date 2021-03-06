---
ms.assetid: d7a4d2e1-217d-4ffc-93f0-817149bd9e7f
title: 손상될 작업 환경
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: b2233a638aa0a422d5792f8c949c46ac8de099ba
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822046"
---
# <a name="avenues-to-compromise"></a>손상될 작업 환경

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*법률 번호 7: 가장 안전한 네트워크는 잘 관리 되는 네트워크입니다.* - [10 가지 불변의 보안 관리 법칙](https://technet.microsoft.com/library/cc722488.aspx)  
  
심각한 손상 이벤트를 경험 하는 조직에서는 일반적으로 조직에서 IT 인프라의 실제 상태에 대 한 표시 여부를 제한 하는 것을 알 수 있습니다 .이는 "문서화 된 대로"와 크게 다를 수 있습니다. 없다고. 이러한 차이는 공격자가 환경을 효과적으로 "소유" 하는 시점으로 손상이 진행 될 때까지 손상이 거의 발생 하지 않는 문제를 해결 하기 위해 환경을 노출 하는 취약점을 야기 합니다.  
  
이러한 조직의 AD DS 구성, Pki (공개 키 인프라), 서버, 워크스테이션, 응용 프로그램, Acl (액세스 제어 목록) 및 기타 기술에 대 한 자세한 평가는 다음과 같은 경우 잘못 된 구성 및 취약성을 표시 합니다. 재구성 되었습니다. 초기 손상을 방지 했을 수 있습니다.  
  
IT 문서, 프로세스 및 절차를 분석 하면 공격자가 악용 한 관리 관행의 격차에 의해 발생 하는 취약성을 식별 하 여 Active Directory 포리스트를 완전히 손상 시키는 데 사용 된 권한을 얻습니다. 완전히 손상 된 포리스트는 공격자가 개별 시스템, 응용 프로그램 또는 사용자 계정 뿐만 아니라 사용자 계정에 대 한 액세스를 에스컬레이션 하 여 포리스트의 모든 측면을 수정 하거나 제거할 수 있는 권한 수준을 얻도록 하는 것입니다. 이러한 수준까지 Active Directory 설치가 손상 된 경우 공격자는 환경을 통해 상태를 유지할 수 있는 변경 작업을 수행 하거나, 디렉터리 및 관리 하는 시스템 및 계정을 제거 하는 등의 작업을 수행할 수 있습니다.  
  
다음 설명에서 일반적으로 사용 되는 많은 취약점은 Active Directory에 대 한 공격을 받지 않지만 공격자가 권한 상승 (권한)을 실행 하는 데 사용할 수 있는 환경에서 발판를 설정할 수 있습니다. 권한 상승)을 공격 하 고 AD DS를 대상으로 하 고 손상 시킵니다.  
  
이 문서의이 섹션에서는 공격자가 인프라에 대 한 액세스 권한을 얻고 결국 권한 상승 공격을 시작 하는 데 일반적으로 사용 하는 메커니즘을 설명 합니다. 다음 섹션도 참조 하세요.  
  
-   [Active Directory 공격 노출 영역 축소](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md) Active Directory의 보안 구성에 대 한 자세한 권장 사항입니다.  
  
-   [손상의 징후가 Active Directory 모니터링](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md) 손상을 검색 하는 데 도움이 되는 권장 사항  
  
-   [손상 계획](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md) IT 및 비즈니스 관점에서 인프라에 대 한 공격을 준비 하는 데 도움이 되는 상위 수준 방법  
  
> [!NOTE]  
> 이 문서는 AD DS 도메인에 속하는 Active Directory 및 Windows 시스템에 중점을 두지만 공격자는 Active Directory 및 Windows에만 초점을 맞출 수 있습니다. 운영 체제, 디렉터리, 응용 프로그램 및 데이터 리포지토리가 혼합 된 환경에서는 Windows 시스템이 아닌 시스템도 손상 된 것을 발견 하는 것이 일반적입니다. 시스템에서 windows 및 UNIX 또는 Linux 클라이언트에서 액세스 하는 파일 서버, 여러 운영 체제에 인증 서비스를 제공 하는 디렉터리 등 windows 환경이 아닌 환경 간에 "브리지"를 제공 하는 경우에 특히 그렇습니다. metadirectories는 서로 다른 디렉터리에서 데이터를 동기화 합니다.  
>   
> AD DS는 Windows 시스템 뿐만 아니라 다른 클라이언트에 게 제공 되는 중앙 액세스 및 구성 관리 기능으로 인해 대상이 지정 됩니다. 인증 및 구성 관리 서비스를 제공 하는 다른 모든 디렉터리 또는 응용 프로그램은 결정 된 공격자의 대상으로 지정 될 수 있습니다. 이 문서는 Active Directory 설치의 손상 가능성을 줄일 수 있는 보호에 중점을 두지만 Windows가 아닌 컴퓨터, 디렉터리, 응용 프로그램 또는 데이터 리포지토리를 포함 하는 모든 조직은 다음을 준비 해야 합니다. 이러한 시스템에 대 한 공격입니다.  
  
## <a name="initial-breach-targets"></a>초기 위반 대상  
아무도 조직을 손상 시킬 수 있도록 노출 하는 IT 인프라를 의도적으로 구축 하지 않습니다. Active Directory 포리스트가 처음 생성 될 때 일반적으로 초기 및 현재입니다. 연도 통과와 새로운 운영 체제 및 응용 프로그램은 포리스트에 추가 됩니다. Active Directory에서 제공 하는 관리 효율성 혜택이 인식 되 고, 더 많은 콘텐츠가 디렉터리에 추가 되 고, 사용자가 컴퓨터 또는 응용 프로그램을 AD DS에 통합 하 고, 도메인이 가장 많이 제공 되는 새로운 기능을 지원 하도록 업그레이드 됩니다. 현재 버전의 Windows 운영 체제입니다. 그러나 시간이 지남에 따라 새 인프라가 추가 되는 경우에도 인프라의 다른 부분을 관리 하는 것은 물론, 시스템 및 응용 프로그램은 제대로 작동 하 고 있으므로 수신 되지 않습니다. 조직에서는 레거시 인프라를 제거 하지 않은 것을 잊지 않습니다. 손상 된 인프라를 평가 하는 것에서 표시 되는 사항에 따라, 더 크고 크고 더 복잡 한 환경에서 일반적으로 사용 되는 취약성의 많은 인스턴스가 있을 가능성이 높습니다.  
  
공격자의 동기에 관계 없이 대부분의 정보 보안 위반은 한 번에 한 두 시스템의 손상으로 시작 합니다. 이러한 초기 이벤트 또는 네트워크에 대 한 진입점은 수정 될 수 있지만 그렇지 않은 취약성을 활용 하는 경우가 많습니다. [2012 데이터 위반 조사 보고서 (DBIR)](http://www.verizonbusiness.com/resources/reports/rp_data-breach-investigations-report-2012_en_xg.pdf)는 Verizon 위험 팀에서 다양 한 국가 보안 기관 및 기타 회사와 협력 하 여 생성 한 연간 연구 이며, 공격의 96%가 매우 어려워집니다. "갖추고는 단순 또는 중간 제어를 통해" 97%의 위반이 발생 했습니다. " 이러한 결과는 다음에 나오는 일반적으로 이용 되는 취약성의 직접적인 결과일 수 있습니다.  
  
### <a name="gaps-in-antivirus-and-antimalware-deployments"></a>바이러스 백신 및 맬웨어 방지 배포의 간격  
*법률 번호 8: 최신 맬웨어 스캐너가 스캐너를 전혀 활용 하지 않는 것 보다 훨씬 더 좋습니다.* - [10 가지 불변 보안 법 (버전 2.0)](https://technet.microsoft.com/security/hh278941.aspx)  
  
조직의 바이러스 백신 및 맬웨어 방지 배포에 대 한 분석은 대부분의 워크스테이션이 사용 하도록 설정 되 고 현재 설정 된 바이러스 백신 및 맬웨어 방지 소프트웨어를 사용 하 여 구성 되는 환경을 나타냅니다. 예외는 일반적으로 바이러스 백신 및 맬웨어 방지 소프트웨어를 배포, 구성 및 업데이트 하기 어려울 수 있는 회사 환경이 나 직원 장치에 자주 연결 하지 않는 워크스테이션입니다.  
  
그러나 서버 채우기는 많은 손상 된 환경에서 일관 되 게 보호 되는 경향이 있습니다. [2012 데이터 위반 조사](http://www.verizonbusiness.com/resources/reports/rp_data-breach-investigations-report-2012_en_xg.pdf)에서 보고 된 것 처럼 모든 데이터 손상의 94%는 이전 해의 18% 증가 및 맬웨어에 통합 된 공격의 69%를 나타내는 관련 서버를 손상 시킵니다. 서버 모집단에서는 바이러스 백신 및 맬웨어 방지 설치가 일관 되 게 구성, 오래 됨, 잘못 구성 되었거나 사용 하지 않도록 설정 되어 있는 것을 확인 하는 것이 일반적이 지 않습니다. 일부 경우에는 바이러스 백신 및 맬웨어 방지 소프트웨어를 관리 담당자가 사용 하지 않도록 설정할 수 있지만 다른 경우에는 공격자가 다른 취약성을 통해 서버를 손상 한 후 소프트웨어를 사용 하지 않도록 설정 해야 합니다. 바이러스 백신 및 맬웨어 방지 소프트웨어를 사용 하지 않도록 설정 하면 공격자가 서버에서 맬웨어를 공장 화 하 고 서버 모집단에서 손상 전파에 집중 합니다.  
  
시스템이 현재, 포괄적인 맬웨어 보호로 보호 되 고, 바이러스 백신 및 맬웨어 방지 소프트웨어를 사용 하지 않도록 설정 하거나 제거 하는 시스템을 모니터링 하 고, 수동으로 사용 하지 않도록 설정 되었습니다. 바이러스 백신 및 맬웨어 방지 소프트웨어가 모든 감염을 방지 하 고 검색 하는 것을 보장할 수는 없지만, 적절 하 게 구성 되 고 배포 된 바이러스 백신 및 맬웨어 방지 구현은 감염 가능성을 줄일 수 있습니다.  
  
### <a name="incomplete-patching"></a>불완전 한 패치  
*법률 번호 3: 보안 픽스를 유지 하지 않는 경우 네트워크를 오랫동안 사용할 수 없습니다.* - [10 가지 불변의 보안 관리 법칙](https://technet.microsoft.com/library/cc722488.aspx)  
  
Microsoft는 매월 두 번째 화요일에 보안 게시판을 릴리스 합니다. 드물지만 보안 업데이트가 매월 보안 업데이트 ("대역 외" 업데이트 라고도 함)에 대 한 보안 업데이트가 출시 되는 경우에도이 취약점을 해결 합니다. 고객 시스템에 대 한 긴급 한 위험. 중소 기업에서 Windows 업데이트 사용 하 여 시스템 및 응용 프로그램 패치를 관리 하거나 대기업에서 Microsoft Endpoint Configuration Manager와 같은 관리 소프트웨어를 사용 하 여 세부 정보에 따라 패치를 배포 하는지 여부 계층적 계획, 많은 고객은 상대적으로 적시에 Windows 인프라를 패치 합니다.  
  
그러나 Windows 컴퓨터 및 Microsoft 응용 프로그램만 포함 하 고 손상 된 환경에서는 조직의 패치 관리 전략에 간격이 포함 되어 있다는 것을 확인 하는 것이 일반적입니다. 이러한 환경의 Windows 시스템은 일관 되 게 패치가 적용 되지 않습니다. Windows 이외의 운영 체제는 산발적으로 패치가 적용 됩니다. 상용 (COTS) 응용 프로그램은 패치가 존재 하지만 적용 되지 않은 취약점을 포함 합니다. 네트워킹 장치는 공장 기본 자격 증명을 사용 하 여 구성 되는 경우가 많으며 설치 후에는 펌웨어 업데이트 연도가 없습니다. 공급 업체에서 더 이상 지원 하지 않는 응용 프로그램 및 운영 체제는 더 이상 취약점에 대해 패치를 적용할 수 없는 경우에도 실행 되는 경우가 많습니다. 이러한 패치가 적용 되지 않은 각 시스템은 공격자의 또 다른 잠재적인 진입점을 나타냅니다.  
  
IT의 소비자 주도에는 직원 소유 장치를 회사 소유의 데이터에 액세스 하는 데 사용 하는 추가 과제가 도입 되었으며, 조직은 직원의 개인 장치에 대 한 패치 및 구성을 거의 제어 하지 않을 수 있습니다. 엔터프라이즈급 하드웨어는 일반적으로 개별 사용자 지정 및 장치 선택에서 적은 비용으로 엔터프라이즈급 구성 옵션 및 관리 기능을 제공 합니다. 직원 중심 하드웨어는 광범위 한 제조업체, 공급 업체, 하드웨어 보안 기능, 소프트웨어 보안 기능, 관리 기능 및 구성 옵션을 제공 하며, 많은 엔터프라이즈 기능이 함께 제공 되지 않을 수 있습니다.  
  
#### <a name="patch-and-vulnerability-management-software"></a>패치 및 취약성 관리 소프트웨어  
Windows 시스템 및 Microsoft 응용 프로그램에 대 한 효과적인 패치 관리 시스템이 준비 된 경우에는 거부 된 취약성으로 인해 생성 되는 공격에 취약 한 부분이 해결 되었습니다. 그러나 비 Windows 시스템, 타사 응용 프로그램, 네트워크 인프라 및 직원 장치를 패치 및 기타 픽스 에서도 최신 상태로 유지 하는 경우에는 인프라가 취약 하 게 유지 됩니다. 응용 프로그램 공급 업체가 자동 업데이트 기능을 제공 하는 경우도 있습니다. 다른 방법으로는 패치 및 기타 픽스를 정기적으로 검색 하 고 적용 하는 방법을 고안 해야 할 수 있습니다.
  
### <a name="outdated-applications-and-operating-systems"></a>오래 된 응용 프로그램 및 운영 체제  
*"6 년 이전 운영 체제에서 6 개월 이전의 공격 으로부터 보호 하는 것은 불가능 합니다."* -Enterprise 설치를 보호 하는 10 년 경험을 갖춘 Information Security Professional  
  
"현재 가져오기, 최신 상태 유지"는 마케팅 구와 같은 소리를 들 수 있지만 오래 된 운영 체제 및 응용 프로그램은 많은 조직의 IT 인프라에서 위험을 생성 합니다. 2003에 출시 된 운영 체제는 여전히 공급 업체에서 지원 될 수 있으며 취약점을 해결 하는 업데이트와 함께 제공 될 수 있지만,이 운영 체제는 최신 버전의 운영 체제에 추가 된 보안 기능을 포함 하지 않을 수 있습니다. 오래 된 시스템에서는 해당 컴퓨터의 더 낮은 기능을 지원 하기 위해 특정 AD DS 보안 구성의 약화 필요할 수도 있습니다.  
  
응용 프로그램을 더 이상 지원 하지 않는 공급 업체의 레거시 인증 프로토콜을 사용 하도록 작성 된 응용 프로그램은 일반적으로 더 강력한 인증 메커니즘을 지원 하기 위해 다시 사용할 수 없습니다. 그러나 조직의 Active Directory 도메인은 이러한 응용 프로그램을 지원 하기 위해 LAN Manager 해시 또는 역방향 암호화 된 암호를 저장 하도록 계속 구성할 수 있습니다. 최신 운영 체제를 도입 하기 전에 작성 된 응용 프로그램은 현재 운영 체제에서 제대로 작동 하지 않거나, 조직에서 이전 시스템 및 이전 시스템을 유지 관리 하 고, 경우에 따라 완전히 지원 되지 않는 하드웨어 및 소프트웨어를 유지 해야 합니다.  
  
조직이 도메인 컨트롤러를 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008로 업데이트 한 경우에도 Windows Server 2003, Windows를 실행 하는 구성원 서버 모집단의 상당 부분을 찾는 것이 일반적입니다. 2000 서버 또는 Windows NT Server 4.0 (완전히 지원 되지 않음) 더 긴 조직은 에이징 시스템을 유지 관리 하 고, 기능 집합 간의 차이가이 증가 하 고, 프로덕션 시스템이 지원 되지 않을 가능성이 높습니다. 또한 더 긴 Active Directory 포리스트가 유지 되 고 있으며, 이전 시스템 및 응용 프로그램이 업그레이드 계획에서 누락 된 것을 확인할 수 있습니다. 이는 단일 응용 프로그램을 실행 하는 단일 컴퓨터에서 Active Directory가 레거시 프로토콜 및 인증 메커니즘을 지원 하도록 구성 되어 있기 때문에 도메인 또는 포리스트 전체 취약점을 도입할 수 있음을 의미할 수 있습니다.  
  
레거시 시스템 및 응용 프로그램을 제거 하려면 먼저 응용 프로그램을 식별 하 고 카탈로그를 지정 하는 데 중점을 두고 응용 프로그램 또는 호스트를 업그레이드할지 아니면 바꿀지를 결정 해야 합니다. 지원 또는 업그레이드 경로가 없는 매우 특수 한 응용 프로그램에 대 한 대체 항목을 찾기가 어려울 수 있지만 "creative 소멸" 이라는 개념을 활용 하 여 레거시 응용 프로그램을 새 응용 프로그램으로 바꿀 수 있습니다. 필요한 기능을 제공 합니다. [손상에 대 한 계획](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md) 은이 문서의 뒷부분에 나오는 "손상 계획"에 자세히 설명 되어 있습니다.  
  
### <a name="misconfiguration"></a>잘못  
*법률 번호 4: 시작 하도록 보안이 유지 되지 않은 컴퓨터에 보안 픽스를 설치 하는 것은 그다지 좋은 방법이 아닙니다.* - [10 가지 불변의 보안 관리 법칙](https://technet.microsoft.com/library/cc722488.aspx)  
  
일반적으로 시스템을 최신 상태로 유지 하 고 패치를 적용 하는 환경 에서도 일반적으로 운영 체제의 간격이 나 잘못 된 부분, 컴퓨터에서 실행 되는 응용 프로그램 및 Active Directory를 식별 합니다. 일부 잘못 된 구성을 통해 손상 된 로컬 컴퓨터만 표시 되지만 컴퓨터를 "소유" 한 후 공격자는 일반적으로 다른 시스템 간에 손상을 전파 하 고 결국에는 Active Directory 하는 데 초점을 둡니다. 다음은 위험을 야기 하는 구성을 식별 하는 몇 가지 일반적인 영역입니다.  
  
#### <a name="in-active-directory"></a>Active Directory에서  
공격자가 가장 일반적으로 대상으로 하는 Active Directory 계정은 도메인 관리자 (DA), Enterprise Admins (EA) 또는 Active의 기본 제공 관리자 (BA) 그룹의 구성원 같은 가장 높은 수준의 권한 있는 그룹의 구성원 인 계정입니다. 디렉터리나. 이러한 그룹의 구성원은 이러한 그룹의 공격 노출 영역이 제한 되도록 가장 적은 수의 계정으로 줄여야 합니다. 이러한 권한 있는 그룹에서 "영구" 멤버 자격을 제거할 수도 있습니다. 즉, 도메인 및 포리스트 차원의 권한이 필요한 경우에만 이러한 그룹을 일시적으로 채울 수 있는 설정을 구현할 수 있습니다. 높은 권한의 계정을 사용 하는 경우 도메인 컨트롤러 또는 보안 관리 호스트와 같은 지정 된 보안 시스템 에서만 사용 해야 합니다. 이러한 모든 구성을 구현 하는 데 도움이 되는 자세한 정보는 [Active Directory 공격 노출 영역을 줄이는](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)데 제공 됩니다.  
  
Active Directory에서 가장 높은 권한 있는 그룹의 멤버 자격을 평가 하는 경우 일반적으로 세 가지 대부분의 권한 있는 그룹에서 과도 한 멤버 자격을 찾습니다. 경우에 따라 조직에는 DA 그룹에 수십 개의 계정이 포함 되어 있습니다. 다른 경우에는 조직에서 기본 제공 관리자 그룹에 직접 계정을 추가 하 여 해당 그룹이 DAs 그룹 보다 "낮은 권한" 이라고 생각 합니다. 그것이 아니야. EA 권한이 거의 필요 하지 않으며 일시적으로 필요한 경우에도 포리스트 루트 도메인에서 EA 그룹의 영구 구성원 중 일부를 종종 찾을 수 있습니다. 실제로 중복 되는 구성 이더라도 세 그룹 모두에서 IT 사용자의 일상적인 관리 계정을 찾는 것도 일반적입니다. [Active Directory 공격 노출 영역 축소](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)에 설명 된 것 처럼 계정이 이러한 그룹 중 하나 또는 모두의 영구 구성원 인지 여부에 관계 없이이 계정을 사용 하 여 AD DS 환경 및 it에서 관리 하는 시스템 및 계정을 제거할 수 있습니다. 보안 구성 및 Active Directory 권한 있는 계정의 사용에 대 한 권장 사항은 [Active Directory 공격 노출 영역을 줄이는](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)데 제공 됩니다.  
  
#### <a name="on-domain-controllers"></a>도메인 컨트롤러에서  
도메인 컨트롤러를 평가 하는 경우 구성원 서버와 다르게 구성 및 관리 되는 항목을 찾는 경우가 종종 있습니다. 도메인 컨트롤러는 도메인 컨트롤러에는 필요 하지만 응용 프로그램이 표준 빌드에 포함 되기 때문에 도메인 컨트롤러는 구성원 서버에 설치 된 것과 동일한 응용 프로그램 및 유틸리티를 실행 하기도 합니다. 이러한 응용 프로그램은 도메인 컨트롤러에 최소의 기능을 제공할 수 있지만, 포트를 열거나, 높은 권한의 서비스 계정을 만들거나, 사용자가 시스템에 액세스 권한을 부여 하는 구성 설정을 요구 하 여 공격 노출 영역에 크게 추가할 수 있습니다. 는 인증 및 그룹 정책 응용 프로그램 이외의 용도로 도메인 컨트롤러에 연결 하면 안 됩니다. 일부 위반에서 공격자는 도메인 컨트롤러에 대 한 액세스 권한을 얻을 뿐만 아니라 도메인 컨트롤러에 이미 설치 되어 있는 도구를 사용 하 여 AD DS 데이터베이스를 수정 하거나 손상 시킬 수 있습니다.  
  
도메인 컨트롤러에 대 한 Internet Explorer 구성 설정을 추출할 때 사용자가 Active Directory에서 높은 수준의 권한을 가진 계정으로 로그온 하 고 해당 계정을 사용 하 여 도메인에서 인터넷 및 인트라넷에 액세스 한 것을 확인할 수 있습니다. 컨트롤러용. 경우에 따라 계정은 도메인 컨트롤러에서 인터넷 콘텐츠를 다운로드할 수 있도록 Internet Explorer 설정을 구성 하 고, 프리웨어 유틸리티는 인터넷 사이트에서 다운로드 되 고 도메인 컨트롤러에 설치 되어 있습니다. Internet Explorer 보안 강화 구성은 기본적으로 사용자 및 관리자에 대해 사용 하도록 설정 되어 있지만 관리자가 사용 하지 않도록 설정 된 것을 종종 관찰 합니다. 높은 권한의 계정이 인터넷에 액세스 하 여 컴퓨터에 콘텐츠를 다운로드 하는 경우 해당 컴퓨터는 심각한 위험에 노출 됩니다. 컴퓨터가 도메인 컨트롤러인 경우 전체 AD DS 설치가 위험에 노출 됩니다.  
  
##### <a name="protecting-domain-controllers"></a>도메인 컨트롤러 보호  
도메인 컨트롤러를 중요 인프라 구성 요소로 처리 하 고, 더 보안이 엄격를 보호 하 고, 파일, 인쇄 및 응용 프로그램 서버 보다 더 많은 엄격을 구성 해야 합니다. 도메인 컨트롤러는 도메인 컨트롤러에서 공격 으로부터 도메인 컨트롤러를 작동 하거나 보호 하지 않아도 되는 소프트웨어를 실행 해서는 안 됩니다. 도메인 컨트롤러는 인터넷 액세스를 허용 하지 않아야 하 고, 보안 설정은 Gpo (그룹 정책 개체)에 의해 구성 및 적용 해야 합니다. 도메인 컨트롤러의 보안 설치, 구성 및 관리에 대 한 자세한 권장 사항은 [도메인 컨트롤러를 공격 으로부터 보호](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)하는 데 제공 됩니다.  
  
#### <a name="within-the-operating-system"></a>운영 체제 내에서  
*법률 번호 2: 악의적인 사용자가 컴퓨터에서 운영 체제를 변경할 수 있는 경우 더 이상 컴퓨터가 아닙니다.* - [10 가지 불변 보안 법 (버전 2.0)](https://technet.microsoft.com/security/hh278941.aspx)  
  
일부 조직에서는 다양 한 유형의 서버에 대 한 기준 구성을 만들고 운영 체제를 설치한 후에 제한적인 사용자 지정을 허용 하지만, 손상 된 환경에 대 한 분석은 종종 수동으로 또는 독립적으로 구성 합니다. 동일한 기능을 수행 하는 두 서버 간의 구성은 완전히 다를 수 있으며 두 서버 모두 안전 하 게 구성 되지 않습니다. 반대로 서버 구성 기준은 일관 되 게 적용 될 수 있지만 일관 되 게 잘못 구성 될 수도 있습니다. 즉, 서버는 지정 된 형식의 모든 서버에서 동일한 취약성을 만드는 방식으로 구성 됩니다. 잘못 된 구성에는 보안 기능을 사용 하지 않도록 설정 하 고, 계정에 과도 한 권한 및 권한을 부여 하 고, 시스템 간에 동일한 로컬 자격 증명을 사용 하 고, 설치를 허용 하는 등의 방법이 포함 됩니다. 권한 없는 응용 프로그램 및 자체의 취약성을 만드는 유틸리티  
  
##### <a name="disabling-security-features"></a>보안 기능 사용 안 함  
조직에서는 경우에 따라 WFAS (고급 보안)이 포함 된 Windows 방화벽을 사용 하지 않도록 설정 하는 것이 더 어렵거나 작업 집약적 구성이 필요 하다 신념으로. 그러나 Windows Server 2008부터 서버에 역할이 나 기능이 설치 된 경우 역할이 나 기능이 서버에 설치 되 면 기본적으로 역할이 나 기능이 작동 하는 데 필요한 최소한의 권한으로 구성 되며, Windows 방화벽은 해당 역할을 지원 하도록 자동으로 구성 됩니다. 또는 기능입니다. 조직에서는 다른 호스트 기반 방화벽을 사용 하지 않고를 사용 하지 않도록 설정 하 여 전체 Windows 환경의 공격 노출 영역을 늘립니다. 경계 방화벽은 인터넷에서 환경을 직접 대상으로 하는 공격에 대 한 보호를 제공 하지만, [드라이브 다운로드](https://www.microsoft.com/security/sir/glossary/drive-by-download-sites.aspx) 공격과 같은 다른 공격 벡터 또는 인트라넷의 손상 된 다른 시스템에서 발생 하는 공격에 대 한 보호를 제공 하지 않습니다.  
  
관리 담당자가 프롬프트를 방해 한다는 메시지를 표시 하기 때문에 UAC (사용자 계정 컨트롤) 설정은 서버에서 사용 하지 않는 경우가 있습니다. [Microsoft 지원 문서 2526083](https://support.microsoft.com/kb/2526083) 에서는 Windows SERVER에서 uac를 사용 하지 않도록 설정할 수 있는 시나리오에 대해 설명 하지만, Server core 설치를 실행 하는 경우 (uac가 의도적으로 사용 하지 않도록 설정 된 경우) 신중 하 게 고려 하지 않고 서버에서 uac를 사용 하지 않도록 설정 해야 합니다.  
  
경우에 따라 조직에서는 windows server 2012, Windows를 실행 하는 컴퓨터에 Windows Server 2003 기준을 적용 하는 등의 오래 된 서버 구성 설정을 새 운영 체제에 적용 하기 때문에 보안 수준이 낮은 값으로 서버 설정이 구성 됩니다. 서버 2008 R2 또는 Windows Server 2008 (운영 체제의 변경 내용을 반영 하도록 기준을 변경 하지 않음) 새 운영 체제를 배포할 때 기존 서버 기준을 새 운영 체제에 전달 하는 대신 보안 변경 내용 및 구성 설정을 검토 하 여 구현 된 설정이 적용 되 고 새 운영 체제에 적합 한지 확인 합니다.  
  
##### <a name="granting-excessive-privilege"></a>과도 한 권한 부여  
거의 모든 환경에서 Windows 시스템의 로컬 및 도메인 기반 계정에 과도 한 권한이 부여 되었습니다. 사용자에 게 해당 워크스테이션에 대 한 로컬 관리자 권한이 부여 되 고, 구성원 서버는 작동 해야 하는 것 이상의 권한으로 구성 된 서비스를 실행 하며, 서버 모집단의 로컬 관리자 그룹에 수십 또는 수백 개의를 포함 합니다. 로컬 및 도메인 계정. 컴퓨터에서 하나의 권한 있는 계정만 손상 되 면 공격자는 컴퓨터에 로그온 하는 모든 사용자 및 서비스의 계정을 손상 시키고 자격 증명을 수집 하 고 활용 하 여 다른 시스템에 손상을 전파할 수 있습니다.  
  
현재는 해시-해시 (PTH) 및 기타 자격 증명 도난 공격을 발생 시킬 수 있지만, 공격자가 관리자를 얻을 때 다른 권한 있는 계정의 자격 증명을 간단 하 고 간편 하 게 추출할 수 있는 무료 도구가 있기 때문입니다. 또는 컴퓨터에 대 한 시스템 수준 액세스입니다. 로그온 세션에서 자격 증명을 수집 하는 도구를 사용할 수 없는 경우에도 컴퓨터에 대 한 특권 수준의 액세스 권한을 가진 공격자는 키 입력, 스크린샷 및 클립보드 내용을 캡처하는 키 링로 거를 쉽게 설치할 수 있습니다. 컴퓨터에 대 한 특권 수준의 액세스 권한을 가진 공격자는 맬웨어 방지 소프트웨어를 사용 하지 않도록 설정 하거나, 루트를 설치 하거나, 보호 된 파일을 수정 하거나, 공격을 자동화 하는 컴퓨터에 맬웨어를 설치 하거나, 서버를 [다운로드 하 여 드라이브로](https://www.microsoft.com/security/sir/glossary/drive-by-download-sites.aspx) 전환할 수 있습니다  
  
단일 컴퓨터 이상으로 위반을 확장 하는 데 사용 되는 전략은 다양 하지만, 손상을 전파 하는 열쇠는 추가 시스템에 대 한 높은 권한의 액세스를 획득 하는 것입니다. 시스템에 대 한 권한 있는 액세스 권한이 있는 계정 수를 줄이면 해당 컴퓨터 뿐만 아니라 공격자가 컴퓨터에서 중요 한 자격 증명을 수집 하는 가능성이 줄어듭니다.  
  
##### <a name="standardizing-local-administrator-credentials"></a>로컬 관리자 자격 증명 표준화  
Windows 컴퓨터에서 로컬 관리자 계정의 이름을 변경 하는 값이 있는지 여부에 대 한 자세한 논의는 보안 전문가 들에 게 있습니다. 로컬 관리자 계정에 대 한 중요 한 것은 여러 컴퓨터에서 동일한 사용자 이름 및 암호를 사용 하 여 구성 되었는지 여부입니다.  
  
로컬 관리자 계정이 서버 전체에서 같은 값으로 명명 되 고 계정에 할당 된 암호가 동일한 값으로 구성 된 경우 공격자는 관리자 또는 시스템 수준 액세스 권한이 있는 컴퓨터에서 계정의 자격 증명을 추출할 수 있습니다. 을 (를) 가져왔습니다. 공격자는 처음에 관리자 계정을 손상 시킬 필요가 없습니다. 로컬 관리자 그룹의 구성원 이거나 LocalSystem 또는 관리자 권한으로 실행 하도록 구성 된 서비스 계정의 사용자 계정만 손상 되어야 합니다. 그런 다음 공격자는 관리자 계정에 대 한 자격 증명을 추출 하 고 네트워크 로그온에서 네트워크의 다른 컴퓨터에 해당 자격 증명을 재생할 수 있습니다.  
  
표시 되는 계정 자격 증명과 동일한 사용자 이름 및 암호를 가진 로컬 계정이 다른 컴퓨터에 있으면 로그온 시도가 성공 하 고 공격자가 대상 컴퓨터에 대 한 권한 있는 액세스 권한을 얻습니다. 현재 버전의 Windows에서는 기본 제공 관리자 계정이 [기본적으로 사용 하지 않도록 설정](https://technet.microsoft.com/library/cc753450.aspx)되어 있지만 레거시 운영 체제에서는 계정이 기본적으로 사용 하도록 설정 되어 있습니다.  
  
> [!NOTE]  
> 일부 조직에서는 하다 신념으로에서 사용 하도록 설정 된 로컬 관리자 계정을 의도적으로 구성 하 여 다른 모든 권한 있는 계정이 시스템에서 잠기는 경우 "안전 하지 않은"를 제공 합니다. 그러나 로컬 관리자 계정이 사용 하지 않도록 설정 되 고 계정을 사용 하도록 설정 하거나 관리자 권한으로 시스템에 로그온 할 수 있는 다른 계정이 없는 경우에도 시스템을 안전 모드로 부팅할 수 있으며 [Microsoft 지원 문서 814777](https://support.microsoft.com/kb/814777)에 설명 된 대로 기본 제공 로컬 관리자 계정을 다시 사용 하도록 설정할 수 있습니다. 또한 시스템에서 Gpo를 성공적으로 적용 하는 경우에는 GPO를 일시적으로 수정 하 여 관리자 계정을 다시 사용 하도록 설정할 수 있습니다. 또는 제한 된 그룹은 도메인 기반 계정을 로컬 관리자 그룹에 추가 하도록 구성할 수 있습니다. 복구를 수행 하 고 관리자 계정을 다시 사용 하지 않도록 설정할 수 있습니다. 기본 제공 로컬 관리자 계정 자격 증명을 사용 하는 측면 손상을 효과적으로 방지 하려면 로컬 관리자 계정에 대 한 고유한 사용자 이름 및 암호를 구성 해야 합니다. GPO를 통해 로컬 관리자 계정에 대 한 고유 암호를 배포 하려면 technet에서 [gpo를 통해 기본 제공 관리자 계정의 암호를 관리](https://technet.microsoft.com/mt227395.aspx) 하는 방법을 참조 하세요.  
  
##### <a name="permitting-installation-of-unauthorized-applications"></a>권한 없는 응용 프로그램 설치 허용  
*법률 번호 1: 악의적인 사용자가 컴퓨터에서 자신의 프로그램을 실행 하도록 유도할 수 있는 경우에는 사용자의 컴퓨터에만 해당 됩니다.* - [10 가지 불변 보안 법 (버전 2.0)](https://technet.microsoft.com/security/hh278941.aspx)  
  
조직에서 서버 간에 일관 된 기준 설정을 배포 하는지 여부에 관계 없이 서버에서 정의한 역할의 일부가 아닌 응용 프로그램을 설치 하는 것은 허용 되지 않습니다. 서버의 지정 된 기능에 포함 되지 않은 소프트웨어 설치를 허용 하면 서버 공격 노출 영역을 늘리고 응용 프로그램 취약성을 야기 하는 소프트웨어의 우발적인 또는 악성 설치에 서버가 노출 됩니다. 시스템이 불안정 합니다.  
  
#### <a name="applications"></a>Applications  
앞에서 설명한 것 처럼 응용 프로그램은 일반적으로 응용 프로그램에 필요한 것 보다 많은 권한이 부여 된 계정을 사용 하도록 설치 및 구성 됩니다. 응용 프로그램의 설명서에서 서비스 계정이 서버의 로컬 관리자 그룹의 구성원 이거나 LocalSystem의 컨텍스트에서 실행 되도록 구성 해야 하는 경우를 지정 합니다. 응용 프로그램에 이러한 권한이 필요 하기는 하지만 응용 프로그램의 서비스 계정에 필요한 권한 및 사용 권한을 결정 하려면 추가 시간과 노력에 투자가 필요 하기 때문입니다. 응용 프로그램 및 구성 된 기능이 작동 하는 데 필요한 최소 권한으로 응용 프로그램을 설치 하지 않는 경우 시스템은 운영 체제 자체에 대 한 공격 없이 응용 프로그램 권한을 활용 하는 공격에 노출 됩니다.  
  
### <a name="lack-of-secure-application-development-practices"></a>보안 응용 프로그램 개발 방법 부족  
비즈니스 작업을 지원 하기 위한 인프라가 있습니다. 이러한 워크 로드가 사용자 지정 응용 프로그램에서 구현 되는 경우 보안 모범 사례를 사용 하 여 응용 프로그램을 개발 하는 것이 중요 합니다. 엔터프라이즈 전체 인시던트의 근본 원인 분석에는 종종 사용자 지정 응용 프로그램 (특히 인터넷에 연결 된 응용 프로그램)을 통해 초기 손상이 영향을 주는 것으로 나타납니다. 이러한 손상의 대부분은 SQLi (SQL 삽입) 및 XSS (사이트 간 스크립팅) 공격과 같은 잘 알려진 공격을 통해 수행 됩니다.  
  
SQL 삽입은 사용자 정의 입력에서 실행을 위해 데이터베이스로 전달 되는 SQL 문을 수정할 수 있는 응용 프로그램 취약점입니다. 이 입력은 응용 프로그램의 필드, 매개 변수 (예: 쿼리 문자열 또는 쿠키) 또는 다른 메서드를 통해 제공 될 수 있습니다. 이 주입의 결과는 데이터베이스에 제공 되는 SQL 문이 개발자가 의도 한 것과 근본적으로 다른 것입니다. 사용자 이름/암호 조합 평가에 사용 되는 일반적인 쿼리를 예로 들어 보겠습니다.  
  
`SELECT userID FROM users WHERE username = 'sUserName' AND password = 'sPassword'`  
  
데이터베이스 서버에서이를 수신 하면 사용자 테이블을 검색 하 고 사용자 이름과 암호가 사용자가 제공한 사용자 이름과 암호 (일종의 로그인 형식을 통해)와 일치 하는 userID 레코드를 반환 하도록 서버에 지시 합니다. 이 경우 개발자는 사용자가 올바른 사용자 이름과 암호를 제공할 수 있는 경우에만 유효한 레코드만 반환 하는 것이 좋습니다. 둘 중 하나가 잘못 된 경우 데이터베이스 서버에서 일치 하는 레코드를 찾을 수 없으며 빈 결과를 반환할 수 없습니다.  
  
이 문제는 공격자가 유효한 데이터 대신 자체 SQL을 제공 하는 것과 같은 예기치 않은 작업을 수행 하는 경우에 발생 합니다. SQL은 데이터베이스 서버에서 즉석으로 해석 되기 때문에 삽입 된 코드는 개발자가 자신에 게 배치한 것 처럼 처리 됩니다. 예를 들어 공격자가 사용자 ID 및 **xyz** 또는 **1 = 1** 에 대 한 **관리자** 를 암호로 입력 한 경우 데이터베이스에서 처리 되는 결과 문은 다음과 같습니다.  
  
`SELECT userID FROM users WHERE username = 'administrator' AND password = 'xyz' OR 1=1`  
  
데이터베이스 서버에서이 쿼리를 처리 하는 경우 1 = 1은 항상 True로 평가 되기 때문에 테이블의 모든 행이 쿼리에서 반환 됩니다. 따라서 올바른 사용자 이름 및 암호를 알고 있거나 지정 하는 것이 중요 하지 않습니다. 대부분의 경우 사용자는 사용자의 데이터베이스에서 첫 번째 사용자로 로그온 됩니다. 대부분의 경우에는 관리자가 됩니다.  
  
단순히 로그온 하는 것 외에도 이러한 형식의 잘못 된 SQL 문을 사용 하 여 데이터베이스에서 데이터를 추가, 삭제 또는 변경 하거나 전체 테이블을 삭제 (삭제) 할 수 있습니다. SQLi를 과도 한 권한으로 결합 하는 가장 극단적인 경우에는 운영 체제 명령을 실행 하 여 새 사용자를 만들거나, 공격 도구를 다운로드 하거나, 선택한 공격자의 다른 작업을 수행할 수 있습니다.  
  
사이트 간 스크립팅에서 취약점은 응용 프로그램의 출력에 도입 됩니다. 응용 프로그램에 잘못 된 형식의 데이터를 제공 하는 공격자는 공격을 시작 하지만이 경우 형식이 잘못 된 데이터는 스크립트 코드 (예: JavaScript)의 형태로 실행 되며이는 공격에 사용 되는 브라우저에서 실행 됩니다. XSS 취약성을 악용 하면 공격자가 브라우저를 시작한 사용자의 컨텍스트에서 대상 응용 프로그램의 모든 기능을 실행할 수 있습니다. 일반적으로 XSS 공격은 사용자가 응용 프로그램에 연결 하는 링크를 클릭 하 고 공격 코드를 실행 하도록 하는 피싱 전자 메일을 통해 시작 됩니다.  
  
XSS는 공격자가 악용 하거나 사용 하는 사용자의 컨텍스트에서 비용을 양도 하는 온라인 뱅킹 및 전자 상거래 시나리오에서 악용 되는 경우가 많습니다. 사용자 지정 웹 기반 id 관리 응용 프로그램에 대 한 대상 공격의 경우 공격자가 자신의 id를 만들고, 권한 및 권한을 수정 하 고, 시스템 손상으로 이어질 수 있습니다.  
  
사이트 간 스크립팅 및 SQL 삽입에 대 한 자세한 내용은이 문서에서 다루지 않지만, [Open Web Application Security Project (OWASP)](https://www.owasp.org/index.php/Main_Page) 는 취약성 및 대책에 대해 심층적인 논의를 포함 하는 상위 10 개 목록을 게시 합니다.  
  
인프라 보안의 투자에 관계 없이, 잘 설계 되 고 작성 된 응용 프로그램이 해당 인프라 내에 배포 되는 경우 환경이 공격에 취약 한 상태가 됩니다. 잘 보호 된 인프라 라도 이러한 응용 프로그램 공격에 효과적인 대책을 제공할 수 없는 경우가 많습니다. 문제를 그래야만 응용 프로그램의 작동을 위해 서비스 계정에 과도 한 권한을 부여 해야 할 수 있습니다.  
  
Microsoft SDL(Security Development Lifecycle)은 서비스를 해제할 때까지 응용 프로그램의 수명 주기를 수집 하 고 확장 하는 요구 사항에 따라 초기부터 보안을 개선 하기 위해 작동 하는 구조적 프로세스 컨트롤의 집합입니다. 효과적인 보안 제어의 이러한 통합은 보안 측면에서 중요 한 것이 아니라 응용 프로그램 보안을 비용 및 일정 하 게 적용 하는 것이 중요 합니다. 응용 프로그램의 보안 문제를 평가 하는 것이 효과적으로 완료 되 면 조직에서는 응용 프로그램을 배포한 후에만 응용 프로그램 보안에 대 한 결정을 내려야 합니다. 조직에서는 응용 프로그램을 프로덕션 환경에 배포 하기 전에 응용 프로그램 결함을 해결 하거나, 비용 및 지연을 발생 시키거나, 알려진 보안 결함으로 프로덕션 환경에 응용 프로그램을 배포 하 여 조직을 손상 시킬 수 있습니다.  
  
일부 조직에서는 $1만 위의 프로덕션 코드에서 발생 하는 보안 문제를 해결 하는 전체 비용을 발생 시킬 수 있으며, 효과적인 SDL 없이 개발 된 응용 프로그램은 10만 줄의 코드를 기준으로 10 개 이상의 높은 심각도 문제를 해결할 수 있습니다. 규모가 많은 응용 프로그램에서 비용은 빠르게 에스컬레이션 됩니다. 이와 대조적으로, 많은 회사에서는 SDL의 최종 코드 검토 단계에서 10만 줄의 코드에 대 한 문제에 대 한 벤치 마크를 설정 하 고 프로덕션 환경에서 위험 수준이 높은 응용 프로그램에서 발생 하는 문제를 해결 합니다.  
  
SDL을 구현 하면 응용 프로그램의 요구 사항을 수집 하 고 디자인 하는 초기에 보안 요구 사항을 포함 하 여 보안을 강화 하 고 위험 수준의 응용 프로그램에 대 한 위협 모델링을 제공 개발자에 게 효과적인 교육 및 모니터링이 필요 합니다. 및에는 명확 하 고 일관 된 코드 표준 및 사례가 필요 합니다. SDL의 효과는 응용 프로그램 보안의 중요 한 기능으로, 응용 프로그램을 개발, 배포, 유지 관리 및 서비스 해제 하는 비용을 절감할 수 있습니다. SDL의 디자인과 구현에 대 한 자세한 내용은이 문서의 범위를 벗어나 있지만 자세한 지침 및 정보는 [Microsoft 보안 개발 수명 주기](https://www.microsoft.com/security/sdl/default.aspx) 를 참조 하세요.  
  


