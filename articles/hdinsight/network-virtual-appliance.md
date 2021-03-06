---
title: Azure HDInsight에서 네트워크 가상 어플라이언스 구성
description: Azure HDInsight에서 네트워크 가상 어플라이언스에 대 한 다양 한 추가 기능을 구성 하는 방법에 대해 알아봅니다.
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: how-to
ms.date: 06/30/2020
ms.openlocfilehash: 805be8d5c9ab4f6316251adbb9bce3e99f4fa01d
ms.sourcegitcommit: 124f7f699b6a43314e63af0101cd788db995d1cb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86086673"
---
# <a name="configure-network-virtual-appliance-in-azure-hdinsight"></a>Azure HDInsight에서 네트워크 가상 어플라이언스 구성

> [!Important]
> 다음 정보는 Azure 방화벽 이외의 NVA (네트워크 가상 어플라이언스)를 구성 하려는 경우에 **만** 필요 합니다.

Azure 방화벽은 몇 가지 일반적인 중요 시나리오에 대 한 트래픽을 허용 하도록 자동으로 구성 됩니다. 다른 네트워크 가상 어플라이언스를 사용 하려면 몇 가지 추가 기능을 구성 해야 합니다. 네트워크 가상 어플라이언스를 구성할 때 다음 요소를 염두에 두어야 합니다.

* 서비스 끝점을 사용 하 여 서비스 끝점을 구성할 수 있습니다. 이러한 서비스 끝점은 일반적으로 비용 또는 성능 고려 사항에 대해 NVA를 우회 합니다.
* IP 주소 종속성은 비 HTTP/S 트래픽 (TCP 및 UDP 트래픽 모두)을 위한 것입니다.
* NVA 장치에서 FQDN HTTP/HTTPS 끝점을 허용 목록 수 있습니다.
* 만든 경로 테이블을 HDInsight 서브넷에 할당 합니다.

## <a name="service-endpoint-capable-dependencies"></a>서비스 끝점 지원 종속성

필요에 따라 NVA를 우회 하는 다음 서비스 끝점을 하나 이상 사용할 수 있습니다. 이 옵션은 비용을 절약 하 고 성능 최적화를 위해 많은 양의 데이터를 전송 하는 데 유용할 수 있습니다. 

| **엔드포인트** |
|---|
| Azure SQL |
| Azure Storage |
| Azure Active Directory |

### <a name="ip-address-dependencies"></a>IP 주소 종속성

| **엔드포인트** | **세부 정보** |
|---|---|
| [여기](hdinsight-management-ip-addresses.md) 에 게시 된 ip | 이러한 Ip는 HDInsight 제어에 사용 되며 비대칭 라우팅을 방지 하기 위해 UDR에 포함 되어야 합니다. |
| AAD-DS 개인 Ip | ESP 클러스터에만 필요 합니다.|


### <a name="fqdn-httphttps-dependencies"></a>FQDN HTTP/HTTPS 종속성

> [!Important]
> 아래 목록은 가장 중요 한 Fqdn 중 일부를 제공 합니다. [이 파일에서](https://github.com/Azure-Samples/hdinsight-fqdn-lists/blob/master/HDInsightFQDNTags.json)nva를 구성 하기 위해 fqdn의 전체 목록 (대부분 Azure Storage 및 Azure Service Bus)을 가져올 수 있습니다. 이러한 종속성은 HDInsight 제어 평면 작업에서 클러스터를 성공적으로 만드는 데 사용 됩니다.

| **엔드포인트**                                                          |
|---|
| azure.archive.ubuntu.com:80                                           |
| security.ubuntu.com:80                                                |
| ocsp.msocsp.com:80                                                    |
| ocsp.digicert.com:80                                                  |

## <a name="next-steps"></a>다음 단계

* [아웃바운드 트래픽을 제한하는 방화벽 사용](./hdinsight-restrict-outbound-traffic.md)
* [Azure HDInsight 가상 네트워크 아키텍처](hdinsight-virtual-network-architecture.md)
