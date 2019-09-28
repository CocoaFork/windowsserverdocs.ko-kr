---
title: bitsadmin addfile
description: '**Bitsadmin addfile** 에 대 한 Windows 명령 항목-지정 된 작업에 파일을 추가 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b31aa93-0364-465b-af36-754968825989
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8dfddda92e506dbfca2a47394a310edf16fe78aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382036"
---
# <a name="bitsadmin-addfile"></a>bitsadmin addfile

지정된 된 작업에 파일을 추가 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /AddFile <Job> <RemoteURL> <LocalName>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|RemoteURL|서버에서 파일의 URL입니다.|
|LocalName|로컬 컴퓨터에 있는 파일의 이름입니다. *LocalName* 파일에 절대 경로 포함 해야 합니다.|

## <a name="BKMK_examples"></a>예와

파일 작업을 추가 합니다. 추가 하려는 각 파일에 대 한이 호출을 반복 합니다. 여러 작업을 사용 하는 경우 *myDownloadJob* 해당 이름으로 바꿔야 *myDownloadJob* 작업을 고유 하 게 식별 하는 작업의 GUID를 가진 합니다.
```
C:\>bitsadmin /addfile myDownloadJob http://downloadsrv/10mb.zip c:\10mb.zip
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)