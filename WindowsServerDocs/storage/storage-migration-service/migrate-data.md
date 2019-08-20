---
title: 저장소 마이그레이션 서비스를 사용 하 여 파일 서버 마이그레이션
description: 검색 엔진 결과의 항목에 대 한 간략 한 설명
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 02/13/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: 7cec2a9c805208baceff8a8afe22a20fd2859edd
ms.sourcegitcommit: e2b565ce85a97c0c51f6dfe7041f875a265b35dd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69584843"
---
# <a name="use-storage-migration-service-to-migrate-a-server"></a>Storage Migration Service를 사용 하 여 서버 마이그레이션

이 항목에서는 [저장소 마이그레이션 서비스](overview.md) 및 Windows 관리 센터를 사용 하 여 해당 파일 및 구성을 비롯 한 서버를 다른 서버로 마이그레이션하는 방법에 대해 설명 합니다. 서비스를 설치 하 고 필요한 방화벽 포트를 연 후에는 서버를 인벤토리 하 고 데이터를 전송 하 고 새 서버로 이동 하는 과정을 단계별로 진행 합니다.

## <a name="step-0-install-storage-migration-service-and-check-firewall-ports"></a>0단계: Storage 마이그레이션 서비스 설치 및 방화벽 포트 확인

시작 하기 전에 저장소 마이그레이션 서비스를 설치 하 고 필요한 방화벽 포트가 열려 있는지 확인 합니다.

1. [저장소 마이그레이션 서비스 요구 사항을](overview.md#requirements) 확인 하 고 PC 또는 관리 서버에 [Windows 관리 센터](../../manage/windows-admin-center/understand/windows-admin-center.md) 를 설치 합니다 (아직 설치 하지 않은 경우).
2. Windows 관리 센터에서 Windows Server 2019를 실행 하는 orchestrator 서버에 연결 합니다. <br>저장소 마이그레이션 서비스를 설치 하 고 마이그레이션을 관리 하는 데 사용 하는 서버입니다. 서버를 하나만 마이그레이션하는 경우에는 Windows Server 2019를 실행 하는 동안 대상 서버를 사용할 수 있습니다. 다중 서버 마이그레이션에는 별도의 오케스트레이션 서버를 사용 하는 것이 좋습니다.
1. **서버 관리자** (Windows 관리 센터) > **storage migration service** 로 이동 하 고 **설치** 를 선택 하 여 저장소 마이그레이션 서비스와 필수 구성 요소 (그림 1에 표시 됨)를 설치 합니다.
    ![설치 단추](media/migrate/install.png) **를 표시 하는 Storage Migration Service 페이지의 스크린샷 그림 1: 저장소 마이그레이션 서비스 설치 중**
1. Windows Server 2019를 실행 하는 모든 대상 서버에 저장소 마이그레이션 서비스 프록시를 설치 합니다. 그러면 대상 서버에 설치 될 때 전송 속도가 두 배가 됩니다. <br>이렇게 하려면 Windows 관리 센터에서 대상 서버에 연결한 다음 **서버 관리자** (Windows 관리 센터) > **역할 및 기능**으로 이동 하 고 **저장소 마이그레이션 서비스 프록시**를 선택한 다음 **설치**를 선택 합니다.
1. 모든 원본 서버와 Windows Server 2012 R2 또는 Windows Server 2016를 실행 하는 대상 서버에서 각 서버에 연결 하 고 **서버 관리자** (Windows 관리 센터) > **방화벽**  >   **으로 이동 합니다. 들어오는 규칙**을 선택한 후 다음 규칙을 사용 하도록 설정 했는지 확인 합니다.
    - 파일 및 프린터 공유(SMB-In)
    - Netlogon 서비스 (NP-IN)
    - WMI(Windows Management Instrumentation) (DCOM-IN)
    - WMI(Windows Management Instrumentation)(WMI-In)

   > [!NOTE]
   > 타사 방화벽을 사용 하는 경우 열 인바운드 포트 범위는 TCP/445 (SMB), TCP/135 (RPC/DCOM 엔드포인트 매퍼) 및 TCP 1025-65535 (RPC/DCOM 임시 포트)입니다. Storage Migration service 포트는 Orchestrator (TCP/28940) 및 TCP/28941 (프록시)입니다.

1. Orchestrator 서버를 사용 하 여 마이그레이션을 관리 하 고 전송 하는 데이터에 대 한 로그 나 이벤트를 다운로드 하려는 경우 해당 서버 에서도 파일 및 프린터 공유 (SMB In) 방화벽 규칙이 사용 되는지 확인 합니다.

## <a name="step-1-create-a-job-and-inventory-your-servers-to-figure-out-what-to-migrate"></a>1단계: 작업을 만들고 서버를 인벤토리 하 여 마이그레이션할 항목을 파악 합니다.

이 단계에서는 마이그레이션할 서버를 지정한 다음 해당 서버를 검색 하 여 파일 및 구성에 대 한 정보를 수집 합니다.

1. **새 작업**을 선택 하 고 작업 이름을 지정한 다음 **확인**을 선택 합니다.
1. **자격 증명 입력** 페이지에서 마이그레이션하려는 서버에서 작동 하는 관리자 자격 증명을 입력 하 고 **다음**을 선택 합니다.
1. **장치 추가**를 선택 하 고 원본 서버 이름을 입력 한 다음 **확인**을 선택 합니다. <br>인벤토리에 추가할 다른 서버에 대해이를 반복 합니다.
1. **검색 시작**을 선택 합니다.<br>검색이 완료 되 면를 표시 하는 페이지를 업데이트 합니다.
    ![](media/migrate/inventory.png) 스캔할**준비가 된 서버를 보여 주는 스크린샷 그림 2: 서버 인벤토리**
1. 각 서버를 선택 하 여 인벤토리에 포함 된 공유, 구성, 네트워크 어댑터 및 볼륨을 검토 합니다. <br><br>Storage Migration Service는 Windows 작업에 방해가 될 수 있는 파일 또는 폴더를 전송 하지 않으므로,이 릴리스에서는 Windows 시스템 폴더에 있는 모든 공유에 대 한 경고를 볼 수 있습니다. 전송 단계에서 이러한 공유를 건너뛰어야 합니다. 자세한 내용은 [전송에서 제외 되는 파일 및 폴더](faq.md#what-files-and-folders-are-excluded-from-transfers)를 참조 하세요.
1. **다음** 을 선택 하 여 데이터 전송으로 이동 합니다.

## <a name="step-2-transfer-data-from-your-old-servers-to-the-destination-servers"></a>2단계: 이전 서버에서 대상 서버로 데이터 전송

이 단계에서는 대상 서버에서 데이터를 보관할 위치를 지정한 후 데이터를 전송 합니다.

1. **데이터** > 전송**자격 증명을 입력** 하십시오. 페이지에서 마이그레이션하려는 대상 서버에서 작동 하는 관리자 자격 증명을 입력 하 고 다음을 선택 합니다.
2. **대상 장치 및 매핑 추가** 페이지에서 첫 번째 원본 서버가 나열 됩니다. 마이그레이션할 서버의 이름을 입력 하 고 **장치 검색**을 선택 합니다.
3. 원본 볼륨을 대상 볼륨에 매핑하고, 전송 하지 않으려는 모든 공유에 대 한 **포함** 확인란의 선택을 취소 하 고 (Windows 시스템 폴더에 있는 모든 관리 공유 포함) **다음**을 선택 합니다.
   ![원본 서버 및 해당 볼륨 및 공유와 대상](media/migrate/transfer.png) **그림 3의 위치로 전송 되는 위치를 보여 주는 스크린샷 원본 서버 및 해당 저장소가 전송 되는 위치**
4. 모든 원본 서버에 대 한 대상 서버 및 매핑을 추가 하 고 **다음**을 선택 합니다.
5. 필요에 따라 전송 설정을 조정 하 고 **다음**을 선택 합니다.
6. **유효성 검사** 를 선택 하 고 **다음**을 선택 합니다.
7. **전송 시작** 을 선택 하 여 데이터 전송을 시작 합니다.<br>처음 전송할 때 대상의 모든 기존 파일을 백업 폴더로 이동 합니다. 이후 전송 시에는 기본적으로 먼저 백업 하지 않고 대상을 새로 고칩니다. <br>또한 저장소 마이그레이션 서비스는 겹치는 공유를 처리할 만큼 지능적 이며 동일한 작업에서 동일한 폴더를 두 번 복사 하지 않습니다.
8. 전송이 완료 되 면 대상 서버를 확인 하 여 모든 것이 제대로 전송 되었는지 확인 합니다. 전송 되지 않은 파일의 로그를 다운로드 하려는 경우에 **만 오류 로그** 를 선택 합니다.

   > [!NOTE]
   > 전송 감사 내역을 유지 하거나 작업에서 둘 이상의 전송을 수행 하려는 경우 **로그 전송** 을 클릭 하 여 CSV 복사본을 저장 합니다. 모든 후속 전송은 이전 실행의 데이터베이스 정보를 덮어씁니다. 

이 시점에는 세 가지 옵션이 있습니다.

- 대상 서버가 원본 서버의 id를 채택 하도록 **다음 단계로 이동**합니다.
- 원본 서버의 id를 거치지 않고 **마이그레이션을 완료 하는 것이 좋습니다** .
- **다시 전송**하 여 마지막 전송 이후에 업데이트 된 파일만 복사 합니다.

Azure와 파일을 동기화 하는 것이 목표 라면 파일 전송 후 또는 대상 서버로의 이동 후에 Azure File Sync를 사용 하 여 대상 서버를 설정할 수 있습니다 ( [Azure File Sync 배포에 대 한 계획](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)참조).

## <a name="step-3-optionally-cut-over-to-the-new-servers"></a>3단계: 필요에 따라 새 서버로 이동

이 단계에서는 원본 서버에서 대상 서버로 이동 하 여 IP 주소와 컴퓨터 이름을 대상 서버로 이동 합니다. 이 단계를 완료 한 후에는 앱과 사용자가 마이그레이션한 서버의 이름과 주소를 통해 새 서버에 액세스 합니다.

 1. 마이그레이션 작업을 벗어난 경우 Windows 관리 센터에서 **서버 관리자** > **Storage migration Service** 로 이동한 다음 완료 하려는 작업을 선택 합니다. 
 1. **새 서버로** > 이동**자격 증명 입력** 페이지에서 **다음** 을 선택 하 여 이전에 입력 한 자격 증명을 사용 합니다.
 1. **가공선 구성** 페이지에서 각 원본 장치의 설정에 대해 수행할 네트워크 어댑터를 지정 합니다. 이렇게 하면 해당 IP 주소를 원본에서 대상으로 이동 하는 과정의 일부로 이동 합니다.
 1. 해당 주소를 대상으로 이동한 후에 원본 서버에 사용할 IP 주소를 지정 합니다. DHCP 또는 고정 주소를 사용할 수 있습니다. 정적 주소를 사용 하는 경우 새 서브넷은 이전 서브넷과 동일 해야 합니다. 그렇지 않으면 사용 하지 않습니다.
    ![원본 서버와 해당 IP 주소 및 컴퓨터 이름을 보여 주는 스크린샷 및](media/migrate/cutover.png)
    **그림 4를 기준으로 하는 방법 원본 서버 및 네트워크 구성을 대상으로 이동 하는 방법**
 1. 대상 서버에서 이름을 사용한 후 원본 서버의 이름을 바꾸는 방법을 지정 합니다. 임의로 생성 된 이름을 사용 하거나 직접 입력할 수 있습니다. 그런 후 **다음**을 선택 합니다.
 1. **설정 반복 설정** 페이지에서 **다음** 을 선택 합니다.
 1. **원본 및 대상 장치 유효성 검사** 페이지에서 **유효성 검사** 를 선택 하 고 **다음**을 선택 합니다.
 1. 이 조치를 수행할 준비가 되 면 **시작 시작**을 선택 합니다. <br>사용자 및 앱은 주소와 이름이 이동 되 고 서버가 각각 여러 번 다시 시작 되는 동안 중단 될 수 있지만, 그렇지 않은 경우 마이그레이션의 영향을 받지 않습니다. 대기 시간은 서버를 다시 시작 하는 속도와 Active Directory 및 DNS 복제 시간에 따라 달라 집니다.

## <a name="see-also"></a>참조

- [Storage Migration Service 개요](overview.md)
- [Storage Migration Services FAQ (질문과 대답)](faq.md)
- [Azure File Sync 배포 계획](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)
