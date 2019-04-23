---
title: winnt32
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a0a6fb3-ba4e-4ace-8984-7f6d3875560e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 28675ac6d5a1f1a7f56a9b72ef11a3e99e4ed130
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851264"
---
# <a name="winnt32"></a>winnt32

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server 2003에서의 설치 또는 제품 업그레이드를 수행합니다. 실행할 수 있습니다 **winnt32** Windows Server 2003에서 Windows 95, Windows 98, Windows Millennium edition, Windows NT, Windows 2000, Windows XP 또는 제품을 실행 하는 컴퓨터에서 명령 프롬프트에서. 실행 하는 경우 **winnt32** Windows NT 버전 4.0 실행 하는 컴퓨터에 먼저 적용 해야 서비스 팩 5 개 이상 있습니다.
## <a name="syntax"></a>구문
```
winnt32 [/checkupgradeonly] [/cmd: <CommandLine>] [/cmdcons] [/copydir:{i386|ia64}\<FolderName>] [/copysource: <FolderName>] [/debug[<Level>]:[ <FileName>]] [/dudisable] [/duprepare: <pathName>] [/dushare: <pathName>] [/emsport:{com1|com2|usebiossettings|off}] [/emsbaudrate: <BaudRate>] [/m: <FolderName>]  [/makelocalsource] [/noreboot] [/s: <Sourcepath>] [/syspart: <DriveLetter>] [/tempdrive: <DriveLetter>] [/udf: <ID>[,<UDB_File>]] [/unattend[<Num>]:[ <AnswerFile>]]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/checkupgradeonly|Windows Server 2003에서 제품으로 업그레이드 호환성을 위해 컴퓨터를 확인합니다.<br /><br />이 옵션을 사용 하는 경우 **/unattend**에 없는 사용자 입력이 필요 합니다.  그렇지 않으면, 화면에 결과가 표시 됩니다 하 고 지정한 파일 이름으로 저장할 수 있습니다. 기본 파일 이름은 **upgrade.txt** systemroot 폴더에 있습니다.|
|/cmd|설치 프로그램의 최종 단계 전에 특정 명령을 실행 하는 설치 하도록 지시 합니다. 이 컴퓨터를 다시 시작한 후 설치가 완료 된 후 필요한 구성 정보를 수집 했습니다 생기기 전에 발생 합니다.|
|\<CommandLine>|설치 프로그램의 최종 단계 전에 수행 하도록 명령줄을 지정 합니다.|
|/cmdcons|X86 기반 컴퓨터에서 시작 옵션으로 복구 콘솔을 설치합니다.  복구 콘솔은 명령줄 인터페이스는 시작 서비스를 중지 하 고 로컬 드라이브 (NTFS로 포맷 된 드라이브 포함)에 액세스 하는 등의 작업을 수행할 수 있습니다. 사용할 수 있습니다.는 **/cmdcons** 설치가 완료 된 후 옵션입니다.|
|/copydir|운영 체제 파일이 설치 되는 폴더 내에 추가 폴더를 만듭니다.  예를 들어, x86 및 x64 기반 컴퓨터를 만들 수 있습니다 라는 폴더 *Private_drivers* 프로그램 설치 및 폴더에 드라이버 파일에 대 한 i386 원본 폴더 내에서. 형식 **/copydir:i386\\* * * Private_drivers* 설치 프로그램을 해당 폴더에 새로 설치 된 컴퓨터에 새 폴더 위치로 복사할 **systemroot** \\*Private_drivers * 합니다.<br /><br />-   **i386** i386를 지정 합니다.<br />-   **ia64** ia64를 지정 합니다.<br /><br />사용할 수 있습니다 **/copydir** 원하는 만큼의 추가 폴더를 만듭니다.|
|\<FolderName>|사이트에 대 한 수정 내용을 저장 하기 위해 만든 폴더를 지정 합니다.|
|/copysource|운영 체제 파일이 설치 되는 폴더 내에 있는 임시 추가 폴더를 만듭니다. 사용할 수 있습니다 **/copysource** 원하는 만큼의 추가 폴더를 만듭니다.<br /><br />폴더와 달리 **/copydir** 만듭니다, **/copysource** 폴더는 설치가 완료 된 후 삭제 됩니다.|
|/debug|예를 들어 지정 하는 수준에서 디버그 로그를 만듭니다 **/debug4:debug.log**합니다.  기본 로그 파일은 **C:\ systemroot\winnt32.log**, 및|
|\<level>|수준 값 및 설명<br /><br />-   0: 심각한 오류<br />-   1: 오류<br />-   2: 기본 수준입니다. 경고<br />-   3: 정보<br />-4: 자세한 디버깅 정보<br /><br />각 수준은 그 아래의 단계를 포함합니다.|
|dudisable /|동적 업데이트를 실행할 수 없습니다. 동적 업데이트를 하지 않고 설치 프로그램은 원래의 설치 파일에만 실행 됩니다. 응답 파일을 사용 하 고 해당 파일에서 동적 업데이트 옵션을 지정 하는 경우에이 옵션에서 동적 업데이트를 비활성화 합니다.|
|/duprepare|Windows Update 웹 사이트에서 다운로드 한 동적 업데이트 파일을 사용할 수 있도록 설치 공유에서 준비 작업을 수행 합니다. 그런 다음이 공유 여러 클라이언트에 대 한 Windows XP를 설치 하는 데 사용할 수 있습니다.|
|\<pathName>|전체 경로 이름을 지정합니다.|
|/dushare|Windows 업데이트 웹 사이트에서 이전에 실행 하는 한 공유는 이전에 다운로드 한 동적 업데이트 파일 (설치 프로그램을 사용에 대 한 업데이트 된 파일)를 지정 **/duprepare: * * * < 경로 >* 합니다. 클라이언트를 실행 하는 경우 지정 하면 클라이언트 설치 하면 업데이트 된 파일에 지정 된 공유에 사용할 <pathName>합니다.|
|/emsport|사용 하거나 설치 하는 동안 및 서버 운영 체제를 설치한 후 응급 관리 서비스를 사용 하지 않도록 설정 합니다. 응급 관리 서비스와 함께 로컬 키보드, 마우스 및 모니터는 네트워크를 사용할 수 없는 경우 등 일반적으로 해야 하는 긴급 상황에서 서버를 원격으로 관리할 수 또는 서버가 제대로 작동 하지 않습니다. 응급 관리 서비스에 특정 하드웨어 요구 사항, 있으며 Windows Server 2003에서 제품에 대해서만 사용할 수 있습니다.<br /><br />-   **com1** x86 기반 컴퓨터 (Itanium 아키텍처 기반 컴퓨터 아님)에 적용 됩니다.<br />-   **com2**x86 기반 컴퓨터 (Itanium 아키텍처 기반 컴퓨터 아님)에 적용 됩니다.<br />-기본값입니다. BIOS 직렬 포트 콘솔 리디렉션 (SPCR) 테이블 또는 Itanium 아키텍처 기반 시스템에 EFI 콘솔 장치 경로 통해 지정 된 설정을 사용 합니다. 지정 하는 경우 **usebiossettings** SPCR 테이블 또는 적절 한 EFI 콘솔의 장치 경로 응급 관리 해 서 사용할 수 있습니다.<br />-   **해제** 응급 관리 서비스를 사용 하지 않도록 설정 합니다. 나중에 부팅 설정을 수정 하 여 사용할 수 있습니다.|
|/emsbaudrate|x86 기반 컴퓨터에 대 한 응급 관리 서비스에 대 한 전송 속도 지정합니다. (옵션은 Itanium 아키텍처 기반 컴퓨터에 적용할 수 있습니다.) 함께 사용 해야 **/emsport:com1** 또는 **/emsport:com2** (그렇지 않으면  **/emsbaudrate** 무시 됩니다).|
|\<BaudRate>|9600의 전송 속도 지정 19200, 57600 또는 115200 합니다. 9600 기본값입니다.|
|/m|대체 위치에서 대체 파일을 복사 하는 설치 프로그램을 지정 합니다.  설치 프로그램이 대체 위치에 먼저 찾아보고 파일이 있으면, 대신 기본 위치에서 파일을 사용 하도록 지시 합니다.|
|/makelocalsource|설치 프로그램을 로컬 하드 디스크에 모든 설치 원본 파일을 복사 하도록 지시 합니다.  사용 하 여 **/makelocalsource** cd 설치에서 나중에 사용할 수 없는 경우 설치 파일을 제공 하는 cd에서 설치 하는 경우.|
|설정|설치 프로그램을 다른 명령을 실행할 수 있도록 설치 프로그램의 파일 복사 단계를 완료 한 후 컴퓨터를 다시 시작 하지 지시 합니다.|
|/s|설치에 대 한 파일의 원본 위치를 지정합니다. 파일 서버를 여러 개를 동시에 복사 하려면 입력 합니다 **/s:**\<Sourcepath > 여러 번 (최대 8) 옵션입니다. 옵션을 여러 번 입력 하는 경우 지정 된 첫 번째 서버를 사용할 수 있어야 하거나 설치에 실패 합니다.|
|\<Sourcepath>|전체 소스 경로 이름을 지정합니다.|
|/syspart|x86 기반 컴퓨터에서 수 하드 디스크에 설치 시작 파일을 복사, 디스크를 활성으로 표시 하 다음 디스크를 다른 컴퓨터에 설치를 지정 합니다. 해당 컴퓨터를 시작할 때 자동으로 설치 프로그램의 다음 단계를 시작 합니다.<br /><br />항상 사용 해야는 **/tempdrive** 매개 변수는 **/syspart** 매개 변수입니다.<br /><br />시작할 수 있습니다 **winnt32** 사용 하 여 합니다 **/syspart** Windows Server 2003에서 Windows NT 4.0, Windows 2000, Windows XP 또는 제품을 실행 하는 x86 기반 컴퓨터에 대 한 옵션입니다. 컴퓨터에서 Windows NT 버전 4.0 실행 중인 경우 서비스 팩 5 이상이 필요 합니다. Windows 95, Windows 98 또는 Windows Millennium edition 컴퓨터를 실행할 수 없습니다.|
|\<DriveLetter>|드라이브 문자를 지정합니다.|
|/tempdrive|설치 프로그램은 지정 된 파티션에 임시 파일을 전달 합니다.<br /><br />새 설치의 경우 서버 운영 체제를 지정 된 파티션에 설치 됩니다.<br /><br />업그레이드 된 **/tempdrive** 임시 파일에만 배치 하는 옵션에 영향을 줍니다; 운영 체제를 실행 하는 파티션에 업그레이드할 **winnt32**.|
|위한 /udf|식별자를 나타냅니다 (\<ID >)를 사용 하 여 고유성 UDB (Database) 파일에서 응답 파일을 수정 하는 방법 지정 (참조를 **/unattend** 옵션).  UDB 응답 파일의 값을 재정의 하 고 식별자 사용 되는 UDB 파일에는 값을 결정 합니다. 예를 들어 **/udf:RAS_user,Our_company.udb** Our_company.udb 파일의 RAS_user 식별자에 대해 지정 된 설정 보다 우선 합니다. 없으면 \<UDB_file >를 지정 하면 포함 된 디스크를 삽입 하 라는 메시지를 설치 합니다 **$Unique$.udb** 파일입니다.|
|\<ID>|고유성 UDB (Database) 파일에서 응답 파일을 수정 하는 방법을 지정 하는 데 사용 되는 식별자를 나타냅니다.|
|\<UDB_file>|고유성 UDB (Database) 파일을 지정합니다.|
|/unattend|X86 기반 컴퓨터에서는 무인된 설치 모드에서 이전 버전의 Windows NT 4.0 Server (서비스 팩 5 이상) 또는 Windows 2000을 업그레이드합니다. 설치 중에 사용자 개입 없이 필요 하므로 이전 설치에서 모든 사용자 설정은 가져옵니다.|
|\<num>|설치 하는 시간 간격 (초)의 복사를 완료 파일과 컴퓨터 다시 시작을 지정 합니다. 사용할 수 있습니다 \<Num > Windows Server 2003에서 Windows 98, Windows Millennium edition, Windows NT, Windows 2000, Windows XP 또는 제품을 실행 하는 컴퓨터에 있습니다. 컴퓨터에서 Windows NT 버전 4.0 실행 중인 경우 서비스 팩 5 이상이 필요 합니다.|
|\<AnswerFile>|설치 프로그램에 사용자 지정 사양을 제공합니다|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
Windows XP 클라이언트 컴퓨터를 배포 하는 경우에 Windows XP와 함께 제공 되는 winnt32.exe의 버전을 사용할 수 있습니다. Windows XP를 배포 하는 또 다른 방법은 Windows 설치 관리자는 IntelliMirror의 일부를 통해 어떤 works 기술 집합이 winnt32.msi를 사용 하는 것입니다. 클라이언트 배포에 대 한 자세한 내용은 참조에 설명 된 Windows Server 2003 Deployment Kit [Windows 배포 및 리소스 키트를 사용 하 여](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx)합니다.

Itanium 기반 컴퓨터에서는 **winnt32** 확장 가능 펌웨어 인터페이스 (EFI)에서 또는 Windows Server 2003 Enterprise, Windows Server 2003 R2 Enterprise, Windows Server 2003 R2 Datacenter, 또는 Windows Server 2003 Datacenter에서 실행할 수 있습니다. 또한 Itanium 아키텍처 기반 컴퓨터에서 **/cmdcons** 및 **/syspart** 업그레이드에 관련 된 옵션 및 사용할 수 없음을 사용할 수 없는 합니다.
하드웨어 호환성에 대 한 자세한 내용은 참조 하세요. [하드웨어 호환성](https://technet.microsoft.com/library/cc757927(v=ws.10).aspx)합니다.
동적 업데이트를 사용 하 고 여러 클라이언트를 설치 하는 방법에 대 한 정보를 자세한 참조에 설명 된 Windows Server 2003 Deployment Kit [Windows 배포 및 리소스 키트를 사용 하 여](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx)입니다.
부팅 설정을 수정 하는 방법에 대 한 내용은 Windows 배포 및 Windows Server 2003 리소스 키트를 참조 하세요. 자세한 내용은 참조 [Windows 배포 및 리소스 키트를 사용 하 여](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx)합니다.
사용 하는 **/unattend** 설치를 자동화 하는 명령줄 옵션은 읽기 있으며는 Microsoft 라이선스 계약에 대 한 Windows Server 2003을 허용 합니다. 자신의 소유가 아닌 조직을 대신 하 여 Windows Server 2003을 설치 하려면이 명령줄 옵션을 사용 하기 전에 확인 해야 하는 최종 사용자 (여부는 개인 또는 단일 엔터티)에서, 읽기, 받고 해당 제품에 대 한 Microsoft 사용권 계약의 조건에 동의 합니다.  Oem은 최종 사용자에 게 판매 되는 컴퓨터에이 키를 지정 하지 않을 수 있습니다.

## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)

