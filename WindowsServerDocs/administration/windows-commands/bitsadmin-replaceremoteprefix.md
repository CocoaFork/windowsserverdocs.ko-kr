---
title: bitsadmin replaceremoteprefix
description: Windows 명령 항목에 대 한 **bitsadmin replaceremoteprefix** -해당 원격 URL로 시작 작업의 모든 파일 *OldPrefix* 사용 하도록 변경 *NewPrefix*합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 848c57736c3530e296cffb970237149b4634de67
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266517"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix



해당 원격 URL로 시작 작업의 모든 파일 *OldPrefix* 를 사용 하도록 변경 *NewPrefix*합니다.

## <a name="syntax"></a>구문

```
bitsadmin /ReplaceRemotePrefix <Job> <OldPrefix> <NewPrefix
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|OldPrefix|기존 URL 접두사|
|NewPrefix|새 URL 접두사|

## <a name="examples"></a>예

다음 예제에서는 명명 된 작업의 모든 파일을 변경 *myDownloadJob* 원격 URL로 시작 갖는 *http://stageserver* 에 *http://prodserver* 합니다.
```
C:\>bitsadmin /ReplaceRemotePrefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>추가 정보

[명령줄 구문 키](command-line-syntax-key.md)