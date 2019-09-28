---
ms.assetid: c81b8291-fba5-4b30-a43d-7feb2f4b66be
title: Windows Server 2012 R2의 AD FS 디자인 가이드
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d79bfa571f420b23b1716cd1bceca33fdc96e038
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359108"
---
# <a name="identify-your-ad-fs-deployment-goals"></a>AD FS 배포 목표 식별

Active Directory Federation Services \(ADFS\) 배포 목표를 정확 하 게 식별 하는 것은 AD FS 디자인 프로젝트의 성공에 필수적입니다. 반복적인 접근 방식을 사용 하 여 AD FS를 디자인 하 고 배포할 수 있도록 배포 목표의 우선 순위를 지정 하 고 결합 합니다. AD FS 디자인과 관련 된 기존의 문서화 되 고 미리 정의 된 AD FS 배포 목표를 활용 하 여 상황에 맞게 작동 하는 솔루션을 개발할 수 있습니다.  
  
이전 버전의 AD FS는 다음을 얻기 위해 가장 일반적으로 배포 되었습니다.  
  
-   회사 내에서 클레임\-\-기반 응용 프로그램에 액세스할 때 직원이 나 고객에 게 웹 기반 SSO 환경을 제공 합니다.  
  
-   직원 또는 고객에 게 페더레이션 파트너 조직의\-리소스에 액세스 하는 웹 기반 SSO 환경을 제공 합니다.  
  
-   내부적으로 호스트 되는 웹 사이트 또는\-서비스에 원격으로 액세스할 때 직원이 나 고객에 게 웹 기반 SSO 환경을 제공 합니다.  
  
-   직원 또는 고객이 클라우드의 리소스 또는 서비스에\-액세스할 때 웹 기반 SSO 환경을 제공 합니다.  
  
이러한 기능 외에도 Windows Server® 2012 r 2의 AD FS에서는 다음을 수행 하는 데 도움이 되는 기능을 추가 합니다.  
  
-   SSO 및 원활한 2단계 인증을 위한 장치 작업 공간 연결. 이를 통해 조직은 사용자의 개인 장치에서 액세스를 허용 하 고 이러한 액세스를 제공할 때 위험을 관리할 수 있습니다.  
  
-   다단계\-액세스 제어를 사용 하 여 위험 관리. AD FS는 어떤 사용자가 어떤 응용 프로그램에 액세스했는지를 제어하는 다양한 수준의 권한 부여를 제공합니다. 이는 UPN, 전자 메일, \(보안 그룹 구성원 자격, 인증 강도 등의 사용자 특성, \(장치가\)작업 공간에 연결\) 되었는지 또는 요청 특성 \(을기반으로할수있습니다.네트워크 위치, IP 주소 또는 사용자 에이전트\)입니다.  
  
-   중요 한 응용 프로그램에\-대 한 추가 multi-factor authentication을 사용 하 여 위험 관리. AD FS를 사용 하 여 전역적으로 또는 응용 프로그램\-별로 multi-factor authentication을 요구 하는 정책을 제어할 수 있습니다. 또한 AD FS는 최종 사용자를 위한 안전 하 고\-원활한 multi-factor\-experience를 위해 모든 다단계 공급 업체에 대 한 확장 지점도 제공 합니다.  
  
-   웹 응용 프로그램 프록시에 의해 보호 되는 엑스트라넷에서 웹 리소스에 액세스 하기 위한 인증 및 권한 부여 기능을 제공 합니다.  
  
요약 하자면, Windows Server 2012 r 2의 AD FS를 배포 하 여 조직에서 다음과 같은 목표를 달성할 수 있습니다.  
  
### <a name="enable-your-users-to-access-resources-on-their-personal-devices-from-anywhere"></a>사용자가 어디서 나 자신의 개인 장치에서 리소스에 액세스할 수 있도록 설정  
  
-   사용자가 개인 장치를 회사 Active Directory에 연결함으로써 이러한 장치에서 회사 리소스에 액세스할 때 액세스 권한 및 원활한 환경을 얻을 수 있는 작업 공간 연결  
  
-   회사\-네트워크 내에서 웹 응용 프로그램 프록시로 보호 되 고 인터넷을 통해 액세스 되는 리소스의 사전 인증입니다.  
  
-   암호가 만료된 경우 리소스에 계속 액세스할 수 있도록 사용자가 작업 공간 연결된 장치에서 암호를 변경할 수 있는 암호 변경  
  
### <a name="enhance-your-access-control-risk-management-tools"></a>액세스 제어 위험 관리 도구 향상  
위험 관리는 모든 IT 조직의 관리 및 규정 준수에서 중요한 측면입니다. 다음을 포함 하 여 Windows Server® 2012 r 2에서 AD FS의 다양 한 액세스 제어 위험 관리 기능이 향상 되었습니다.  
  
-   사용자가 AD FS\-보안 응용 프로그램에 액세스 하기 위해 인증 하는 방법을 제어 하는 네트워크 위치를 기반으로 하는 유연한 제어  
  
-   사용자의 데이터, 장치 데이터 및 네트워크 위치에 따라\-multi-factor authentication을 수행 해야 하는지를 결정 하는 유연한 정책입니다.  
  
-   SSO\-를 무시 하 고 사용자가 중요 한 응용 프로그램에 액세스할 때마다 자격 증명을 제공 하도록 하는 응용 프로그램 제어 단위  
  
-   사용자 데이터, 장치 데이터 또는 네트워크 위치에 따라응용프로그램액세스정책에따라유연합니다.\-  
  
-   관리자가 인터넷의 무차별 암호 대입 공격으로부터 Active Directory 계정을 보호할 수 있는 AD FS 엑스트라넷 잠금.  
  
-   Active Directory에서 사용할 수 없도록 설정되거나 삭제된 작업 공간 연결 장치에 대한 액세스 해지  
  
### <a name="use-ad-fs-to-enhance-the-sign-in-experience"></a>AD FS를 사용 하 여 로그인\-환경 개선  
다음은 관리자가 로그인\-환경을 사용자 지정 하 고 향상 시킬 수 있도록 하는 Windows Server® 2012 r 2의 새로운 AD FS 기능입니다.  
  
-   AD FS 서비스의 사용자 지정 통합으로 한 번 변경하면 변경 내용이 지정된 팜의 나머지 AD FS 페더레이션 서버로 자동으로 전파  
  
-   최신으로\-표시 되 고 다양 한 폼 팩터를 자동으로 확인 하는 업데이트 된 로그인 페이지입니다.  
  
-   회사 도메인에 가입 되어 있지\-않지만 여전히 회사 네트워크 \(인트라넷\)내에서 액세스 요청을 생성 하는 장치에 대해 양식 기반 인증으로 자동 대체를 지원 합니다.  
  
-   회사 로고, 그림 이미지, IT 지원에 대한 표준 링크, 홈페이지, 개인 정보 등을 사용자 지정하는 간단한 컨트롤  
  
-   로그인\-페이지에서 설명 메시지의 사용자 지정  
  
-   웹 테마 사용자 지정  
  
-   회사 파트너의 \(개인 정보\) 보호를 위해 사용자의 조직 접미사를 기반으로 하는 홈 영역 검색 hrd  
  
-   응용 프로그램을 기반으로 영역\-을 자동으로 선택 하기 위해 응용 프로그램 별로 hrd 필터링을 사용 합니다.  
  
-   한\-번의 클릭으로 오류 보고를 통해 쉽게 문제를 해결할 수 있습니다.  
  
-   사용자 지정 가능한 오류 메시지  
  
-   둘 이상의 인증 공급자를 사용할 수 있는 경우 사용자 인증 선택  
  
## <a name="see-also"></a>관련 항목  
[Windows Server 2012 R2의 AD FS 디자인 가이드](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

