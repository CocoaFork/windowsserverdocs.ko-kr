---
title: Windows server 2016를 Windows Server 2019로 업그레이드 | Microsoft Docs
description: Windows Server 2016에서 Windows Server 2019로 이동 하는 전체 업그레이드를 수행 하는 방법에 대해 알아봅니다.
ms.prod: windows server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/16/2019
ms.openlocfilehash: 99133f2c582b180f240740fc2f39e99527bc0cf8
ms.sourcegitcommit: 27f0caf74e88781054250455c3c1adf06deb6234
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71124823"
---
# <a name="upgrade-windows-server-2016-to-windows-server-2019"></a>Windows server 2016을 Windows Server 2019로 업그레이드

서버를 평면화 하지 않고 이미 설정한 동일한 하드웨어 및 모든 서버 역할을 유지 하려는 경우에는 전체 업그레이드를 수행 하는 것이 좋습니다. 전체 업그레이드를 사용 하면 이전 운영 체제에서 최신 버전으로 전환 하는 동시에 설정, 서버 역할 및 데이터를 그대로 유지할 수 있습니다. 이 문서는 Windows Server 2016에서 Windows Server 2019로 이동 하는 데 도움이 됩니다.

## <a name="before-you-begin-your-in-place-upgrade"></a>전체 업그레이드를 시작 하기 전에

Windows Server 업그레이드를 시작 하기 전에 진단 및 문제 해결을 위해 장치에서 일부 정보를 수집 하는 것이 좋습니다. 이 정보는 업그레이드가 실패 하는 경우에만 사용할 수 있으므로 장치에서 정보를 가져올 수 있는 위치에 저장 해야 합니다.

### <a name="to-collect-your-info"></a>정보를 수집 하려면

1. 명령 프롬프트를 열고로 `c:\Windows\system32`이동한 다음 **printbrm.exe**를 입력 합니다.

2. 결과 시스템 정보를 장치 어딘가에 복사 하 여 붙여넣고 저장 합니다.

3. 명령 프롬프트에 **ipconfig/all** 을 입력 한 다음 결과 구성 정보를 복사 하 여 위와 동일한 위치에 붙여 넣습니다.

4. 레지스트리 편집기를 열고 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion hive로 이동한 다음 Windows Server **Buildlabex** (버전) 및 **EditionID** (버전)를 위와 동일한 위치에 복사 하 여 붙여 넣습니다.

모든 Windows Server 관련 정보를 수집한 후에는 운영 체제, 앱 및 가상 컴퓨터를 백업 하는 것이 좋습니다. 또한 서버에서 현재 실행 중인 모든 가상 컴퓨터를 **종료**하거나, **신속**하 게 마이그레이션하거나, **실시간으로 마이그레이션해야** 합니다. 전체 업그레이드 중에는 가상 컴퓨터를 실행할 수 없습니다.

## <a name="to-perform-the-upgrade"></a>업그레이드를 수행 하려면

1. **Buildlab ex** 값이 Windows Server 2016를 실행 하 고 있는지 확인 합니다.

2. Windows Server 2019 설치 미디어를 찾은 **다음 setup.exe를 선택 합니다**.

    ![Setup.exe 파일을 보여 주는 Windows 탐색기](media/upgrade-2016-2019/setup-2019.png)

3. **예** 를 선택 하 여 설치 프로세스를 시작 합니다.

    ![설치 프로그램을 시작할 수 있는 권한을 요청 하는 사용자 계정 컨트롤](media/upgrade-2016-2019/start-setup-uac-box.png)

4. 인터넷에 연결 된 장치의 경우 **다운로드 업데이트, 드라이버 및 선택적 기능 (권장)** 옵션을 선택 하 고 **다음**을 선택 합니다.

    ![중요 한 Windows 업데이트를 얻기 위해 온라인으로 전환 하도록 선택 하는 화면](media/upgrade-2016-2019/online-updates-win-setup.png)

5. 설치 프로그램에서 장치 구성을 확인 하 고, 작업이 완료 될 때까지 기다렸다가 **다음**을 선택 합니다.

6. Windows Server 미디어를 받은 배포 채널 (일반 정품, 볼륨 라이선스, OEM, ODM 등)과 서버 라이선스에 따라 라이선스 키를 입력 하 여 계속 하 라는 메시지가 표시 될 수 있습니다.

7. 설치 하려는 Windows Server 2019 버전을 선택 하 고 **다음**을 선택 합니다.

    ![설치할 Windows Server 2016 버전을 선택 하는 화면](media/upgrade-2016-2019/select-os-edition.png)

8. **동의** 함을 선택 하 여 배포 채널 (예: 소매, 볼륨 라이선스, OEM, ODM 등)에 따라 사용권 계약의 약관에 동의 합니다.

    ![사용권 계약에 동의 하는 화면](media/upgrade-2016-2019/license-terms.png)

9. **개인 파일 및 앱 유지** 를 선택 하 여 전체 업그레이드를 선택한 후 **다음**을 선택 합니다.

    ![설치 유형을 선택 하는 화면](media/upgrade-2016-2019/choose-install-upgrade.png)

10. 설치 프로그램에서 장치를 분석 한 후 **설치**를 선택 하 여 업그레이드를 계속할지 묻는 메시지를 표시 합니다.

    ![업그레이드를 시작할 준비가 되었음을 보여 주는 화면](media/upgrade-2016-2019/ready-to-install.png)

    현재 위치의 업그레이드를 시작 하 여 진행 중인 **Windows 업그레이드** 화면을 보여 줍니다. 업그레이드가 완료 되 면 서버가 다시 시작 됩니다.

    ![업그레이드 진행률을 보여 주는 화면](media/upgrade-2016-2019/upgrading-windows-with-progress.png)

## <a name="after-your-upgrade-is-done"></a>업그레이드가 완료 된 후

업그레이드가 완료 되 면 Windows Server 2019로의 업그레이드가 성공 했는지 확인 해야 합니다.

### <a name="to-make-sure-your-upgrade-was-successful"></a>업그레이드에 성공 했는지 확인 하려면

1. 레지스트리 편집기를 열고 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion hive로 이동 하 여 **ProductName**을 봅니다. Windows server 2019 **Datacenter와 2019**같은 windows server 버전이 표시 되어야 합니다.

2. 모든 응용 프로그램이 실행 중이 고 응용 프로그램에 대 한 클라이언트 연결이 성공적인 지 확인 합니다.

업그레이드 하는 동안 문제가 발생할 수 있다고 생각 되는 `%SystemRoot%\Panther` 경우 (일반적으로 `C:\Windows\Panther`) 디렉터리를 복사 하 여 압축 하 고 Microsoft 지원에 문의 하세요.

## <a name="related-articles"></a>관련 문서

- Windows Server 2019에 대 한 자세한 내용 및 정보는 [Windows server 2019 시작](https://docs.microsoft.com/windows-server/get-started-19/get-started-19)을 참조 하세요.