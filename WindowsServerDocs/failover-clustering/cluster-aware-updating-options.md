---
ms.assetid: 2f4b6641-0ec2-4b1c-85fb-a1f1d16685c8
title: 클러스터 인식 업데이트 고급 옵션 및 업데이트 실행 프로필
ms.topic: article
ms.prod: windows-server
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 08/06/2018
description: CAU (클러스터 인식 업데이트)에 대 한 고급 옵션 및 업데이트 실행 프로필을 구성 하는 방법
ms.openlocfilehash: 500eb4d9affe38fe5f22f3720893b7960190948e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361313"
---
# <a name="cluster-aware-updating-advanced-options-and-updating-run-profiles"></a>클러스터 인식 업데이트 고급 옵션 및 업데이트 실행 프로필

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012.

이 항목에서는 CAU ( [클러스터 인식 업데이트](cluster-aware-updating.md) ) 업데이트 실행에 대해 구성할 수 있는 업데이트 실행 옵션에 대해 설명 합니다. 이러한 고급 옵션은 업데이트를 적용 하거나 자체 업데이트 옵션을 구성 하기 위해 CAU UI 또는 CAU Windows PowerShell cmdlet 중 하나를 사용 하는 경우 구성할 수 있습니다.

대부분의 구성 설정은 업데이트 실행 프로필이라는 XML 파일로 저장되며 이후에 업데이트 실행 시 다시 사용할 수 있습니다. CAU에서 제공되는 업데이트 실행 옵션의 기본값은 많은 클러스터 환경에서도 사용할 수 있습니다.

각 업데이트 실행 및 업데이트 실행 프로필에 대해 지정할 수 있는 추가 옵션에 대한 자세한 내용을 보려면 이 항목 후반부에 나오는 다음 섹션을 참조하십시오.

업데이트 실행을 요청할 때 지정 하는 옵션 업데이트 실행 프로필에서 설정할 수 있는 업데이트 실행 프로필 옵션을 사용 합니다.

다음 표에는 CAU 업데이트 실행 프로필에서 설정할 수 있는 옵션이 나열되어 있습니다. 

> [!NOTE] 
> PreUpdateScript 또는 PostUpdateScript 옵션을 설정 하려면 Windows PowerShell 및 .NET Framework 4.6 또는 4.5이 설치 되어 있고 클러스터의 각 노드에서 PowerShell 원격을 사용 하도록 설정 되어 있는지 확인 합니다. 자세한 내용은 [클러스터 인식 업데이트에 대 한 요구 사항 및 모범 사례](cluster-aware-updating-requirements.md)에서 원격 관리를 위한 노드 구성을 참조 하세요.


|옵션|기본값|설명|  
|------------|-------------------|-------------|  
|**StopAfter**|무제한 시간|업데이트 실행이 완료되지 않은 경우 중지할 때까지 남은 시간(분)입니다. **참고:**  사전 업데이트 또는 사후 업데이트 PowerShell 스크립트를 지정 하는 경우 스크립트 실행 및 업데이트 수행의 전체 프로세스를 **StopAfter** 시간 제한 내에 완료 해야 합니다.|  
|**WarnAfter**|기본적으로 경고 표시 안 함|업데이트 실행(구성된 경우 사전 업데이트 스크립트 및 사후 업데이트 스크립트 포함)이 완료되지 않은 경우 경고가 나타날 때까지 남은 시간(분)입니다.|  
|**MaxRetriesPerNode**|3|노드당 업데이트 프로세스(구성된 경우 사전 업데이트 스크립트 및 사후 업데이트 스크립트 포함)를 재시도할 최대 횟수입니다. 최대값은 64입니다.|  
|**MaxFailedNodes**|대부분의 클러스터의 경우 클러스터 노드 수의 약 1/3이 정수입니다.|노드 오류이거나 클러스터 서비스에서 실행이 중단되어 업데이트가 실패할 수 있는 최대 노드 수입니다. 하나 이상의 노드가 실패하면 업데이트 실행이 중지됩니다.<br /><br /> 값의 유효한 범위는 클러스터 노드 수보다 적은 0에서 1입니다.|  
|**RequireAllNodesOnline**|없음|모든 노드가 온라인 상태이고 업데이트를 시작하기 전에 연결 가능 상태가 되도록 지정합니다.|  
|**RebootTimeoutMinutes**|15|CAU에서 노드를 다시 시작하고(다시 시작해야 하는 경우) 모든 자동 시작 서비스를 시작하도록 허용된 시간입니다. 이 시간 내에 다시 시작 프로세스가 완료 되지 않으면 해당 노드에서 업데이트 실행이 실패로 표시 됩니다.|  
|**PreUpdateScript**|없음|업데이트가 시작 되기 전, 노드가 유지 관리 모드로 전환 되기 전에 각 노드에서 실행할 PowerShell 스크립트의 경로와 파일 이름입니다. 파일 이름 확장명은 **.** p s 1 이어야 하며, 경로와 파일 이름의 전체 길이는 260 자를 초과 하면 안 됩니다. 모든 클러스터 노드에서 항상 액세스할 수 있도록 클러스터 저장소의 디스크나 항상 사용할 수 있는 네트워크 파일 공유에 스크립트를 두는 것이 가장 좋습니다. 스크립트가 네트워크 파일 공유에 있을 경우 Everyone 그룹에 대한 읽기 권한에 대해 파일 공유를 구성하고 승인되지 않은 사용자가 파일을 변조하는 행위를 방지하기 위해 쓰기 액세스 권한이 제한되도록 설정해야 합니다.<br /><br /> 사전 업데이트 스크립트를 지정하는 경우 스크립트를 성공적으로 실행할 수 있도록 시간 제한(예: **StopAfter**) 등의 설정을 구성해야 합니다. 이러한 제한은 업데이트 설치 프로세스만이 아니라 스크립트 실행과 업데이트 설치의 전체 프로세스에 적용됩니다.|  
|**PostUpdateScript**|없음|업데이트 완료 후 (노드가 유지 관리 모드를 종료 한 후) 실행할 PowerShell 스크립트의 경로 및 파일 이름입니다. 파일 이름 확장명은 **.** p s 1 이어야 하며, 경로와 파일 이름의 전체 길이는 260 자를 초과 하면 안 됩니다. 모든 클러스터 노드에서 항상 액세스할 수 있도록 클러스터 저장소의 디스크나 항상 사용할 수 있는 네트워크 파일 공유에 스크립트를 두는 것이 가장 좋습니다. 스크립트가 네트워크 파일 공유에 있을 경우 Everyone 그룹에 대한 읽기 권한에 대해 파일 공유를 구성하고 승인되지 않은 사용자가 파일을 변조하는 행위를 방지하기 위해 쓰기 액세스 권한이 제한되도록 설정해야 합니다.<br /><br /> 사후 업데이트 스크립트를 지정하는 경우 스크립트를 성공적으로 실행할 수 있도록 시간 제한(예: **StopAfter**) 등의 설정을 구성해야 합니다. 이러한 제한은 업데이트 설치 프로세스만이 아니라 스크립트 실행과 업데이트 설치의 전체 프로세스에 적용됩니다.|  
|**ConfigurationName**|스크립트를 실행하는 경우에만 이 설정이 적용됩니다.<br /><br /> 사전 업데이트 스크립트 또는 사후 업데이트 스크립트를 지정 했지만 **ConfigurationName**을 지정 하지 않은 경우 Powershell (Microsoft. powershell)의 기본 세션 구성이 사용 됩니다.|**PreUpdateScript** 및 **PostUpdateScript**로 지정 된 스크립트를 실행 하는 세션을 정의 하는 PowerShell 세션 구성을 지정 하 고 실행할 수 있는 명령을 제한할 수 있습니다.|  
|**CauPluginName**|**Microsoft.windowsupdateplugin**|업데이트를 미리 보거나 업데이트 실행을 하는 데 사용할 클러스터 인식 업데이트를 구성하는 플러그 인입니다. 자세한 내용은 [클러스터 인식 업데이트 플러그 인 작동 방식](cluster-aware-updating-plug-ins.md)을 참조 하세요.|  
|**CauPluginArguments**|없음|플러그 인 업데이트에 사용할 한 쌍의 *name=value*(인수) 집합입니다. 예를 들면 다음과 같습니다.<br /><br /> **도메인 = 도메인 로컬**<br /><br /> 이러한 *name=value* 쌍은 **CauPluginName**에서 지정하는 플러그 인에 의미가 있어야 합니다.<br /><br /> CAU UI를 사용하여 인수를 지정하려면 *name*을 입력하고, 탭 키를 누른 다음 해당 *value*를 입력합니다. 다음 인수를 제공하려면 Tab 키를 다시 누릅니다. 각 *name* 및 *value*는 등호(=)로 자동 분리됩니다. 여러 쌍은 세미콜론으로 자동 분리됩니다.<br /><br /> 기본 **microsoft.windowsupdateplugin** 플러그 인에는 인수가 필요 하지 않습니다. 그러나 표준 Windows 업데이트 에이전트 쿼리 문자열을 지정하여 플러그 인으로 적용되는 업데이트 집합을 필터링하는 경우와 같이 인수를 선택적으로 지정할 수도 있습니다. *이름*에 대해 **QueryString**을 사용 하 고 *값*에 대해 전체 쿼리를 따옴표로 묶습니다.<br /><br /> 자세한 내용은 [클러스터 인식 업데이트 플러그 인 작동 방식](cluster-aware-updating-plug-ins.md)을 참조 하세요.|  
  
##  <a name="BKMK_runtime"></a>업데이트 실행을 요청할 때 지정 하는 옵션  
 다음 표에는 업데이트 실행을 요청할 때 지정할 수 있는 옵션(업데이트 실행 프로필에 없는 옵션)이 나열되어 있습니다. 업데이트 실행 프로필에서 설정할 수 있는 옵션에 대한 내용은 이전 표를 참조하십시오.  
  
|옵션|기본값|설명|  
|------------|-------------------|-------------|  
|**ClusterName**|없음 <br>**참고:**  이 옵션은 CAU UI가 장애 조치(failover) 클러스터 노드에서 실행되지 않는 경우에만 설정해야 합니다. 그렇지 않으면 CAU UI에서 실행하는 장애 조치(failover) 클러스터와 다른 클러스터를 참조해야 할 수 있습니다.|업데이트 실행을 수행할 클러스터의 NetBIOS 이름입니다.|  
|**증명서**|현재 계정 자격 증명|업데이트 실행을 할 대상 클러스터에 대한 관리자 자격 증명입니다. 클러스터에 대 한 관리자 권한 및 사용 권한이 있는 계정에서 CAU UI를 시작 하거나 (CAU PowerShell cmdlet을 사용 하는 경우 PowerShell 세션을 연 경우) 이미 필요한 자격 증명이 있을 수 있습니다.|  
|**NodeOrder**|기본적으로 CAU는 가장 적은 수의 클러스터된 역할을 소유한 노드부터 시작되어, 그 다음 두 번째로 가장 적은 수를 가진 노드로 진행되는 방식으로 이뤄집니다.|가능한 경우 업데이트해야 하는 순서로 나열된 클러스터 노드의 이름입니다.|  
  
##  <a name="BKMK_profile"></a>업데이트 실행 프로필 사용  
 각 업데이트 실행을 특정 업데이트 실행 프로필과 연결할 수 있습니다. 기본 업데이트 실행 프로필은 *%windir%\cluster* 폴더에 저장 됩니다. CAU UI를 원격 업데이트 모드로 사용 하는 경우 업데이트를 적용할 때 업데이트 실행 프로필을 지정 하거나 기본 업데이트 실행 프로필을 사용할 수 있습니다. 자동 업데이트 모드에서 CAU를 사용 하는 경우 자동 업데이트 옵션을 구성할 때 지정 된 업데이트 실행 프로필에서 설정을 가져올 수 있습니다. 두 경우 모두 필요에 따라 업데이트 실행 옵션에 대해 표시된 값을 재정의할 수 있습니다. 원할 경우 업데이트 실행 프로필 옵션을 같은 파일 이름이나 다른 파일 이름을 사용하여 업데이트 실행 프로필로 저장할 수 있습니다. 다음 번에 업데이트를 적용하거나 자동 업데이트 옵션을 구성할 경우 CAU에서 이전에 선택했던 업데이트 실행 프로필을 자동으로 선택합니다.  
  
 CAU UI에서 **업데이트 실행 프로필 만들기 또는 수정** 을 선택 하 여 기존 업데이트 실행 프로필을 수정 하거나 새로 만들 수 있습니다.

업데이트 실행 프로필 사용에 대 한 몇 가지 중요 한 참고 사항은 다음과 같습니다.

* 업데이트 실행 프로필은 관리 자격 증명과 같은 클러스터 관련 정보를 저장 하지 않습니다. 자동 업데이트 모드에서 CAU를 사용 하는 경우 업데이트 실행 프로필에도 자동 업데이트 일정 정보가 저장 되지 않습니다. 이를 통해 지정된 클래스의 모든 장애 조치(failover) 클러스터에서 업데이트 실행 프로필을 공유할 수 있게 됩니다.
* 업데이트 실행 프로필을 사용 하 여 자동 업데이트 옵션을 구성 하 고 나중에 업데이트 실행 옵션에 대해 다른 값으로 프로필을 수정 하면 자동 업데이트 구성이 자동으로 변경 되지 않습니다. 새 업데이트를 실행 설정을 적용하려면 자동 업데이트 옵션을 다시 구성해야 합니다.
* 실행 프로필 편집기는 파일 경로 (예: *C:\Program files*)를 포함 하는 파일 경로를 지원 하지 않습니다. 한 가지 해결 방법으로, 사전 및 사후 업데이트 스크립트를 공백이 포함 되지 않은 경로에 저장 하거나, PowerShell을 독점적으로 사용 하 여 실행 프로필을 관리 하 고, **invoke-caurun**실행 시 경로 주위에 따옴표를 추가 합니다.

### <a name="windows-powershell-equivalent-commands"></a>Windows PowerShell 해당 명령
  
 **Invoke-caurun**, **add-cauclusterrole**또는 **Add-cauclusterrole** Cmdlet을 실행할 때 업데이트 실행 프로필에서 설정을 가져올 수 있습니다.  
  
 다음 예제에서는 *C:\Windows\Cluster\DefaultParameters.xml*에 지정된 업데이트 실행 옵션을 사용하여 *CONTOSO-FC1*이라는 이름의 클러스터에서 스캔 및 전체 업데이트 실행을 수행하는 과정을 보여줍니다. 기본값은 나머지 cmdlet 매개변수에 대해 사용됩니다.  
  
```powershell  
$MyRunProfile = Import-Clixml C:\Windows\Cluster\DefaultParameters.xml  
Invoke-CauRun –ClusterName CONTOSO-FC1 @MyRunProfile   
```  
  
 업데이트 실행 프로필을 사용하여 예외 관리, 시간 범위 및 기타 조작 매개변수에 대한 일관된 설정으로 장애 조치(failover) 클러스터를 반복 가능한 방식으로 업데이트할 수 있습니다. 이러한 설정은 일반적으로 "모든 Microsoft SQL Server 서버" 또는 "내 업무상 중요한 클러스터"와 같은 장애 조치(failover) 클러스터의 클래스에만 적용되기 때문에 사용되는 장애 조치(failover) 클러스터의 클래스에 따라 업데이트 실행 프로필 이름을 각자 지정하려 할 수도 있습니다. 또한, IT 조직에서 특정 클래스의 모든 장애 조치(failover) 클러스터에 액세스할 수 있는 파일 공유에서 업데이트 실행 프로필을 관리하려 할 수도 있습니다.  
  
  
  
## <a name="see-also"></a>참조

-   [클러스터 인식 업데이트](cluster-aware-updating.md)
  
-   [Windows PowerShell의 클러스터 인식 업데이트 Cmdlet](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps)