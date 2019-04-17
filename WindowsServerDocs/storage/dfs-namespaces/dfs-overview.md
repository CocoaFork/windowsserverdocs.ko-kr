---
title: "DFS 네임스페이스 개요"
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 07/10/2017
description: "이 항목에서는 다른 서버에 있는 여러 공유 폴더를 하나 이상의 논리적으로 구성된 네임스페이스로 그룹화할 수 있도록 하는 Windows Server의 역할 서비스인 DFS 네임스페이스에 대해 설명합니다."
ms.openlocfilehash: f3a76208fa1d6e1207edd699f830fc05a360bee5
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="dfs-namespaces-overview"></a>DFS 네임스페이스 개요

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

DFS 네임스페이스는 다른 서버에 있는 공유 폴더를 하나 이상의 논리적으로 구성된 네임스페이스로 그룹화할 수 있도록 하는 Windows Server의 역할 서비스입니다. 이를 통해 사용자에게 공유 폴더의 가상 보기를 제공할 수 있습니다. 여기서 다음 그림과 같이 여러 서버에 위치한 파일이 한 경로로 연결됩니다.

![DFS 네임스페이스 기술 요소](media/dfs-overview.png)

DFS 네임스페이스를 구성하는 요소에 대한 설명:

- **네임스페이스 서버** - 네임스페이스를 호스팅하는 네임스페이스 서버입니다. 네임스페이스 서버는 구성원 서버 또는 도메인 컨트롤러일 수 있습니다.
- **네임스페이스 루트** - 네임스페이스 루트는 네임스페이스의 시작점입니다. 이전 그림에서 루트 이름은 Public이며 네임스페이스 경로는 \\\\Contoso\\Public입니다. 이 유형의 네임스페이스는 도메인 이름(예: Contoso)으로 시작하고 메타데이터가 AD DS(Active Directory Domain Services)에 저장되므로 도메인 기반 네임스페이스입니다. 이전 그림에는 하나의 네임스페이스 서버만 표시되었지만, 도메인 기반 네임스페이스는 네임스페이스의 가용성을 늘리기 위해 여러 네임스페이스 서버에서 호스팅할 수 있습니다.
- **폴더** - 폴더 대상이 없는 폴더는 네임스페이스에 구조와 계층을 추가하고, 폴더 대상이 있는 폴더는 사용자에게 실제 콘텐츠를 제공합니다. 사용자가 네임스페이스에서 폴더 대상이 있는 폴더를 찾을 경우, 클라이언트 컴퓨터는 폴더 대상 중 하나로 투명하게 리디렉션되는 추천을 받습니다.
- **폴더 대상** - 폴더 대상은 공유 폴더의 UNC 경로이거나 네임스페이스의 폴더와 연결된 다른 네임스페이스입니다. 폴더 대상은 데이터와 콘텐츠가 저장되는 곳입니다. 이전 그림에서, Tools라는 폴더에는 런던과 뉴욕에 각각 하나씩, 두 개의 폴더 대상이 있으며 Training Guides라는 폴더에는 뉴욕에 하나의 폴더 대상이 있습니다. 사용자가 \\\\Contoso\\Public\\Software\\Tools를 탐색하면 사용자가 현재 어디에 있는지에 따라 공유 폴더 \\\\LDN-SVR-01\\Tools 또는 \\\\NYC-SVR-01\\Tools로 투명하게 리디렉션됩니다.

이 항목에서는 DFS 설치 방법, 새로운 기능, 평가 및 배포 정보를 찾을 수 있는 위치 등을 알아봅니다.

네임스페이스는 DFS 관리, [Windows PowerShell Cmdlet DFS 네임스페이스(DFSN)](https://technet.microsoft.com/library/jj884270.aspx), **DfsUtil** 명령 또는 WMI를 호출하는 스크립트를 사용하여 관리할 수 있습니다.

## <a name="server-requirements-and-limits"></a>서버 요구 사항 및 제한

DFS 관리 실행 또는 DFS 네임스페이스 사용을 위한 추가 하드웨어 또는 소프트웨어 요구 사항은 없습니다.

네임스페이스 서버는 네임스페이스를 호스팅하는 도메인 컨트롤러 또는 구성원 서버입니다. 서버에서 호스팅할 수 있는 네임스페이스의 수는 네임스페이스 서버에서 실행 중인 운영 체제에 따라 결정됩니다.

다음 운영 체제를 실행하는 서버는 여러 도메인 기반 네임스페이스와 하나의 독립 실행형 네임스페이스를 호스팅할 수 있습니다. 

- Windows Server(반기 채널)
- WindowsServer 2016 
- WindowsServer 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 Datacenter/Enterprise

다음 운영 체제를 실행하는 서버는 하나의 독립 실행형 네임스페이스를 호스팅할 수 있습니다.

- Windows Server 2008 R2 Standard


다음 표는 네임스페이스를 호스팅할 서버를 선택할 때 고려해야 하는 추가 요인을 설명합니다.

|독립 실행형 네임스페이스를 호스팅하는 서버|도메인 기반 네임스페이스를 호스팅하는 서버|
|---|---|
|네임스페이스를 호스팅할 NTFS 볼륨이 있어야 합니다.|네임스페이스를 호스팅할 NTFS 볼륨이 있어야 합니다.|
|구성원 서버 또는 도메인 컨트롤러일 수 있습니다.|구성원 서버 또는 네임스페이스가 구성된 도메인의 도메인 컨트롤러여야 합니다. (이 요구 사항은 지정된 도메인 기반 네임스페이스를 호스팅하는 모든 네임스페이스 서버에 적용됩니다.)|
|네임스페이스의 가용성을 높이기 위해 장애 조치(failover) 클러스터로 호스팅할 수 있습니다.|네임스페이스는 장애 조치(failover) 클러스터에서 클러스터링된 리소스일 수 없습니다. 그러나 네임스페이스를 해당 서버의 로컬 리소스만 사용하도록 구성하는 경우, 장애 조치(failover) 클러스터에서 노드의 역할도 하는 서버에 네임스페이스를 배치할 수 있습니다.|

## <a name="installing-dfs-namespaces"></a>DFS 네임스페이스 설치

DFS 네임스페이스 및 DFS 복제는 파일 및 저장소 서비스 역할의 일부입니다. DFS 관리 도구(DFS 관리, Windows PowerShell용 DFS 네임스페이스 모듈 및 명령줄 도구)는 원격 서버 관리 도구의 일부로 별도로 설치됩니다.

다음 섹션에 설명된 대로 서버 관리자 또는 PowerShell을 사용하여 DFS 네임스페이스를 설치합니다.

### <a name="to-install-dfs-by-using-server-manager"></a>서버 관리자를 사용하여 DFS를 설치하려면

1. 서버 관리자를 열고 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 나타납니다.

2. **서버 선택** 페이지에서 DFS를 설치할 오프라인 가상 컴퓨터의 서버 또는 VHD(가상 하드 디스크)를 선택합니다.

3. 설치할 역할 서비스 및 기능을 선택합니다.

    - DFS 네임스페이스 서비스를 설치하려면 **서버 역할** 페이지에서 **DFS 네임스페이스**를 선택합니다.

    - DFS 관리 도구만 설치하려면 **기능** 페이지에서 **원격 서버 관리 도구**, **원격 관리 도구**, **파일 서비스 도구**를 차례로 확장하고 **DFS 관리 도구**를 선택합니다.

         **DFS 관리 도구**는 DFS 관리 스냅인, Windows PowerShell용 DFS 네임스페이스 모듈 및 명령줄 도구를 설치하지만 DFS 서비스를 서버에 설치하지는 않습니다.

### <a name="to-install-dfs-by-using-windows-powershell"></a>Windows PowerShell을 사용하여 DFS를 설치하려면

관리자 권한으로 Windows PowerShell 세션을 열고 다음 명령을 입력합니다. 여기서 <name\>은 설치할 역할 서비스 또는 기능입니다. 관련 역할 서비스 또는 기능 이름 목록은 다음 표를 참조하세요.

```PowerShell
Install-WindowsFeature <name>
```

|역할 서비스 또는 기능|이름|
|---|---|
|DFS 네임스페이스|`FS-DFS-Namespace`|
|DFS 관리 도구|`RSAT-DFS-Mgmt-Con`|

예를 들어 원격 서버 관리 도구 기능의 분산 파일 시스템 도구 부분을 설치하려면 다음을 입력합니다.

```PowerShell
Install-WindowsFeature RSAT-DFS-Mgmt-Con
```

DFS 네임스페이스 및 원격 서버 관리 도구 기능의 분산 파일 시스템 도구 부분을 설치하려면 다음을 입력합니다.

```PowerShell
Install-WindowsFeature FS-DFS-Namespace, RSAT-DFS-Mgmt-Con
```

## <a name="interoperability-with-azure-virtual-machines"></a>Azure 가상 컴퓨터와의 상호 운용성

Microsoft Azure의 가상 컴퓨터에서 DFS 네임스페이스 사용이 테스트되었지만 몇 가지 제한 사항 및 요구 사항을 따라야 합니다.

- Azure 가상 컴퓨터에서 독립 실행형 네임스페이스를 클러스터링할 수 없습니다.

- Azure Active Directory를 사용한 환경을 포함하여 Azure 가상 시스템에서 도메인 기반 네임스페이스를 호스팅할 수 있지만, Active Directory Federation Services를 사용하는 경우에도 하나의 네임스페이스가 온-프레미스 네임스페이스 서버와 Azure VM에서 호스팅하는 네임스페이스 서버 둘 다를 포함할 수는 없습니다.

Azure 가상 컴퓨터를 시작하는 방법에 대해 자세히 알아보려면 [Azure 가상 컴퓨터 문서](https://docs.microsoft.com/azure/virtual-machines/)를 참조하세요.

## <a name="see-also"></a>참고 항목

자세한 내용은 다음 리소스를 참조하세요.

|콘텐츠 유형|참조|
|------------------|----------------|
|**제품 평가**|[Windows Server에서 제공되는 DFS 네임스페이스 및 DFS 복제의 새로운 기능](https://technet.microsoft.com/library/dn281957(v=ws.11).aspx)|
|**배포**|[DFS 네임스페이스 확장성 고려 사항](http://blogs.technet.com/b/filecab/archive/2012/08/26/dfs-namespace-scalability-considerations.aspx)|
|**운영**|[DFS 네임스페이스: 질문과 대답](http://technet.microsoft.com/library/ee404780.aspx)|
|**커뮤니티 리소스**|[파일 서비스 및 저장소 TechNet 포럼](http://social.technet.microsoft.com/forums/winserverfiles/threads/)|
|**프로토콜**|[파일 서비스 Windows Server 프로토콜](http://msdn.microsoft.com/library/cc239875.aspx)|
|**관련 기술**| [장애 조치(failover) 클러스터링](../../failover-clustering/failover-clustering-overview.md)|