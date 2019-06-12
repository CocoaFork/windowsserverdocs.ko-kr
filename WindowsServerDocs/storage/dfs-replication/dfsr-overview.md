---
Title: DFS 복제 개요
ms.date: 03/08/2019
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: dd381c04b02889a7f2e7b8992ff6050d1b0f078a
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453063"
---
# <a name="dfs-replication-overview"></a>DFS 복제 개요

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server (반기 채널)

DFS 복제는 여러 서버 및 사이트에서 폴더 (DFS 네임 스페이스 경로 참조 된 포함)을 효율적으로 복제할 수 있도록 Windows Server에서 역할 서비스. DFS 복제는 폴더의 제한 된 대역폭 네트워크 연결을 통해 서버 간에 동기화를 유지 하는 데 사용할 수 있는 효율적이 고 다중 마스터 복제 엔진. Windows Server 2008 또는 이상 도메인 기능 수준을 사용 하는 도메인의 Active Directory Domain Services (AD DS) SYSVOL 폴더를 복제 뿐 아니라 DFS 네임 스페이스에 대 한 복제 엔진으로 복제 서비스 FRS (파일)를 대체 합니다.

DFS 복제에서는 RDC(원격 차등 압축)라는 압축 알고리즘을 사용합니다. RDC는 파일의 데이터 변경 내용을 검색 하 고 전체 파일 대신 변경 된 파일 블록만 복제 하려면 DFS 복제를 활성화 합니다.

DFS 복제를 사용 하 여 SYSVOL을 복제 하는 방법에 대 한 자세한 내용은 참조 하십시오 [DFS 복제 SYSVOL 복제 마이그레이션](migrate-sysvol-to-dfsr.md)합니다.

DFS 복제를 사용 하려면 복제 그룹을 만들고 그룹에 복제 된 폴더를 추가 합니다. 복제 그룹, 복제 된 폴더 및 멤버는 다음 그림에 나와 있습니다.

![두 멤버 사이의 연결을 포함 하는 복제 그룹을 개 몇 복제 된 폴더](media/dfsr-overview.gif)

이 그림 복제 그룹을 하나 이상의 복제 된 폴더의 복제에 참여 하는 서버를 구성원 이라고 집합이 임을 보여 줍니다. 복제 된 폴더는 각 멤버에 동기화 된 상태로 유지 되는 폴더입니다. 그림에서 두 개의 복제 된 폴더: 프로젝트 및 제안 합니다. 각 복제 된 폴더의 데이터가 변경 되 면 복제 그룹의 멤버 간 연결을 통해 변경 내용이 복제 됩니다. 복제 토폴로지를 구성 하는 모든 멤버 간의 연결입니다.
단일 복제 그룹에 여러 복제 된 폴더를 만들고 각 복제 된 폴더에 적용 되므로 토폴로지, 일정 및 대역폭 복제 그룹에 대 한 제한 된 복제 폴더를 배포 하는 과정을 간소화 합니다. 추가 복제 된 폴더를 배포 하려면 사용할 수 있습니다 Dfsradmin.exe 또는 작업 지침 마법사에서 새 복제 폴더에 대 한 권한을 확인 하 고 로컬 경로 정의 하려면.

복제 된 각 폴더는 파일 및 하위 폴더 필터와 같은 고유한 설정을 있으므로 다양 한 파일 및 복제 된 각 폴더에 대 한 하위 폴더를 필터링 할 수 있습니다.

멤버의 다른 볼륨에 각 멤버에 저장 된 복제 된 폴더를 배치할 수 있습니다 하 고 복제 된 폴더를 공유 폴더 또는 네임 스페이스의 일부를 사용할 필요가 없습니다. 그러나 DFS 관리 스냅인을 쉽게 복제 된 폴더를 공유 하 고 필요에 따라 기존 네임 스페이스에서 게시 합니다.

DFS 관리, DfsrAdmin 및 Dfsrdiag 명령 또는 WMI를 호출 하는 스크립트를 사용 하 여 DFS 복제를 관리할 수 있습니다.

## <a name="requirements"></a>요구 사항

DFS 복제를 배포하려면 다음과 같이 서버를 구성해야 합니다.

- Windows Server 2003 R2 또는 이후 스키마 추가 포함 하도록 Active Directory Domain Services (AD DS) 스키마를 업데이트 합니다. Windows Server 2003 R2 또는 이전 스키마 추가 사용 하 여 읽기 전용 복제 폴더를 사용할 수 없습니다.
- 복제 그룹에 있는 모든 서버가 같은 포리스트에 있는지 확인합니다. 다른 포리스트에 있는 서버에서 복제를 사용할 수 없습니다.
- 복제 그룹의 구성원 역할을 하게 되는 모든 서버에 DFS 복제를 설치합니다.
- 바이러스 백신 소프트웨어 공급업체에 문의하여 바이러스 백신 소프트웨어가 DFS 복제와 호환되는지 확인합니다.
- NTFS 파일 시스템으로 포맷된 볼륨에서 복제할 폴더를 찾습니다. DFS 복제는 ReFS(복원 파일 시스템) 또는 FAT 파일 시스템을 지원하지 않습니다. 또한 DFS 복제는 클러스터 공유 볼륨에 저장된 콘텐츠 복제를 지원하지 않습니다.

## <a name="interoperability-with-azure-virtual-machines"></a>Azure 가상 컴퓨터와의 상호 운용성

Windows 서버를 사용 하 여 Azure에서 가상 컴퓨터에서 DFS 복제를 사용 하는 테스트 그러나 몇 가지 제한 사항 및 수행 해야 하는 요구 사항입니다.

- SYSVOL 폴더 외 모든 것을 복제하기 위해 DFS 복제를 실행하는 서버를 복원하는 데 스냅샷 또는 저장된 상태를 사용하면 DFS 복제가 실패할 수 있는데, 이 경우 특별한 데이터베이스 복구 단계가 필요합니다. 마찬가지로, 가상 컴퓨터를 내보내거나, 복제 또는 복사하지 마세요. 자세한 내용은 Microsoft 기술 자료 문서 [2517913](http://support.microsoft.com/kb/2517913) 및 [안전하게 DFSR 가상화](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)를 참조하세요.
- 가상 컴퓨터에서 호스트된 복제된 폴더에 데이터를 백업할 때 게스트 가상 컴퓨터 내에서 백업 소프트웨어를 사용해야 합니다.
- DFS 복제를 사용 하면 물리적 또는 가상화 된 도메인 컨트롤러에 대 한 액세스-Azure AD와 직접 통신할 수 없습니다.
- DFS 복제를 사용하려면 온-프레미스 복제 그룹 구성원과 Azure VM에서 호스트된 구성원 간의 VPN 연결이 필요합니다. 또한 RPC 끝점 매퍼(포트 135) 및 49152와 65535 사이에 임의로 할당된 포트를 VPN 연결을 통해 전달할 수 있도록 온-프레미스 라우터(예: Forefront Threat Management Gateway)를 구성해야 합니다. 임의 포트 대신 정적 포트를 지정 하려면 Set-dfsrmachineconfiguration cmdlet 또는 Dfsrdiag 명령줄 도구를 사용할 수 있습니다. DFS 복제에 고정 포트를 지정하는 방법에 대한 자세한 내용은 [Set-DfsrServiceConfiguration](https://docs.microsoft.com/powershell/module/dfsr/set-dfsrserviceconfiguration)을 참조하세요. Windows Server를 관리하기 위해 열려는 관련 포트에 대한 자세한 내용은 Microsoft 기술 자료 문서 [832017](http://support.microsoft.com/kb/832017) 을 참조하세요.

Azure 가상 컴퓨터를 시작하는 방법에 대해 자세히 알아보려면 [Microsoft Azure 웹 사이트](https://docs.microsoft.com/azure/virtual-machines/)를 방문하세요.

## <a name="installing-dfs-replication"></a>DFS 복제를 설치합니다.

DFS 복제는 File and Storage Services 역할의 일부입니다. DFS (DFS 관리, Windows PowerShell 및 명령줄 도구에 대 한 DFS 복제 모듈)에 대 한 관리 도구는 원격 서버 관리 도구의 일부로 별도로 설치 됩니다.

DFS 복제를 사용 하 여 설치 [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md), 서버 관리자 또는 PowerShell에서 다음 섹션에 설명 된 대로 합니다.

### <a name="to-install-dfs-by-using-server-manager"></a>서버 관리자를 사용하여 DFS를 설치하려면

1. 서버 관리자를 열고 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 나타납니다.

2. **서버 선택** 페이지에서 DFS를 설치할 오프라인 가상 컴퓨터의 서버 또는 VHD(가상 하드 디스크)를 선택합니다.

3. 설치할 역할 서비스 및 기능을 선택합니다.

    - DFS 복제 서비스를 설치 하는 **서버 역할** 페이지에서 **DFS 복제**합니다.

    - DFS 관리 도구만 설치하려면 **기능** 페이지에서 **원격 서버 관리 도구**, **원격 관리 도구**, **파일 서비스 도구**를 차례로 확장하고 **DFS 관리 도구**를 선택합니다.

         **DFS 관리 도구** DFS 관리 스냅인, DFS 복제 및 DFS 네임 스페이스 모듈 Windows PowerShell 및 명령줄 도구를 사용 하지만에 대 한 설치 서버에서 DFS 서비스를 설치 하지 않습니다.

### <a name="to-install-dfs-replication-by-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 DFS 복제를 설치 하려면

다음 명령을 입력 하 고 관리자 권한으로 Windows PowerShell 세션을 엽니다 여기서 < 이름\> 은 역할 서비스 또는 기능 설치 하려는 (관련 역할 서비스 또는 기능 이름 목록은 다음 표 참조).

```PowerShell
Install-WindowsFeature <name>
```

|역할 서비스 또는 기능|이름|
|---|---|
|DFS 복제|`FS-DFS-Replication`|
|DFS 관리 도구|`RSAT-DFS-Mgmt-Con`|

예를 들어 원격 서버 관리 도구 기능의 분산 파일 시스템 도구 부분을 설치하려면 다음을 입력합니다.

```PowerShell
Install-WindowsFeature "RSAT-DFS-Mgmt-Con"
```

DFS 복제 및 원격 서버 관리 도구 기능의 분산 파일 시스템 도구 부분을 설치 하려면 다음을 입력 합니다.

```PowerShell
Install-WindowsFeature "FS-DFS-Replication", "RSAT-DFS-Mgmt-Con"
```

## <a name="see-also"></a>참조

- [DFS 네임 스페이스 및 DFS 복제 개요](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v%3dws.11))
- [검사 목록: DFS 복제를 배포 합니다.](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772201(v%3dws.11))
- [검사 목록: DFS 복제를 관리 합니다.](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755035(v%3dws.11))
- [DFS 복제를 배포합니다.](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [DFS 복제를 관리합니다.](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [DFS 복제 문제 해결](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732802(v%3dws.11))
