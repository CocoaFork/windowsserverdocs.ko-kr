---
title: SET 옵션
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d8d4921-9fdd-4a3c-bb0f-9df5458c4b84
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b9174f219654e99eb9441abe3342c31b5089ef5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384052"
---
# <a name="set-option"></a>SET 옵션



섀도 복사본 만들기에 대 한 옵션을 설정합니다. 매개 변수 없이 사용 하는 경우 **옵션을 설정** 명령 프롬프트에서 도움말을 표시 합니다.

## <a name="syntax"></a>구문

```
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
```

## <a name="parameters"></a>매개 변수

|     매개 변수     |                                                                                                  설명                                                                                                  |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   [차등   |                                                                                                     플렉스로                                                                                                     |
|  가능한  |                       섀도 복사본을 아직 가져와야 하지 임을 지정 합니다. 나중에 메타 데이터.cab 파일 같거나 다른 컴퓨터에 섀도 복사본을 가져오는 데 사용할 수 있습니다.                       |
| [rollbackrecover] |                     신호를 사용 하 여 작성자 *자동 복구* 중는 **PostSnapshot** 이벤트입니다. 이는 섀도 복사본을 롤백에 사용 하는 경우에 유용 합니다 (예: 데이터 마이닝 사용).                      |
|   [트랜잭션 복원]    |                                                               VSS 섀도 복사본을 만드는 동안 트랜잭션 측면에서 일관 되도록 요청 합니다.                                                                |
|  [noautorecover 저장]  | 중지 작성자 및 파일 시스템에서 트랜잭션 측면에서 일관 된 상태로 섀도 복사본을 복구 변경 내용을 적용 합니다. **Noautorecover** 함께 사용할 수 없습니다 **txfrecover** 또는 **rollbackrecover**합니다. |

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)