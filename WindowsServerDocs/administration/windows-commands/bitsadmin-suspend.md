---
title: bitsadmin suspend
description: Windows 명령 항목에 대 한 **bitsadmin 일시 중단** -지정된 된 된 작업을 일시 중단 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f9d42500-7bea-4aa8-a9f0-c22f6ed3e73b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87e1bbd1b068d68fb60655043735c6c1aeb07707
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825924"
---
# <a name="bitsadmin-suspend"></a>bitsadmin suspend

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 작업을 일시 중단합니다.

## <a name="syntax"></a>구문

```
bitsadmin /Suspend <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

작업을 다시 시작 하려면 사용 합니다 [bitsadmin resume](bitsadmin-resume.md) 전환 합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업을 일시 중단 *myDownloadJob*합니다.

```
C:\>bitsadmin /Suspend myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
