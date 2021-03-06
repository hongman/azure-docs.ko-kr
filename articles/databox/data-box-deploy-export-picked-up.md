---
title: 내보내기 순서로 Azure Data Box를 반송하는 자습서 | Microsoft Docs
description: 내보내기 순서가 완료된 후 Azure Data Box를 Microsoft로 배송하는 방법 알아보기
services: databox
author: alkohli
ms.service: databox
ms.subservice: pod
ms.topic: tutorial
ms.date: 07/10/2020
ms.author: alkohli
ms.openlocfilehash: 7023d29bcb559f4edf11b374b9bfb959e968f626
ms.sourcegitcommit: 3541c9cae8a12bdf457f1383e3557eb85a9b3187
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86208861"
---
# <a name="tutorial-return-azure-data-box-preview"></a>자습서: Azure Data Box 반환(미리 보기)


이 자습서에서는 Azure Data Box를 반환하는 방법을 설명하고 디바이스가 Azure 데이터에서 수신되면 데이터가 지워집니다.

이 자습서에서는 다음과 같은 주제에 대해 학습합니다.

> [!div class="checklist"]
> * 필수 구성 요소
> * 배송 준비
> * Microsoft에 Data Box 배송
> * Data Box에서 데이터 지우기

[!INCLUDE [Data Box feature is in preview](../../includes/data-box-feature-is-preview-info.md)]

## <a name="prerequisites"></a>필수 구성 요소

시작하기 전에 다음 사항을 확인합니다.

- [자습서: Azure Data Box에서 데이터 복사](data-box-deploy-export-copy-data.md)를 완료했습니다. 
- 복사 작업이 완료되었습니다. 복사 작업이 진행 중이면 배송 준비를 실행할 수 없습니다.

## <a name="prepare-to-ship"></a>배송 준비

[!INCLUDE [data-box-export-prepare-to-ship](../../includes/data-box-export-prepare-to-ship.md)]

다음 단계는 디바이스를 반송하는 위치에 따라 결정됩니다.

## <a name="ship-data-box-back"></a>Data Box 반송

디바이스에서 데이터 복사가 완료되고 **배송 준비** 실행이 성공했는지 확인합니다. 디바이스를 배송하는 지역에 따라 절차가 다릅니다.

## <a name="in-us-canada-europe"></a>[미국, 캐나다, 유럽에서](#tab/in-us-canada-europe)

미국, 캐나다 또는 유럽에서 디바이스를 반송하는 경우 다음 단계를 수행합니다.

1. 디바이스의 전원이 꺼져 있고 케이블이 분리되었는지 확인합니다. 
2. 디바이스와 함께 제공된 전원 코드를 디바이스 뒷면에 스풀링하고 안전하게 고정합니다.
3. 배송 레이블이 E-ink 디스플레이에 표시되는지 확인하고 운송업체에 픽업을 예약합니다. 레이블이 손상 또는 손실되었거나 E-ink 디스플레이에 표시되지 않으면 Microsoft 지원에 문의하세요. 고객 지원팀에서 제안하는 경우 Azure Portal에서 **개요 > 배송 레이블 다운로드**로 차례로 이동합니다. 배송 레이블을 다운로드하여 디바이스에 부착합니다. 
4. 디바이스를 반송하는 경우 UPS로 픽업을 예약합니다. 픽업을 예약하려면 다음을 수행합니다.

    - 로컬 UPS(국가/지역별 무료 전화 번호)에 전화합니다.
    - 통화에서 E-ink 디스플레이 또는 인쇄된 레이블에서 표시한 대로 역방향 배송 추적 번호를 알려줍니다.
    - 추적 번호를 알려주지 않으면 픽업 시 UPS에서 추가 요금을 지불하도록 요구합니다.

    픽업을 예약하는 대신 가장 가까운 반납 위치에 Data Box를 반납할 수도 있습니다.
4. 운송업체에서 Data Box를 픽업하고 나면 포털의 주문 상태가 **픽업됨**으로 업데이트됩니다. 추적 ID도 표시됩니다.


## <a name="in-australia"></a>[오스트레일리아에서](#tab/in-australia)

오스트레일리아의 Azure 데이터 센터에는 추가 보안 알림이 있습니다. 모든 인바운드 배송에는 고급 알림이 있어야 합니다. 오스트레일리아에서 배송하려면 다음 단계를 수행합니다.


1. 반품 발송을 위해 디바이스를 배송하는 데 사용된 원래 상자를 보관하세요.
2. 디바이스로 데이터 복사가 완료되고 **배송 준비** 실행이 성공했는지 확인합니다.
3. 디바이스의 전원을 끄고 케이블을 분리합니다.
4. 디바이스와 함께 제공된 전원 코드를 디바이스 뒷면에 스풀링하고 안전하게 고정합니다.
5. [DHL 링크](https://mydhl.express.dhl/au/en/schedule-pickup.html#/schedule-pickup#label-reference)에서 온라인으로 픽업을 예약합니다.

## <a name="in-japan"></a>[일본에서](#tab/in-japan) 

1. 반품 발송을 위해 디바이스를 배송하는 데 사용된 원래 상자를 보관하세요.
2. 디바이스의 전원을 끄고 케이블을 분리합니다.
3. 디바이스와 함께 제공된 전원 코드를 디바이스 뒷면에 스풀링하고 안전하게 고정합니다.
4. 탁송 운송장에 회사 이름과 주소 정보를 보낸 사람 정보로 작성합니다.
5. 다음 이메일 템플릿을 사용하여 Quantium Solutions에 이메일을 전송합니다.

    - Japan Post Chakubarai 탁송 운송장이 포함되지 않거나 누락된 경우 이를 이메일에서 언급해야 합니다. Quantium Solutions Japan은 Japan Post에 픽업 시 탁송 운송장을 가져올 것을 요청합니다.
    - 주문이 여러 개인 경우에는 개별 픽업을 보장하도록 이메일을 보냅니다.

    ```
    To: Customerservice.JP@quantiumsolutions.com
    Subject: Pickup request for Azure Data Box｜Job name： 
    Body: 
    - Japan Post Yu-Pack tracking number (reference number)：
    - Requested pickup date：mmdd (Select a requested time slot from below).
    a. 08：00-13：00 
    b. 13：00-15：00 
    c. 15：00-17：00 
    d. 17：00-19：00 
    ```

3. 픽업을 예약한 후 Quantium Solutions에서 이메일 확인을 수신합니다. 이메일 확인에는 Chakubarai 탁송 운송장에 대한 정보도 포함되어 있습니다.

필요한 경우 다음 정보로 Quantium Solutions 지원(일본어)에 문의할 수 있습니다. 

- 이메일: Customerservice.JP@quantiumsolutions.com 
- 전화: 03-5755-0150 


## <a name="in-singapore"></a>[싱가포르에서](#tab/in-singapore) 

1. 반품 발송을 위해 디바이스를 배송하는 데 사용된 원래 상자를 보관하세요.
2. Data Box 로컬 웹 UI의 배송 준비 페이지에 참조 번호로 표시된 추적 번호를 적어둡니다. 이는 배송 준비 단계가 성공적으로 완료된 후에 사용할 수 있습니다. 이 페이지에서 배송 레이블을 다운로드하고 압축 상자에 붙여넣습니다. 
3. 디바이스의 전원을 끄고 케이블을 분리합니다.
4. 디바이스와 함께 제공된 전원 코드를 디바이스 뒷면에 스풀링하고 안전하게 고정합니다. 
5. 추적 번호가 포함된 다음 이메일 템플릿을 사용하여 SingPost Customer Service에 이메일을 보냅니다.

    ```
    To: kadcustcare@singpost.com
    Subject: Microsoft Azure Pick-up - OrderName 
    Body: 
        1. Requestor name  
        2. Requestor contact number
        3. Requestor collection address
        4. Preferred collection date
    ```

   > [!NOTE]
   > 영업일에 수신된 예약 요청:
   > - 오후 3시 이전에는 오전 9시에서 오후 1시 사이에 다음 영업일에 픽업합니다.
   > - 오후 3시 이후에는 오후 2시에서 오후 6시 사이에 다음 영업일에 픽업합니다.  


## <a name="self-managed"></a>[자체 관리](#tab/in-selfmanaged) 

일본, 싱가포르, 대한민국 및 서유럽에서 Data Box를 사용 중이고 주문 생성 중에 자체 관리 배송 옵션을 선택한 경우 다음 지침을 따르세요. 

1. 이 단계가 성공적으로 완료된 후 Data Box 로컬 웹 UI의 배송 준비 페이지에 표시된 인증 코드를 적어둡니다.
2. 디바이스의 전원을 끄고 케이블을 분리합니다. 디바이스와 함께 제공된 전원 코드를 디바이스 뒷면에 스풀링하고 안전하게 고정합니다.
3. 디바이스를 반환할 준비가 되면 아래 템플릿을 사용하여 Azure Data Box 운영 팀에 이메일을 보냅니다.
    
    ```
    To: adbops@microsoft.com 
    Subject: Request for Azure Data Box drop-off for order: ‘orderName’ 
    Body: 
        1. Order name  
        2. Authorization code available after Prepare to Ship has completed [Yes/No]  
        3. Contact name of the person dropping off. You will need to display a Government approved ID during the drop off.
    ```
---

## <a name="erasure-of-data-from-data-box"></a>Data Box에서 데이터 지우기
 
디바이스가 Azure 데이터 센터에 도달하면 Data Box는 [NIST SP 800-88 개정 1 지침](https://csrc.nist.gov/News/2014/Released-SP-800-88-Revision-1,-Guidelines-for-Medi)에 따라 디스크의 데이터를 지웁니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음과 같은 항목에 대해 알아보았습니다.

> [!div class="checklist"]
> * 필수 구성 요소
> * 배송 준비
> * Microsoft에 Data Box 배송
> * Data Box에서 데이터 지우기

다음 문서로 넘어가서 Data Box를 관리하는 방법을 알아보세요.

> [!div class="nextstepaction"]
> [Azure Portal을 통해 Data Box 관리](./data-box-portal-admin.md)


