# [스토리지](storage.md)
## [스토리지의 새로운 기능](whats-new-in-storage.md)
## [데이터 중복 제거](data-deduplication/overview.md)
### [데이터 중복 제거의 새로운 기능](data-deduplication/whats-new.md)
### [데이터 중복 제거 이해](data-deduplication/understand.md)
### [데이터 중복 제거 설치 및 사용](data-deduplication/install-enable.md)
### [데이터 중복 제거 실행](data-deduplication/run.md)
### [고급 데이터 중복 제거 설정](data-deduplication/advanced-settings.md)
### [데이터 중복 제거 상호 운용성](data-deduplication/interop.md)
## [DFS 네임스페이스](dfs-namespaces/dfs-overview.md)
### [검사 목록: DFS 네임스페이스 배포](dfs-namespaces/checklist-deploy-dfs-namespaces.md)
### [검사 목록: DFS 네임스페이스 튜닝](dfs-namespaces/checklist-tune-a-dfs-namespace.md)
### [DFS 네임스페이스 배포](dfs-namespaces/deploying-dfs-namespaces.md)
#### [네임스페이스 형식 선택](dfs-namespaces/choose-a-namespace-type.md)
#### [DFS 네임스페이스 만들기](dfs-namespaces/create-a-dfs-namespace.md)
#### [도메인 기반 네임스페이스를 Windows Server 2008 모드로 마이그레이션](dfs-namespaces/migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)
#### [도메인 기반 DFS 네임스페이스에 네임스페이스 서버 추가](dfs-namespaces/add-namespace-servers-to-a-domain-based-DFS-namespace.md)
#### [DFS 네임스페이스에 폴더 만들기](dfs-namespaces/create-a-folder-in-a-dfs-namespace.md)
#### [폴더 대상 추가](dfs-namespaces/add-folder-targets.md)
#### [DFS 복제를 사용하여 폴더 대상 복제](dfs-namespaces/replicate-folder-targets-using-dfs-replication.md)
#### [DFS 네임스페이스에 대한 관리 권한 위임](dfs-namespaces/delegate-management-permissions-for-dfs-namespaces.md)
### [DFS 네임스페이스 튜닝](dfs-namespaces/tuning-dfs-namespaces.md)
#### [조회 및 클라이언트 장애 복구 사용 또는 사용 안 함](dfs-namespaces/enable-or-disable-referrals-and-client-failback.md)
#### [클라이언트에서 조회를 캐시하는 기간 변경](dfs-namespaces/change-the-amount-of-time-that-clients-cache-referrals.md)
#### [조회 대상의 순서를 지정하는 방법 설정](dfs-namespaces/set-the-ordering-method-for-targets-in-referrals.md)
#### [대상 우선 순위를 설정하여 조회 순서 지정 재정의](dfs-namespaces/set-target-priority-to-override-referral-ordering.md)
#### [네임스페이스 폴링 최적화](dfs-namespaces/optimize-namespace-polling.md)
#### [네임스페이스에 액세스 기반 열거 사용](dfs-namespaces/enable-access-based-enumeration-on-a-namespace.md)
#### [액세스 기반 열거에 상속된 권한 사용](dfs-namespaces/using-inherited-permissions-with-access-based-enumeration.md)
## [DFS 복제](dfs-replication/dfsr-overview.md)
### [SYSVOL 복제를 DFS 복제로 마이그레이션](dfs-replication/migrate-sysvol-to-dfsr.md)
### [robocopy를 사용하여 DFS 복제용 파일 미리 시드](dfs-replication/preseed-dfsr-with-robocopy.md)
### [DFS 복제: FAQ(질문과 대답)](dfs-replication/dfsr-faq.md)
## [디스크 관리](disk-management/overview-of-disk-management.md)
## [파일 서버 및 SMB](file-server/file-server-smb-overview.md)
### [SMB 다이렉트](file-server/smb-direct.md)
### [SMB 보안 강화](file-server/smb-security.md)
### [SMB: 파일 및 프린터 공유 포트가 열려 있어야 함](file-server/best-practices-analyzer/smb-open-file-sharing-ports.md)
### [네트워크 파일 시스템 개요](nfs/nfs-overview.md)
### [네트워크 파일 시스템 배포](nfs/deploy-nfs.md)
### [NTFS 개요](file-server/ntfs-overview.md)
### [볼륨 섀도 복사본 서비스](file-server/volume-shadow-copy-service.md)
### [디스크 정리 사용](file-server/disk-cleanup.md)
### [SMB에 대한 고급 문제 해결](file-server/Troubleshoot/troubleshooting-smb.md)
#### [SMBv1, SMBv2 및 SMBv3 검색, 사용 및 사용 안 함](file-server/Troubleshoot/detect-enable-and-disable-smbv1-v2-v3.md)
#### [SMBv1은 기본적으로 설치되지 않음](file-server/Troubleshoot/smbv1-not-installed-by-default-in-windows.md)
### [SMB 알려진 문제](file-server/Troubleshoot/smb-known-issues.md)
#### [TCP 3방향 핸드셰이크 오류](file-server/Troubleshoot/tcp-three-way-handshake-fails.md)
#### [협상, 세션 설정 및 트리 연결 실패](file-server/Troubleshoot/negotiate-session-setup-tree-connect-fails.md)
#### [유효성 검사 협상 중 TCP 연결이 중단됨](file-server/Troubleshoot/abort-during-validate-negotiate.md)
#### [느린 SMB 파일 전송 속도](file-server/Troubleshoot/slow-file-transfer.md)
#### [높은 CPU 사용량](file-server/Troubleshoot/high-cpu-usage-issue-on-smb-server.md)
#### [이벤트 ID 50 문제 해결](file-server/Troubleshoot/troubleshoot-event-id-50-error.md)
#### [SMB 다중 채널 문제 해결](file-server/Troubleshoot/smb-multichannel-troubleshooting.md)
## [파일 서버 리소스 관리자](fsrm/fsrm-overview.md)
### [검사 목록: 볼륨 또는 폴더에 할당량 적용](fsrm/checklist-apply-quota-to-volume-or-folder.md)
### [검사 목록: 볼륨 또는 폴더에 파일 차단 적용](fsrm/checklist-apply-file-screen-to-volume-or-folder.md)
### [파일 서버 리소스 관리자 옵션 설정](fsrm/setting-file-server-resource-manager-options.md)
#### [이메일 알림 구성](fsrm/configure-email-notifications.md)
#### [알림 제한 구성](fsrm/configure-notification-limits.md)
#### [스토리지 보고서 구성](fsrm/configure-storage-reports.md)
#### [파일 차단 감사 구성](fsrm/configure-file-screen-audit.md)
### [할당량 관리](fsrm/quota-management.md)
#### [할당량 만들기](fsrm/create-quota.md)
#### [할당량 자동 적용 만들기](fsrm/create-auto-apply-quota.md)
#### [할당량 템플릿 만들기](fsrm/create-quota-template.md)
#### [할당량 템플릿 속성 편집](fsrm/edit-quota-template-properties.md)
#### [할당량 자동 적용 속성 편집](fsrm/edit-auto-apply-quota-properties.md)
### [파일 차단 관리](fsrm/file-screening-management.md)
#### [차단을 위한 파일 그룹 정의](fsrm/define-file-groups-for-screening.md)
#### [파일 화면 만들기](fsrm/create-file-screen.md)
#### [파일 차단 예외 만들기](fsrm/create-file-screen-exception.md)
#### [파일 차단 템플릿 만들기](fsrm/create-file-screen-template.md)
#### [파일 차단 템플릿 속성 편집](fsrm/edit-file-screen-template-properties.md)
### [스토리지 보고서 관리](fsrm/storage-reports-management.md)
#### [보고서 세트 예약](fsrm/schedule-set-of-reports.md)
#### [주문형 보고서 생성](fsrm/generate-reports-on-demand.md)
### [분류 관리](fsrm/classification-management.md)
#### [자동 분류 규칙 만들기](fsrm/create-automatic-classification-rule.md)
#### [분류 속성 만들기](fsrm/create-classification-property.md)
### [파일 관리 작업](fsrm/file-management-tasks.md)
#### [파일 만료 작업 만들기](fsrm/create-file-expiration-task.md)
#### [사용자 지정 파일 관리 작업 만들기](fsrm/create-custom-file-management-task.md)
### [원격 스토리지 리소스 관리](fsrm/managing-remote-storage-resources.md)
#### [원격 컴퓨터에 연결](fsrm/connect-to-remote-computer.md)
#### [명령줄 도구](fsrm/command-line-tools.md)
### [파일 서버 리소스 관리자 문제 해결](fsrm/troubleshooting-file-server-resource-manager.md)
## [폴더 리디렉션 및 로밍 사용자 프로필](folder-redirection/folder-redirection-rup-overview.md)
### [로밍 사용자 프로필 배포](folder-redirection/deploy-roaming-user-profiles.md)
### [폴더 리디렉션 배포](folder-redirection/deploy-folder-redirection.md)
### [기본 컴퓨터 배포](folder-redirection/deploy-primary-computers.md)
### [폴더에서 오프라인 파일 사용 안 함](folder-redirection/disable-offline-files-on-folders.md)
### [항상 오프라인 모드 사용](folder-redirection/enable-always-offline.md)
### [최적화된 폴더 이동 사용](folder-redirection/enable-optimized-moving.md)
### [사용자 프로필 문제 해결](folder-redirection/troubleshoot-user-profiles-events.md)
## iSCSI
### [iSCSI 대상 서버](iscsi/iscsi-target-server.md)
### [iSCSI 대상 서버 확장성 제한](iscsi/iscsi-target-server-limits.md)
### [iSCSI 부팅](iscsi/iscsi-boot-overview.md)

## [ReFS](refs/refs-overview.md)
### [미러 가속 패리티](refs/mirror-accelerated-parity.md)
### [블록 복제](refs/block-cloning.md)
### [무결성 스트림](refs/integrity-streams.md)

## 스토리지 마이그레이션 서비스
### [개요](storage-migration-service/overview.md)
### [서버 마이그레이션](storage-migration-service/migrate-data.md)
### [FAQ(질문과 대답)](storage-migration-service/faq.md)
### [알려진 문제](storage-migration-service/known-issues.md)

## [스토리지 복제본](storage-replica/storage-replica-overview.md)
### [공유 스토리지를 사용하여 확장 클러스터 복제](storage-replica/stretch-cluster-replication-using-shared-storage.md)
### [서버 간 스토리지 복제](storage-replica/server-to-server-storage-replication.md)
### [클러스터 간 스토리지 복제](storage-replica/cluster-to-cluster-storage-replication.md)
### [Azure에서 교차 지역 클러스터 간 스토리지 복제](storage-replica/cluster-to-cluster-azure-cross-region.md)
### [Azure에서 동일 지역 내 클러스터 간 스토리지 복제](storage-replica/cluster-to-cluster-azure-one-region.md)
### [스토리지 복제본: 알려진 문제](storage-replica/storage-replica-known-issues.md)
### [스토리지 복제본: 질문과 대답](storage-replica/storage-replica-frequently-asked-questions.md)
## [스토리지 공간](storage-spaces/overview.md)
### [독립 실행형 서버에 스토리지 공간 배포](storage-spaces/deploy-standalone-storage-spaces.md)
### [성능 상태 및 작동 상태](storage-spaces/storage-spaces-states.md)
## [스토리지 공간 다이렉트](storage-spaces/storage-spaces-direct-overview.md)
### 이해
#### [캐시 이해](storage-spaces/understand-the-cache.md)
#### [내결함성 및 스토리지 효율성](storage-spaces/Storage-Spaces-Fault-Tolerance.md)
#### [드라이브 대칭 고려 사항](storage-spaces/drive-symmetry-considerations.md)
#### [스토리지 다시 동기화 이해 및 모니터링](storage-spaces/understand-storage-resync.md)
#### [클러스터 및 풀 쿼럼](storage-spaces/understand-quorum.md)
#### [클러스터 세트](storage-spaces/cluster-sets.md)
### 계획
#### [하드웨어 요구 사항](storage-spaces/storage-spaces-direct-hardware-requirements.md)
#### [CSV 메모리 내 읽기 캐시 사용](storage-spaces/csv-cache.md)
#### [드라이브 선택](storage-spaces/choosing-drives.md)
#### [볼륨 계획](storage-spaces/plan-volumes.md)
#### [게스트 VM 클러스터](storage-spaces/storage-spaces-direct-in-vm.md)
#### [재해 복구](storage-spaces/storage-spaces-direct-disaster-recovery.md)
### 배포 게스트 클러스터에
#### [스토리지 공간 다이렉트 배포](storage-spaces/deploy-storage-spaces-direct.md)
#### [볼륨 만들기](storage-spaces/create-volumes.md)
#### [중첩된 복원력](storage-spaces/nested-resiliency.md)
#### [쿼럼 구성](../failover-clustering/manage-cluster-quorum.md)
#### [스토리지 공간 다이렉트 클러스터 업그레이드](storage-spaces/upgrade-storage-spaces-direct-to-windows-server-2019.md)
#### [영구 메모리 이해 및 배포](storage-spaces/deploy-pmem.md)

### 관리
#### [Windows Admin Center를 통해 관리](../manage/windows-admin-center/use/manage-hyper-converged.md)
#### [서버 또는 드라이브 추가](storage-spaces/add-nodes.md)
#### [유지 관리를 위해 서버를 오프라인으로 전환](storage-spaces/maintain-servers.md)
#### [서버 제거](storage-spaces/remove-servers.md)
#### [드라이브 펌웨어 업데이트](update-firmware.md)
#### [볼륨 확장](storage-spaces/resize-volumes.md)
#### [볼륨 삭제](storage-spaces/delete-volumes.md)
#### [성능 기록](storage-spaces/performance-history.md)
##### [드라이브](storage-spaces/performance-history-for-drives.md)
##### [네트워크 어댑터](storage-spaces/performance-history-for-network-adapters.md)
##### [서버](storage-spaces/performance-history-for-servers.md)
##### [VHD](storage-spaces/performance-history-for-vhds.md)
##### [VM](storage-spaces/performance-history-for-vms.md)
##### [볼륨](storage-spaces/performance-history-for-volumes.md)
##### [클러스터](storage-spaces/performance-history-for-clusters.md)
##### [스크립팅 샘플](storage-spaces/performance-history-scripting.md)
#### [볼륨 할당 구분](storage-spaces/delimit-volume-allocation.md)
#### [Azure Monitor를 사용하여 모니터](storage-spaces/configure-azure-monitor.md)

### 문제 해결
#### [문제 해결 시나리오](storage-spaces/troubleshooting-storage-spaces.md)
#### [성능 상태 및 작동 상태](storage-spaces/storage-spaces-states.md)
#### [데이터 수집](storage-spaces/data-collection.md)
#### [질문과 대답](storage-spaces/storage-spaces-direct-faq.md)
#### [스토리지 클래스 메모리 상태 관리](storage-spaces/Storage-class-memory-health.md)

## [클라우드 폴더](work-folders/work-folders-overview.md)
### [클라우드 폴더 구현 디자인](work-folders/plan-work-folders.md)
### [클라우드 폴더 배포](work-folders/deploy-work-folders.md)
### [AD FS 및 WAP(웹 애플리케이션 프록시)를 사용하여 클라우드 폴더 배포](work-folders/deploy-work-folders-adfs-overview.md)
#### [1단계, AD FS 설정](work-folders/deploy-work-folders-adfs-step1.md)
#### [2단계, AD FS 사후 구성](work-folders/deploy-work-folders-adfs-step2.md)
#### [3단계, 클라우드 폴더 설정](work-folders/deploy-work-folders-adfs-step3.md)
#### [4단계, WAP 설정](work-folders/deploy-work-folders-adfs-step4.md)
#### [5단계, 클라이언트 설정](work-folders/deploy-work-folders-adfs-step5.md)
## [스토리지 QoS](storage-qos/storage-qos-overview.md)
## [스토리지 항목에 대한 변경 기록](storage-change-history.md)

