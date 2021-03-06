---
title: dcgpofix
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 81d5fa65-2aea-49d3-b353-357441846c00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2592210ae688f47dcf2d32c7bef560d52223141c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378765"
---
# <a name="dcgpofix"></a>dcgpofix



도메인에 대 한 기본 그룹 정책 개체 (Gpo)를 다시 만듭니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
DCGPOFix [/ignoreschema] [/target: {Domain | DC | Both}] [/?]
```

### <a name="parameters"></a>매개 변수

|    매개 변수    |                                                                                                 설명                                                                                                 |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  생성  | Active Directory® 스키마 mc의 버전을 무시합니다.</br>이 명령을 실행 하면 됩니다. 그렇지 않으면이 명령은 명령이 배송 된 Windows 버전으로 같은 스키마 버전 에서만 작동 합니다. |
| /target {도메인 |                                                                                                     DC                                                                                                      |
|       /?        |                                                                                    명령 프롬프트에 도움말을 표시합니다.                                                                                     |

## <a name="remarks"></a>설명

-   **Dcgpofix** 명령은 server Core 설치를 제외 하 고 windows Server 2008 R2 및 windows server 2008에서 사용할 수 있습니다.
-   그룹 정책 관리 콘솔 (GPMC)는 Windows Server 2008 R2 및 Windows Server 2008과 함께 배포 되지만 서버 관리자를 통해 그룹 정책 관리 기능으로 설치 해야 합니다.

## <a name="BKMK_Examples"></a>예와

기본 도메인 정책 GPO를 원래 상태로 복원 합니다. 이 GPO에 대 한 변경 내용을 손실 됩니다. 모범 사례로, 기본 계정 정책 설정, 암호 정책, 계정 잠금 정책 및 Kerberos 정책 관리에 기본 도메인 정책 GPO를 구성 해야 합니다. Active Directory 스키마의 버전을 무시 하면이 예제에서는 있도록는 **dcgpofix** 명령 명령이 배송 된 Windows 버전으로 동일한 스키마에 제한 되지 않습니다.
```
dcgpofix /ignoreschema /target:Domain
```
기본 도메인 컨트롤러 정책 GPO를 원래 상태로 복원 합니다. 이 GPO에 대 한 변경 내용을 손실 됩니다. 모범 사례로, 기본 도메인 컨트롤러 정책 GPO 사용자 권한을 설정 하 고 감사 정책에만 구성 해야 합니다. Active Directory 스키마의 버전을 무시 하면이 예제에서는 있도록는 **dcgpofix** 명령 명령이 배송 된 Windows 버전으로 동일한 스키마에 제한 되지 않습니다.
```
dcgpofix /ignoreschema /target:DC
```

#### <a name="additional-references"></a>추가 참조

-   [그룹 정책 TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   [명령줄 구문 키](command-line-syntax-key.md)