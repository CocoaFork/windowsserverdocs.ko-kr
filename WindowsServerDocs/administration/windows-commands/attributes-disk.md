---
title: 특성 디스크
description: '**특성 디스크** 에 대 한 Windows 명령 항목-디스크의 특성을 표시, 설정 또는 지웁니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eed57071-c1c6-4394-9542-62b52a878c92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 415125208b13d82adeed736107f59fda9489a953
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382572"
---
# <a name="attributes-disk"></a>특성 디스크



표시 설정 하거나 디스크의 특성을 지웁니다.

> [!IMPORTANT]
> 이 매개 변수는 Windows Vista의 모든 버전에서 사용할 수 없습니다.

## <a name="syntax"></a>구문

```
attributes disk [{set | clear}] [readonly] [noerr]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|집합|포커스가 있는 디스크의 지정된 된 특성을 설정합니다.|
|clear|포커스가 있는 디스크의 지정된 된 특성을 지웁니다.|
|읽기 전용|디스크가 읽기 전용으로 지정 합니다.|
|noerr|스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|

## <a name="remarks"></a>설명

-   때 **특성 디스크** 은 디스크의 현재 속성을 표시 하는 데 사용, 시동 디스크 특성 컴퓨터를 시작 하는 데 사용 되는 디스크를 나타냅니다. 동적 미러 서버에 대 한 부팅 볼륨의 부팅 플렉스를 포함 하는 디스크에 대 한 표시 됩니다.
-   디스크를 선택 해야는 **특성 디스크** 명령을 성공적으로 합니다. 사용 된 **디스크 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="BKMK_examples"></a>예와

선택된 된 디스크의 특성을 보려면 다음을 입력 합니다.
```
attributes disk
```
선택한 디스크를 읽기 전용으로 설정 하려면 다음을 입력 합니다.
```
attributes disk set readonly
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

