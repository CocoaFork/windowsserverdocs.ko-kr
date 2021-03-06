---
title: 선택
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9eeb40c0-4258-46e2-8dbc-94f63497e771
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7dc3bc8775f971968f096ba4344348e77c112cfa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384114"
---
# <a name="select"></a>선택



디스크, 파티션, 볼륨 또는 가상 하드 디스크 (VHD)에 포커스를 이동합니다.

## <a name="syntax"></a>구문

```
select disk
select partition
select volume
select vdisk
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[디스크 선택](select-disk.md)|디스크에 포커스를 이동합니다.|
|[파티션 선택](select-partition.md)|파티션의 포커스가 이동합니다.|
|[볼륨 선택](select-volume.md)|볼륨에 포커스를 이동합니다.|
|[Vdisk 선택](select-vdisk.md)|VHD에 포커스를 이동합니다.|

## <a name="remarks"></a>설명

-   해당 파티션이 있는 볼륨을 선택 하면 파티션이 자동으로 선택 됩니다.
-   파티션이 해당 볼륨을 선택 하는 경우 볼륨 자동으로 선택 됩니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

