---
title: bitsadmin 피어 캐싱 및 getconfigurationflags
description: '**Bitsadmin 피어 캐싱 및 getconfigurationflags** 에 대 한 Windows 명령 항목-컴퓨터가 피어에 콘텐츠를 제공 하는지 여부를 결정 하는 구성 플래그를 가져오며 피어에서 콘텐츠를 다운로드할 수 있습니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94c7eb1a115fe9152b149b8cf65765b179080cc3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381097"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>bitsadmin 피어 캐싱 및 getconfigurationflags



구성 플래그를 결정 하는 경우 컴퓨터 피어 컴퓨터에 콘텐츠를 제공 합니다. 피어 로부터 콘텐츠를 다운로드할 수를 가져옵니다.

## <a name="syntax"></a>구문

```
bitsadmin /PeerCaching /GetConfigurationFlags <Job> 
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 구성 플래그를 가져옵니다 *myJob*합니다.
```
C:\> Bitsadmin /PeerCaching /GetConfigurationFlags myJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)