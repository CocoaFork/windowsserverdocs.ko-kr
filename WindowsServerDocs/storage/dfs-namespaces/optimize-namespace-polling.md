---
title: "네임스페이스 폴링 최적화"
description: "이 문서에서는 네임스페이스 폴링을 최적화하여 여러 네임스페이스 서버에서 일관된 도메인 기반 네임스페이스를 유지하는 방법을 설명합니다."
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: be9a7623089d99a5b9c791b219dbcc64d61466cf
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="optimize-namespace-polling"></a>네임스페이스 폴링 최적화

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

네임스페이스 서버 간에 일관된 도메인 기반 네임스페이스를 유지 관리하려면 네임스페이스 서버가 AD DS(Active Directory Domain Services)를 정기적으로 폴링하여 최신 네임스페이스 데이터를 가져와야 합니다. 

## <a name="to-optimize-namespace-polling"></a>네임스페이스 폴링을 최적화하려면

다음 절차를 사용하여 네임스페이스 폴링이 발생하는 방법을 최적화할 수 있습니다.

1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **DFS 관리**를 클릭합니다.

2.  콘솔 트리의 **네임스페이스** 노드에서 도메인 기반 네임스페이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

3.  **고급** 탭에서 네임스페이스를 일관성 또는 확장성을 위해 최적화할지 선택합니다.

    -   네임스페이스를 호스트하는 네임스페이스 서버가 16개 이하인 경우에는 **일관성을 위한 최적화**를 선택합니다.
    -   네임스페이스 서버가 16개보다 많은 경우에는 **확장성을 위한 최적화**를 선택합니다. 이 경우 PDC(주 도메인 컨트롤러) 에뮬레이터의 로드가 감소되지만, 모든 네임스페이스 서버에 복제할 네임스페이스를 변경하는 데 필요한 시간은 늘어납니다. 변경 내용이 모든 서버에 복제될 때까지 사용자에게 표시되는 네임스페이스 내용이 다를 수 있습니다.

> [!NOTE]
> Windows PowerShell을 사용하여 네임스페이스 폴링 모드를 설정하려면 Windows Server 2012에서 도입된 [Set-DfsnRoot EnableRootScalability](https://technet.microsoft.com/library/jj884281.aspx) cmdlet을 사용합니다.

## <a name="see-also"></a>참고 항목

-   [DFS 네임스페이스 조정](tuning-dfs-namespaces.md)
-   [DFS 네임스페이스에 대한 관리 권한 위임](delegate-management-permissions-for-dfs-namespaces.md)