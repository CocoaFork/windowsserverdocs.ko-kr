---
title: ftp send_1
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd9f658b4fbfa5f6c9fa9a58fb0c524ad53627bc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376003"
---
# <a name="ftp-send_1"></a>ftp: send_1

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 컴퓨터에 로컬 파일을 복사 합니다.   
## <a name="syntax"></a>구문  
```  
send <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>매개 변수  

|  매개 변수   |                    설명                    |
|--------------|---------------------------------------------------|
| <LocalFile>  |         복사할 로컬 파일을 지정 합니다.         |
| <remoteFile> | 원격 컴퓨터에서 사용 하 여 이름을 지정 합니다. |

## <a name="remarks"></a>설명  
- **보낼** 명령은 동일 합니다는 **배치** 명령입니다.  
- *Remotefile* 을 지정 하지 않으면 파일에 *localfile* 이름이 지정 됩니다.  
  ## <a name="BKMK_Examples"></a>예와  
  로컬 파일 **test.txt** 를 복사 하 고 원격 컴퓨터에서 이름을 **test1** 로 설정 합니다.  
  ```  
  send test.txt test1.txt  
  ```  
  로컬 파일 **프로그램** 을 원격 컴퓨터에 복사 합니다.  
  ```  
  send program.exe  
  ```  
  ## <a name="additional-references"></a>추가 참조  
- [명령줄 구문 키](command-line-syntax-key.md)  
