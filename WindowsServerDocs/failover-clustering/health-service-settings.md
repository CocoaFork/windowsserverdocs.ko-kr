---
title: 상태 서비스 설정
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 569cf7ba30fd3f993394efd3735a56d116c067e0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858334"
---
# <a name="health-service-settings"></a>상태 서비스 설정
> 적용 대상: Windows Server 2016

상태 관리 서비스는 저장소 공간 다이렉트를 실행 하는 클러스터에 대 한 작업 경험과 일상적인 모니터링을 향상 시키는 Windows Server 2016의 새로운 기능입니다.

다양 한 상태 관리 서비스의 동작을 제어 하는 매개 변수는 설정으로 노출 됩니다. 오류 또는 작업의 강도 조정, 켬/끔 등 특정 동작을 설정 하 고 수정할 수 있습니다.

설정 하거나 설정을 수정 하려면 다음 PowerShell cmdlet을 사용 합니다.

### <a name="usage"></a>사용법

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name <SettingName> -Value <Value>  
```

#### <a name="example"></a>예제

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.Volume.CapacityThreshold.Warning" -Value 70
```

### <a name="common-settings"></a>일반 설정

일반적으로 수정 된 일부 설정은 해당 기본값으로 함께 아래 나열 됩니다.

#### <a name="volume-capacity-threshold"></a>볼륨 용량 임계값

```
"System.Storage.Volume.CapacityThreshold.Enabled"  = True
"System.Storage.Volume.CapacityThreshold.Warning"  = 80
"System.Storage.Volume.CapacityThreshold.Critical" = 90
```

#### <a name="pool-reserve-capacity-threshold"></a>풀의 예약 용량 임계값

```
"System.Storage.StoragePool.CheckPoolReserveCapacity.Enabled" = True
```

#### <a name="physical-disk-lifecycle"></a>실제 디스크 수명 주기

```
"System.Storage.PhysicalDisk.AutoPool.Enabled"                             = True
"System.Storage.PhysicalDisk.AutoRetire.OnLostCommunication.Enabled"       = True
"System.Storage.PhysicalDisk.AutoRetire.OnUnresponsive.Enabled"            = True
"System.Storage.PhysicalDisk.AutoRetire.DelayMs"                           = 900000 (i.e. 15 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountResetIntervalSeconds" = 360 (i.e. 60 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountAllowed"              = 3
```

#### <a name="supported-components-document"></a>지원 되는 구성 요소 문서

이전 섹션을 참조 하세요.

#### <a name="firmware-rollout"></a>펌웨어 출시

```
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.SingleDrive.Enabled"       = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.Enabled"           = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelaySeconds"  = 604800 (i.e. 7 days)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.ShortDelaySeconds" = 86400 (i.e. 1 day)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelayCount"    = 1
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.FailureTolerance"  = 3
```

#### <a name="platform--quiescence"></a>플랫폼 / 정지

```
"Platform.Quiescence.MinDelaySeconds" = 120 (i.e. 2 minutes)
"Platform.Quiescence.MaxDelaySeconds" = 420 (i.e. 7 minutes)
```

#### <a name="metrics"></a>메트릭

```
"System.Reports.ReportingPeriodSeconds" = 1
```

#### <a name="debugging"></a>디버깅

```
"System.LogLevel" = 4
```

## <a name="see-also"></a>참조

- [Windows Server 2016의에서 상태 관리 서비스](health-service-overview.md)
- [Windows Server 2016의에서 저장소 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md)