---
title: 액세스 권한
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버에 대 한 네트워크 정책 액세스 권한의 개요를 제공합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d6d1ca5e-bde0-4509-9e14-dc3fa9ff447e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cdec41fb7925061bb8c8402634e1d9b1625bf301
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849494"
---
# <a name="access-permission"></a>액세스 권한

>적용 대상: Windows Server (반기 채널), Windows Server 2016

액세스 권한을 구성 합니다 **개요** 각 네트워크 정책에서 네트워크 정책 (NPS 서버)의 탭 합니다. 

이 설정을 사용 하면 허용 하거나 연결 요청 조건 및 네트워크 정책의 제약 조건과 일치 하는 경우 사용자에 게 액세스를 거부 하는 정책을 구성할 수 있습니다. 

액세스 권한 설정의 영향:

- **액세스 권한을 부여**합니다. 액세스 연결 요청 조건 및 정책에 구성 된 제약 조건과 일치 하는 경우 권한이 부여 됩니다.
- **액세스 거부**합니다. 연결 요청 조건 및 정책에 구성 된 제약 조건과 일치 하는 경우 액세스가 거부 되었습니다.

액세스 권한 부여 되거나 거부 또한 각 사용자 계정 전화 접속 속성의 구성을 기반으로 합니다.

>[!NOTE]
>사용자 계정 및 전화 접속 속성 등 해당 속성 중 하나는 Active Directory 사용자 및 컴퓨터 또는 로컬 사용자 및 그룹 Microsoft Management Console에서 구성 됩니다 \(MMC\) 스냅인을 해야 하는지 여부에 따라 Active Directory&reg; Domain Services (AD DS) 설치 합니다.

사용자 계정 설정 **네트워크 액세스 권한**사용자 계정 전화 접속 속성에서 구성 된, 재정의 네트워크 정책 액세스 권한을 설정 합니다. 로 사용자 계정 네트워크 액세스 권한이 설정 된 경우는 **NPS 네트워크 정책을 통해 액세스를 제어할** 옵션인 네트워크 정책 액세스 권한 설정 사용자 권한이 부여 되었거나 액세스가 거부 여부를 결정 합니다.

>[!NOTE]
>Windows Server 2016에서 기본값인 **네트워크 액세스 권한** AD DS 사용자 계정 전화 접속 속성의 **NPS 네트워크 정책을 통해 액세스를 제어할**합니다.

NPS에 구성 된 네트워크 정책에 대 한 연결 요청으로 계산 되는 경우 다음 작업을 수행 합니다.

- 첫 번째 정책의 조건과 일치 하지 않는 경우에 NPS 다음 정책을 평가 및 일치 하는 또는 일치 하는 모든 정책을 평가 될 때까지이 프로세스를 계속 합니다.
- 조건 및 정책의 제약 조건과 일치 하는 경우 NPS 부여 하거나 정책에 대 한 액세스 권한 설정의 값에 따라 액세스를 거부 합니다.
- 조건 일치 하지만 정책에서 제약 조건에 일치 하지 않는 경우 NPS 연결 요청을 거부 합니다.
- 모든 정책의 조건과 일치 하지 않는 경우 NPS 연결 요청을 거부 합니다.

## <a name="ignore-user-account-dial-in-properties"></a>사용자 계정 전화 접속 속성 무시

하거나 선택 취소 하 여 사용자 계정 전화 접속 속성을 무시 하도록 NPS 네트워크 정책을 구성할 수 있습니다 합니다 **사용자 계정 전화 접속 속성을 무시** 확인란 합니다 **개요** 네트워크 탭 정책입니다. 

일반적으로 NPS 연결 요청 권한 부여를 수행 하는 경우 여기서 값을 설정 하는 네트워크 액세스 권한 영향을 줄 수는 사용자가 네트워크에 연결할 권한이 있는지 여부를 사용자 계정에 전화 접속 속성을 확인 합니다. 권한 부여 하는 동안 사용자 계정 전화 접속 속성을 무시 하도록 NPS를 구성할 때 네트워크 정책 설정은 사용자가 네트워크에 대 한 액세스를 부여 되었는지 여부를 결정 합니다.

사용자 계정 전화 접속 속성 다음을 포함 합니다.

- 네트워크 액세스 권한
- 호출자 ID
- 콜백 옵션
- 고정 IP 주소
- 고정 경로

여러 유형의 NPS 인증 및 권한 부여 제공 하는 연결을 지원 하려면 사용자 계정 전화 접속 속성의 처리를 사용 하지 않도록 설정 해야 할 수도 있습니다. 이 특정 전화 접속 속성이 필요 하지 않은 시나리오를 지원 하기 위해 수행할 수 있습니다.

네트워크 액세스 서버에 전화를 거는 클라이언트에 호출자 ID, 콜백, 고정 IP 주소 및 고정 경로 속성은 디자인 하는 예를 들어 \(NAS\), 무선 액세스 지점에 연결 하는 클라이언트용 없습니다. NPS에서 RADIUS 메시지에 이러한 설정을 수신 하는 무선 액세스 지점 못할를 처리 하는 데 연결을 끊을 수 무선 클라이언트를 유발할 수 있습니다.

NPS 인증 및 권한 부여에 전화 걸기 및 무선 액세스 지점을 통해 조직 네트워크에 액세스할 사용자에 게 제공 하는 경우에 두 전화 접속 연결을 지원 하려면 전화 접속 속성을 구성 해야 \(여 전화 접속 속성 설정\) 또는 무선 연결 \(전화 접속 속성을 설정 하지 않으면\)합니다.

NPS를 사용 하 여 전화 접속 속성 일부 시나리오에서는 사용자 계정에 대 한 처리를 사용 하도록 설정 하려면 \(전화 접속 등\) 전화 접속 속성 다른 시나리오에서 처리 안 함으로 \(802.1 X 무선 같은 및 스위치 인증\)합니다.

사용할 수도 있습니다 **사용자 계정 전화 접속 속성을 무시** 그룹 및 네트워크 정책에 대 한 액세스 권한 설정을 통해 네트워크 액세스 제어를 관리할 수 있습니다. 선택 하는 경우는 **사용자 계정 전화 접속 속성을 무시** 확인란을 사용자 계정에 네트워크 액세스 권한을 무시 됩니다.

이 구성만 단점은 추가 사용자 계정 전화 접속 속성 호출자 ID, 콜백, 고정 IP 주소 및 고정 경로 사용할 수 없다는 것입니다.

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.