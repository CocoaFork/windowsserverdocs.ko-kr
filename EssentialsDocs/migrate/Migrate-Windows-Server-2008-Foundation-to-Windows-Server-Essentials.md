---
title: Windows Server 2008 Foundation에서 Windows Server Essentials로 마이그레이션
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f22fc0a4-cb82-4e60-afe6-2d03145745e7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 22721833d3ba97c7860c949764d565415bbc7cab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813764"
---
# <a name="migrate-windows-server-2008-foundation-to-windows-server-essentials"></a>Windows Server 2008 Foundation에서 Windows Server Essentials로 마이그레이션

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 가이드에서는 기존 Windows Server 2008 Foundation 도메인을 새 하드웨어의 Windows Server® 2012 Essentials로 마이그레이션하는 방법을 설명 하 고 마이그레이션한 다음 설정 및 데이터를 합니다. 이 가이드에는 마이그레이션을 완료 한 후 Windows Server Essentials 네트워크에서 기존 서버를 제거 하는 방법을 설명 합니다.  
  
> [!NOTE]
>  마이그레이션하는 동안 문제를 방지 하려면 Windows Server Essentials 제품 개발 팀의 마이그레이션을 시작 하기 전에이 문서를 읽기을 적극 권장 합니다.  
  
## <a name="additional-resources"></a>추가 자료  
 마이그레이션 프로세스에 도움이 되는 추가 정보, 도구 및 커뮤니티 리소스에 대한 링크는 [Windows Small Business Server 마이그레이션](https://go.microsoft.com/fwlink/?LinkId=217520)을 참조하세요.  
  
## <a name="terms-and-definitions"></a>용어 및 정의  
 **원본 서버:** 이 기존 서버에서 설정 및 데이터를 마이그레이션합니다.  
  
 **대상 서버:** 이 새 서버로 설정 및 데이터를 마이그레이션합니다.  
  
## <a name="migration-process-summary"></a>마이그레이션 프로세스 요약  
 이 마이그레이션 가이드는 다음 단계로 이루어집니다.  
  

1.  [Windows Server Essentials의 원본 서버에 대 한 마이그레이션을 준비](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)합니다.  원본 서버 및 네트워크가 마이그레이션할 준비가 되었는지 확인해야 합니다. 이 섹션에서는 원본 서버를 백업하고, 원본 서버 시스템 상태를 평가하고, 최신 서비스 팩 및 수정 프로그램을 설치하고, 네트워크 구성을 확인하는 과정을 안내합니다.  
  
2.  [마이그레이션 모드로 Windows Server Essentials 설치](Install-Windows-Server-Essentials-in-migration-mode.md)합니다.  이 섹션에서는 마이그레이션 모드에서 대상 서버에서 Windows Server Essentials를 설치 하는 위해 수행 해야 하는 단계를 설명 합니다.  
  
3.  [새 Windows Server Essentials 네트워크에 컴퓨터 연결](Join-computers-to-the-new-Windows-Server-Essentials-network.md)합니다.  이 섹션에서는 새 Windows Server Essentials 네트워크 및 그룹 정책 설정을 업데이트 하려면 클라이언트 컴퓨터를 가입을 다룹니다.  
  
4.  [대상 서버에서 Windows Server 2008 Foundation 설정 및 데이터 이동](Move-Windows-Server-2008-Foundation-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  이 섹션에서는 원본 서버에서 데이터 및 설정을 마이그레이션하는 방법에 대한 정보를 제공합니다.  
  
5.  [수준 내리기 및 새 Windows Server Essentials 네트워크에서 원본 서버 제거](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)합니다.  네트워크에서 원본 서버를 제거하기 전에 그룹 정책을 강제로 업데이트하고 원본 서버의 수준을 내려야 합니다.  
  
6.  [Windows Server Essentials 마이그레이션을 위한 마이그레이션 후 작업 수행](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md)합니다.  모든 설정 및 데이터를 Windows Server Essentials로 마이그레이션를 마친 후에 사용자 계정에 허용 되는 컴퓨터를 매핑하는 것이 좋습니다.  
  
7.  [Windows Server Essentials 모범 사례 분석기 실행](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)합니다.  마이그레이션 설정 및 데이터를 Windows Server Essentials를 마친 후 Windows Server Essentials BPA를 실행 해야 합니다.  

1.  [Windows Server Essentials의 원본 서버에 대 한 마이그레이션을 준비](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)합니다.  원본 서버 및 네트워크가 마이그레이션할 준비가 되었는지 확인해야 합니다. 이 섹션에서는 원본 서버를 백업하고, 원본 서버 시스템 상태를 평가하고, 최신 서비스 팩 및 수정 프로그램을 설치하고, 네트워크 구성을 확인하는 과정을 안내합니다.  
  
2.  [마이그레이션 모드로 Windows Server Essentials 설치](../migrate/Install-Windows-Server-Essentials-in-migration-mode.md)합니다.  이 섹션에서는 마이그레이션 모드에서 대상 서버에서 Windows Server Essentials를 설치 하는 위해 수행 해야 하는 단계를 설명 합니다.  
  
3.  [새 Windows Server Essentials 네트워크에 컴퓨터 연결](../migrate/Join-computers-to-the-new-Windows-Server-Essentials-network.md)합니다.  이 섹션에서는 새 Windows Server Essentials 네트워크 및 그룹 정책 설정을 업데이트 하려면 클라이언트 컴퓨터를 가입을 다룹니다.  
  
4.  [대상 서버에서 Windows Server 2008 Foundation 설정 및 데이터 이동](../migrate/Move-Windows-Server-2008-Foundation-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  이 섹션에서는 원본 서버에서 데이터 및 설정을 마이그레이션하는 방법에 대한 정보를 제공합니다.  
  
5.  [수준 내리기 및 새 Windows Server Essentials 네트워크에서 원본 서버 제거](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)합니다.  네트워크에서 원본 서버를 제거하기 전에 그룹 정책을 강제로 업데이트하고 원본 서버의 수준을 내려야 합니다.  
  
6.  [Windows Server Essentials 마이그레이션을 위한 마이그레이션 후 작업 수행](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md)합니다.  모든 설정 및 데이터를 Windows Server Essentials로 마이그레이션를 마친 후에 사용자 계정에 허용 되는 컴퓨터를 매핑하는 것이 좋습니다.  
  
7.  [Windows Server Essentials 모범 사례 분석기 실행](../migrate/Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)합니다.  마이그레이션 설정 및 데이터를 Windows Server Essentials를 마친 후 Windows Server Essentials BPA를 실행 해야 합니다.  

  
 일부 마이그레이션 절차에서는 관리자 권한으로 명령 프롬프트 창을 열어야 합니다.  
  
###  <a name="BKMK_OpenACommandPromptAsAdmin"></a> 관리자로 원본 서버에서 명령 프롬프트 창을 열려면  
  
1.  **시작**을 클릭합니다.  
  
2.  검색 상자에 **cmd**를 입력합니다.  
  
3.  결과 목록에서 **cmd**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>대상 서버에서 관리자 권한으로 명령 프롬프트 창을 열려면  
  
1.  **시작** 화면의 검색 상자에 **cmd**를 입력합니다.  
  
2.  결과 목록에서 **cmd**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.
