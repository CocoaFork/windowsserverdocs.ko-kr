---
title: 기능 제거 또는 Windows Server 버전 1903부터 대체 계획
description: 다음은 기능의 목록이 및 Windows Server 버전 1903에에서는 제품에서 제거 되었거나 기능 릴리스 또는 후속 릴리스에서 잠재적인 대체에 대 한 것으로 간주 하기 시작 합니다. 상용 환경에서 운영 체제를 업데이트하는 IT 전문가가 참조하시면 유용합니다.
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
ms.date: 05/21/2019
author: jasongerend
ms.author: jgerend
manager: daveba
ms.openlocfilehash: e2f51af55ba7005cb20d8a1c22f6ba9edc20c704
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65983423"
---
# <a name="features-removed-or-planned-for-replacement-starting-with-windows-server-version-1903"></a>기능 제거 또는 Windows Server 버전 1903부터 대체 계획

>적용 대상: Windows Server 버전 1903

다음은 기능의 목록이 및 Windows Server 버전 1903에에서는 제품에서 제거 되었거나 기능 릴리스 또는 후속 릴리스에서 잠재적인 대체에 대 한 것으로 간주 하기 시작 합니다. 상용 환경에서 운영 체제를 업데이트하는 IT 전문가가 참조하시면 유용합니다. **이 목록은 후속 릴리스에서 변경 될 수 있습니다 이며 모든 영향을 받는 기능 또는 기능을 포함 하지 않을 수 있습니다.**

도 참조 하세요 [기능 제거 또는 교체를 시작 하는 Windows Server 2019에 대해 계획 된](removed-features-19.md)합니다.

## <a name="features-were-no-longer-developing"></a>더 이상 개발하지 않는 기능

이러한 기능을 더 이상 적극적으로 개발 하 고 향후 업데이트에서이 제거할 수 없습니다. 일부 기능이 다른 기능으로 대체되었으며 일부 기능은 이제 다른 소스에서 사용할 수 있습니다. 

이러한 기능에 대한 교체 제안에 대한 피드백이 있는 경우 [피드백 허브 앱](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)을 사용할 수 있습니다. 

| 기능 | 대신 사용할 수 있습니다. |
|-----------|---------------------|
|Wi-fi WEP 및 TKIP (**새**)| 이전 WEP 및 TKIP 암호화를 사용 하 여 Wi-fi 네트워크 WPA2 등 WPA3 AES를 사용 하는 것으로 보호 되지 않습니다. Windows 10, 버전, 1903 WEP 또는 TKIP 네트워크 연결 표시 됩니다는 네트워크 보안 되지 않은 경고 메시지가 있지만 메시지가 없는 Windows Server 버전 1903에 표시 됩니다. 향후 릴리스에서 이러한 이전 암호를 사용 하 여 Wi-fi 네트워크에 대 한 연결을 사용할 수 없습니다. WEP 및 TKIP의 보안 위험에 대 한 자세한 내용은 참조 [블로그 게시물](https://go.microsoft.com/fwlink/p/?linkid=2008426)합니다.|
|XDDM 기반 원격 디스플레이 드라이버 (**새**)|이 릴리스부터 원격 데스크톱 서비스를 Windows 디스플레이 드라이버 모델 (WDDM)를 사용 하 여 단일 세션 원격 데스크톱에 대 한 간접 디스플레이 드라이버 (IDD)를 기반 합니다. Windows 2000 디스플레이 드라이버 모델 (XDDM) 기반 원격 디스플레이 드라이버 지원은 이후 릴리스에서 제거 됩니다. XDDM 기반 원격 디스플레이 드라이버를 사용 하는 독립 소프트웨어 공급 업체는 WDDM 드라이버 모델으로의 마이그레이션을 계획 해야 합니다. 표시 하는 원격을 구현 하는 방법은 간접 디스플레이 드라이버 Isv에 게 연결할 수 [ rdsdev@microsoft.com ](mailto:rdsdev@microsoft.com)합니다.|
|UCS 로그 컬렉션 도구 (**새**)|그럼에도 불구 하 고 명시적으로 Windows Server를 사용 하 여 사용 하기 위한 하는 동안에 UCS 로그 컬렉션 도구 Windows 10 피드백 허브 교체 되 고 있습니다.|
|Hyper-v에서 키 저장소 드라이브|Hyper-v에서 키 저장소 드라이브 기능이 더 이상 작업 중입니다. 1 세대 Vm을 사용 하는 경우 체크 아웃 [세대 1 VM 가상화 보안](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/generation-1-virtual-machine-security-settings-for-hyper-v) 옵션 앞에 대 한 정보에 대 한 합니다. 만드는 경우 새 Vm 보다 안전한 솔루션에 대 한 TPM 장치를 사용 하 여 2 세대 가상 컴퓨터를 사용 합니다. |
|신뢰할 수 있는 플랫폼 모듈 (TPM) 관리 콘솔|TPM 관리 콘솔에서 이전에 제공 되는 정보에 제공 됩니다. 합니다 [ **장치 보안** ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/wdsc-device-security) 페이지를 [Windows Defender 보안 센터](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/windows-defender-security-center)합니다.|
|호스트 보호자 서비스에 대 한 Active Directory 증명 모드|호스트 보호자 서비스에 대 한 Active Directory 증명 모드를 더 이상 개발 하는 것-대신 새 증명 모드를 추가 했습니다 [호스트 키 증명](../security/guarded-fabric-shielded-vm/guarded-fabric-create-host-key.md), 훨씬 더 간단 하 고 동일 하 게 Active Directory 기반과 호환 되는 증명 합니다.  이 새로운 모드는 설치 환경, 간편해 진 관리 및 Active Directory 증명 보다 더 적은 인프라 종속성을 사용 하 여 동일한 기능을 제공 합니다. 호스트 키 증명 필요한 어떤 Active Directory 증명 이외의 추가 하드웨어 요구 사항이 없습니다 있으므로 모든 기존 시스템에 새 모드와 호환 상태로 유지 됩니다. 참조 [보호 된 호스트 배포](../security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md) 증명 옵션에 대 한 자세한 내용은 합니다.|
|OneSync 서비스|OneSync 서비스 메일, 일정 및 사용자 앱에 대 한 데이터를 동기화합니다. 동일한 동기화를 제공 하는 Outlook 앱에 동기화 엔진을 추가 했습니다.|
|원격 차등 압축 API 지원|네트워크를 통해 전송 되는 데이터 양을 최소화 하는 압축 기술을 사용 하 여 원격 소스와 데이터 동기화를 사용 하는 원격 차등 압축 API 지원 합니다. 이 지원은 Microsoft 제품에서 현재 사용 되지 않습니다.|
|WFP 간단한 필터 스위치 확장|WFP 간단한 필터 스위치 확장에는 개발자가 만들 수 [Hyper-v 가상 스위치 확장을 필터링 하는 단순한 네트워크 패킷](https://docs.microsoft.com/en-us/windows-hardware/drivers/network/using-virtual-switch-filtering)합니다. 전체 필터링 확장 프로그램을 만들어 동일한 기능을 얻을 수 있습니다. 따라서 우리가에서는 제거할이 확장 나중에입니다.|
