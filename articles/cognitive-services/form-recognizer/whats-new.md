---
title: Form Recognizer의 새로운 기능
titleSuffix: Azure Cognitive Services
description: 양식 인식기 API에 대 한 최신 변경 내용을 이해 합니다.
author: PatrickFarley
manager: nitinme
ms.service: cognitive-services
ms.subservice: forms-recognizer
ms.topic: conceptual
ms.date: 05/19/2020
ms.author: pafarley
ms.openlocfilehash: 22eab216714d45e4b8a91fd58325424d4baef95e
ms.sourcegitcommit: dccb85aed33d9251048024faf7ef23c94d695145
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87272949"
---
# <a name="whats-new-in-form-recognizer"></a>Form Recognizer의 새로운 기능

양식 인식기 서비스는 지속적으로 업데이트 됩니다. 이 문서를 사용 하면 향상 된 기능, 수정 사항 및 설명서 업데이트를 최신 상태로 유지할 수 있습니다.

> [!NOTE]
> 폼 인식기에 대 한 빠른 시작 및 가이드는 지정 되지 않은 경우 항상 최신 버전의 API를 사용 합니다.

## <a name="july-2020"></a>2020년 7월

### <a name="new-features"></a>새로운 기능
* v2.0 **참조 사용 가능** [.Net](https://docs.microsoft.com/dotnet/api/overview/azure/ai.formrecognizer-readme-pre?view=azure-dotnet), [Python](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python), [JAVA](https://docs.microsoft.com/java/api/overview/azure/ai-formrecognizer-readme-pre?view=azure-java-preview)및 [JavaScript](https://docs.microsoft.com/javascript/api/overview/azure/?view=azure-node-latest)용 v2.0 [API 참조](https://westus2.dev.cognitive.microsoft.com/docs/services/form-recognizer-api-v2/operations/AnalyzeWithCustomForm) 및 업데이트 된 sdk를 봅니다.
* 향상 된 **테이블 향상** 기능 및 향상 된 기능으로는 향상 된 기능 및 테이블 추출 향상 된 기능, 특히 레이블 없이 사용자 지정 학습에서 테이블 헤더와 구조를 학습 하는 기능이 있습니다. 
* **통화 지원** 전역 통화 기호의 검색 및 추출
* **Azure .gov** 이제 Azure .Gov 에서도 폼 인식기를 사용할 수 있습니다.
* **향상 된 보안 기능**: 
   * 사용자 **고유의 키 가져오기**  양식 인식기는 클라우드로 지속 될 때 데이터를 자동으로 암호화 하 여 보호 하 고 조직의 보안 및 규정 준수 약정을 충족 하는 데 도움을 줍니다. 기본적으로 구독은 Microsoft에서 관리 하는 암호화 키를 사용 합니다. 이제 사용자 고유의 암호화 키를 사용 하 여 구독을 관리할 수도 있습니다. [BYOK (사용자 고유 키 사용) 라고도 하는 CMK (고객 관리 키)](https://docs.microsoft.com/azure/cognitive-services/form-recognizer/form-recognizer-encryption-of-data-at-rest)는 액세스 제어를 보다 유연 하 게 만들고, 회전 하 고, 사용 하지 않도록 설정 하 고, 취소할 수 있는 유연성을 제공 합니다. 데이터를 보호 하는 데 사용 되는 암호화 키를 감사할 수도 있습니다.  
   * **개인 끝점** – 가상 네트워크 (VNet)에서 [개인 링크를 통해 안전](https://docs.microsoft.com/azure/private-link/private-link-overview) 하 게 데이터에 액세스할 수 있습니다.


## <a name="june-2020"></a>2020년 6월

### <a name="new-features"></a>새로운 기능
* **클라이언트 sdk에 추가 된 Copymodel API** 이제 클라이언트 Sdk를 사용 하 여 한 구독에서 다른 구독으로 모델을 복사할 수 있습니다. 이 기능에 대 한 일반 정보는 [모델 백업 및 복구](./disaster-recovery.md) 를 참조 하세요.
* **Azure Active Directory 통합** 이제 AAD 자격 증명을 사용 하 여 Sdk에서 양식 인식기 클라이언트 개체를 인증할 수 있습니다.
* **SDK 관련 변경 내용** 여기에는 보조 기능 추가 및 주요 변경 내용이 모두 포함 됩니다. 자세한 내용은 SDK changelogs를 참조 하십시오.
  * [C # SDK Preview 3 변경 로그](https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/formrecognizer/Azure.AI.FormRecognizer/CHANGELOG.md)
  * [Python SDK Preview 3 변경 로그](https://github.com/Azure/azure-sdk-for-python/blob/master/sdk/formrecognizer/azure-ai-formrecognizer/CHANGELOG.md)
  * [Java SDK Preview 3 변경 로그](https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/formrecognizer/azure-ai-formrecognizer/CHANGELOG.md)
  * [JavaScript SDK Preview 3 변경 로그](https://github.com/Azure/azure-sdk-for-js/blob/%40azure/ai-form-recognizer_1.0.0-preview.3/sdk/formrecognizer/ai-form-recognizer/CHANGELOG.md)

## <a name="april-2020"></a>2020년 4월

### <a name="new-features"></a>새로운 기능
* **양식 인식기 API v 2.0 공개 미리 보기에 대 한 SDK 지원** 이번 달에는 폼 인식기 v2.0 (미리 보기) 릴리스에 대 한 미리 보기 SDK를 포함 하도록 서비스 지원을 확장 했습니다. 아래 링크를 사용 하 여 원하는 언어로 시작 하세요. 
   * [.NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/ai.formrecognizer-readme-pre?view=azure-dotnet)
   * [Java SDK](https://docs.microsoft.com/java/api/overview/azure/ai-formrecognizer-readme-pre?view=azure-java-preview)
   * [Python SDK](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)
   * [JavaScript SDK](https://docs.microsoft.com/javascript/api/overview/azure/?view=azure-node-latest)

  새 SDK는 폼 인식기에 대 한 v2.0 REST API의 모든 기능을 지원 합니다. 예를 들어 레이블을 사용 하거나 사용 하지 않고 모델을 학습 하 고, 폼에서 텍스트, 키 값 쌍 및 테이블을 추출 하 고, 미리 작성 된 수신 서비스를 사용 하 여 수신 확인에서 데이터를 추출 하 고, 문서의 레이아웃 서비스를 사용 하 여 텍스트와 테이블을 추출할 수 있습니다. [Sdk 피드백 양식](https://aka.ms/FR_SDK_v1_feedback)을 통해 sdk에서 사용자 의견을 공유할 수 있습니다.
 
* **사용자 지정 모델 복사** 이제 새 사용자 지정 모델 복사 기능을 사용 하 여 지역과 구독 간에 모델을 복사할 수 있습니다. 사용자 지정 모델 복사 API를 호출 하기 전에 먼저 대상 리소스 끝점에 대해 복사 권한 부여 작업을 호출 하 여 대상 리소스에 복사할 권한 부여를 가져와야 합니다.
   * [복사본 권한 부여 생성](https://westus2.dev.cognitive.microsoft.com/docs/services/form-recognizer-api-v2/operations/CopyCustomFormModelAuthorization) REST API
   * [사용자 지정 모델 복사](https://westus2.dev.cognitive.microsoft.com/docs/services/form-recognizer-api-v2/operations/CopyCustomFormModel) REST API 

### <a name="security-improvements"></a>향상된 보안 기능

* 이제 폼 인식기에서 고객 관리 키를 사용할 수 있습니다. 자세한 내용은 [폼 인식기에 대 한 미사용 데이터 암호화](https://docs.microsoft.com/azure/cognitive-services/form-recognizer/form-recognizer-encryption-of-data-at-rest)를 참조 하세요.
* Azure Active Directory를 사용 하 여 Azure 리소스에 액세스 하기 위해 관리 되는 Id를 사용 합니다. 자세한 내용은 [관리 되는 id에 대 한 액세스 권한 부여](https://docs.microsoft.com/azure/cognitive-services/authentication#authorize-access-to-managed-identities)를 참조 하세요.

## <a name="march-2020"></a>2020년 3월 

### <a name="new-features"></a>새로운 기능

* **레이블 지정을 위한 값 형식** 이제 폼 인식기 샘플 레이블 지정 도구를 사용 하 여 레이블을 지정 하는 값의 형식을 지정할 수 있습니다. 현재 지원되는 값 형식 및 변형은 다음과 같습니다.
  * `string`
    * 기본값, `no-whitespaces`, `alphanumeric`
  * `number`
    * 기본값, `currency`
  * `date` 
    * 기본값, `dmy`, `mdy`, `ymd`
  * `time`
  * `integer`

  이 기능을 사용 하는 방법에 대 한 자세한 내용은 [샘플 레이블 도구](./quickstarts/label-tool.md#specify-tag-value-types) 가이드를 참조 하세요.


* **테이블 시각화** 이제 샘플 레이블 지정 도구는 문서에서 인식 된 테이블을 표시 합니다. 이렇게 하면 레이블 지정 및 분석 전에 문서에서 인식 되 고 추출 된 테이블을 볼 수 있습니다. 계층 옵션을 사용 하 여이 기능을 설정/해제할 수 있습니다.

  다음은 테이블을 인식 하 고 추출 하는 방법의 예입니다.

  > [!div class="mx-imgBorder"]
  > ![샘플 레이블 지정 도구를 사용 하는 테이블 시각화](./media/whats-new/formre-table-viz.png)

    추출 된 테이블은의 JSON 출력에서 사용할 수 있습니다 `"pageResults"` .

  > [!IMPORTANT]
  > 테이블 레이블 지정은 지원 되지 않습니다. 테이블이 인식 되지 않고 자동으로 extrated 키/값 쌍 으로만 레이블을 지정할 수 있습니다. 테이블에 키/값 쌍으로 레이블을 지정 하는 경우 각 셀에 고유한 값으로 레이블을 지정 합니다.

### <a name="extraction-enhancements"></a>향상 된 압축 풀기

이 릴리스에는 추출 향상 및 정확성 향상, 특히 동일한 텍스트 줄에서 여러 키/값 쌍에 대 한 레이블을 만들고 추출 하는 기능이 포함 되어 있습니다. 
 
### <a name="sample-labeling-tool-is-now-open-source"></a>이제 샘플 레이블 지정 도구는 오픈 소스입니다.

이제 폼 인식기 샘플 레이블 지정 도구를 오픈 소스 프로젝트로 사용할 수 있습니다. 솔루션 내에서 통합 하 고 요구 사항에 맞게 고객 관련 변경을 수행할 수 있습니다.

폼 인식기 샘플 레이블 지정 도구에 대 한 자세한 내용은 [GitHub](https://github.com/microsoft/OCR-Form-Tools/blob/master/README.md)에서 제공 되는 설명서를 참조 하세요.

### <a name="tls-12-enforcement"></a>TLS 1.2 적용

이제 TLS 1.2는 이 서비스에 대한 모든 HTTP 요청에 적용됩니다. 자세한 내용은 [Azure Cognitive Services 보안](../cognitive-services-security.md)을 참조하세요.

## <a name="january-2020"></a>2020년 1월

이 릴리스에는 폼 인식기 2.0 (미리 보기)가 도입 되었습니다. 아래 섹션에는 새로운 기능, 향상 된 기능 및 변경 내용에 대 한 자세한 내용이 나와 있습니다. 

### <a name="new-features"></a>새로운 기능

* **사용자 지정 모델**
  * **레이블로 학습** 이제 수동으로 레이블이 지정 된 데이터를 사용 하 여 사용자 지정 모델을 학습 시킬 수 있습니다. 이 방법은 모델 성능이 향상되며, 복잡한 양식 또는 키 없는 값을 포함하는 양식과 함께 작동하는 모델을 생성할 수 있습니다.
  * **비동기 API** 비동기 API 호출을 사용 하 여 대량 데이터 집합 및 파일을 학습 하 고 분석할 수 있습니다.
  * **TIFF 파일 지원** 이제 TIFF 문서에서 데이터를 학습 하 고 추출할 수 있습니다.
  * **추출 정확도 향상**

* **미리 작성된 영수증 모델**
  * **팁 금액** 이제 팁 양과 기타 필기 값을 추출할 수 있습니다.
  * **줄 항목 추출** 수신 확인에서 품목 값을 추출할 수 있습니다.
  * **신뢰도 값** 추출 된 각 값에 대 한 모델의 신뢰도를 볼 수 있습니다.
  * **추출 정확도 향상**

* **레이아웃 추출** 이제 레이아웃 API를 사용 하 여 폼에서 텍스트 데이터 및 테이블 데이터를 추출할 수 있습니다.

### <a name="custom-model-api-changes"></a>사용자 지정 모델 API 변경

사용자 지정 모델을 학습 하 고 사용 하는 모든 Api의 이름이 변경 되었으며, 일부 동기 메서드는 비동기입니다. 주요 변경 내용은 다음과 같습니다.

* 모델 학습 프로세스는 이제 비동기식입니다. **/Dev/sd** API 호출을 통해 학습을 시작 합니다. 이 호출은 **사용자 지정/모델/{modelID}** 에 전달 하 여 학습 결과를 반환할 수 있는 작업 ID를 반환 합니다.
* 이제 키/값 추출이 **/Custom/models/{modelID}/analyze** API 호출에 의해 시작 됩니다. 이 호출은 **사용자 지정/모델/{modelID}/analyzeResults/{resultID}** 에 전달 하 여 추출 결과를 반환할 수 있는 작업 ID를 반환 합니다.
* 이제 학습 작업에 대 한 작업 Id가 **작업 위치** 헤더가 아니라 HTTP 응답의 **Location** 헤더에 있습니다.

### <a name="receipt-api-changes"></a>수신 API 변경

판매 영수증을 읽기 위한 Api의 이름이 변경 되었습니다.

* 이제 **/Prebuilt/receipt/analyze** API 호출을 통해 수신 데이터 추출을 시작 합니다. 이 호출은 **/prebuilt/receipt/analyzeResults/{resultID}** 에 전달 하 여 추출 결과를 반환할 수 있는 작업 ID를 반환 합니다.

### <a name="output-format-changes"></a>출력 형식 변경

모든 API 호출에 대 한 JSON 응답에는 새 형식이 있습니다. 일부 키 및 값이 추가, 제거 또는 이름이 변경 되었습니다. 현재 JSON 형식의 예제는 빠른 시작을 참조 하세요.

## <a name="next-steps"></a>다음 단계

[빠른 시작](quickstarts/curl-train-extract.md)을 수행하여 [Form Recognizer API](https://westus2.dev.cognitive.microsoft.com/docs/services/form-recognizer-api-v2/operations/AnalyzeWithCustomForm)를 시작합니다.