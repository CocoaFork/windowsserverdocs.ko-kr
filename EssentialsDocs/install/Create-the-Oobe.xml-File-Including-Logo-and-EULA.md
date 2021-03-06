---
title: 로고 및 EULA를 포함한 Oobe.xml 파일 만들기
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a7b3cc1-21bb-4344-8110-f5d5959b370d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 5d7dac41ba6d6f73b0d3d65d3481fe45ff99a6bc
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433615"
---
# <a name="create-the-oobexml-file-including-logo-and-eula"></a>로고 및 EULA를 포함한 Oobe.xml 파일 만들기

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Oobe.xml 파일을 사용하여 초기 구성에 사용자 고유의 EULA(최종 사용자 사용권 계약)를 추가할 수 있습니다. Oobe.xml은 초기 구성, Windows 시작 및 최종 사용자에게 나타나는 기타 페이지에 대한 텍스트와 이미지를 제공하기 위해 사용되는 파일입니다. 여러 Oobe.xml 파일을 추가하여 최종 사용자의 언어와 국가 또는 지역 선택 사항을 기반으로 내용을 사용자 지정할 수 있습니다. 자세한 내용은 [Windows 8용 Windows Assessment and Deployment Kit](https://go.microsoft.com/fwlink/?LinkId=248694) 문서를 참조하세요.  
  
 Microsoft EULA 외에도 사용자가 근무하는 회사의 EULA가 표시됩니다. Microsoft EULA는 초기 구성 최종 사용자 환경에서 처음으로 표시되는 EULA이며, 그 다음에 사용자의 EULA가 표시됩니다. EULA는 서버의 아무 위치에서든지 표시할 수 있으며 Oobe.xml 파일에서 그 위치를 지정합니다.  
  
#### <a name="to-add-your-company-eula-and-logo"></a>회사 EULA 및 로고를 추가하려면  
  
1. Oobe.xml 파일을 메모장과 같은 텍스트 편집기에서 엽니다.  
  
2. 내에서 < /logopath&gt\>< / /logopath&gt\> 태그에 로고 파일의 절대 경로 입력 합니다. 이 파일에는 240 x 100 픽셀의 32비트 .png(이동 네트워크 그래픽) 파일이 있어야 합니다.  
  
3. 내에서 < /eulafilename&gt\>< / /eulafilename&gt\> 태그에 EULA 파일의 절대 경로 입력 합니다. EULA 파일은 서식 있는 텍스트(.rtf) 파일이어야 합니다.  
  
4. 내에서 < 이름\>< / 이름\> 태그에 회사 이름을 입력 합니다.  
  
    다음 예제에서는 Oobe.xml 파일의 태그를 보여 줍니다.  
  
   ```  
  
   <FirstExperience>  
      <oobe>  
         <oem>  
            <name>Fabrikam</name>  
            <logopath>c:\fabrikam\fabrikam.png</logopath>  
            <eulafilename>c:\fabrikam\fabrikam_eula.rtf</eulafilename>  
         </oem>  
      </oobe>  
   </FirstExperience>  
  
   ```  
  
5. 파일을 저장합니다.  
  
6. Oobe.xml 파일을 다음 위치 중 한 곳에 배치합니다.  
  
   |Oobe.xml 위치|위치를 결정하는 조건|  
   |-----------------------|----------------------------------------|  
   |%windir%\system32\oobe\info\|서버는 단일 국가/지역 및 단일 언어 시스템으로 배송 됩니다.|  
   |%windir%\system32\oobe\info\default\\<language\>|서버는 단일 국가/지역 및 다중 언어 시스템으로 배송됩니다.|  
   |%windir%\system32\oobe\info\\< 국가/지역 > \ 및 %windir%\system32\oobe\info\\< 국가/지역 >\\< 언어\>\|서버는 둘 이상의 국가로 배송 됩니다 / 설정과 지역을 단일 언어를 사용 하 여 각 국가/지역 단위로 사용자 지정 해야합니다. 여기서 < 국가/지역 > 국가 또는 지역의 위치 서버를 배포의 지리적 위치 식별자 (GeoID)의 10 진수 버전은 및 < 언어\> 는 LCID (로캘 식별자)의 10 진수 버전입니다.|  
  
   배경이 파란색이므로 흰색 텍스트로 된 대체 회사 로고가 있다면 그 로고가 설정 흐름에서 더 잘 표시될 수 있습니다.  선택적으로 레지스트리 키 및 값을 설정하여 이 로고를 지정할 수 있습니다.  
  
#### <a name="to-specify-a-company-logo-by-setting-the-oem-registry-key"></a>OEM 레지스트리 키를 설정하여 회사 로고를 지정하려면  
  
1.  서버에서 마우스를 화면 오른쪽 상단 구석으로 옮긴 후 **검색**을 클릭합니다.  
  
2.  검색 상자에 **regedit**를 입력하고 Regedit 응용 프로그램을 클릭합니다.  
  
3.  탐색 창에서  **HKEY_LOCAL_MACHINE**으로 이동하여 **SOFTWARE**, **Microsoft**, **Windows Server**를 차례로 확장합니다. OEM 키가 없는 경우 다음과 같이 키를 만듭니다.  
  
    1.  **Windows Server**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **키**를 클릭합니다.  
  
    2.  키 이름에 **OEM**을 입력합니다.  
  
4.  (옵션) 로고에 대한 항목을 만들 경우 여러 키를 만들어 로고의 언어 버전을 구분할 수 있습니다. 예를 들어 로고의 영어 버전과 독일어 버전을 모두 보유한 경우 en-us 키와 de-de 키를 만들 수 있습니다. 로고 파일은 모두 동일한 폴더에 저장되므로 각 언어별로 고유한 이름을 사용하여 로고 이미지 파일의 인스턴스를 제공해야 합니다. 예를 들어 LogoWithWhiteText_en.png 및 LogoWithWhiteText_de.png라는 파일을 만들 수 있습니다.  
  
5.  **OEM**을 마우스 오른쪽 단추로 클릭하거나 적절한 언어 키를 마우스 오른쪽 단추로 클릭하고, **새로 만들기**를 클릭한 다음 **문자열 값**을 클릭합니다.  
  
6.  문자열로 LogoWithWhiteText를 입력한 다음 Enter 키를 누릅니다.  
  
7.  새 문자열을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
8.  로고 이미지가 포함된 경로를 입력한 다음 확인을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Windows Server Essentials ADK 시작 하기](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)