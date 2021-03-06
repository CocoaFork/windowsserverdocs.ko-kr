---
title: RADIUS 서버로 작동하는 NPS 계획
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버 RADIUS 서버 배포 계획에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 2900dd2c-0f70-4f8d-9650-ed83d51d509a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bbcf3338f2cd6d8662a84faf263b486e31b140e5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405340"
---
# <a name="plan-nps-as-a-radius-server"></a>RADIUS 서버로 작동하는 NPS 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

NPS\) \(네트워크 정책 서버를 RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 서버로 배포 하는 경우 NPS는 로컬 도메인 및 로컬 도메인을 신뢰 하는 도메인에 대 한 연결 요청에 대 한 인증, 권한 부여 및 계정을 수행 합니다. 이러한 계획 지침을 사용 하 여 RADIUS 배포를 간소화할 수 있습니다.

이러한 계획 지침에는 NPS를 RADIUS 프록시로 배포 하려는 경우는 포함 되지 않습니다. Nps를 RADIUS 프록시로 배포할 때 nps는 NPS 또는 원격 도메인, 트러스트 되지 않은 도메인 또는 둘 다의 다른 RADIUS 서버를 실행 하는 서버에 연결 요청을 전달 합니다. 

네트워크의 RADIUS 서버로 NPS를 배포 하기 전에 다음 지침을 사용 하 여 배포를 계획 합니다.

- NPS 구성을 계획 합니다.

- RADIUS 클라이언트를 계획 합니다.

- 인증 방법의 사용을 계획 합니다.

- 네트워크 정책을 계획 합니다.

- NPS 계정 계획

## <a name="plan-nps-configuration"></a>NPS 구성 계획

NPS가 구성원 인 도메인을 결정 해야 합니다. 다중 도메인 환경의 경우 NPS는 해당 계정이 구성원 인 도메인의 사용자 계정에 대 한 자격 증명과 NPS의 로컬 도메인을 신뢰 하는 모든 도메인에 대 한 자격 증명을 인증할 수 있습니다. NPS가 권한 부여 프로세스 중에 사용자 계정의 전화 접속 속성을 읽을 수 있도록 하려면 NPS의 컴퓨터 계정을 각 도메인의 RAS 및 NPSs 그룹에 추가 해야 합니다.

NPS의 도메인 멤버 자격을 확인 한 후에는 RADIUS 프로토콜을 사용 하 여 네트워크 액세스 서버 라고도 하는 RADIUS 클라이언트와 통신 하도록 서버를 구성 해야 합니다. 또한 NPS가 이벤트 로그에 기록 하는 이벤트 유형을 구성할 수 있으며 서버에 대 한 설명을 입력할 수 있습니다.

### <a name="key-steps"></a>주요 단계

NPS 구성 계획 중에 다음 단계를 사용할 수 있습니다.

- NPS가 RADIUS 클라이언트에서 RADIUS 메시지를 수신 하는 데 사용 하는 RADIUS 포트를 결정 합니다. 기본 포트는 radius 인증 메시지의 경우 UDP 포트 1812 및 1645, RADIUS 계정 메시지의 경우 포트 1813 및 1646입니다.

- NPS가 여러 네트워크 어댑터를 사용 하 여 구성 된 경우 RADIUS 트래픽이 허용 될 어댑터를 결정 합니다.

- NPS가 이벤트 로그에 기록 하도록 할 이벤트 유형을 결정 합니다. 거부 된 인증 요청, 성공한 인증 요청 또는 두 유형의 요청을 기록할 수 있습니다.

- 둘 이상의 NPS를 배포 하 고 있는지 여부를 확인 합니다. RADIUS 기반 인증 및 계정에 대 한 내결함성을 제공 하려면 둘 이상의 NPSs를 사용 합니다. 한 NPS는 기본 RADIUS 서버로 사용 되며 다른 NPS는 백업으로 사용 됩니다. 그러면 각 RADIUS 클라이언트는 NPSs에서 구성 됩니다. 기본 NPS를 사용할 수 없게 되 면 RADIUS 클라이언트는 대체 NPS에 액세스 요청 메시지를 보냅니다.

- 한 NPS 구성을 다른 NPSs로 복사 하는 데 사용 되는 스크립트를 계획 하 여 관리 오버 헤드를 절감 하 고 서버의 잘못 된 구성 방지 합니다. NPS는 다른 NPS로 가져오기 위해 NPS 구성의 전체 또는 일부를 복사 하는 데 사용할 수 있는 Netsh 명령을 제공 합니다. Netsh 프롬프트에서 명령을 수동으로 실행할 수 있습니다. 그러나 명령 시퀀스를 스크립트로 저장 하는 경우 서버 구성을 변경 하려는 경우 나중에 스크립트를 실행할 수 있습니다.

## <a name="plan-radius-clients"></a>RADIUS 클라이언트 계획

RADIUS 클라이언트는 무선 액세스 지점과 VPN (가상 사설망) 서버, 802.1 X 가능 스위치 및 전화 접속 서버와 같은 네트워크 액세스 서버입니다. 연결 요청 메시지를 RADIUS 서버로 전달 하는 RADIUS 프록시는 RADIUS 클라이언트 이기도 합니다. NPS는 RFC 2865, "RADIUS (원격 인증 전화 접속 사용자 서비스)", RFC 2866, "RADIUS 계정"에 설명 된 대로 RADIUS 프로토콜을 준수 하는 모든 네트워크 액세스 서버 및 RADIUS 프록시를 지원 합니다.

>[!IMPORTANT]
>클라이언트 컴퓨터와 같은 액세스 클라이언트는 RADIUS 클라이언트가 아닙니다. RADIUS 프로토콜을 지 원하는 네트워크 액세스 서버 및 프록시 서버만 RADIUS 클라이언트입니다.

또한 두 무선 액세스 지점과 스위치 모두 802.1 X 인증을 수행할 수 있어야 합니다. EAP\) 또는 EAP\)\(EAP (extensible authentication protocol) \(를 배포 하려는 경우 액세스 지점과 스위치는 EAP 사용을 지원 해야 합니다.

무선 액세스 지점에 대 한 PPP 연결의 기본 상호 운용성을 테스트 하려면 액세스 지점과 PAP (암호 인증 프로토콜)를 사용 하도록 액세스 클라이언트를 구성 합니다. 네트워크 액세스에 사용 하려는 항목을 테스트할 때까지 PEAP와 같은 추가 PPP 기반 인증 프로토콜을 사용 합니다.

### <a name="key-steps"></a>주요 단계

RADIUS 클라이언트를 계획 하는 동안 다음 단계를 사용할 수 있습니다.

- NPS에서 구성 해야 하는 Vsa (공급 업체 관련 특성)를 문서화 합니다. 네트워크 액세스 서버에 Vsa가 필요한 경우 NPS에서 네트워크 정책을 구성할 때 나중에 사용할 수 있도록 VSA 정보를 기록 합니다. 

- RADIUS 클라이언트와 NPS의 IP 주소를 문서화 하 여 모든 장치의 구성을 간소화 합니다. RADIUS 클라이언트를 배포 하는 경우 radius 프로토콜을 사용 하도록 구성 하 고 인증 서버로 입력 된 NPS IP 주소를 사용 하도록 구성 해야 합니다. 그리고 RADIUS 클라이언트와 통신 하도록 NPS를 구성 하는 경우 NPS 스냅인에 RADIUS 클라이언트 IP 주소를 입력 해야 합니다.

- RADIUS 클라이언트와 NPS 스냅인에서 구성에 대 한 공유 암호를 만듭니다. Nps에서 RADIUS 클라이언트를 구성 하는 동안 NPS 스냅인에도 입력 하는 공유 암호 또는 암호를 사용 하 여 RADIUS 클라이언트를 구성 해야 합니다.

## <a name="plan-the-use-of-authentication-methods"></a>인증 방법 사용 계획

NPS는 암호 기반 인증 방법과 인증서 기반 인증 방법을 모두 지원 합니다. 그러나 모든 네트워크 액세스 서버에서 동일한 인증 방법을 지 원하는 것은 아닙니다. 경우에 따라 네트워크 액세스의 유형에 따라 다른 인증 방법을 배포 하는 것이 좋습니다.

예를 들어, 조직에 대 한 무선 및 VPN 액세스를 모두 배포할 수 있지만 각 액세스 유형에 대해 다른 인증 방법을 사용 합니다. eap-tls (Transport Layer Security)를 사용 하는 강력한 보안으로 인해 VPN 연결에 대 한 eap-tls는 eap-tls (Transport Layer Security)를 사용 합니다. 는 802.1 X 무선 연결을 위한 및 PEAP-CHAP v2를 제공 합니다.

Microsoft 챌린지 핸드셰이크 인증 프로토콜 버전 2 (PEAP-CHAP v2)를 사용 하는 PEAP는 휴대용 컴퓨터 및 기타 무선 장치에 사용 하도록 특별히 설계 된 빠른 다시 연결 이라는 기능을 제공 합니다. 빠른 다시 연결을 사용 하면 무선 클라이언트가 새 액세스 지점과 연결할 때마다 다시 인증 하지 않고도 동일한 네트워크의 무선 액세스 지점 간에 이동할 수 있습니다. 이는 무선 사용자에 게 더 나은 환경을 제공 하 고 자격 증명을 다시 입력 하지 않고도 액세스 점수 간을 이동할 수 있도록 합니다.
빠른 다시 연결 및 PEAP-CHAP v2에서 제공 하는 보안 때문에 PEAP-CHAP v2는 무선 연결에 대 한 인증 방법으로 논리적으로 선택 됩니다.

VPN 연결의 경우 EAP-TLS는 홈 또는 모바일 컴퓨터에서 조직의 VPN 서버로 인터넷을 통해 전송 되는 경우에도 네트워크 트래픽을 보호 하는 강력한 보안을 제공 하는 인증서 기반 인증 방법입니다.

### <a name="certificate-based-authentication-methods"></a>인증서 기반 인증 방법

인증서 기반 인증 방법에는 강력한 보안을 제공 하는 이점이 있습니다. 또한 암호 기반 인증 방법 보다 배포 하기가 더 어려울 수 있습니다.

PEAP-CHAP v2와 EAP-TLS는 모두 인증서 기반 인증 방법 이지만 이러한 방법 간에는 여러 가지 차이점이 있습니다.

### <a name="eap-tls"></a>EAP-TLS

EAP-TLS는 클라이언트와 서버 인증 모두에 인증서를 사용 하며 조직에 PKI (공개 키 인프라)를 배포 해야 합니다. PKI를 배포 하는 것은 복잡할 수 있으며 NPS를 RADIUS 서버로 사용 하기 위한 계획과 독립적인 계획 단계가 필요 합니다.

EAP-TLS를 사용 하면 NPS는 인증 기관 \(CA\)에서 서버 인증서를 등록 하 고 인증서는 인증서 저장소의 로컬 컴퓨터에 저장 됩니다. 인증 프로세스 중에 NPS가 액세스 클라이언트에 해당 서버 인증서를 전송 하 여 해당 id를 액세스 클라이언트에 게 증명할 때 서버 인증이 발생 합니다. 액세스 클라이언트는 다양 한 인증서 속성을 검사 하 여 인증서가 유효 하 고 서버 인증 중에 사용 하기에 적합 한지 여부를 확인 합니다. 서버 인증서가 최소 서버 인증서 요구 사항을 충족 하 고 액세스 클라이언트에서 신뢰 하는 CA에서 발급 된 경우 NPS는 클라이언트에서 성공적으로 인증 됩니다.

마찬가지로 클라이언트 인증은 nps에 클라이언트 인증서를 전송 하 여 NPS에 대 한 id를 증명 하는 인증 프로세스 중에 발생 합니다. NPS는 인증서를 검사 하며, 클라이언트 인증서가 최소 클라이언트 인증서 요구 사항을 충족 하 고 NPS가 신뢰 하는 CA에서 발급 된 경우 액세스 클라이언트는 NPS에서 성공적으로 인증 됩니다.

서버 인증서를 NPS의 인증서 저장소에 저장 해야 하지만 클라이언트나 사용자 인증서는 클라이언트의 인증서 저장소나 스마트 카드에 저장할 수 있습니다.

이 인증 프로세스가 성공 하려면 모든 컴퓨터에서 로컬 컴퓨터 및 현재 사용자에 대 한 신뢰할 수 있는 루트 인증 기관 인증서 저장소에 조직의 CA 인증서를 포함 해야 합니다.

### <a name="peap-ms-chap-v2"></a>PEAP-ms-chap v2

PEAP-CHAP v2는 서버 인증에 인증서를 사용 하 고 사용자 인증에 암호 기반 자격 증명을 사용 합니다. 인증서는 서버 인증에만 사용 되므로 PEAP-CHAP v2를 사용 하기 위해 PKI를 배포할 필요가 없습니다. PEAP-MS-CHAP v2를 배포할 때 다음 두 가지 방법 중 하나로 NPS에 대 한 서버 인증서를 가져올 수 있습니다.

- Active Directory 인증서 서비스 (AD CS)를 설치한 다음 인증서를 NPSs로 자동 등록할 수 있습니다. 이 방법을 사용 하는 경우 NPS에 발급 된 인증서를 신뢰 하도록 네트워크에 연결 하는 클라이언트 컴퓨터에 CA 인증서도 등록 해야 합니다.

- VeriSign과 같은 공용 CA에서 서버 인증서를 구매할 수 있습니다. 이 방법을 사용 하는 경우 클라이언트 컴퓨터에서 이미 신뢰 하는 CA를 선택 해야 합니다. 클라이언트 컴퓨터가 CA를 신뢰 하는지 여부를 확인 하려면 클라이언트 컴퓨터에서 인증서 MMC (Microsoft Management Console) 스냅인을 열고 로컬 컴퓨터 및 현재 사용자에 대 한 신뢰할 수 있는 루트 인증 기관 저장소를 확인 합니다. 이러한 인증서 저장소에 CA의 인증서가 있는 경우 클라이언트 컴퓨터는 CA를 신뢰 하므로 CA에서 발급 한 모든 인증서를 신뢰 하 게 됩니다.

PEAP-CHAP v2를 사용 하는 인증 프로세스 중에 NPS가 서버 인증서를 클라이언트 컴퓨터로 보낼 때 서버 인증이 발생 합니다. 액세스 클라이언트는 다양 한 인증서 속성을 검사 하 여 인증서가 유효 하 고 서버 인증 중에 사용 하기에 적합 한지 여부를 확인 합니다. 서버 인증서가 최소 서버 인증서 요구 사항을 충족 하 고 액세스 클라이언트에서 신뢰 하는 CA에서 발급 된 경우 NPS는 클라이언트에서 성공적으로 인증 됩니다.

사용자 인증은 네트워크에 연결 하려고 시도 하는 사용자가 암호 기반 자격 증명을 사용 하 여 로그온을 시도할 때 발생 합니다. NPS는 자격 증명을 수신 하 고 인증 및 권한 부여를 수행 합니다. 사용자가 인증 되 고 권한이 부여 되 고 클라이언트 컴퓨터에서 NPS를 성공적으로 인증 한 경우에는 연결 요청이 허용 됩니다.

### <a name="key-steps"></a>주요 단계

인증 방법 사용을 계획 하는 동안 다음 단계를 사용할 수 있습니다.

- 무선, VPN, 802.1 X 가능 스위치 및 전화 접속 액세스와 같이 제공할 네트워크 액세스 유형을 식별 합니다.

- 각 액세스 유형에 사용 하려는 인증 방법을 결정 합니다. 강력한 보안을 제공 하는 인증서 기반 인증 방법을 사용 하는 것이 좋습니다. 그러나 PKI를 배포 하는 것은 실용적이 지 않을 수 있으므로 네트워크에 필요한 사항에 따라 다른 인증 방법을 사용할 수 있습니다.

- EAP-TLS를 배포 하는 경우 PKI 배포를 계획 합니다. 여기에는 서버 인증서 및 클라이언트 컴퓨터 인증서에 사용할 인증서 템플릿을 계획 하는 작업이 포함 됩니다. 도메인 구성원과 도메인 구성원이 아닌 컴퓨터에 인증서를 등록 하는 방법 및 스마트 카드 사용 여부를 결정 하는 방법도 포함 됩니다.

- PEAP-MS-CHAP v 2를 배포 하는 경우 NPSs에 서버 인증서를 발급 하기 위해 AD CS를 설치할지 또는 VeriSign과 같은 공용 CA에서 서버 인증서를 구매할 지 여부를 결정 합니다.

### <a name="plan-network-policies"></a>네트워크 정책 계획

네트워크 정책은 NPS에서 RADIUS 클라이언트에서 받은 연결 요청에 권한이 있는지 확인 하는 데 사용 됩니다. 또한 NPS는 사용자 계정의 전화 접속 속성을 사용 하 여 권한 부여 결정을 내리는 데 사용 됩니다.

네트워크 정책은 NPS 스냅인에 표시 되는 순서 대로 처리 되기 때문에 정책 목록에서 가장 제한적인 정책을 가장 먼저 저장 하도록 계획 합니다. 각 연결 요청에 대해 NPS는 정책 조건과 연결 요청 속성을 일치 시 키 려 고 합니다. NPS는 일치 항목을 찾을 때까지 각 네트워크 정책을 순서 대로 검사 합니다. 일치 항목을 찾지 못하면 연결 요청이 거부 됩니다.

### <a name="key-steps"></a>주요 단계

네트워크 정책을 계획 하는 동안 다음 단계를 사용할 수 있습니다.

- 가장 제한적인 네트워크 정책의 기본 NPS 처리 순서를 결정 합니다.

- 정책 상태를 확인 합니다. 정책 상태는 사용 또는 사용 안 함 값을 가질 수 있습니다. 이 정책을 사용 하도록 설정 하면 권한 부여를 수행 하는 동안 NPS에서 정책을 평가 합니다. 정책을 사용 하지 않는 경우에는 평가 되지 않습니다.

- 정책 유형을 결정 합니다. 정책 조건이 연결 요청에 의해 일치 하는 경우 정책에서 액세스를 허용 하도록 디자인 되었는지 아니면 정책 조건이 연결 요청에 의해 일치 하는 경우 정책에서 액세스를 거부 하도록 설계 되었는지 여부를 결정 해야 합니다. 예를 들어 Windows 그룹의 구성원에 대 한 무선 액세스를 명시적으로 거부 하려는 경우 그룹, 무선 연결 방법을 지정 하 고 액세스 거부의 정책 유형 설정을 포함 하는 네트워크 정책을 만들 수 있습니다.

- NPS에서 정책의 기반이 되는 그룹의 구성원 인 사용자 계정의 전화 접속 속성을 무시할지 여부를 결정 합니다. 이 설정을 사용 하지 않으면 사용자 계정의 전화 접속 속성이 네트워크 정책에 구성 된 설정을 재정의 합니다. 예를 들어 사용자에 게 액세스 권한을 부여 하는 네트워크 정책이 구성 되어 있지만 해당 사용자에 대 한 사용자 계정의 전화 접속 속성은 액세스 거부로 설정 되어 있으면 해당 사용자의 액세스가 거부 됩니다. 그러나 정책 유형 설정인 사용자 계정 전화 접속 속성 무시를 사용 하도록 설정 하면 동일한 사용자에 게 네트워크에 대 한 액세스 권한이 부여 됩니다.

- 정책에서 정책 원본 설정을 사용 하는지 여부를 확인 합니다. 이 설정을 통해 모든 액세스 요청에 대 한 소스를 쉽게 지정할 수 있습니다. 가능한 소스는 TS 게이트웨이 (터미널 서비스 게이트웨이), 원격 액세스 서버 (VPN 또는 전화 접속), DHCP 서버, 무선 액세스 지점 및 상태 등록 기관 서버입니다. 또는 공급 업체별 원본을 지정할 수 있습니다.

- 네트워크 정책을 적용 하기 위해 일치 해야 하는 조건을 결정 합니다.

- 네트워크 정책의 조건이 연결 요청에 의해 일치 하는 경우 적용 되는 설정을 결정 합니다.

- 기본 네트워크 정책을 사용할지, 수정 하거나, 삭제할지를 결정 합니다.

## <a name="plan-nps-accounting"></a>NPS 계정 계획

NPS는 사용자 인증 및 계정 요청과 같은 RADIUS 계정 데이터를 IAS 형식, 데이터베이스 호환 형식 및 Microsoft SQL Server 로깅의 세 가지 형식으로 기록 하는 기능을 제공 합니다. 

IAS 형식 및 데이터베이스 호환 형식 텍스트 파일 형식으로 로컬 NPS에 로그 파일을 만듭니다. 

SQL Server 로깅은 SQL Server 2000 또는 SQL Server 2005 XML 규격 데이터베이스에 기록할 수 있는 기능을 제공 하 고, RADIUS 계정을 확장 하 여 관계형 데이터베이스에 로깅할 수 있는 장점을 활용 합니다.

### <a name="key-steps"></a>주요 단계

NPS 계정 계획 중에 다음 단계를 사용할 수 있습니다.

- NPS 계정 데이터를 로그 파일 또는 SQL Server 데이터베이스에 저장할지 여부를 결정 합니다.

### <a name="nps-accounting-using-local-log-files"></a>로컬 로그 파일을 사용 하는 NPS 계정

사용자 인증 및 계정 요청을 로그 파일에 기록 하는 작업은 주로 연결 분석과 요금 청구를 위해 사용 되며, 다음의 악의적인 사용자의 활동을 추적 하는 방법을 제공 하는 보안 조사 도구로도 유용 합니다. 범위.

### <a name="key-steps"></a>주요 단계

로컬 로그 파일을 사용 하는 NPS 계정 계획 중에 다음 단계를 사용할 수 있습니다.

- NPS 로그 파일에 사용 하려는 텍스트 파일 형식을 결정 합니다.

- 로깅할 정보 유형을 선택 합니다. 계정 요청, 인증 요청 및 정기 상태를 기록할 수 있습니다.

- 로그 파일을 저장 하려는 하드 디스크 위치를 결정 합니다.

- 로그 파일 백업 솔루션을 설계 합니다. 로그 파일을 저장 하는 하드 디스크 위치는 데이터를 쉽게 백업할 수 있는 위치 여야 합니다. 또한 로그 파일이 저장 된 폴더에 대 한 ACL (액세스 제어 목록)을 구성 하 여 하드 디스크 위치를 보호 해야 합니다.

- 새 로그 파일을 만들려는 빈도를 결정 합니다. 파일 크기에 따라 로그 파일을 만들려면 NPS에서 새 로그 파일을 만들기 전에 허용 되는 최대 파일 크기를 확인 합니다.

- 하드 디스크에 저장 공간이 부족 한 경우 NPS에서 이전 로그 파일을 삭제할지 여부를 결정 합니다.

- 계정 데이터를 보고 보고서를 생성 하는 데 사용 하려는 응용 프로그램을 결정 합니다.

### <a name="nps-sql-server-logging"></a>NPS SQL Server 로깅

NPS SQL Server 로깅은 보고서 작성 및 데이터 분석을 위해 세션 상태 정보가 필요 하 고, 회계 데이터의 관리를 중앙 집중화 하 고 간소화 하는 데 사용 됩니다.

NPS는 SQL Server 로깅을 사용 하 여 하나 이상의 네트워크 액세스 서버에서 받은 사용자 인증 및 계정 요청을 Microsoft SQL Server Desktop Engine \(MSDE 2000\)를 실행 하는 컴퓨터의 데이터 원본 또는 SQL Server 2000 보다 이후 버전의 SQL Server에 기록할 수 있는 기능을 제공 합니다.

계정 데이터는 NPS에서 XML 형식으로 데이터베이스의 저장 프로시저로 전달 됩니다 .이는 구조적 쿼리 언어 \(SQL\) 및 XML \(SQLXML\)를 모두 지원 합니다. XML 규격 SQL Server 데이터베이스에 사용자 인증 및 계정 요청을 기록 하면 여러 NPSs에서 하나의 데이터 원본을 사용할 수 있습니다.

### <a name="key-steps"></a>주요 단계

Nps SQL Server 로깅을 사용 하 여 NPS 계정 계획 중에 다음 단계를 사용할 수 있습니다.

- 사용자 또는 조직의 다른 구성원이 SQL Server 2000 또는 SQL Server 2005 관계형 데이터베이스 개발 환경을 보유 하 고 있는지 확인 합니다. 이러한 제품을 사용 하 여 SQL Server 데이터베이스를 생성, 수정, 관리 및 관리 하는 방법을 이해 해야 합니다.

- SQL Server NPS 또는 원격 컴퓨터에 설치 되어 있는지 확인 합니다.

- SQL Server 데이터베이스에서 NPS 계정 데이터를 포함 하는 들어오는 XML 파일을 처리 하는 데 사용할 저장 프로시저를 디자인 합니다.

- SQL Server 데이터베이스 복제 구조와 흐름을 디자인 합니다.

- 계정 데이터를 보고 보고서를 생성 하는 데 사용 하려는 응용 프로그램을 결정 합니다.

- 모든 계정 요청에서 클래스 특성을 전송 하는 네트워크 액세스 서버를 사용 하도록 계획 합니다. 클래스 특성은 액세스 수락 메시지에서 RADIUS 클라이언트로 전송 되며, 계정 요청 메시지와 인증 세션의 상관 관계를 상호 연결 하는 데 유용 합니다. 클래스 특성을 계정 요청 메시지의 네트워크 액세스 서버에서 보내는 경우이를 사용 하 여 계정 및 인증 레코드를 일치 시킬 수 있습니다. 고유한 일련 번호, 서비스 다시 부팅 시간 및 서버 주소 특성의 조합은 서버에서 허용 하는 각 인증에 대 한 고유 id 여야 합니다.

- 중간 계정을 지 원하는 네트워크 액세스 서버를 사용 하도록 계획 합니다.

- 계정 설정 및 계정 해제 메시지를 보내는 네트워크 액세스 서버를 사용 하도록 계획 합니다.

- 계정 데이터의 저장 및 전달 기능을 지 원하는 네트워크 액세스 서버를 사용 하도록 계획 합니다. 네트워크 액세스 서버에서 NPS와 통신할 수 없는 경우이 기능을 지 원하는 네트워크 액세스 서버에서 계정 데이터를 저장할 수 있습니다. NPS를 사용할 수 있는 경우 네트워크 액세스 서버는 저장 된 레코드를 NPS에 전달 하 여이 기능을 제공 하지 않는 네트워크 액세스 서버 보다 높은 수준의 안정성을 제공 합니다.

- 네트워크 정책에서 항상 계정-중간 간격 특성을 구성할 계획입니다. 계정-중간 간격 특성은 네트워크 액세스 서버에서 보내는 각 중간 업데이트 사이의 간격 (초)을 설정 합니다. RFC 2869에 따르면 계정-중간 간격 특성의 값은 60 초 또는 1 분 보다 작을 수 없으며 600 초 또는 10 분 보다 작을 수 없습니다. 자세한 내용은 RFC 2869, "RADIUS 확장"을 참조 하세요.

- NPSs에서 정기 상태 로깅이 사용 되는지 확인 합니다.

