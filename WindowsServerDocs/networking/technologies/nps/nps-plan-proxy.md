---
title: RADIUS 프록시로 작동하는 NPS 계획
description: 이 항목에서는 네트워크 정책 서버 RADIUS 프록시 배포 Windows Server 2016에서 계획에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ca77d64a-065b-4bf2-8252-3e75f71b7734
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 83fbe57ee62480439190dcc53428e02a4f8e6897
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829564"
---
# <a name="plan-nps-as-a-radius-proxy"></a>RADIUS 프록시로 작동하는 NPS 계획

>적용 대상: Windows Server (반기 채널), Windows Server 2016

네트워크 정책 (NPS 서버)는 원격 인증 전화 접속 사용자 서비스를 배포 하는 경우 \(RADIUS\) 같은 네트워크 액세스 서버 또는 다른 RADIUS 프록시가 RADIUS 클라이언트에서 연결 요청을 수신 하는 프록시, NPS 및 NPS 또는 다른 RADIUS 서버를 실행 하는 서버에 이러한 연결 요청을 전달 합니다. RADIUS 배포를 간소화 하기 위해 다음 계획 지침을 사용할 수 있습니다.

다음 계획 지침에는 NPS를 RADIUS 서버로 배포 하려는 경우 포함 되지 않습니다. NPS를 RADIUS 서버로 배포 하면 NPS 인증, 권한 부여 및 계정을 로컬 도메인을 신뢰 하는 도메인 및 로컬 도메인에 대 한 연결 요청을 수행 합니다.

NPS를 RADIUS 프록시로 네트워크에 배포 하기 전에 배포를 계획 하려면 다음 지침을 따르세요.

- NPS 구성을 계획 합니다.

- RADIUS 클라이언트를 계획 합니다.

- 원격 RADIUS 서버 그룹을 계획 합니다.

- 메시지 전달에 대 한 특성 조작 규칙을 계획 합니다.

- 연결 요청 정책을 계획 합니다.

- NPS 계정 관리를 계획 합니다.

## <a name="plan-nps-configuration"></a>NPS 구성 계획

RADIUS 프록시로 NPS를 사용 하는 경우 NPS 연결 요청을 NPS 또는 처리를 위해 다른 RADIUS 서버로 전달 합니다. 이 때문에 도메인 구성원 NPS 프록시는 관련이 없습니다. 프록시는 Active Directory Domain Services에 등록 하지 않아도 \(AD DS\) 사용자 계정 전화 접속 속성에 대 한 액세스 되지 않아도 되기 때문입니다. 또한 프록시 연결 요청에 대 한 권한 부여를 수행 하지 않으므로 NPS 프록시에서 네트워크 정책을 구성할 필요가 없습니다. NPS 프록시 도메인 구성원 이거나 없는 도메인 구성원 자격을 사용 하 여 독립 실행형 서버 수 있습니다.

NPS는 RADIUS 프로토콜을 사용 하 여 네트워크 액세스 서버 라고도 하는 RADIUS 클라이언트와 통신 하도록 구성 되어야 합니다. 또한 구성할 수 있습니다. 있습니다 이벤트 유형을 NPS에서 기록 하는 이벤트 로그에 서버에 대 한 설명을 입력할 수 있습니다.

### <a name="key-steps"></a>주요 단계

NPS 프록시 구성에 대 한 계획 하는 동안 다음 단계를 사용할 수 있습니다.

- RADIUS 클라이언트에서 RADIUS 메시지를 수신 하 고 원격 RADIUS 서버 그룹의 구성원에 게 RADIUS 메시지를 보낼 NPS 프록시는 RADIUS 포트를 결정 합니다. 기본 사용자 데이터 그램 프로토콜 (UDP) 포트가 RADIUS 인증 메시지 및 UDP 포트 RADIUS 계정 메시지 1646과 1813 1645와 1812입니다.

- 에 여러 네트워크 어댑터를 사용 하 여 NPS 프록시가 구성 되어 있는 경우 원하는 RADIUS 트래픽을 허용 해야 하는 어댑터를 확인 합니다.

- 이벤트 로그에 기록 하기 위해 NPS를 원하는 이벤트 유형을 결정 합니다. 거부 된 연결 요청, 성공적으로 연결 요청 중 하나 또는 둘 다를 기록할 수 있습니다.

- 둘 이상의 NPS 프록시를 배포 하는 여부를 결정 합니다. 내결함성을 제공 하려면 두 개 이상의 NPS 프록시를 사용 합니다. 주 RADIUS 프록시로 하나 NPS 프록시를 사용 하 고 다른 백업으로 사용 됩니다. 그런 다음 각 RADIUS 클라이언트 둘 다 NPS 프록시 구성 됩니다. 기본 NPS 프록시를 사용할 수 없는 경우 RADIUS 클라이언트는 다음 액세스 요청 메시지 대체 NPS 프록시를 보냅니다.

- 하나의 NPS 프록시 구성을 관리 오버 헤드에 저장 하 고 잘못 된 구성 서버를 방지 하기 위해 다른 NPS 프록시에 복사 하는 데 스크립트를 계획 합니다. NPS는 다른 NPS 프록시에 가져오기에 대 한 NPS 프록시 구성의 일부나 전부를 복사할 수 있도록 하는 Netsh 명령을 제공 합니다. 명령 프롬프트에서 Netsh 수동으로 실행할 수 있습니다. 그러나 스크립트에 명령 시퀀스를 저장 하면 프록시 구성을 변경 하려는 경우 나중에 스크립트를 실행할 수 있습니다.

## <a name="plan-radius-clients"></a>RADIUS 클라이언트를 계획 합니다.

RADIUS 클라이언트는 네트워크 액세스 서버를 같은 무선 액세스 지점, 가상 사설망 \(VPN\) 서버에 802.1 X 가능 스위치 및 전화 접속 서버. 연결 RADIUS 서버에 요청 메시지를 전달 하는 RADIUS 프록시를 RADIUS 클라이언트 이기도 합니다. RFC 2865에 설명 된 대로 모든 네트워크 액세스 서버 및 RADIUS 프록시가 RADIUS 프로토콜을 준수 하는 NPS 지원 "원격 인증 전화 접속 사용자 서비스 \(RADIUS\)," 및 RFC 2866 "RADIUS 계정입니다."

또한 무선 액세스 지점 및 스위치 802.1 X 인증을 수행할 수 여야 합니다. Extensible Authentication Protocol (EAP) 또는 PEAP Protected Extensible Authentication Protocol ()를 배포 하려는 경우 액세스 지점 및 스위치는 EAP의 사용을 지원 해야 합니다.

무선 액세스 지점에 대 한 PPP 연결에 대 한 기본 상호 운용성을 테스트 하려면 액세스 지점 및 인증 프로토콜이 PAP (암호)를 사용 하는 액세스 클라이언트를 구성 합니다. PEAP 등의 추가 PPP 기반 인증 프로토콜을를 사용 하 여 네트워크 액세스에 사용 하려는 것을 테스트 합니다.

### <a name="key-steps"></a>주요 단계

RADIUS 클라이언트에 대 한 계획 하는 동안 다음 단계를 사용할 수 있습니다.

- 문서 공급 업체별 특성 (Vsa) NPS에 구성 해야 합니다. Nas에 Vsa를 요구 하는 경우 NPS에서 네트워크 정책을 구성할 때 나중에 사용할 VSA 정보를 기록 합니다.

- 모든 장치의 구성을 단순화 하기 위해 RADIUS 클라이언트와 NPS 프록시 IP 주소를 문서화 합니다. RADIUS 클라이언트를 배포할 때 인증 서버와 입력 한 NPS 프록시 IP 주소를 사용 하 여 RADIUS 프로토콜을 사용 하도록 구성 해야 합니다. 및 NPS 스냅인에 RADIUS 클라이언트 IP 주소를 입력 해야 RADIUS 클라이언트와 통신 하는 NPS를 구성한 경우.

- NPS 스냅인에서 RADIUS 클라이언트에 구성에 대 한 공유 암호를 만듭니다. 공유 암호 또는 암호와 NPS에서 RADIUS 클라이언트를 구성 하는 동안 NPS 스냅인에 입력 하는 RADIUS 클라이언트를 구성 해야 합니다.

## <a name="plan-remote-radius-server-groups"></a>원격 RADIUS 서버 그룹 계획

NPS 프록시에서 원격 RADIUS 서버 그룹을 구성 하는 경우에 일부 또는 모든 연결에서 네트워크 액세스 서버와 NPS 프록시 또는 다른 RADIUS 프록시에서 수신한 요청 메시지를 보낼 위치를 NPS 프록시 게 됩니다.

NPS를 RADIUS 프록시로 연결 전달할 하나에 요청 하거나 더 많은 원격 RADIUS 서버 그룹 및 각 그룹에서 하나 이상의 RADIUS 서버를 포함할 수 있습니다에 사용할 수 있습니다. 여러 그룹에 메시지를 전달 하도록 NPS 프록시를 하려는 경우에 그룹당 한 연결 요청 정책을 구성 합니다. 연결 요청 정책을 NPS 프록시 정책에서 지정한 원격 RADIUS 서버 그룹에 보낼 메시지를 알려주는 특성 조작 규칙 같은 추가 정보를 포함 합니다.

NPS 용 Netsh 명령을 사용 하 여, 직접를 NPS 스냅인에서 원격 RADIUS 서버 그룹에서 그룹을 구성 하 여 또는 새 연결 요청 정책 마법사를 실행 하 여 원격 RADIUS 서버 그룹을 구성할 수 있습니다.

### <a name="key-steps"></a>주요 단계

원격 RADIUS 서버 그룹에 대 한 계획 하는 동안 다음 단계를 사용할 수 있습니다.

- NPS 연결 요청을 전달 하도록 프록시 하려는 RADIUS 서버를 포함 하는 도메인을 확인 합니다. 이러한 도메인을 배포한 RADIUS 클라이언트를 통해 네트워크에 연결 하는 사용자 계정이 포함 됩니다.

- 새 RADIUS 서버는 RADIUS 배포 되지 않은 이미 도메인에 추가 해야 하는지 여부를 결정 합니다.

- 원격 RADIUS 서버 그룹에 추가 하려는 RADIUS 서버의 IP 주소를 문서화 합니다.

- 만들어야 하는 방법을 많은 원격 RADIUS 서버 그룹을 결정 합니다. 경우에 따라 도메인당 하나의 원격 RADIUS 서버 그룹을 만들고 다음 도메인에 대 한 RADIUS 서버 그룹 추가에 적합 합니다. 그러나 많은 양의 리소스를 하나의 도메인에 많은 수의 사용자 계정 사용 하 여 사용자를 포함 하 여 많은 수의 RADIUS 서버, 도메인 및 많은 도메인 컨트롤러에가 경우 있을 수 있습니다. 또는 도메인 넓은 지역을 일으키는 네트워크 액세스 서버 및 RADIUS 서버는 서로 멀리 떨어진 위치에 포함 될 수 있습니다. 이러한 및 가능한 경우 다른 경우에서는 도메인당 여러 개의 원격 RADIUS 서버 그룹을 만들 수 있습니다.

- NPS 프록시 및 원격 RADIUS 서버 구성에 대 한 공유 암호를 만듭니다.

## <a name="plan-attribute-manipulation-rules-for-message-forwarding"></a>메시지 전달에 대 한 특성 조작 규칙 계획

연결 요청 정책에서 구성 되는 특성 조작 규칙을 사용 하면 특정 원격 RADIUS 서버 그룹에 전달 하려는 액세스 요청 메시지를 식별 하 수 있습니다.

특성 조작 규칙을 사용 하지 않고 하나의 원격 RADIUS 서버 그룹에 모든 연결 요청을 전달 하도록 NPS를 구성할 수 있습니다.

그러나 연결 요청을 전달 하려면 둘 이상의 위치에 있는 경우 해야 각 위치에 대 한 연결 요청 정책을 만든 다음 메시지를 전달 하려는 원격 RADIUS 서버 그룹을 사용 하 여 정책을 구성 및 전달할 메시지를 NPS에 알려주는 특성 조작 규칙입니다.

다음과 같은 특성에 대 한 규칙을 만들 수 있습니다.

- 호출-스테이션-id입니다. 네트워크 액세스 서버 (NAS)의 전화 번호입니다. 이 특성의 값은 문자열. 지역 번호를 지정할 패턴 일치 구문을 사용할 수 있습니다.

- 호출 스테이션 id 호출자가 사용할 전화 번호입니다. 이 특성의 값은 문자열. 지역 번호를 지정할 패턴 일치 구문을 사용할 수 있습니다.

- 사용자 이름입니다. 가 제공 하는 액세스 클라이언트와 RADIUS 액세스 요청 메시지에 NAS가 포함 되어 있는 사용자 이름입니다. 이 특성의 값에는 일반적으로 사용자 계정 이름 및 영역 이름을 포함 하는 문자열입니다.

올바르게 대체 연결 요청의 사용자 이름에 영역 이름을 변환, 적절 한 연결 요청 정책에서 사용자 이름 특성에 대 한 특성 조작 규칙 구성 해야 합니다.

### <a name="key-steps"></a>주요 단계

조작 규칙 특성에 대 한 계획 하는 동안 다음 단계를 사용할 수 있습니다.

- RADIUS 서버에 메시지를 전달 하는 논리 경로 확인 하려면 원격 RADIUS 서버에 프록시를 통해 NAS에서 메시지 라우팅을 계획 합니다.

- 각 연결 요청 정책에 사용 하려는 하나 이상의 특성을 결정 합니다.

- 각 연결 요청 정책에 대해 사용 하려는 특성 조작 규칙을 문서화 하 고 메시지가 전달 되는 원격 RADIUS 서버 그룹 규칙과 일치 합니다.

## <a name="plan-connection-request-policies"></a>연결 요청 정책 계획

NPS를 RADIUS 서버로 사용할 기본 연결 요청 정책 구성 됩니다. 추가 연결 요청 정책은 특정 한 조건을 정의 하 원격 RADIUS 서버 그룹에 전달 하 고 고급 특성을 지정할 수 있는 메시지를 NPS에 알려주는 조작 규칙 특성을 만들어 사용할 수 있습니다. 새 연결 요청 정책 마법사를 사용 하 여 공용 또는 사용자 지정 연결 요청 정책을 만듭니다.

### <a name="key-steps"></a>주요 단계

연결 요청 정책에 대 한 계획 하는 동안 다음 단계를 사용할 수 있습니다.

- RADIUS 프록시로 NPS 해당 함수를 실행 하는 각 서버에서 기본 연결 요청 정책을 삭제 합니다.

- 추가 조건 및 원격 RADIUS 서버 그룹 및 정책에 대 한 계획 특성 조작 규칙을 사용 하 여이 정보를 결합 하는 각 정책에 대해 필요한 설정을 계획 합니다.

- 모든 NPS 프록시에 일반적인 연결 요청 정책을 배포 하는 계획을 디자인 합니다. 정책을 여러 NPS 프록시에 공통적으로 적용 한 NPS에서 만들고 사용 하 여 NPS 용 Netsh 명령은 다른 모든 프록시에 연결 요청 정책 및 서버 구성을 가져올 수 있습니다.

## <a name="plan-nps-accounting"></a>NPS 계정 계획

NPS를 RADIUS 프록시로 구성 하는 경우 RADIUS 계정 NPS 형식 로그 파일, 데이터베이스 호환 형식으로 로그 파일 또는 NPS SQL Server를 사용 하 여 로깅 수행 하도록 구성할 수 있습니다.

또한 이러한 로깅 형식 중 하나를 사용 하 여 계정 관리를 수행 하는 원격 RADIUS 서버 그룹에 계정 메시지를 전달할 수 있습니다.

### <a name="key-steps"></a>주요 단계

NPS 계정에 대 한 계획 하는 동안 다음 단계를 사용할 수 있습니다.

- 계정 서비스를 수행 하거나 계정에 대 한 원격 RADIUS 서버 그룹에 계정 메시지를 전달 하도록 NPS 프록시를 사용할지를 결정 합니다.

- 다른 서버로 계정 메시지를 전달 하려는 경우를 고려 하는 로컬 NPS 프록시를 사용 하지 않도록 설정 하려고 합니다.

- 다른 서버에 대 한 계정 메시지를 전달 하려는 경우 연결 요청 정책 구성 단계를 계획 합니다. NPS 프록시에 대 한 로컬 계정, 사용 하지 않으면에서 해당 프록시를 구성 하는 각 연결 요청 정책 회계 메시지 전달을 사용 하도록 설정 하 고 올바르게 구성 되어 있어야 합니다.

- 사용 하려는 로깅 형식을 결정 합니다. IAS 형식 로그 파일, 데이터베이스 호환 형식으로 로그 파일 또는 NPS SQL Server 로깅.

부하 분산을 구성할 nps를 RADIUS 프록시로, 참조 [NPS 프록시 서버 부하 분산](nps-manage-proxy-lb.md)합니다.
