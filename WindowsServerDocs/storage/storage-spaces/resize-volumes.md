---
title: 저장소 공간 다이렉트에서 볼륨 확장
ms.assetid: fa48f8f7-44e7-4a0b-b32d-d127eff470f0
ms.prod: windows-server-threshold
ms.author: cosmosdarwin
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 01/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51f58ec23c55a6cb1664d800d6f4a75dae545899
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824974"
---
# <a name="extending-volumes-in-storage-spaces-direct"></a>저장소 공간 다이렉트에서 볼륨 확장
> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 [저장소 공간 다이렉트](storage-spaces-direct-overview.md)에서 볼륨의 크기를 조정하는 데 대한 지침을 제공합니다.

## <a name="prerequisites"></a>사전 요구 사항

### <a name="capacity-in-the-storage-pool"></a>저장소 풀의 용량

볼륨의 크기를 조정하기 전에 저장소 풀에 새롭고 더 큰 사용 공간을 수용할 수 있는 충분한 용량이 있는지 확인합니다. 예를 들어 3방향 미러 볼륨의 크기를 1TB에서 2TB로 조정할 때 사용 공간은 3TB에서 6TB로 증가합니다. 크기를 성공적으로 조정하려면 저장소 풀에서 최소 (6-3) = 3TB의 용량을 사용할 수 있어야 합니다.

### <a name="familiarity-with-volumes-in-storage-spaces"></a>저장소 공간 다이렉트의 볼륨에 대한 지식

저장소 공간 다이렉트에서 모든 볼륨은 여러 개의 누적된 개체(클러스터 공유 볼륨(CSV)(볼륨), 파티션, 디스크(가상 디스크) 및 하나 이상의 저장소 계층(해당되는 경우))으로 구성되어 있습니다. 볼륨의 크기를 조정하려면 이러한 몇 가지 개체의 크기를 조정해야 합니다.

![volumes-in-smapi](media/resize-volumes/volumes-in-smapi.png)

이러한 개체에 대해 알아보려면 PowerShell에서 해당하는 명사를 사용하여 **Get-** 을 실행해 보세요.

예를 들어 다음과 같은 가치를 제공해야 합니다.

```PowerShell
Get-VirtualDisk
```

스택에 있는 개체 간의 연결을 확인하려면 하나의 **Get-** cmdlet을 다음으로 파이프합니다.

예를 들어 가상 디스크에서 볼륨까지 가져오는 방법은 다음과 같습니다.

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-Disk | Get-Partition | Get-Volume 
```

## <a name="step-1--resize-the-virtual-disk"></a>1단계 - 가상 디스크의 크기 조정

가상 디스크는 만들어진 방법에 따라 저장소 계층을 사용할 수도 있고 사용하지 못할 수도 있습니다.

확인하려면 다음 cmdlet을 실행합니다.

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier 
```

cmdlet이 아무 것도 반환하지 않는 경우 가상 디스크는 저장소 계층을 사용하지 않습니다.

### <a name="no-storage-tiers"></a>저장소 계층이 없음

가상 디스크에 저장소 계층이 없는 경우 **Resize-VirtualDisk** cmdlet을 사용하여 직접 크기를 조정할 수 있습니다.

**-Size** 매개 변수에 새로운 크기를 제공합니다.

```PowerShell
Get-VirtualDisk <FriendlyName> | Resize-VirtualDisk -Size <Size>
```

**VirtualDisk**의 크기를 조정할 때 **Disk**도 자동으로 따라가며 크기도 조정됩니다.

![Resize-VirtualDisk](media/resize-volumes/Resize-VirtualDisk.gif)

### <a name="with-storage-tiers"></a>저장소 계층이 있음

가상 디스크가 저장소 계층을 사용하는 경우 **Resize-StorageTier** cmdlet을 사용하여 각 계층의 크기를 개별적으로 조정할 수 있습니다.

가상 디스크의 연결을 따라가서 저장소 계층의 이름을 얻습니다.

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier | Select FriendlyName
```

그런 다음 각 계층에 대해 **-Size** 매개 변수에 새로운 크기를 제공합니다.

```PowerShell
Get-StorageTier <FriendlyName> | Resize-StorageTier -Size <Size>
```

> [!TIP]
> 계층의 물리적 미디어 유형(**MediaType = SSD** 및 **MediaType = HDD** 등)이 서로 다른 경우 저장소 풀에 있는 각 미디어 유형에 각 계층의 새롭고 더 큰 저장 공간을 수용할 수 있는 충분한 용량이 있는지 확인해야 합니다.

**StorageTier**의 크기를 조정할 때 **VirtualDisk** 및 **Disk**도 자동으로 따라가며 크기도 조정됩니다.

![Resize-StorageTier](media/resize-volumes/Resize-StorageTier.gif)

## <a name="step-2--resize-the-partition"></a>2단계 - 파티션 크기 조정

다음으로 **Resize-Partition** cmdlet을 사용하여 파티션의 크기를 조정합니다. 가상 디스크에는 두 개의 파티션이 있는데 첫 번째 파티션은 예약되어 있으므로 수정할 수 없습니다. 크기를 조정해야 하는 파티션에는 **PartitionNumber = 2** 및 **Type = Basic**이 있습니다.

**-Size** 매개 변수에 새로운 크기를 제공합니다. 아래와 같이 최소 지원 크기를 사용하는 것이 좋습니다.

```PowerShell
# Choose virtual disk
$VirtualDisk = Get-VirtualDisk <FriendlyName>

# Get its partition
$Partition = $VirtualDisk | Get-Disk | Get-Partition | Where PartitionNumber -Eq 2

# Resize to its maximum supported size 
$Partition | Resize-Partition -Size ($Partition | Get-PartitionSupportedSize).SizeMax
```

**Partition**의 크기를 조정할 때 **Volume** 및 **ClusterSharedVolume**도 자동으로 따라가며 크기도 조정됩니다.

![파티션 크기 조정](media/resize-volumes/Resize-Partition.gif)

정말 간단하죠.

> [!TIP]
> **Get-Volume**을 실행하여 볼륨이 새로운 크기인지 확인할 수 있습니다.

## <a name="see-also"></a>참조

- [Windows Server 2016의에서 저장소 공간 다이렉트](storage-spaces-direct-overview.md)
- [저장소 공간 다이렉트 볼륨 계획](plan-volumes.md)
- [저장소 공간 다이렉트에서 볼륨 만들기](create-volumes.md)
