---
title: 암호 개요
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f608960e-2039-4c91-9c8c-9b81053c675e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 6c1b8d56b5c0da738e7dae5c0072be81040f90d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869604"
---
# <a name="passwords-overview"></a>암호 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IT 전문가 위한이 항목에서는 Windows 운영 체제 및 설명서 및 자격 증명 관리 전략에서의 암호를 사용 하는 방법에 대 한 토론에 대 한 링크에서 사용 되는 암호를 설명 합니다.

## <a name="BKMK_OVER"></a>기능 설명
운영 체제 및 응용 프로그램에 현재 암호 관련 설계 됩니다 및 스마트 카드 또는 생체 인식 시스템을 사용 하는 경우에 여전히 모든 계정에는 암호가 여전히 사용할 수에 따라서는 합니다. 일부 계정, 서비스를 실행 하는 데 사용 된 계정에 특히 스마트 카드 및 생체 인식 토큰에도 사용할 수 없습니다 하 고 따라서 인증 하는 암호를 사용 해야 합니다. Windows 암호화 해시를 사용 하 여 암호를 보호 합니다.

Windows 암호에 대 한 자세한 내용은 참조 하세요. [암호 기술 개요](https://technet.microsoft.com/library/hh994558(WS.10).aspx)합니다.

## <a name="BKMK_APP"></a>실제 응용 프로그램
Windows 및 다른 여러 운영 체제에서 사용자의 id를 인증 하기 위한 가장 일반적인 방법은 비밀 암호 또는 암호를 사용 하는 것입니다. 보안 네트워크 환경에 모든 사용자가 강력한 암호를 사용 하는 필요 합니다. 이 수동 메서드를 통해 여부 또는 도구를 사용 하 여 손상 된 사용자 계정의 자격 증명을 획득 하 여 취약 한 암호를 추측 하는 악의적인 사용자의 위협 방지 됩니다. 관리자 계정에 특히 그렇습니다. 정기적으로 복잡 한 암호를 변경한 경우에 해당 계정을 손상 시 키 지 암호 공격의 가능성이 줄어듭니다.

## <a name="BKMK_NEW"></a>새로운 기능과 변경 된 기능
Windows Server 2012 및 Windows 8에서 그림 암호는 새 합니다. 사진 암호는 일련의 제스처와 결합 되어 사용자 선택한 이미지의 조합입니다. 도메인에서 그림 암호 기능이 해제 된\-컴퓨터를 가입 합니다. 사진 암호에 대 한 자세한 정보에 대 한 링크에 나와 [참고](#BKMK_LINKS) 아래.

Windows Server 2012 및 Windows 8의 암호 기능 변경 되지 않았습니다. 새 그룹 정책 설정이 추가 되었습니다. 그러나 향상 된 기능 및 향상 된 기능에서에서 변경 된 자격 증명 \(및 암호\) 관리 사진 암호, 자격 증명 보관 및 Microsoft 계정을 사용 하 여 Windows 8에 로그인을 사용 하 여 이전의 Windows Live ID와 같은 .

## <a name="BKMK_DEP"></a>사용 되지 않는 기능
Windows Server 2012 및 Windows 8 되지 암호 기능이 없습니다.

## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항
엔터프라이즈 환경에서 암호는 일반적으로 Active Directory Domain Services를 사용 하 여 관리 됩니다. 로컬 보안 설정, 계정 정책은 암호 정책에는 설정을 사용 하 여 로컬 컴퓨터의 암호를 관리할 수도 있습니다.

## <a name="BKMK_LINKS"></a>참고 항목
이 표에 암호 기능에 대 한 추가 리소스가 나와 기술 및 자격 증명 관리 합니다.

|콘텐츠 형식|참조|
|--------|-------|
|**시나리오 설명서**|[디지털 id 보호](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)|
|**작업**|[Active Directory 사용자 및 컴퓨터](https://technet.microsoft.com/library/cc754217.aspx)|
|**문제 해결**|[암호가 만료 된 경우에 대해 알아보세요 \- Active Directory PowerShell 블로그](http://blogs.msdn.com/b/adpowershell/archive/2010/08/09/9970198.aspx)|
|**보안**| Windows Server 2008 R2 및 Windows 7 [위협 및 대책 가이드: 계정 정책](https://technet.microsoft.com/library/hh125920(v=ws.10).aspx)<br /><br />지침을 [변경 하 고 강력한 암호 만들기](https://www.microsoft.com/security/online-privacy/passwords-create.aspx)|
|**도구 및 설정**|[Windows 및 Microsoft 다운로드 센터에서 Windows Server 용 그룹 정책 설정 참조](https://www.microsoft.com/download/en/details.aspx?amp;displaylang=en&displaylang=en&id=25250)|
|**커뮤니티 리소스**|[디지털 id 보호](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)<br /><br />[Windows Live ID 사용 하 여 Windows 8에 로그인](http://blogs.msdn.com/b/b8/archive/2011/09/26/signing-in-to-windows-8-with-a-windows-live-id.aspx)<br /><br />[그림 암호 로그인](http://blogs.msdn.com/b/b8/archive/2011/12/16/signing-in-with-a-picture-password.aspx)<br /><br />[그림 암호 보안을 최적화](http://blogs.msdn.com/b/b8/archive/2011/12/19/optimizing-picture-password-security.aspx)|


