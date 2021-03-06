---
title: Azure Backup에서 암호화
description: Azure Backup의 암호화 기능을 통해 백업 데이터를 보호 하 고 비즈니스의 보안 요구 사항을 충족 하는 방법을 알아봅니다.
ms.topic: conceptual
ms.date: 04/30/2020
ms.custom: references_regions
ms.openlocfilehash: 099e736bfb321f0f92bd3a57f9c24e88293b42bb
ms.sourcegitcommit: 3543d3b4f6c6f496d22ea5f97d8cd2700ac9a481
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86538754"
---
# <a name="encryption-in-azure-backup"></a>Azure Backup에서 암호화

모든 백업 된 데이터는 Azure Storage 암호화를 사용 하 여 클라우드에 저장 될 때 자동으로 암호화 되므로 보안 및 규정 준수 약정을 충족할 수 있습니다. 미사용 데이터는 256 비트 AES 암호화를 사용 하 여 암호화 되 고, 사용 가능한 가장 강력한 블록 암호화 중 하나 이며, FIPS 140-2 규격입니다.

휴지 상태의 암호화 외에도 전송 중인 모든 백업 데이터는 HTTPS를 통해 전송 됩니다. 항상 Azure 백본 네트워크에 남아 있습니다.

자세한 내용은 [미사용 데이터에 대한 Azure Storage 암호화](../storage/common/storage-service-encryption.md)를 참조하세요. [AZURE BACKUP FAQ](./backup-azure-backup-faq.md#encryption) 를 참조 하 여 암호화에 대해 발생할 수 있는 질문에 대 한 답변을 받을 수 있습니다.

## <a name="encryption-of-backup-data-using-platform-managed-keys"></a>플랫폼 관리 키를 사용 하 여 백업 데이터 암호화

기본적으로 모든 데이터는 플랫폼 관리 키를 사용 하 여 암호화 됩니다. 이 암호화를 사용 하도록 설정 하기 위해 끝에서 명시적인 조치를 취할 필요는 없으며 Recovery Services 자격 증명 모음에 백업 되는 모든 워크 로드에 적용 됩니다.

## <a name="encryption-of-backup-data-using-customer-managed-keys"></a>고객 관리 키를 사용 하 여 백업 데이터 암호화

Azure Virtual Machines를 백업할 때 이제 사용자가 소유 하 고 관리 하는 키를 사용 하 여 데이터를 암호화할 수 있습니다. Azure Backup를 사용 하면 Azure Key Vault에 저장 된 RSA 키를 사용 하 여 백업을 암호화할 수 있습니다. 백업 암호화에 사용 되는 암호화 키는 원본에 사용 된 것과 다를 수 있습니다. 데이터는 AES 256 기반 DEK (데이터 암호화 키)를 사용 하 여 보호 됩니다. 즉, 키를 사용 하 여 보호 됩니다. 이를 통해 데이터와 키에 대 한 모든 권한을 제공 합니다. 암호화를 허용 하려면 Recovery Services 자격 증명 모음에 Azure Key Vault 암호화 키에 대 한 액세스 권한을 부여 해야 합니다. 필요할 때마다 키를 사용 하지 않도록 설정 하거나 액세스를 취소할 수 있습니다. 그러나 자격 증명 모음에 대 한 항목을 보호 하기 전에 키를 사용 하 여 암호화를 사용 하도록 설정 해야 합니다.

고객 관리 키를 사용 하 여 백업 데이터를 암호화 하는 방법에 대 한 자세한 내용은 [여기](encryption-at-rest-with-cmk.md)를 참조 하세요.

## <a name="backup-of-managed-disk-vms-encrypted-using-customer-managed-keys"></a>고객 관리 키를 사용 하 여 암호화 된 관리 디스크 Vm 백업

또한 Azure Backup를 사용 하면 [저장소 서비스 암호화](../storage/common/storage-service-encryption.md)를 위해 키를 사용 하는 Azure vm을 백업할 수 있습니다. 디스크 암호화에 사용 되는 키는 Azure Key Vault에 저장 되며 사용자가 관리 합니다. ADE는 고객 관리 키를 사용 하는 저장소 서비스 암호화 Azure Disk Encryption와 다릅니다. 즉, ADE는 BitLocker (Windows 용) 및 DM (Linux)을 활용 하 여 게스트 간 암호화를 수행 하므로 SSE는 저장소 서비스의 데이터를 암호화 하 여 Vm에 대 한 모든 OS 또는 이미지를 사용할 수 있도록 합니다. 자세한 내용은 [고객 관리 키를 사용 하 여 관리 디스크 암호화](../virtual-machines/windows/disk-encryption.md#customer-managed-keys) 를 참조 하세요.

## <a name="infrastructure-level-encryption-for-backup-data"></a>백업 데이터에 대 한 인프라 수준 암호화

고객 관리 키를 사용 하 여 Recovery Services 자격 증명 모음에서 데이터를 암호화 하는 것 외에도 저장소 인프라에 추가 암호화 계층을 구성 하도록 선택할 수 있습니다. 이 인프라 암호화는 플랫폼에 의해 관리 되며, 고객이 관리 하는 키를 사용 하 여 미사용 암호화와 함께 백업 데이터의 2 계층 암호화를 허용 합니다. 미사용 암호화에 고유한 키를 사용 하도록 처음 선택 하는 경우에만 인프라 암호화를 구성할 수 있습니다. 인프라 암호화는 플랫폼 관리 키를 사용 하 여 데이터를 암호화 합니다.

>[!NOTE]
>인프라 암호화는 현재 제한 된 미리 보기로 제공 되며 미국 동부, 미국 West2, 미국 남부 중부, US Gov 애리조나 및 US .GOV 버지니아 지역 에서만 사용할 수 있습니다. 이러한 지역에서이 기능을 사용 하려면 [이 양식을](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR0H3_nezt2RNkpBCUTbWEapUN0VHNEpJS0ZUWklUNVdJSTEzR0hIOVRMVC4u) 작성 하 고에 전자 메일을 보내 주세요 [AskAzureBackupTeam@microsoft.com](mailto:AskAzureBackupTeam@microsoft.com) .

## <a name="backup-of-vms-encrypted-using-ade"></a>ADE를 사용 하 여 암호화 된 Vm 백업

Azure Backup를 사용 하면 Azure Disk Encryption를 사용 하 여 암호화 된 OS 또는 데이터 디스크를 포함 하는 Azure 가상 컴퓨터도 백업할 수 있습니다. ADE는 Windows Vm에 BitLocker를 사용 하 고 Linux Vm의 경우 DM을 사용 하 여 게스트 간 암호화를 수행 합니다. 자세한 내용은 [Azure Backup를 사용 하 여 암호화 된 가상 컴퓨터 백업 및 복원](./backup-azure-vms-encryption.md)을 참조 하세요.

## <a name="next-steps"></a>다음 단계

- [암호화 된 Azure VM 백업 및 복원](backup-azure-vms-encryption.md)
