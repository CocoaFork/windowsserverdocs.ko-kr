# [보안 및 보증](security-and-assurance.md)
## [Windows Server 2016에 대한 GDPR(일반 데이터 보호 규정) 여정 시작](gdpr/gdpr-winserver-whitepaper.md)
## [SQL Server의 상시 암호화에 대한 HGS 설정](set-up-hgs-for-always-encrypted-in-sql-server.md)
## [보호된 패브릭 및 보호된 VM에 대한 HGS 설정](guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md)
### [개요](guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md)
### [계획](guarded-fabric-shielded-vm/guarded-fabric-plan-overview.md)
#### [호스터 계획](guarded-fabric-shielded-vm/guarded-fabric-planning-for-hosters.md)
##### [호환되는 하드웨어](guarded-fabric-shielded-vm/guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md)
#### [테넌트 계획](guarded-fabric-shielded-vm/guarded-fabric-shielded-vm-planning-for-tenants.md)
### [배포](guarded-fabric-shielded-vm/guarded-fabric-deploying-hgs-overview.md)
#### [빠른 시작](guarded-fabric-shielded-vm/guarded-fabric-deployment-overview.md)
#### [HGS 배포](guarded-fabric-shielded-vm/guarded-fabric-setting-up-the-host-guardian-service-hgs.md)
##### [필수 구성 요소](guarded-fabric-shielded-vm/guarded-fabric-prepare-for-hgs.md)
##### [인증서 획득](guarded-fabric-shielded-vm/guarded-fabric-obtain-certs.md) 
##### [HGS 설치](guarded-fabric-shielded-vm/guarded-fabric-choose-where-to-install-hgs.md)
###### [새 포리스트(기본값)](guarded-fabric-shielded-vm/guarded-fabric-install-hgs-default.md)
###### [배스천 포리스트](guarded-fabric-shielded-vm/guarded-fabric-install-hgs-in-a-bastion-forest.md)
##### [HGS 초기화](guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs.md)
###### [TPM 모드](guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-tpm-mode.md)
####### [전용 포리스트(기본값)](guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-tpm-mode-default.md)
####### [배스천 포리스트](guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-tpm-mode-bastion.md)
####### [TPM 루트 인증서 설치](guarded-fabric-shielded-vm/guarded-fabric-install-trusted-tpm-root-certificates.md)
####### [패브릭 DNS 구성](guarded-fabric-shielded-vm/guarded-fabric-configuring-fabric-dns-tpm.md)
###### [키 모드](guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-key-mode.md)
####### [전용 포리스트(기본값)](guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-key-mode-default.md)
####### [배스천 포리스트](guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-key-mode-bastion.md)
###### [AD 모드](guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-ad-mode.md)
####### [전용 포리스트(기본값)](guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-ad-mode-default.md)
####### [배스천 포리스트](guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-ad-mode-bastion.md)
####### [패브릭 DNS 구성](guarded-fabric-shielded-vm/guarded-fabric-configuring-fabric-dns-ad.md)
####### [HGS DNS 및 단방향 트러스트 구성](guarded-fabric-shielded-vm/guarded-fabric-configure-dns-forwarding-and-trust.md)
##### [HTTPS 구성](guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-https.md)
##### [노드 추가](guarded-fabric-shielded-vm/guarded-fabric-configure-additional-hgs-nodes.md)
##### [구성 확인](guarded-fabric-shielded-vm/guarded-fabric-verify-hgs-configuration.md)
#### [보호된 호스트 배포](guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)
##### [필수 구성 요소](guarded-fabric-shielded-vm/guarded-fabric-guarded-host-prerequisites.md)
##### [TPM 모드](guarded-fabric-shielded-vm/guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)
##### [키 모드](guarded-fabric-shielded-vm/guarded-fabric-create-host-key.md)
##### [AD 모드](guarded-fabric-shielded-vm/guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)
##### [증명 확인](guarded-fabric-shielded-vm/guarded-fabric-confirm-hosts-can-attest-successfully.md)
##### [VMM 사용](https://docs.microsoft.com/system-center/vmm/guarded-deploy-host?toc=/windows-server/virtualization/toc.json)
#### [보호된 VM 배포](guarded-fabric-shielded-vm/guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
##### [Windows 템플릿 디스크 만들기](guarded-fabric-shielded-vm/guarded-fabric-create-a-shielded-vm-template.md)
##### [Linux 템플릿 디스크 만들기](guarded-fabric-shielded-vm/guarded-fabric-create-a-linux-shielded-vm-template.md)
##### [Windows Azure 팩 설치](guarded-fabric-shielded-vm/guarded-fabric-hoster-sets-up-windows-azure-pack.md)
##### [OS 전문화 응답 파일 만들기](guarded-fabric-shielded-vm/guarded-fabric-sample-unattend-xml-file.md)
##### [보호 데이터 파일 만들기](guarded-fabric-shielded-vm/guarded-fabric-tenant-creates-shielding-data.md)
##### [PowerShell을 사용하여 보호된 VM 배포](guarded-fabric-shielded-vm/guarded-fabric-create-a-shielded-vm-using-powershell.md)
##### [VMM을 사용하여 배포](guarded-fabric-shielded-vm/guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)
##### [Windows Azure 팩을 사용하여 배포](guarded-fabric-shielded-vm/guarded-fabric-shielded-vm-windows-azure-pack.md)
##### [기존 VM 보호](guarded-fabric-shielded-vm/guarded-fabric-vm-shielding-helper-vhd.md)
### [관리](guarded-fabric-shielded-vm/guarded-fabric-manage-overview.md)
#### [호스트 보호 서비스 관리](guarded-fabric-shielded-vm/guarded-fabric-manage-hgs.md)
#### [지사 고려 사항](guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office.md)
#### [보호된 패브릭을 Windows Server 2019로 업그레이드](guarded-fabric-shielded-vm/guarded-fabric-upgrade-to-2019.md)
### [문제 해결](guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-overview.md)
#### [보호된 패브릭 진단 도구](guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-diagnostics.md)
#### [HGS](guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hgs.md)
#### [보호된 호스트](guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hosts.md)
#### [보호된 VM](guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-shielded-vms.md)
## [디바이스 상태 증명](device-health-attestation.md)
## [Windows Server 2016에서 시스템 서비스 비활성화](windows-services/security-guidelines-for-disabling-system-services-in-windows-server.md)
## [Windows에서 사용자 단위 서비스 비활성화](https://docs.microsoft.com/windows/application-management/per-user-services-in-windows)
## [Windows 인증](windows-authentication/windows-authentication-overview.md)
### [Windows 인증 기술 개요](windows-authentication/windows-authentication-technical-overview.md)
#### [Windows 인증 개념](windows-authentication/windows-authentication-concepts.md)
#### [Windows 로그온 시나리오](windows-authentication/windows-logon-scenarios.md)
#### [Windows 인증 아키텍처](windows-authentication/windows-authentication-architecture.md)
##### [보안 지원 공급자 인터페이스 아키텍처](windows-authentication/security-support-provider-interface-architecture.md)
##### [Windows 인증의 자격 증명 프로세스](windows-authentication/credentials-processes-in-windows-authentication.md)
#### [Windows 인증에 사용되는 그룹 정책 설정](windows-authentication/group-policy-settings-used-in-windows-authentication.md)
## [자격 증명 보호 및 관리](credentials-protection-and-management/credentials-protection-and-management.md)
### [추가 LSA 보호 구성](credentials-protection-and-management/configuring-additional-lsa-protection.md)
### [자격 증명 보호의 새로운 기능](credentials-protection-and-management/whats-new-in-credential-protection.md)
### [Credential Guard를 사용하여 파생된 도메인 자격 증명 보호](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard)
### [원격 Credential Guard를 사용하여 원격 데스크톱 자격 증명 보호](https://technet.microsoft.com/itpro/windows/keep-secure/remote-credential-guard)
### [보호된 사용자 보안 그룹](credentials-protection-and-management/protected-users-security-group.md)
### [인증 정책 및 인증 정책 사일로](credentials-protection-and-management/authentication-policies-and-authentication-policy-silos.md)
## [그룹 관리 서비스 계정](group-managed-service-accounts/group-managed-service-accounts-overview.md)
### [그룹 관리 서비스 계정 시작](group-managed-service-accounts/getting-started-with-group-managed-service-accounts.md)
#### [키 배포 서비스 KDS 루트 키 만들기](group-managed-service-accounts/create-the-key-distribution-services-kds-root-key.md)
## [Kerberos 인증](kerberos/kerberos-authentication-overview.md)
### [Kerberos 인증의 새로운 기능](kerberos/whats-new-in-kerberos-authentication.md)
### [도메인 가입 디바이스 공개 키 인증](kerberos/domain-joined-device-public-key-authentication.md)
### [Kerberos 제한 위임](kerberos/kerberos-constrained-delegation-overview.md)
### [Kerberos가 RC4 비밀 키를 사용하는 암호를 변경하지 못하도록 설정](kerberos/preventing-kerberos-change-password-that-uses-rc4-secret-keys.md)
### [IP 주소에 대한 Kerberos 구성](kerberos/configuring-kerberos-over-ip.md)
## [NTLM](kerberos/ntlm-overview.md)
## [암호](kerberos/passwords-overview.md)
## [TLS - SSL(Schannel SSP)](tls/tls-ssl-schannel-ssp-overview.md)
### [Windows 10 및 Windows Server 2016의 TLS 변경 내용](tls/tls-schannel-ssp-changes-in-windows-10-and-windows-server.md)
### [TLS 관리](tls/manage-tls.md)
### [TLS 레지스트리 설정](tls/tls-registry-settings.md)
### [Schannel 보안 지원 공급자 기술 참조](tls/schannel-security-support-provider-technical-reference.md)
#### [전송 계층 보안 프로토콜](tls/transport-layer-security-protocol.md)
#### [데이터그램 전송 계층 보안 프로토콜](tls/datagram-transport-layer-security-protocol.md)
## [사용자 계정 컨트롤 작동 방식](user-account-control/how-user-account-control-works.md)
## [토큰 바인딩](token-binding/introducing-token-binding.md)
## [Windows Defender 바이러스 백신](windows-defender/windows-defender-overview-windows-server.md)