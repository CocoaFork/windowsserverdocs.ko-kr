---
title: 시작-Namespace 하위 명령
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2dd1c11e-6ab7-4129-9e3a-3f80e0ba59c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5dc484a3b159cd510d7a61484f4f46b1f1db7a4e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877134"
---
# <a name="subcommand-start-namespace"></a>하위 명령: 시작-네임 스페이스

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012에는 예약 된 캐스트 네임 스페이스를 시작 합니다.
## <a name="syntax"></a>구문
```
wdsutil /start-Namespace /Namespace:<Namespace name> [/Server:<Server name>]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/ Namespace:<Namespace name>|네임 스페이스의 이름을 지정합니다. Note 이름, 이것이 하 고 고유 해야 합니다.<br /><br />-   **배포 서버**: 네임 스페이스 이름에 대 한 구문은 /Namspace:WDS:<Image group>/<Image name>/<Index>합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다. **WDS:ImageGroup1/install.wim/1**<br />-   **전송 서버**: 이 이름은 서버에서 만들어졌을 때 네임 스페이스에 지정 된 이름과 일치 해야 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
## <a name="BKMK_examples"></a>예제
네임 스페이스를 시작 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /start-Namespace /Namespace:"Custom Auto 1"
wdsutil /start-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1"
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[get AllNamespaces 명령을 사용 하 여](using-the-get-allnamespaces-command.md)
[새 네임 스페이스 명령을 사용 하 여](using-the-new-namespace-command.md)
[제거 네임 스페이스 명령을 사용 하 여](using-the-remove-namespace-command.md)
