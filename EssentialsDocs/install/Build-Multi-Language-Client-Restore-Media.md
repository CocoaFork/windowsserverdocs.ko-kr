---
title: 다국어 클라이언트 복원 미디어 제작
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fdbc016-d464-43cb-bd75-8a63e61588a2
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1ad934d297c3092050bd6adbb6bb0f50d1ec6f36
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879874"
---
# <a name="build-multi-language-client-restore-media"></a>다국어 클라이언트 복원 미디어 제작

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

> [!NOTE]
>  에 설명 된 대로 다국어 Windows 이미지를 먼저 만들어야 합니다를 [연습: 다국어 Windows 이미지 만들기](https://technet.microsoft.com/library/jj126995) Windows Server Essentials 언어 팩을 install.wim에 추가 하기 전에 합니다.  
  
 다국어 서버 설치 DVD를 만들 때 Server install.wim에 대한 언어 팩이 설치됩니다. 복원 마법사를 위한 지역화된 리소스가 언어 팩의 일부로서 설치됩니다.  
  
### <a name="to-build-a-multi-language-client-restore-media"></a>다국어 클라이언트 복원 미디어를 만들려면  
  
1.  install.wim을 c:\mount에 마운트합니다. c:\mount\Program Files\Windows Server\bin\ClientRestore 폴더를 클라이언트 복원 미디어의 루트라고 합니다(아래의 [RestoreMediaRoot]).  
  
    ```  
    dism /mount-wim /wimfile:install.wim /index:1 /mountdir:c:\mount  
    ```  
  
2.  클라이언트 복원 WIM 파일을 [RestoreMediaRoot]\Sources\Boot.wim(boot_x86.wim 파일도 동일한 단계 적용 )에 탑재합니다. 명령줄은 다음과 같습니다.  
  
    ```  
    dism /mount-wim /wimfile:boot.wim /index:1 /mountdir:c:\mountRestore  
    ```  
  
3.  다음을 실행하여 WinPE-Setup.cab 패키지를 복원 미디어에 추가합니다.  
  
    ```  
    dism /image:c:\mountRestore /add-package /packagepath:WinPE-Setup.cab  
    ```  
  
4.  메모장을 사용하여 c:\mountRestore\windows\system32\winpeshl.ini를 다음 내용으로 편집합니다.  
  
    ```  
    [LaunchApp]  
    AppPath = %SYSTEMDRIVE%\sources\SelectLanguage.exe  
    ```  
  
5.  복원 미디어에 언어 팩을 추가합니다. 다음 명령을 실행하여 언어 팩을 추가할 수 있습니다.  
  
    ```  
    dism /image:c:\mountRestore /add-package /packagepath:[language pack path]  
    ```  
  
     다음 언어 팩을 추가해야 합니다.  
  
    1.  WinPE 언어 팩(lp.cab)  
  
    2.  WinPE-Setup 언어 팩(WinPE-Setup_[lang].cab(예: WinPE-Setup_en-us.cab))  
  
    3.  zh-cn, zh-tw, zh-hk, ko-kr, ja-jp를 포함한 아시아 글꼴의 경우 추가 글꼴 팩 설치가 필요합니다(winpe-fontsupport-[lang].cab - 예: winpe-fontsupport-zh-cn.cab).  
  
6.  다음을 실행하여 새로운 Lang.ini 파일을 만듭니다.  
  
    ```  
    dism /image:c:\mountRestore /Gen-LangINI /distribution:mount  
    ```  
  
7.  다음을 실행하여 이미지를 커밋하고 탑재 해제합니다.  
  
    ```  
    dism /unmount-wim /mountdir:c:\mountRestore /commit  
    ```  
  
8.  [RestoreMediaroot]\Sources\Boot_x86.wim에 대해 2~7단계를 반복합니다.  
  
9. 다음을 실행하여 이미지를 커밋하고 탑재 해제합니다.  
  
    ```  
    dism /unmount-wim /mountdir:c:\mount /commit  
    ```  
  
## <a name="see-also"></a>관련 항목  

 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)

 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](../install/Additional-Customizations.md)   
 [배포용 이미지 준비](../install/Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](../install/Testing-the-Customer-Experience.md)

