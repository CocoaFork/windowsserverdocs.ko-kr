---
title: 시작 소프트웨어 인벤토리 로깅
description: 설치 및 소프트웨어 인벤토리 로깅 사용을 시작 하는 방법을 설명 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: manage-software-inventory-logging
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed51c13c-7cbf-4144-a675-011fd29379d4
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6944eac179c605db6c7b6f3e08f87c2329fb777f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435370"
---
# <a name="get-started-with-software-inventory-logging"></a>시작 소프트웨어 인벤토리 로깅

>적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

 소프트웨어 인벤토리 로깅은 서버 단위로 Microsoft 소프트웨어 인벤토리 데이터를 수집합니다. Windows Server 2012 R2를 사용 하 여 소프트웨어 인벤토리 로깅을 사용 하기 전에 해야 해당 Windows 업데이트 [KB 3000850](https://support.microsoft.com/kb/3000850) 하 고 [KB 3060681](https://support.microsoft.com/kb/3060681) 에 각 시스템에 설치 됩니다. Windows 업데이트가 Windows Server 2016에 필요 합니다. 또한 SIL의 기능을 사용 하 여 집계 서버로 데이터를 전달 하려는 경우 해야 네트워크에 대 한 유효한 SSL 인증서를 사용 해야 합니다.

## <a name="BKMK_OVER"></a>기능 설명
Windows Server의 소프트웨어 인벤토리 로깅은 서버 관리자가 서버에 설치된 Microsoft 소프트웨어 목록을 검색하는 데 도움이 되는 간단한 PowerShell cmdlet 집합이 포함된 기능입니다. 또한 이 데이터를 수집하고 집계를 위해 HTTPS 프로토콜을 사용하여 네트워크를 통해 정기적으로 대상 웹 서버에 전달하는 기능을 제공합니다. 주로 시간별 수집 및 전달을 위한 기능 관리도 PowerShell 명령을 통해 수행됩니다.

> [!NOTE]
> 웹 서비스를 실행하는 집계 서버는 별도로 구성될 수 있습니다. [소프트웨어 인벤토리 로깅 집계](software-inventory-logging-aggregator.md)에 대해 자세히 알아봅니다.

> [!IMPORTANT]
> 소프트웨어 인벤토리 로깅에서 수집한 데이터는 이 기능의 일부로 Microsoft에 전송되지 않습니다.

## <a name="BKMK_APP"></a>실제 응용 프로그램
소프트웨어 인벤토리 로깅은 서버에 로컬로 배포된 Microsoft 소프트웨어에 대한 정확한 정보를 검색하는 운영 비용을 줄이기 위한 목적으로 제공되지만 특히 IT 환경의 여러 서버(IT 환경에서 배포되고 사용하도록 설정된 것으로 가정)에서 그렇습니다. 이 데이터를 집계 서버(IT 관리자가 별도로 설정한 경우)로 전달하면 단일화된 자동 프로세스를 통해 한곳에서 데이터를 수집할 수 있습니다. 인터페이스를 직접 쿼리하여 이 작업을 수행할 수도 있지만 소프트웨어 인벤토리 로깅에서는 각 서버에서 시작되는 전달(네트워크를 통해) 아키텍처를 사용하여 많은 소프트웨어 인벤토리 및 자산 관리 시나리오에서 일반적으로 발생하는 시스템 검색 문제를 방지할 수 있습니다. 관리자의 집계 서버에 HTTPS를 통해 전달되는 데이터는 SSL을 사용하여 보안됩니다. 데이터를 한 곳(하나의 서버)에 두면 데이터를 보다 쉽게 분석, 조작 및 보고할 수 있습니다. 이러한 데이터는 이 기능의 일부로 Microsoft에 전송되지 않습니다. 소프트웨어 인벤토리 로깅 데이터 및 기능은 서버 소프트웨어의 라이선스 소유자 및 관리자만 사용할 수 있습니다.

소프트웨어 인벤토리 로깅은 서버 관리자가 다음 작업을 수행하는 데 도움을 줄 수 있습니다.

-   Windows Server에서 원격으로 요청에 따라 소프트웨어 및 서버 인벤토리 정보 검색

-   각 서버의 소프트웨어 인벤토리 로깅 기능을 사용하도록 설정하고 웹 서버 대상 URI 및 인증을 위한 인증서 지문을 선택하여 광범위한 소프트웨어 자산 관리 시나리오를 위한 소프트웨어 및 서버 인벤토리 정보 집계

## <a name="see-also"></a>관련 항목
[소프트웨어 인벤토리 로깅 집계](https://technet.microsoft.com/library/mt572043.aspx)<br>
[소프트웨어 인벤토리 로깅 관리](manage-software-inventory-logging.md)<br>
[Windows PowerShell의 소프트웨어 인벤토리 로깅 Cmdlet](https://technet.microsoft.com/library/dn283390.aspx)<br>
[Microsoft Assessment and Planning Toolkit](https://www.microsoft.com/download/en/details.aspx?id=7826)
[Volume Activation Management Tool](http://blogs.technet.com/b/volume-licensing/)
