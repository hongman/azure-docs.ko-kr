---
title: Privileged Identity Management 이전 보안 마법사의 Azure AD 역할 검색 및 정보 (미리 보기)-Azure Active Directory
description: 검색 및 정보 (이전의 보안 마법사)는 영구 Azure AD 역할 할당을 Privileged Identity Management를 사용 하 여 just-in-time 할당으로 변환 하는 데 도움이 됩니다.
services: active-directory
documentationcenter: ''
author: curtand
manager: daveba
editor: ''
ms.service: active-directory
ms.topic: how-to
ms.workload: identity
ms.subservice: pim
ms.date: 08/07/2020
ms.author: curtand
ms.custom: pim ; H1Hack27Feb2017
ms.collection: M365-identity-device-management
ms.openlocfilehash: ef1de7e98a9cb57f83b87589ceddedc3cdd80927
ms.sourcegitcommit: 98854e3bd1ab04ce42816cae1892ed0caeedf461
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "88005953"
---
# <a name="discovery-and-insights-preview-for-azure-ad-roles-formerly-security-wizard"></a>Azure AD 역할에 대 한 검색 및 통찰력 (미리 보기) (이전의 보안 마법사)

Azure Active Directory (Azure AD) 조직에서 Privileged Identity Management (PIM)를 시작 하는 경우 **검색 및 정보 활용 (미리 보기)** 페이지를 사용 하 여 시작할 수 있습니다. 이 기능은 조직의 권한 있는 역할에 할당 된 사용자 및 PIM을 사용 하 여 영구 역할 할당을 적시에 할당으로 신속 하 게 변경 하는 방법을 보여 줍니다. **검색 및 정보 (미리 보기)** 에서 영구 권한 있는 역할 할당을 보거나 변경할 수 있습니다. 분석 도구 및 작업 도구입니다.

## <a name="discovery-and-insights-preview"></a>검색 및 정보 (미리 보기)

조직에서 Privileged Identity Management 사용을 시작 하기 전에 모든 역할 할당이 영구적입니다. 사용자는 권한이 필요 하지 않은 경우에도 항상 할당 된 역할에 포함 됩니다. 이전 보안 마법사를 대체 하는 검색 및 정보 (미리 보기)는 권한 있는 역할 목록과 현재 이러한 역할에 있는 사용자 수를 보여 줍니다. 역할에 대 한 할당을 나열 하 여 할당 된 사용자 중 하나 이상이 익숙하지 않은 경우 해당 사용자에 대 한 자세한 정보를 확인할 수 있습니다.

: heavy_check_mark: 로그인 할 때 다단계 인증을 요구 하지 않는 전역 관리자 역할에 영구적으로 할당 되는 2 개의 중단 된 계정을 유지 하는 것 **이 좋습니다** . 이는 모든 브레이크 유리 시나리오에서 사용할 수도 있고, 전역 관리자 역할로 상승 하지 못하는 경우에 사용할 수도 있습니다.

또한 사용자에 게 Microsoft 계정 (즉, Skype 또는 Outlook.com와 같은 Microsoft 서비스에 로그인 하는 데 사용 하는 계정)가 있는 경우 역할 할당을 영구적으로 유지 합니다. 이러한 역할에서 multi-factor authentication을 활성화 해야 하는 경우 사용자가 잠깁니다.

## <a name="open-discovery-and-insights-preview"></a>검색 및 통찰력 열기 (미리 보기)

1. [Azure Portal](https://portal.azure.com/)에 로그인합니다.

1. **Azure AD Privileged Identity Management**를 엽니다.

1. **AZURE AD 역할** 을 선택한 다음 **검색 및 Insights (미리 보기)** 를 선택 합니다. 페이지를 열면 검색 프로세스가 시작 되어 관련 역할 할당을 찾습니다.

    ![Azure AD 역할-3 가지 옵션을 보여 주는 검색 및 정보 페이지](./media/pim-security-wizard/new-preview-link.png)

1. **전역 관리자 줄이기**를 선택 합니다.

    ![전역 관리자 줄이기-모든 멤버를 표시 하는 역할 창](./media/pim-security-wizard/new-preview-page.png)

1. 전역 관리자 역할 할당의 목록을 검토 합니다.

    ![전역 관리자 줄이기-모든 멤버를 표시 하는 역할 창](./media/pim-security-wizard/new-global-administrator-list.png)

1. **다음** 을 선택 하 여 적합 한 사용자 또는 그룹을 선택 하 고 **적격 설정** 또는 **할당 제거**를 선택 합니다.

    ![역할에 적합 한 멤버를 선택 하는 옵션을 사용 하 여 멤버를 적격 페이지로 변환 합니다.](./media/pim-security-wizard/new-global-administrator-buttons.png)

1. 모든 전역 관리자가 자신의 액세스를 검토 하도록 요구할 수도 있습니다.

    ![액세스 검토 섹션을 보여 주는 전역 관리자 페이지](./media/pim-security-wizard/new-global-administrator-access-review.png)

1. 이러한 변경 내용 중 하나를 선택 하면 Azure 알림이 표시 됩니다.

1. 그런 다음, 고정 **액세스 제거** 또는 **서비스 사용자 검토** 를 선택 하 여 다른 권한 있는 역할 및 서비스 사용자 역할 할당에 대해 위의 단계를 반복 합니다. 서비스 사용자 역할 할당의 경우 역할 할당만 제거할 수 있습니다.

    ![연결을 제거 하 고 서비스 주체를 검토 하는 추가 정보 옵션 ](./media/pim-security-wizard/new-preview-page-service-principals.png)

## <a name="next-steps"></a>다음 단계

- [Privileged Identity Management에서 Azure AD 역할 할당](pim-how-to-add-role-to-user.md)
- [다른 관리자에 게 Privileged Identity Management을 관리할 수 있는 권한 부여](pim-how-to-give-access-to-pim.md)
