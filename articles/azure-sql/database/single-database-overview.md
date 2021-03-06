---
title: 단일 데이터베이스는 무엇 인가요?
description: Azure SQL Database의 단일 데이터베이스 리소스 형식에 대해 알아봅니다.
services: sql-database
ms.service: sql-database
ms.subservice: single-database
ms.custom: sqldbrb=1
ms.devlang: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
ms.reviewer: ''
ms.date: 04/08/2019
ms.openlocfilehash: 8f92fe8e4a4ebbc2d970bf28e415859249b9f67c
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "84343322"
---
# <a name="what-is-a-single-database-in-azure-sql-database"></a>Azure SQL Database의 단일 데이터베이스는 무엇입니까?
[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]

단일 데이터베이스 리소스 유형은 자체 리소스 집합을 사용 하 여 Azure SQL Database에 데이터베이스를 만들고 [서버](logical-servers.md)를 통해 관리 됩니다. 단일 데이터베이스를 사용 하는 경우 각 데이터베이스는 격리 되 고 이식 가능 합니다. 각에는 [DTU 기반 구매 모델](service-tiers-dtu.md) 또는 [vcore 기반 구매 모델](service-tiers-vcore.md) 및 보장 된 계산 크기에 고유한 서비스 계층이 있습니다.

> [!IMPORTANT]
> 단일 데이터베이스는 Azure SQL Database에 대 한 하나의 리소스 유형입니다. 다른는 [탄력적 풀](elastic-pool-overview.md)입니다.

## <a name="dynamic-scalability"></a>동적 확장성

서버를 사용 하지 않는 계산 계층 또는 프로 비전 된 계산 계층의 작은 계산 크기에서 저렴 한 가격으로 소규모 단일 데이터베이스에 첫 번째 앱을 빌드할 수 있습니다. 언제 든 지 수동으로 또는 프로그래밍 방식으로 [계산 또는 서비스 계층](single-database-scale.md) 을 변경 하 여 솔루션의 요구 사항을 충족할 수 있습니다. 앱이나 고객에게 가동 중지 시간 없이 성능을 조정할 수 있습니다. 동적 확장성을 통해 데이터베이스는 급변하는 리소스 요구 사항에 투명하게 대응할 수 있으며, 필요할 때 필요한 리소스에 대해서만 비용을 지불할 수 있습니다.

## <a name="single-databases-and-elastic-pools"></a>단일 데이터베이스 및 탄력적 풀

리소스를 공유하기 위해 단일 데이터베이스를 [탄력적 풀](elastic-pool-overview.md)의 내부 또는 외부로 이동할 수 있습니다. 특히 사용 패턴이 비교적 예측 가능한 경우 많은 비즈니스 및 애플리케이션에서 단일 데이터베이스를 만들고 필요에 따라 충분히 성능을 확장하거나 축소할 수 있습니다. 하지만 사용 패턴을 예측할 수 없는 경우 비용과 비즈니스 모델을 관리하기 어려워질 수 있습니다. 탄력적 풀은 이 문제를 해결하도록 설계되었습니다. 개념은 간단합니다. 개별 데이터베이스가 아니라 풀에 성능 리소스를 할당하고 단일 데이터베이스 성능이 아니라 풀의 전체 성능 리소스에 대해 요금을 지불합니다.

## <a name="monitoring-and-alerting"></a>모니터링 및 경고

성능 등급과 결합 된 기본 제공 [성능 모니터링](performance-guidance.md) 및 [경고 도구](alerts-insights-configure-portal.md)를 사용 합니다. 이 도구를 사용하면 현재 또는 프로젝트의 성능 요구에 기반하여 확장 또는 축소의 영향을 신속하게 평가할 수 있습니다. 또한 보다 쉽게 모니터링할 수 있도록 [메트릭과 리소스 로그를 내보낼](metrics-diagnostic-telemetry-logging-streaming-export-configure.md) 수 SQL Database.

## <a name="availability-capabilities"></a>가용성 기능

단일 데이터베이스 및 탄력적 풀은 다양 한 가용성 특성을 제공 합니다. 자세한 내용은 [가용성 특성](sql-database-paas-overview.md#availability-capabilities)을 참조하세요.

## <a name="transact-sql-differences"></a>Transact-SQL 차이점

애플리케이션에서 사용하는 대부분의 Transact-SQL 기능은 Microsoft SQL Server와 Azure SQL Database 모두에서 완전하게 지원됩니다. 예를 들어, 데이터 형식, 연산자, 문자열, 산술, 논리 및 커서 함수 같은 핵심 SQL 구성 요소는 SQL Server 및 SQL Database에서 동일하게 작동합니다. 그러나 DDL(데이터 정의 언어) 및 DML(데이터 조작 언어) 요소에는 몇 가지 T-SQL 차이점이 있으며 그 결과 T-SQL 문 및 쿼리가 부분적으로만 지원됩니다(이 문서의 뒷부분에서 설명).

또한 Azure SQL Database은 master 데이터베이스 및 운영 체제에 대 한 종속성의 기능을 격리 하도록 디자인 되었기 때문에 지원 되지 않는 일부 기능 및 구문도 있습니다. 따라서 대부분의 서버 수준 작업이 SQL Database에 적합하지 않습니다. T-sql 문과 옵션은 서버 수준 옵션을 구성 하거나 운영 체제 구성 요소를 구성 하거나 파일 시스템 구성을 지정 하는 경우 사용할 수 없습니다. 이러한 기능이 필요한 경우 SQL Database 또는 다른 Azure 기능이나 서비스에서 다른 방법으로 사용할 수 있는 적합한 대안이 있는 경우가 많습니다.

자세한 내용은 [SQL Database로의 마이그레이션 중 Transact-SQL 차이점 해결](transact-sql-tsql-differences-sql-server.md)을 참조하세요.

## <a name="security"></a>보안

SQL Database는 다양한 [기본 제공 보안 및 규정 준수 기능](security-overview.md)을 제공하여 애플리케이션이 다양한 보안 및 규정 준수 요구 사항을 충족할 수 있도록 도와줍니다.

> [!IMPORTANT]
> Azure SQL Database는 다양 한 규정 준수 표준에 대해 인증 되었습니다. 자세한 내용은 SQL Database 준수 인증의 최신 목록을 찾을 수 있는 [Microsoft Azure 보안 센터](https://gallery.technet.microsoft.com/Overview-of-Azure-c1be3942)를 참조 하세요.

## <a name="next-steps"></a>다음 단계

- 단일 데이터베이스를 신속 하 게 시작 하려면 [단일 데이터베이스 빠른 시작 가이드](quickstart-content-reference-guide.md)를 시작 하세요.
- SQL Server 데이터베이스를 Azure로 마이그레이션하는 방법에 대한 자세한 내용은 [Azure SQL Database로 마이그레이션](migrate-to-database-from-sql-server.md)을 참조하세요.
- 지원되는 기능에 대한 자세한 내용은 [기능](features-comparison.md)을 참조하세요.
