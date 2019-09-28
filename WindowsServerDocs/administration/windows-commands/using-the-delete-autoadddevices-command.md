---
title: Delete AutoaddDevices 명령을 사용 하 여
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8dcaca6a-212e-4c36-98e3-00938eef6b9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5e914506f731685b17117b359359f60ea91992dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363541"
---
# <a name="using-the-delete-autoadddevices-command"></a>Delete AutoaddDevices 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

자동 추가 데이터베이스에서 보류 중이거나 거부 되거나 승인 된 컴퓨터를 삭제 합니다. 이 데이터베이스는 서버에서 이러한 컴퓨터에 대 한 정보를 저장합니다.
## <a name="syntax"></a>구문
```
wdsutil /delete-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices |ApprovedDevices}
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|/Devicetype: {PendingDevices &#124; RejectedDevices &#124;ApprovedDevices}|데이터베이스에서 삭제할 컴퓨터의 유형을 지정 합니다. 이 다음 세 가지 유형 중 하나일 수 있습니다.<br /><br />-   **PendingDevices** 는 데이터베이스에서 보류 중 상태의 모든 컴퓨터를 반환 합니다.<br />-   **RejectedDevices** 는 데이터베이스에서 상태가 거부 됨 인 모든 컴퓨터를 반환 합니다.<br />-   **ApprovedDevices** 는 승인 됨 상태의 모든 컴퓨터를 반환 합니다.|
## <a name="BKMK_examples"></a>예와
모든 거부 된 컴퓨터를 삭제 하려면 다음을 입력 합니다.
```
wdsutil /delete-AutoaddDevices /Devicetype:RejectedDevices
```
승인 된 모든 컴퓨터를 삭제 하려면 다음을 입력 합니다.
```
wdsutil /verbose /delete-AutoaddDevices /Server:MyWDSServer /Devicetype:ApprovedDevices
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
 @no__t[승인](using-the-approve-autoadddevices-command.md)-autoadddevices 명령을 사용 하 여-3 @no__t[get](using-the-get-autoadddevices-command.md)autoadddevices 명령을 사용 하 여-5[거부 autoadddevices 명령을 사용](using-the-reject-autoadddevices-command.md) 하 여
