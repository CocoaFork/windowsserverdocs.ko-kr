---
title: bitsadmin 캐시 및 정보
description: Windows 명령 항목에 대 한 **bitsadmin 캐시 및 정보** -특정 캐시 엔트리를 덤프 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 61ff57b33e575921f2032d4e13a2d9b74accae60
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813324"
---
# <a name="bitsadmin-cache-and-info"></a>bitsadmin 캐시 및 정보



특정 캐시 엔트리를 덤프합니다.

## <a name="syntax"></a>구문

```
bitsadmin /Cache /Info RecordID [/Verbose] 
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|RecordID|캐시 항목에 연결 된 GUID입니다.|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 recordid {6511FB02-E195-40A2-B595-E8E2F8F47702}의 캐시 엔트리를 덤프합니다.
```
C:\>bitsadmin /Cache /Info {6511FB02-E195-40A2-B595-E8E2F8F47702} 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)