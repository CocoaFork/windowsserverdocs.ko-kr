---
title: bitsadmin info
description: 의 Windows 명령 항목에서는 **지정 된 작업에 대 한 요약 정보를 표시 합니다.** -bitsadmin 정보
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b6710d73860315fcd13670669871cd310ffb41c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381082"
---
# <a name="bitsadmin-info"></a>bitsadmin info



지정된 된 작업에 대 한 요약 정보를 표시 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /Info <Job> [/verbose]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

사용 하는 자세한 정보 표시 / 매개 변수는 작업에 대 한 자세한 정보를 제공 합니다.

## <a name="BKMK_examples"></a>예와

명명 된 작업에 대 한 정보를 검색 하는 다음 예제에서는 *myDownloadJob*합니다.
```
C:\>bitsadmin /Info myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)