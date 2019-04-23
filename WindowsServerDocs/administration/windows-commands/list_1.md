---
title: 목록
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69b105a1-9710-4a06-8102-38cc9e475ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ef9262a04f469f54e43cf3a83efe30fac7ad8580
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854674"
---
# <a name="list"></a>목록



디스크, 디스크의 파티션, 디스크에 볼륨 또는 가상 하드 디스크 (Vhd)의 목록을 표시합니다.

## <a name="syntax"></a>구문

```
list { disk | partition | volume | vdisk }
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|디스크|디스크에 대 한 정보와, 크기, 사용 가능한 공간, 디스크는 기본 또는 동적 디스크 인지 및 디스크는 마스터 부트 레코드 (MBR) 또는 GUID 파티션 테이블 (GPT) 파티션 스타일을 사용 하는 여부 등의 목록을 표시 합니다.|
|파티션|현재 디스크의 파티션 테이블에 나열 된 파티션을 표시 합니다.|
|볼륨|모든 디스크에 기본 및 동적 볼륨 목록을 표시합니다.|
|vdisk|Vhd 연결 하거나 선택한의 목록을 표시 합니다. 이 명령은 현재 선택 되어; 경우 분리 된 Vhd를 나열 그러나, VHD가 연결 될 때까지 알 수 없는 디스크 유형 설정 됩니다. 별표 (*)로 표시 된 VHD에 포커스가 있습니다.</br>참고: 이 명령은 Windows 7 및 Windows Server 2008 r 2에만 있습니다.|

## <a name="remarks"></a>설명

-   동적 디스크에 파티션을 나열할 때 동적 볼륨은 디스크에 파티션이 없습니다 해당할 수 있습니다. 이러한 차이로 인해 시스템 볼륨 또는 부팅 볼륨 (있는 경우 디스크에서)에 대 한 파티션 테이블에 항목이 동적 디스크에 포함 하기 때문에 발생 합니다. 또한 동적 볼륨에 사용할 공간을 예약 하기 위해 디스크의 나머지 부분을 차지 하는 파티션을 포함 합니다.
-   별표 (*)로 표시 된 개체에 포커스가 있습니다.
-   디스크가 없을 경우 디스크를 나열 하는 경우 해당 디스크 번호 M가 붙습니다. 예를 들어, 첫 번째 누락 된 디스크는 번호가 지정 m 0입니다.

## <a name="BKMK_examples"></a>예제

```
list disk
list partition
list volume
list vdisk
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

