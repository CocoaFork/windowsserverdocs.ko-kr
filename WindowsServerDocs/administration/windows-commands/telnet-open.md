---
title: 텔넷 열기
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 186664a75978f589a9a26047c72b9db74dd2dc4d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441121"
---
# <a name="telnet-open"></a>텔넷: 열기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

텔넷 서버에 연결합니다.    
## <a name="syntax"></a>구문  
```  
o[pen] <hostname> [<Port>]  
```  
### <a name="parameters"></a>매개 변수  

| 매개 변수  |                                        설명                                         |
|------------|--------------------------------------------------------------------------------------------|
| <hostname> |                         컴퓨터 이름 또는 IP 주소를 지정합니다.                         |
|  [<Port>]  | 텔넷 서버에서 수신 대기 중인 TCP 포트를 지정 합니다. 기본값은 23 TCP 포트. |

## <a name="BKMK_Examples"></a>예제  
Telnet.microsoft.com에 텔넷 서버에 연결 합니다.  
```  
o telnet.microsoft.com  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
