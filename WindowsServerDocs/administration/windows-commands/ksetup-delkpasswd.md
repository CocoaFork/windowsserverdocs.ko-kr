---
title: 'ksetup: delkpasswd'
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dce7d9666040ff0c234139932ea60e3589dfecb2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375127"
---
# <a name="ksetupdelkpasswd"></a>ksetup: delkpasswd

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

영역에 대 한 Kerberos 암호 서버 (Kpasswd)를 제거 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.
## <a name="syntax"></a>구문
```
ksetup /delkpasswd <RealmName> <KpasswdName>
```
### <a name="parameters"></a>매개 변수

|   매개 변수   |                                                                                                   설명                                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <RealmName>  |                                영역 이름은 CORP와 같은 대문자 DNS 이름으로 명시 됩니다. CONTOSO.COM는 **ksetup** 가 실행 될 때 기본 영역 또는 영역 =으로 나열 됩니다.                                |
| <KpasswdName> | Kerberos 암호 서버로 사용할 KDC 이름은 대/소문자를 구분 하지 않고 정규화 된 도메인 이름 (예: mitkdc.contoso.com)으로 명시 됩니다. KDC 이름이 생략 된 경우 Kdc 찾을 DNS는 사용할 수 있습니다. |

## <a name="remarks"></a>설명
명령을 실행 **ksetup** KDC 이름을 확인할 수 있습니다. **Kpasswd =** 가 출력에 표시 되지 않으면 매핑이 구성 되지 않은 것입니다. 설정 된 경우 여러 매핑이 나열 됩니다.
## <a name="BKMK_Examples"></a>예와
영역 CORP를 확인 합니다. CONTOSO.COM는 암호 서버로 비 Windows KDC 서버 mitkdc.contoso.com를 사용 합니다.
```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
명령이 의도 한 대로 작동 하는지 확인 하려면 Windows 컴퓨터에서 **ksetup** 를 실행 하 여 영역 CORP를 확인 합니다. CONTOSO.COM가 Kerberos 암호 서버 (KDC 이름)에 매핑되지 않았습니다.
## <a name="additional-references"></a>추가 참조
-   [ksetup](ksetup.md)
-   [ksetup: delkpasswd](ksetup-delkpasswd.md)
-   [명령줄 구문 키](command-line-syntax-key.md)
