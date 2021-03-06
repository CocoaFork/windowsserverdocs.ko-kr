---
title: 웹 클라이언트 시작
description: 원격 데스크톱 웹 클라이언트에 로그인하는 방법을 설명합니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 08/27/2019
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: 6c37c28fded08ba68e46a10a534ee0269c714938
ms.sourcegitcommit: 89aea00fe0e00fc8b1a6e20af36ad04df8c9fe5b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/19/2019
ms.locfileid: "74189469"
---
# <a name="get-started-with-the-web-client"></a>웹 클라이언트 시작

원격 데스크톱 웹 클라이언트에서는 호환 웹 브라우저를 사용하여 관리자가 사용자에게 게시한 조직의 원격 리소스(앱 및 데스크톱)에 액세스할 수 있습니다. 어디에서 작업하는지 관계없이, 다른 데스크톱 PC로 전환하지 않고도 로컬 PC를 사용할 때처럼 원격 앱 및 데스크톱과 상호 작용할 수 있습니다. 관리자가 원격 리소스를 설정하면, 도메인, 사용자 이름, 암호 및 관리자가 보낸 URL과 지원되는 웹 브라우저만 있으면 계속 진행할 수 있습니다.

>[!NOTE]
>웹 클라이언트의 새 릴리스가 궁금하신가요? [원격 데스크톱 웹 클라이언트의 새로운 기능](web-client-whatsnew.md)을 확인하세요.

## <a name="what-youll-need-to-use-the-web-client"></a>웹 클라이언트를 사용하는 데 필요한 조건

* 웹 클라이언트의 경우 Windows, macOS, ChromeOS 또는 Linux를 실행하는 PC가 필요합니다. 현재 모바일 디바이스는 지원되지 않습니다.
* Microsoft Edge, Internet Explorer 11, Google Chrome, Safari 또는 Mozilla Firefox(v55.0 이상)와 같은 최신 브라우저
* 관리자가 보낸 URL

>[!NOTE]
>지금은 웹 클라이언트의 Internet Explorer 버전에 오디오가 없습니다.
>Safari는 브라우저의 크기가 조정되거나 전체 화면으로 여러 번 전환될 경우 회색 화면을 표시할 수 있습니다.

## <a name="start-using-the-remote-desktop-client"></a>원격 데스크톱 클라이언트 사용 시작

클라이언트에 로그인하려면 관리자가 보낸 URL로 이동합니다. 로그인 페이지에서 도메인 및 사용자 이름을 ```DOMAIN\username``` 형식으로 입력하고, 암호를 입력한 후 **로그인**을 선택합니다.

>[!NOTE]
>웹 클라이언트에 로그인하여 PC가 조직의 보안 정책을 준수한다는 데 동의합니다.

로그인한 후 클라이언트는 **모든 리소스** 탭으로 이동됩니다. 여기서 "작업 리소스" 그룹과 같은 하나 이상의 축소 가능한 그룹 아래에 모든 항목이 게시됩니다. 관리자가 작업 그룹에 사용할 수 있도록 지정한 앱, 데스크톱 또는 더 많은 앱 또는 데스크톱을 포함하는 그룹을 나타내는 여러 개의 아이콘이 표시됩니다. 언제든지 이 탭으로 돌아와 추가 리소스를 시작할 수 있습니다.

앱 또는 데스크톱 사용을 시작하려면 사용하려는 항목을 선택하고, 웹 클라이언트에 로그인할 때 사용한 것과 동일한 사용자 이름 및 암호를 입력하고(지정하도록 요구될 경우), **제출**을 선택합니다. 클립보드 및 프린터와 같은 로컬 리소스에 액세스하기 위한 동의 대화 상자도 표시될 수 있습니다. 이러한 항목을 리디렉션하지 않도록 선택하거나 **허용**을 선택하여 기본 설정을 사용 할 수 있습니다. 웹 클라이언트에서 연결을 설정할 때까지 기다린 후 평소와 같이 리소스를 사용하기 시작합니다.

작업이 끝나면 화면 상단에 있는 도구 모음에서 **로그아웃** 단추를 선택하거나 브라우저 창을 닫아 세션을 끝낼 수 있습니다.

## <a name="printing-from-the-remote-desktop-web-client"></a>원격 데스크톱 웹 클라이언트에서 인쇄

웹 클라이언트에서 인쇄하려면 다음 단계를 수행합니다.

1. 인쇄하려는 앱에서 일반적으로 수행하는 것처럼 인쇄 프로세스를 시작합니다.
2. 프린터를 선택하라는 메시지가 표시되면 **원격 데스크톱 가상 프린터**를 선택합니다.
3. 기본 설정을 선택한 후 **인쇄**를 선택합니다.
4. 브라우저는 인쇄 작업의 PDF 파일을 생성합니다.
5. PDF를 열고 해당 내용을 로컬 프린터로 인쇄하거나 나중에 사용하기 위해 사용자 PC에 저장하도록 선택할 수 있습니다.

## <a name="copy-and-paste-from-the-remote-desktop-web-client"></a>원격 데스크톱 웹 클라이언트에서 복사 및 붙여넣기

웹 클라이언트는 현재 텍스트만 복사 및 붙여넣을 수 있도록 지원합니다. 파일은 웹 클라이언트에서 복사 또는 붙여넣을 수 없습니다. 또한 텍스트를 복사하고 붙여넣을 때는 **Ctrl+C** 및 **Ctrl+V**만 사용할 수 있습니다.

## <a name="use-an-input-method-editor-ime-in-the-remote-session"></a>원격 세션에서 IME(입력기) 사용

입력기를 사용하여 복잡한 문자를 원격 세션에 입력하려면 탐색 모음에서 톱니바퀴 아이콘을 선택하여 **설정** 측면 패널을 열고 **입력기 사용** 스위치를 **켜기**로 설정합니다. 입력기가 설치되었고 원격 세션에서 활성화되어 있어야 합니다. 

## <a name="get-help-with-the-web-client"></a>웹 클라이언트에 대한 도움 받기

이 문서의 정보로 해결할 수 없는 문제가 발생한 경우 웹 클라이언트의 정보 페이지에 있는 주소로 이메일을 보내 웹 클라이언트에 대한 도움을 얻을 수 있습니다.
