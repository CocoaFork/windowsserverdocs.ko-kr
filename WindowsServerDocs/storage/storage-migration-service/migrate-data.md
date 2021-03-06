---
title: 저장소 마이그레이션 서비스를 사용 하 여 파일 서버 마이그레이션
description: 검색 엔진 결과의 항목에 대 한 간략 한 설명
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 02/13/2019
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: 20aa5fbc40efc5a3a439361dadfac0f47f4b41d8
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822626"
---
# <a name="use-storage-migration-service-to-migrate-a-server"></a>Storage Migration Service를 사용 하 여 서버 마이그레이션

이 항목에서는 [저장소 마이그레이션 서비스](overview.md) 및 Windows 관리 센터를 사용 하 여 해당 파일 및 구성을 비롯 한 서버를 다른 서버로 마이그레이션하는 방법에 대해 설명 합니다. 서비스를 설치 하 고 필요한 방화벽 포트를 연 후에는 서버를 인벤토리 하 고 데이터를 전송 하 고 새 서버로 이동 하는 과정을 단계별로 진행 합니다.

## <a name="step-0-install-storage-migration-service-and-check-firewall-ports"></a>0 단계: Storage 마이그레이션 서비스 설치 및 방화벽 포트 확인

시작 하기 전에 저장소 마이그레이션 서비스를 설치 하 고 필요한 방화벽 포트가 열려 있는지 확인 합니다.

1. [저장소 마이그레이션 서비스 요구 사항을](overview.md#requirements) 확인 하 고 PC 또는 관리 서버에 [Windows 관리 센터](../../manage/windows-admin-center/understand/windows-admin-center.md) 를 설치 합니다 (아직 설치 하지 않은 경우). 도메인에 가입 된 원본 컴퓨터를 마이그레이션하는 경우 원본 컴퓨터와 동일한 도메인 또는 포리스트에 가입 된 서버에서 저장소 마이그레이션 서비스를 설치 하 고 실행 해야 합니다.
2. Windows 관리 센터에서 Windows Server 2019를 실행 하는 orchestrator 서버에 연결 합니다. <br>저장소 마이그레이션 서비스를 설치 하 고 마이그레이션을 관리 하는 데 사용 하는 서버입니다. 서버를 하나만 마이그레이션하는 경우에는 Windows Server 2019를 실행 하는 동안 대상 서버를 사용할 수 있습니다. 다중 서버 마이그레이션에는 별도의 오케스트레이션 서버를 사용 하는 것이 좋습니다.
3. **서버 관리자** (Windows 관리 센터) > **storage migration service** 로 이동 하 고 **설치** 를 선택 하 여 저장소 마이그레이션 서비스와 필수 구성 요소 (그림 1에 표시 됨)를 설치 합니다.
    설치 단추를 표시 하는 Storage Migration Service 페이지의 ![스크린샷](media/migrate/install.png) **그림 1: Storage Migration Service 설치**
4. Windows Server 2019를 실행 하는 모든 대상 서버에 저장소 마이그레이션 서비스 프록시를 설치 합니다. 그러면 대상 서버에 설치 될 때 전송 속도가 두 배가 됩니다. <br>이렇게 하려면 Windows 관리 센터에서 대상 서버에 연결한 다음 **서버 관리자** (Windows 관리 센터)에서 **역할 및 기능**> 하 고 > **기능**으로 이동한 후 **저장소 마이그레이션 서비스 프록시**를 선택 하 고 **설치**를 선택 합니다. 
5. Windows 장애 조치 (Failover) 클러스터에서 또는로 마이그레이션하려면 orchestrator 서버에 장애 조치 (Failover) 클러스터링 도구를 설치 합니다. <br>이렇게 하려면 Windows 관리 센터에서 orchestrator 서버에 연결한 다음 **서버 관리자** (Windows 관리 센터)로 이동 하 여 **역할 및 기능**> > **기능**, > **원격 서버 관리 도구**> **기능 관리 도구**를 선택한 다음 **장애 조치 (Failover) 클러스터링 도구**를 선택 하 고 **설치**를 선택 합니다. 
6. Windows 관리 센터에서 모든 원본 서버와 Windows Server 2012 R2 또는 Windows Server 2016를 실행 하는 대상 서버에서 각 서버에 연결 하 고 **서버 관리자** (Windows 관리 센터) > **방화벽** > **들어오는 규칙**으로 이동한 후 다음 규칙을 사용 하도록 설정 했는지 확인 합니다.
    - 파일 및 프린터 공유(SMB-In)
    - Netlogon 서비스 (NP-IN)
    - WMI(Windows Management Instrumentation) (DCOM-IN)
    - WMI(Windows Management Instrumentation)(WMI-In)

   타사 방화벽을 사용 하는 경우 열 인바운드 포트 범위는 TCP/445 (SMB), TCP/135 (RPC/DCOM 엔드포인트 매퍼) 및 TCP 1025-65535 (RPC/DCOM 임시 포트)입니다. Storage Migration service 포트는 Orchestrator (TCP/28940) 및 TCP/28941 (프록시)입니다.

7. Orchestrator 서버를 사용 하 여 마이그레이션을 관리 하 고 전송 하는 데이터에 대 한 로그 나 이벤트를 다운로드 하려는 경우 해당 서버 에서도 파일 및 프린터 공유 (SMB In) 방화벽 규칙이 사용 되는지 확인 합니다.

## <a name="step-1-create-a-job-and-inventory-your-servers-to-figure-out-what-to-migrate"></a>1 단계: 마이그레이션할 항목을 확인 하기 위해 작업 만들기 및 서버 인벤토리

이 단계에서는 마이그레이션할 서버를 지정한 다음 해당 서버를 검색 하 여 파일 및 구성에 대 한 정보를 수집 합니다.

1. **새 작업**을 선택 하 고 작업 이름을 지정한 다음, Samba를 사용 하는 Windows 서버 및 클러스터 또는 Linux 서버를 마이그레이션할지 여부를 선택 합니다. 그런 다음 **확인을**선택 합니다.
2. **자격 증명 입력** 페이지에서 마이그레이션하려는 서버에서 작동 하는 관리자 자격 증명을 입력 하 고 **다음**을 선택 합니다. <br>Linux 서버에서 마이그레이션하는 경우 대신, **Samba 자격 증명** 및 **linux 자격** 증명 페이지에 SSH 암호나 개인 키를 포함 한 자격 증명을 입력 합니다. 

3. **장치 추가**를 선택 하 고, 원본 서버 이름 또는 클러스터 된 파일 서버의 이름을 입력 한 다음, **확인**을 선택 합니다. <br>인벤토리에 추가할 다른 서버에 대해이를 반복 합니다.

4. **검색 시작**을 선택 합니다.<br>검색이 완료 되 면를 표시 하는 페이지를 업데이트 합니다.
    스캔할 준비가 된 서버를 보여 주는 ![스크린샷](media/migrate/inventory.png) **그림 2: 서버 인벤토리**
5. 각 서버를 선택 하 여 인벤토리에 포함 된 공유, 구성, 네트워크 어댑터 및 볼륨을 검토 합니다. <br><br>Storage Migration Service는 Windows 작업에 방해가 될 수 있는 파일 또는 폴더를 전송 하지 않으므로,이 릴리스에서는 Windows 시스템 폴더에 있는 모든 공유에 대 한 경고를 볼 수 있습니다. 전송 단계에서 이러한 공유를 건너뛰어야 합니다. 자세한 내용은 [전송에서 제외 되는 파일 및 폴더](faq.md#what-files-and-folders-are-excluded-from-transfers)를 참조 하세요.
6. **다음** 을 선택 하 여 데이터 전송으로 이동 합니다.

## <a name="step-2-transfer-data-from-your-old-servers-to-the-destination-servers"></a>2 단계: 이전 서버에서 대상 서버로 데이터 전송

이 단계에서는 대상 서버에서 데이터를 보관할 위치를 지정한 후 데이터를 전송 합니다.

1. **데이터 전송** > **자격 증명을 입력 하세요** . 페이지에서 마이그레이션할 대상 서버에서 작동 하는 관리자 자격 증명을 입력 하 고 **다음**을 선택 합니다.
2. **대상 장치 및 매핑 추가** 페이지에서 첫 번째 원본 서버가 나열 됩니다. 마이그레이션할 서버 또는 클러스터 된 파일 서버의 이름을 입력 하 고 **장치 검색**을 선택 합니다. 도메인에 가입 된 원본 컴퓨터에서 마이그레이션하는 경우 대상 서버는 동일한 도메인에 가입 되어 있어야 합니다. "새 Azure VM 만들기"를 클릭 한 다음 마법사를 사용 하 여 Azure에서 새 대상 서버를 배포할 수도 있습니다. 그러면 자동으로 VM 크기를 조정 하 고, 저장소를 프로 비전 하 고, 디스크를 포맷 하 고, 도메인에 가입 하 고, Windows Server 2019 대상에 저장소 마이그레이션 서비스 프록시를 추가 합니다. 모든 크기의 windows Server 2019 (권장), Windows Server 2016 및 Windows Server 2012 R2 Vm 중에서 선택할 수 있으며 관리 디스크를 사용할 수 있습니다.   

 > [!NOTE]
   > "새 Azure VM 만들기"를 사용 하려면 다음이 필요 합니다.
   > - 유효한 Azure 구독.
   > - 만들기 권한이 있는 기존 Azure Compute 리소스 그룹입니다.
   > - 기존 Azure Virtual Network 및 서브넷. 
   > - 이 Azure IaaS VM에서 온-프레미스 클라이언트, 도메인 컨트롤러, Storage Migration Service orchestrator 컴퓨터, Windows 관리 센터 컴퓨터와의 연결을 허용 하는 Azure Express 경로 또는 VPN 솔루션을 Virtual Network 및 서브넷에 연결 합니다. 마이그레이션할 원본 컴퓨터를 지정할 수 있습니다.

3. 원본 볼륨을 대상 볼륨에 매핑하고, 전송 하지 않으려는 모든 공유에 대 한 **포함** 확인란의 선택을 취소 하 고 (Windows 시스템 폴더에 있는 모든 관리 공유 포함) **다음**을 선택 합니다.
   원본 서버 및 해당 볼륨 및 공유를 보여 주는 ![스크린샷](media/migrate/transfer.png) **그림 3: 원본 서버와 해당 저장소가 전송** 되는 위치
4. 모든 원본 서버에 대 한 대상 서버 및 매핑을 추가 하 고 **다음**을 선택 합니다.
5. **전송 설정 조정** 페이지에서 원본 서버의 로컬 사용자 및 그룹을 마이그레이션할지 여부를 지정한 후 **다음**을 선택 합니다. 이렇게 하면 로컬 사용자 및 그룹으로 설정 된 파일 또는 공유 권한이 손실 되지 않도록 대상 서버에서 로컬 사용자 및 그룹을 다시 만들 수 있습니다. 로컬 사용자 및 그룹을 마이그레이션할 때의 옵션은 다음과 같습니다.

    - 기본적으로 **이름이 같은 계정 이름을 바꾸고** 원본 서버의 모든 로컬 사용자 및 그룹을 마이그레이션합니다. 원본 및 대상에서 이름이 같은 로컬 사용자 또는 그룹을 검색 하는 경우 기본 제공 (예: 관리자 사용자 및 관리자 그룹)이 아닌 경우 대상에서 이름을 바꿉니다. 원본 또는 대상 서버가 도메인 컨트롤러인 경우이 설정을 사용 하지 마십시오.
    - **동일한 이름을 가진 계정을 다시 사용** 하면 원본 및 대상에서 이름이 같은 사용자 및 그룹이 매핑됩니다. 원본 또는 대상 서버가 도메인 컨트롤러인 경우이 설정을 사용 하지 마십시오.
    - **사용자 및 그룹을 전송 하지 않으면** 원본 또는 대상이 도메인 컨트롤러인 경우 또는 DFS 복제 (DFS 복제 로컬 그룹과 사용자를 지원 하지 않음)에 대 한 데이터를 시드 할 때 필요한 로컬 사용자 및 그룹의 마이그레이션이 생략 됩니다.

   > [!NOTE]
   > 마이그레이션된 사용자 계정은 대상에서 사용 하지 않도록 설정 되 고 복잡 하 고 임의적인 127 문자 암호를 할당 합니다. 따라서 사용을 계속 하려면 사용 하도록 설정 하 고 새 암호를 할당 해야 합니다. 이렇게 하면 원본에서 잊어버린 암호를 사용 하는 이전 계정이 대상에서 계속 해 서 보안 문제가 되지 않도록 할 수 있습니다. 로컬 관리자 암호를 관리 하는 방법으로 [로컬 관리자 암호 솔루션 (LAPS)](https://www.microsoft.com/download/details.aspx?id=46899) 을 체크 아웃할 수도 있습니다.

6. **유효성 검사** 를 선택 하 고 **다음**을 선택 합니다.
7. **전송 시작** 을 선택 하 여 데이터 전송을 시작 합니다.<br>처음 전송할 때 대상의 모든 기존 파일을 백업 폴더로 이동 합니다. 이후 전송 시에는 기본적으로 먼저 백업 하지 않고 대상을 새로 고칩니다. <br>또한 저장소 마이그레이션 서비스는 겹치는 공유를 처리할 만큼 지능적 이며 동일한 작업에서 동일한 폴더를 두 번 복사 하지 않습니다.
8. 전송이 완료 되 면 대상 서버를 확인 하 여 모든 것이 제대로 전송 되었는지 확인 합니다. 전송 되지 않은 파일의 로그를 다운로드 하려는 경우에 **만 오류 로그** 를 선택 합니다.

   > [!NOTE]
   > 전송 감사 내역을 유지 하거나 작업에서 둘 이상의 전송을 수행 하려는 경우 **전송 로그** 또는 다른 로그 저장 옵션을 클릭 하 여 CSV 복사본을 저장 합니다. 모든 후속 전송은 이전 실행의 데이터베이스 정보를 덮어씁니다. 

이 시점에는 세 가지 옵션이 있습니다.

- 대상 서버가 원본 서버의 id를 채택 하도록 **다음 단계로 이동**합니다.
- 원본 서버의 id를 거치지 않고 **마이그레이션을 완료 하는 것이 좋습니다** .
- **다시 전송**하 여 마지막 전송 이후에 업데이트 된 파일만 복사 합니다.

Azure와 파일을 동기화 하는 것이 목표 라면 파일 전송 후 또는 대상 서버로의 이동 후에 Azure File Sync를 사용 하 여 대상 서버를 설정할 수 있습니다 ( [Azure File Sync 배포에 대 한 계획](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)참조).

## <a name="step-3-cut-over-to-the-new-servers"></a>3 단계: 새 서버로 잘라내기

이 단계에서는 원본 서버에서 대상 서버로 이동 하 여 IP 주소와 컴퓨터 이름을 대상 서버로 이동 합니다. 이 단계를 완료 한 후에는 앱과 사용자가 마이그레이션한 서버의 이름과 주소를 통해 새 서버에 액세스 합니다.

1. 마이그레이션 작업을 벗어난 경우 Windows 관리 센터에서 **서버 관리자** > **Storage migration Service** 로 이동한 다음 완료 하려는 작업을 선택 합니다.
2. **새 서버로** 이동 > **자격 증명 입력** 페이지에서 **다음** 을 선택 하 여 이전에 입력 한 자격 증명을 사용 합니다.

   대상이 클러스터 된 파일 서버인 경우 도메인에서 클러스터를 제거할 수 있는 권한이 있는 자격 증명을 제공 하 고 새 이름으로 다시 추가 해야 할 수 있습니다.

3. **가공선 구성** 페이지에서 원본에 있는 각 어댑터의 설정을 사용 하 여 대상의 네트워크 어댑터를 지정 합니다. 이렇게 하면 원본 서버에 새 DHCP 또는 고정 IP 주소를 지정 하 여 원본에서 대상으로 IP 주소를 이동 합니다. 모든 네트워크 마이그레이션 또는 특정 인터페이스를 건너뛸 수 있는 옵션이 있습니다. 
4. 해당 주소를 대상으로 이동한 후에 원본 서버에 사용할 IP 주소를 지정 합니다. DHCP 또는 고정 주소를 사용할 수 있습니다. 정적 주소를 사용 하는 경우 새 서브넷은 이전 서브넷과 동일 해야 합니다. 그렇지 않으면 사용 하지 않습니다.
    원본 서버와 해당 IP 주소 및 컴퓨터 이름을 보여 주는 ![스크린샷 및](media/migrate/cutover.png) **그림 4: 원본 서버와 대상으로 이동 하는 방법**
5. 대상 서버에서 이름을 사용한 후 원본 서버의 이름을 바꾸는 방법을 지정 합니다. 임의로 생성 된 이름을 사용 하거나 직접 입력할 수 있습니다. 그런 후 **다음**을 선택 합니다.
6. **설정 반복 설정** 페이지에서 **다음** 을 선택 합니다.
7. **원본 및 대상 장치 유효성 검사** 페이지에서 **유효성 검사** 를 선택 하 고 **다음**을 선택 합니다.
8. 이 조치를 수행할 준비가 되 면 **시작 시작**을 선택 합니다. <br>사용자 및 앱은 주소와 이름이 이동 되 고 서버가 각각 여러 번 다시 시작 되는 동안 중단 될 수 있지만, 그렇지 않은 경우 마이그레이션의 영향을 받지 않습니다. 대기 시간은 서버를 다시 시작 하는 속도와 Active Directory 및 DNS 복제 시간에 따라 달라 집니다.

## <a name="see-also"></a>참고 항목

- [Storage Migration Service 개요](overview.md)
- [Storage Migration Services FAQ (질문과 대답)](faq.md)
- [Azure File Sync 배포 계획](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)
