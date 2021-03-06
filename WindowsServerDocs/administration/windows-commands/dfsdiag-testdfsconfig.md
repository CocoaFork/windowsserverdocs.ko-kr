---
title: dfsdiag Testdfs 구성
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 106aeeb9-ea79-4e6e-829c-eca06309bab2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8008e02d588edaa6fe7700a331c43f9680d89431
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378425"
---
# <a name="dfsdiag-testdfsconfig"></a>dfsdiag Testdfs 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

분산 파일 시스템의 구성을 확인 \(DFS\) 다음 작업을 수행 하 여 네임 스페이스:  
  
-   모든 네임 스페이스 서버에서 DFS 네임 스페이스 서비스가 실행 중이 고 해당 시작 유형이 자동으로 설정 되어 있는지 확인 합니다.  
  
-   네임 스페이스 서버 간에 DFS 레지스트리 구성이 일치 하는지 확인 합니다.  
  
-   Windows Server 2008 이상을 실행 하는 클러스터 된 네임 스페이스 서버에서 다음 종속성의 유효성을 검사 합니다.  
  
    -   네임 스페이스 루트 리소스에 대 한 종속성 네트워크 이름 리소스입니다.  
  
    -   IP 주소 리소스에 네트워크 이름 리소스 종속성입니다.  
  
    -   실제 디스크 리소스에 네임 스페이스 루트 리소스 종속성입니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:<namespace>  
```  
  
### <a name="parameters"></a>매개 변수  
  
|       매개 변수       |               설명               |
|-----------------------|-----------------------------------------|
| \/DFSRoot:<namespace> | 네임 스페이스 \(DFS 루트\) 를 진단 합니다. |
  
## <a name="BKMK_Examples"></a>예와  
TBD를 입력 합니다.  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:\\Contoso.com\MyNamespace  
```  
  
## <a name="additional-references"></a>추가 참조  
  
-   [명령줄 구문 키](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

