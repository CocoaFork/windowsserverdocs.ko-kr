---
title: bitsadmin removeclientcertificate
description: '**Bitsadmin removeclientcertificate** 에 대 한 Windows 명령 항목-작업에서 클라이언트 인증서를 제거 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c664ba9b26f3511dedf35477a1cd393db709337e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381037"
---
# <a name="bitsadmin-removeclientcertificate"></a>bitsadmin removeclientcertificate



작업에서 클라이언트 인증서를 제거합니다.

## <a name="syntax"></a>구문

```
bitsadmin /RemoveClientCertificate <Job> 
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 라는 작업에서 클라이언트 인증서가 제거 *myJob*합니다.
```
C:\>Bitsadmin /RemoveClientCertificate myJob 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)