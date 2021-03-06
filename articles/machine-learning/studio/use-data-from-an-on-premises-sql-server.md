---
title: 'ML Studio (클래식): 온-프레미스 SQL Server-Azure'
description: SQL Server 데이터베이스의 데이터를 사용 하 여 Azure Machine Learning Studio (클래식)을 통해 고급 분석을 수행할 수 있습니다.
services: machine-learning
ms.service: machine-learning
ms.subservice: studio
ms.topic: how-to
author: likebupt
ms.author: keli19
ms.custom: seodec18
ms.date: 03/13/2017
ms.openlocfilehash: 133de2c6b4fd4f970595a0e46c24167ab10c0aea
ms.sourcegitcommit: 0b8320ae0d3455344ec8855b5c2d0ab3faa974a3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87432122"
---
# <a name="perform-analytics-with-azure-machine-learning-studio-classic-using-a-sql-server-database"></a>SQL Server 데이터베이스를 사용 하 여 Azure Machine Learning Studio (클래식)으로 분석 수행

**적용 대상:** ![ 예 ](../../../includes/media/aml-applies-to-skus/yes.png) Machine Learning Studio (클래식) ![ 아니요](../../../includes/media/aml-applies-to-skus/no.png)[Azure Machine Learning](../compare-azure-ml-to-studio-classic.md)  


온-프레미스 데이터로 작업하는 기업에서는 종종 기계 학습 워크로드를 위해 클라우드의 규모와 민첩성을 활용하려고 합니다. 하지만 클라우드로 온-프레미스 데이터를 이동하여 현재 비즈니스 프로세스 및 워크플로를 중단하지 않으려고 합니다. Azure Machine Learning Studio (클래식)에서는 이제 SQL Server 데이터베이스에서 데이터를 읽은 다음이 데이터를 사용 하 여 모델을 학습 하 고 점수를 매길 수 있습니다. 더 이상 클라우드 및 온-프레미스 서버 간에 데이터를 수동으로 복사하고 동기화할 필요가 없습니다. 대신 Azure Machine Learning Studio (클래식)의 **데이터 가져오기** 모듈에서 학습 및 점수 매기기 작업을 위해 SQL Server 데이터베이스에서 직접 읽을 수 있습니다.

이 문서에서는 SQL Server 데이터를 Azure Machine Learning Studio (클래식)로 수신 하는 방법에 대 한 개요를 제공 합니다. 사용자가 작업 영역, 모듈, 데이터 집합, *실험 등의*Studio (클래식) 개념을 잘 알고 있다고 가정 합니다.

> [!NOTE]
> 이 기능을 무료 작업 영역에서는 사용할 수 없습니다. Machine Learning 가격 책정 및 계층에 대한 자세한 내용은 [Azure Machine Learning 가격 책정](https://azure.microsoft.com/pricing/details/machine-learning/)을 참조하세요.
>
>

<!-- -->



## <a name="install-the-data-factory-self-hosted-integration-runtime"></a>Data Factory 자체 호스팅 통합 런타임 설치
Azure Machine Learning Studio (클래식)에서 SQL Server 데이터베이스에 액세스 하려면 이전에 데이터 관리 게이트웨이의 Data Factory 자체 호스팅 Integration Runtime를 다운로드 하 여 설치 해야 합니다. Machine Learning Studio (클래식)에서 연결을 구성 하는 경우 아래에 설명 된 **데이터 게이트웨이 다운로드 및 등록** 대화 상자를 사용 하 여 IR (Integration Runtime)을 다운로드 하 고 설치할 수 있습니다.


[Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=39717)에서 MSI 설치 패키지를 다운로드하고 실행하여 IR을 미리 설치할 수도 있습니다. MSI를 사용하여 모든 설정을 유지하면서 기존 IR을 최신 버전으로 업그레이드할 수도 있습니다.

Data Factory 자체 호스팅 통합 런타임에는 다음과 같은 필수 조건이 있습니다.

* Data Factory 자체 호스팅 통합에는 .NET Framework 4.6.1 이상이 있는 64비트 운영 체제가 필요합니다.
* 지원되는 Windows 운영 체제 버전은 Windows 10 , Windows Server 2012, Windows Server 2012 R2, Windows Server 2016입니다. 
* IR 머신에 대한 권장 구성은 최소한 2GHz, 코어 CPU 4개, 8GB RAM 및 80GB 디스크입니다.
* 호스트 컴퓨터가 최대 절전 모드인 경우 IR은 데이터 요청에 응답 하지 않습니다. 따라서 IR을 설치하기 전에 컴퓨터에서 전원 계획을 적절하게 구성합니다. 머신이 최대 절전 모드로 구성된 경우, IR 설치에서 메시지가 표시됩니다.
* 복사 활동은 특정 주기에 실행되므로 컴퓨터에서 리소스 사용(CPU, 메모리)은 유휴 시간 사용량이 가장 많을 때와 동일한 패턴을 따릅니다. 리소스 사용률은 이동하는 데이터 양에 따라 달라집니다. 여러 복사 작업이 진행 중인 경우 사용량이 많은 시간 동안 리소스 사용량이 증가하는 것을 볼 수 있습니다. 위에 나열된 최소 구성이 기술적으로는 충분하지만 데이터 이동에 대한 특정 부하에 따라 최소 구성보다 더 많은 리소스를 사용하는 구성이 좋습니다.

Data Factory 자체 호스팅 통합 런타임을 설정하고 사용하는 경우, 다음 사항을 고려하세요.

* 단일 컴퓨터에 IR 인스턴스를 한 개만 설치할 수 있습니다.
* 여러 온-프레미스 데이터 원본에 대해 단일 IR을 사용할 수 있습니다.
* 서로 다른 컴퓨터의 여러 IR을 동일한 온-프레미스 데이터 원본에 연결할 수 있습니다.
* 한 번에 하나의 작업 영역에 대 한 IRs 구성 합니다. 현재 작업 영역에서 IRs를 공유할 수 없습니다.
* 단일 작업 영역에 대해 여러 IR을 구성할 수 있습니다. 예를 들어 개발 중에 테스트 데이터 원본에 연결 된 IR을 사용 하 고 운영 준비가 되 면 프로덕션 IR을 사용할 수 있습니다.
* IR이 데이터 원본과 동일한 머신에 있을 필요는 없습니다. 그러나 게이트웨이를 데이터 원본 가까이에 배치하면 게이트웨이가 데이터 원본에 연결하는 데 걸리는 시간을 줄일 수 있습니다. 게이트웨이와 데이터 원본이 리소스를 경합하지 않도록 온-프레미스 데이터 원본을 호스트하는 머신이 아닌 다른 머신에 IR을 설치하는 것이 좋습니다.
* Power BI 또는 Azure Data Factory 시나리오를 처리 하는 컴퓨터에 IR이 이미 설치 되어 있는 경우 Azure Machine Learning Studio (클래식)에 대 한 별도 IR을 다른 컴퓨터에 설치 합니다.

  > [!NOTE]
  > 동일한 컴퓨터에서 Data Factory 자체 호스팅 통합 런타임과 Power BI Gateway를 실행할 수는 없습니다.
  >
  >
* 다른 데이터에 대해 Azure Express 경로를 사용 하는 경우에도 Azure Machine Learning Studio (클래식)에 대 한 Data Factory 자체 호스팅 Integration Runtime를 사용 해야 합니다. ExpressRoute를 사용하더라도 데이터 원본은 방화벽으로 보호되는 온-프레미스 데이터 원본으로 취급해야 합니다. Data Factory 자체 호스팅 통합 런타임을 사용하여 Machine Learning과 데이터 원본 간의 연결을 설정합니다.

[Data Factory의 통합 런타임](../../data-factory/concepts-integration-runtime.md) 문서에서 설치 필수 조건, 설치 단계 및 문제 해결 팁에 대한 자세한 정보를 확인할 수 있습니다.

## <a name="span-idusing-the-data-gateway-step-by-step-walk-classanchorspan-id_toc450838866-classanchorspanspaningress-data-from-your-sql-server-database-into-azure-machine-learning"></a><span id="using-the-data-gateway-step-by-step-walk" class="anchor"><span id="_Toc450838866" class="anchor"></span></span>SQL Server 데이터베이스에서 Azure Machine Learning로 데이터를 수신 합니다.
이 연습에서는 Azure Machine Learning 작업 영역에서 Azure Data Factory Integration Runtime를 설정 하 고 구성한 다음 SQL Server 데이터베이스에서 데이터를 읽습니다.

> [!TIP]
> 시작 하기 전에에 대 한 브라우저의 팝업 차단을 사용 하지 않도록 설정 `studio.azureml.net` 합니다. Google Chrome 브라우저를 사용하는 경우 Google Chrome 웹 저장소 [Click Once App Extension](https://chrome.google.com/webstore/search/clickonce?_category=extensions)에서 사용할 수 있는 일부 플러그 인 중에서 하나를 다운로드하여 설치합니다.
>
> [!NOTE]
> Azure Data Factory 자체 호스팅 통합 런타임은 이전에 데이터 관리 게이트웨이라고 했습니다. 단계별 자습서에서는 계속 게이트웨이로 부릅니다.  

### <a name="step-1-create-a-gateway"></a>1단계: 게이트웨이 만들기
첫 번째 단계는 SQL database에 액세스 하도록 게이트웨이를 만들고 설정 하는 것입니다.

1. [Azure Machine Learning Studio (클래식)](https://studio.azureml.net/Home/) 에 로그인 하 여 작업 하려는 작업 영역을 선택 합니다.
2. 왼쪽에서 **설정** 블레이드를 클릭하고 위쪽의 **데이터 게이트웨이** 탭을 클릭합니다.
3. 화면 아래쪽에 있는 **새 데이터 게이트웨이** 를 클릭합니다.

    ![새 데이터 게이트웨이](./media/use-data-from-an-on-premises-sql-server/new-data-gateway-button.png)
4. **새 데이터 게이트웨이** 대화 상자에서 **게이트웨이 이름**을 입력하고 필요에 따라 **설명**을 추가합니다. 오른쪽 아래에 있는 화살표를 클릭하여 구성의 다음 단계로 이동합니다.

    ![게이트웨이 이름 및 설명 입력](./media/use-data-from-an-on-premises-sql-server/new-data-gateway-dialog-enter-name.png)
5. 데이터 게이트웨이 다운로드 및 등록 대화 상자에서 게이트웨이 등록 키를 클립보드에 복사합니다.

    ![다운로드 및 데이터 게이트웨이 등록](./media/use-data-from-an-on-premises-sql-server/download-and-register-data-gateway.png)
6. <span id="note-1" class="anchor"></span>Microsoft 데이터 관리 게이트웨이를 아직 다운로드해서 설치하지 않은 경우 **데이터 관리 게이트웨이 다운로드**를 클릭합니다. 이렇게 하면 필요한 게이트웨이 버전을 선택하고 다운로드한 후 설치할 수 있는 Microsoft 다운로드 센터로 이동하게 됩니다. [온-프레미스 원본과 클라우드 간에 데이터 관리 게이트웨이로 데이터 이동](../../data-factory/tutorial-hybrid-copy-portal.md)문서의 시작 섹션에서 설치 필수 구성 요소, 설치 단계 및 문제 해결 팁에 대한 자세한 정보를 찾을 수 있습니다.
7. 게이트웨이가 설치되면 데이터 관리 게이트웨이 구성 관리자가 열리고 **게이트웨이 등록** 대화 상자가 표시됩니다. 클립보드에 복사한 **게이트웨이 등록 키**를 붙여 넣고 **등록**을 클릭합니다.
8. 게이트웨이가 이미 설치되어 있는 경우 데이터 관리 게이트웨이 구성 관리자를 실행합니다. **키 변경**을 클릭하고 이전 단계에서 클립보드에 복사한 **게이트웨이 등록 키**를 붙여 넣고 **확인**을 클릭합니다.
9. 설치가 완료되면 Microsoft 데이터 관리 게이트웨이 구성 관리자에 대한 **게이트웨이 등록** 대화 상자가 표시됩니다. 이전 단계에서 클립보드에 복사한 게이트웨이 등록 키를 붙여 넣고 **등록**을 클릭합니다.

    ![게이트웨이 등록](./media/use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-register-gateway.png)
10. Microsoft 데이터 관리 게이트웨이 구성 관리자의 **홈** 탭에서 다음 값에 설정되면 게이트웨이 구성이 완료된 것입니다.

    * **게이트웨이 이름** 및 **인스턴스 이름**이 게이트웨이의 이름으로 설정됩니다.
    * **등록**이 **등록됨**으로 설정됩니다.
    * **상태**가 **시작됨**으로 설정됩니다.
    * 아래쪽의 상태 표시줄에는 녹색 확인 표시와 함께 **데이터 관리 게이트웨이 클라우드 서비스에 연결 됨** 이 표시 됩니다.

      ![데이터 관리 게이트웨이 관리자](./media/use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-registered.png)

      등록에 성공 하면 Azure Machine Learning Studio (클래식)도 업데이트 됩니다.

    ![게이트웨이 등록 성공](./media/use-data-from-an-on-premises-sql-server/gateway-registered.png)
11. **데이터 게이트웨이 다운로드 및 등록** 대화 상자에서 확인 표시를 클릭하여 설정을 완료합니다. **설정** 페이지에 게이트웨이 상태가 "온라인"으로 표시됩니다. 오른쪽 창에서 상태 및 기타 유용한 정보를 찾을 수 있습니다.

    ![게이트웨이 설정](./media/use-data-from-an-on-premises-sql-server/gateway-status.png)
12. Microsoft 데이터 관리 Gateway에서 **인증서** 탭으로 전환 Configuration Manager 합니다. 이 탭에 지정 된 인증서는 포털에서 지정한 온-프레미스 데이터 저장소에 대 한 자격 증명을 암호화/해독 하는 데 사용 됩니다. 이 인증서는 기본 인증서입니다. 이 인증서를 인증서 관리 시스템에서 백업하는 자체 인증서로 변경하는 것이 좋습니다. **변경** 을 클릭하여 그 대신 사용자 고유의 인증서를 사용합니다.

    ![게이트웨이 인증서 변경](./media/use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-certificate.png)
13. (선택 사항) 게이트웨이와 관련된 문제를 해결하기 위해 자세한 정보 표시 로깅을 사용하도록 설정하려면 Microsoft 데이터 관리 게이트웨이 구성 관리자에서 **진단** 탭으로 전환하고 **문제 해결용 자세한 정보 표시 로깅 사용** 옵션을 선택합니다. 로깅 정보는 Windows 이벤트 뷰어의 **응용 프로그램 및 서비스 로그**  - &gt; **데이터 관리 게이트웨이** 노드 아래에서 찾을 수 있습니다. 또한 **진단** 탭을 사용하여 게이트웨이를 사용하여 온-프레미스 데이터 원본에 대한 연결을 테스트할 수도 있습니다.

    ![자세한 정보 로깅 사용](./media/use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-verbose-logging.png)

Azure Machine Learning Studio (클래식)에서 게이트웨이 설치 프로세스를 완료 합니다.
이제 온-프레미스 데이터를 사용할 준비가 되었습니다.

각 작업 영역에 대해 Studio (클래식)에서 여러 게이트웨이를 만들고 설정할 수 있습니다. 예를 들어 개발 중에는 테스트 데이터 원본에 연결하기 위한 게이트웨이를 사용하고 프로덕션 데이터 원본에 연결할 때는 다른 게이트웨이를 사용할 수 있습니다. Azure Machine Learning Studio (클래식)은 회사 환경에 따라 여러 게이트웨이를 설정 하는 유연성을 제공 합니다. 현재 작업 영역 간에 게이트웨이를 공유할 수 없으며 단일 컴퓨터에 하나의 게이트웨이만 설치할 수 있습니다. 자세한 내용은 [온-프레미스 원본과 클라우드 간에 데이터 관리 게이트웨이로 데이터 이동](../../data-factory/tutorial-hybrid-copy-portal.md)을 참조하세요.

### <a name="step-2-use-the-gateway-to-read-data-from-an-on-premises-data-source"></a>2단계: 게이트웨이를 사용하여 온-프레미스 데이터 원본에서 데이터 읽기
게이트웨이를 설정한 후에 SQL Server 데이터베이스의 데이터를 입력 하는 실험에 **데이터 가져오기** 모듈을 추가할 수 있습니다.

1. Machine Learning Studio (클래식)에서 **실험** 탭을 선택 하 고, 왼쪽 아래 모서리에서 **+ 새로 만들기** 를 클릭 하 고, **빈 실험** 을 선택 하거나, 사용할 수 있는 몇 가지 샘플 실험 중 하나를 선택 합니다.
2. **데이터 가져오기** 모듈을 찾아 실험 캔버스로 끌어 놓습니다.
3. 캔버스 아래에서 **다른 이름으로 저장** 을 클릭합니다. 실험 이름에 "Azure Machine Learning Studio (클래식) 온-프레미스 SQL Server 자습서"를 입력 하 고 작업 영역을 선택한 후 **확인** 확인 표시를 클릭 합니다.

   ![실험을 새 이름으로 저장](./media/use-data-from-an-on-premises-sql-server/experiment-save-as.png)
4. **데이터 가져오기** 모듈을 클릭하여 선택하고 캔버스 오른쪽에 있는 **속성** 창의 **데이터 원본** 드롭다운 목록에서 "온-프레미스 SQL Database"를 선택합니다.
5. 설치하여 등록한 **데이터 게이트웨이** 를 선택합니다. "(새 데이터 게이트웨이 추가...)"를 선택하여 다른 게이트웨이를 설정할 수 있습니다.

   ![데이터 가져오기 모듈에 대해 데이터 게이트웨이 선택](./media/use-data-from-an-on-premises-sql-server/import-data-select-on-premises-data-source.png)
6. SQL **Database 서버 이름** 및 **Database 이름**과 실행하려는 SQL **Database 쿼리**를 입력합니다.
7. **사용자 이름 및 암호** 아래에서 **값 입력**을 클릭하고 데이터베이스 자격 증명을 입력합니다. SQL Server 구성 된 방법에 따라 Windows 통합 인증 또는 SQL Server 인증을 사용할 수 있습니다.

   ![데이터베이스 자격 증명 입력](./media/use-data-from-an-on-premises-sql-server/database-credentials.png)

   "값 필요" 메시지가 녹색 확인 표시가 있는 "값 설정"으로 변경됩니다. 데이터베이스 정보 또는 암호를 변경하지 않는 한, 자격 증명은 한 번만 입력하면 됩니다. Azure Machine Learning Studio (클래식)는 게이트웨이를 설치할 때 제공한 인증서를 사용 하 여 클라우드의 자격 증명을 암호화 합니다. Azure는 암호화되지 않은 온-프레미스 자격 증명을 절대 저장하지 않습니다.

   ![데이터 모듈 속성 가져오기](./media/use-data-from-an-on-premises-sql-server/import-data-properties-entered.png)
8. **실행** 을 클릭하여 실험을 실행합니다.

실험 실행이 완료되면 **데이터 가져오기** 모듈의 출력 포트를 클릭하고 **시각화**를 선택하여 데이터베이스에서 가져온 데이터를 시각화할 수 있습니다.

실험 개발이 끝나면 모델을 배포하고 운영할 수 있습니다. Batch 실행 서비스를 사용 하 여 **데이터 가져오기** 모듈에 구성 된 SQL Server 데이터베이스의 데이터를 읽고 점수를 매기는 데 사용 합니다. 온-프레미스 데이터의 점수를 매기는 데 요청 응답 서비스를 사용할 수 있지만, 대신 [Excel 추가 기능](excel-add-in-for-web-services.md) 을 사용하는 것이 좋습니다. 현재 실험 또는 게시 된 웹 서비스에서 **데이터 내보내기** 를 통해 SQL Server 데이터베이스에 대 한 쓰기를 지원 하지 않습니다.
