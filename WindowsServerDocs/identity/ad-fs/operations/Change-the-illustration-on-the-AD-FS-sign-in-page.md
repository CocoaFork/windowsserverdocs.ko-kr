---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: AD FS 로그인 페이지에서 그림을 변경 합니다.
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a182b6243777d119394615008cee63b5e5a71ab8
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189955"
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>AD FS 로그인 페이지에서 그림을 변경 합니다.

## <a name="change-the-illustration"></a>그림을 변경 합니다.  


로그인에 표시 되는 왼쪽에서 그래픽 그림을 변경 하려면\-페이지에서 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  

![일러스트레이션 변경](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> 일러스트레이션 크기는 96dpi에서 1420x1080픽셀이고, 파일 크기는 200KB 이내인 것이 좋습니다.  
  
 
    Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}  

## <a name="additional-references"></a>추가 참조 
[AD FS 사용자 로그인 사용자 지정](AD-FS-user-sign-in-customization.md)  
  
  
