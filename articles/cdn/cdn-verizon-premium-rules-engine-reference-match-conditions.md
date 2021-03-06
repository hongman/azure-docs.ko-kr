---
title: Verizon Premium의 Azure CDN 규칙 엔진 일치 조건
description: Verizon Premium의 Azure Content Delivery Network 규칙 엔진 일치 조건에 대한 참조 설명서
services: cdn
author: asudbring
ms.service: azure-cdn
ms.topic: article
ms.date: 05/26/2020
ms.author: allensu
ms.openlocfilehash: efd6e6a93cd4ca79e6c4b6de69f8514e2d71b252
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "84323317"
---
# <a name="azure-cdn-from-verizon-premium-rules-engine-match-conditions"></a>Verizon Premium의 Azure CDN 규칙 엔진 일치 조건

이 문서에서는 Verizon Premium의 Azure CDN(Content Delivery Network) [규칙 엔진](cdn-verizon-premium-rules-engine.md)에 사용할 수 있는 일치 조건에 대해 자세히 설명합니다.

규칙의 두 번째 부분이 일치 조건입니다. 일치 조건은 기능 집합에 대해 수행할 특정 요청 유형을 식별합니다.

예를 들어 다음을 수행하는 데 일치 조건을 사용할 수 있습니다.

- 특정 위치에서 콘텐츠에 대한 필터 요청
- 특정 IP 주소 또는 국가/지역에서 생성된 요청 필터링
- 헤더 정보에 의한 필터 요청

## <a name="match-conditions"></a><a name="top"></a>일치 조건

* [항상](#always)
* [디바이스](#device)
* [위치](#location)
* [원본](#origin)
* [요청](#request)
* [URL](#url)

### <a name="always"></a><a name="always"></a>항상

[항상 일치 조건은](https://docs.vdms.com/cdn/Content/HRE/M/Always.htm) 모든 요청에 기본 기능 집합을 적용 하도록 디자인 되었습니다.

### <a name="device"></a><a name="device"></a>장치

이러한 일치 조건은 클라이언트의 사용자 에이전트에 따라 요청을 식별 하도록 설계 되었습니다.

| Name       | 목적                                                           |
|------------|-------------------------------------------------------------------|
| 브랜드 이름 | 장치의 브랜드 이름이과 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([브랜드 이름 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/D-Brand-Name-Literal.htm)) <br> **-** 정규식 ([브랜드 이름 Regex](https://docs.vdms.com/cdn/Content/HRE/M/D-Brand-Name-Regex.htm)) <br> **-** 특정 패턴 ([브랜드 이름 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/D-Brand-Name-Wildcard.htm)) |
| 디바이스 OS | 장치의 OS가과 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([장치 OS 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/D-Device-OS-Literal.htm)) <br> **-** 정규식 ([장치 OS Regex](https://docs.vdms.com/cdn/Content/HRE/M/D-Device-OS-Regex.htm)) <br> **-** 특정 패턴 ([장치 OS 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/D-Device-OS-Wildcard.htm)) |
| 디바이스 OS 버전 | 장치의 OS 버전이과 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([장치 OS 버전 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/D-Device-OS-Version-Literal.htm)) <br> **-** 정규식 ([장치 OS 버전 Regex](https://docs.vdms.com/cdn/Content/HRE/M/D-Device-OS-Version-Regex.htm)) <br> **-** 특정 패턴 ([장치 OS 버전 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/D-Device-OS-Version-Wildcard.htm)) |
| [이중 방향 인가요?](https://docs.vdms.com/cdn/Content/HRE/M/D-Dual-Orientation.htm) | 장치에서 이중 방향을 지원 하는지 여부에 따라 요청을 식별 합니다. |
| HTML 기본 DTD | 장치의 HTML 기본 설정 DTD가과 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([HTML 기본 설정 DTD 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/D-HTML-Preferred-DTD-Literal.htm)) <br> **-** 정규식 ([HTML 기본 설정 DTD Regex](https://docs.vdms.com/cdn/Content/HRE/M/D-HTML-Preferred-DTD-Regex.htm)) <br> **-** 특정 패턴 ([HTML 기본 설정 DTD 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/D-HTML-Preferred-DTD-Wildcard.htm)) |
| [이미지 인라인?](https://docs.vdms.com/cdn/Content/HRE/M/D-Image-Inlining.htm) | 장치에서 Base64 인코딩 이미지를 지원 하는지 여부에 따라 요청을 식별 합니다. |
| [Android 입니까?](https://docs.vdms.com/cdn/Content/HRE/M/D-Is-Android.htm) | 장치에서 Android OS를 사용 하는지 여부에 따라 요청을 식별 합니다. |
| [앱 인가요?](https://docs.vdms.com/cdn/Content/HRE/M/D-Is-App.htm) | 네이티브 응용 프로그램에서 콘텐츠를 요청 했는지 여부에 따라 요청을 식별 합니다. |
| [전체 데스크톱 입니까?](https://docs.vdms.com/cdn/Content/HRE/M/D-Is-Full-Desktop.htm) | 장치에서 전체 데스크톱 환경을 제공 하는지 여부에 따라 요청을 식별 합니다. |
| [IOS 인가요?](https://docs.vdms.com/cdn/Content/HRE/M/D-Is-iOS.htm) | 장치에서 iOS를 사용 하는지 여부에 따라 요청을 식별 합니다. |
| [로봇 입니까?](https://docs.vdms.com/cdn/Content/HRE/M/D-Is-Robot.htm) | 장치가 자동화 된 HTTP 클라이언트 (예: 로봇 크롤러)로 간주 되는지 여부에 따라 요청을 식별 합니다. |
| [스마트 TV 인가요?](https://docs.vdms.com/cdn/Content/HRE/M/D-Is-Smart-TV.htm) | 장치가 스마트 TV 인지 여부에 따라 요청을 식별 합니다. |
| [스마트폰 입니까?](https://docs.vdms.com/cdn/Content/HRE/M/D-Is-Smartphone.htm) | 장치가 스마트폰 인지 여부에 따라 요청을 식별 합니다.
| [태블릿 인가요?](https://docs.vdms.com/cdn/Content/HRE/M/D-Is-Tablet.htm) | 장치가 태블릿 인지 여부에 따라 요청을 식별 합니다. |
| [터치 스크린 입니까?](https://docs.vdms.com/cdn/Content/HRE/M/D-Is-Touchscreen.htm) | 장치의 기본 포인팅 장치가 터치 스크린 인지 여부에 따라 요청을 식별 합니다. |
| [Windows Phone?](https://docs.vdms.com/cdn/Content/HRE/M/D-Is-Windows-Phone.htm) | 장치가 Windows Mobile 6.5/Windows Phone 7 이상 인지 여부에 따라 요청을 식별 합니다. |
| [무선 장치 인가요?](https://docs.vdms.com/cdn/Content/HRE/M/D-Is-Wireless-Device.htm) | 장치가 무선 인지 여부에 따라 요청을 식별 합니다. 
| 마케팅 이름 | 장치의 마케팅 이름이과 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([마케팅 이름 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/D-Marketing-Name-Literal.htm)) <br> **-** Regular expression ([Marketing Name Regex](https://docs.vdms.com/cdn/Content/HRE/M/D-Marketing-Name-Regex.htm)) <br> **-** 특정 패턴 ([마케팅 이름 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/D-Marketing-Name-Wildcard.htm)) |
| 모바일 브라우저 | 장치의 브라우저가과 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([모바일 브라우저 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/D-Mobile-Browser-Literal.htm)) <br> **-** 정규식 ([모바일 브라우저 Regex](https://docs.vdms.com/cdn/Content/HRE/M/D-Mobile-Browser-Regex.htm)) <br> **-** 특정 패턴 ([모바일 브라우저 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/D-Mobile-Browser-Wildcard.htm)) |
| 모바일 브라우저 버전 | 장치의 브라우저 버전이과 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([모바일 브라우저 버전 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/D-Mobile-Browser-Version-Literal.htm)) <br> **-** 정규식 ([모바일 브라우저 버전 Regex](https://docs.vdms.com/cdn/Content/HRE/M/D-Mobile-Browser-Version-Regex.htm)) <br> **-** 특정 패턴 ([모바일 브라우저 버전 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/D-Mobile-Browser-Version-Wildcard.htm)) |
| 모델 이름 | 장치의 모델 이름이과 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([모델 이름 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/D-Model-Name-Literal.htm)) <br> **-** 정규식 ([모델 이름 Regex](https://docs.vdms.com/cdn/Content/HRE/M/D-Model-Name-Regex.htm)) <br> **-** 특정 패턴 ([모델 이름 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/D-Model-Name-Wildcard.htm)) |
| [점진적 다운로드](https://docs.vdms.com/cdn/Content/HRE/M/D-Progressive-Download.htm) | 장치가 점진적 다운로드를 지원 하는지 여부에 따라 요청을 식별 합니다. |
| 출시 날짜 | 장치의 릴리스 날짜가과 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([릴리스 날짜 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/D-Release-Date-Literal.htm)) <br> **-** 정규식 ([릴리스 날짜 Regex](https://docs.vdms.com/cdn/Content/HRE/M/D-Release-Date-Regex.htm)) <br> **-** 특정 패턴 ([릴리스 날짜 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/D-Release-Date-Wildcard.htm)) |
| [해상도 높이](https://docs.vdms.com/cdn/Content/HRE/M/D-Resolution-Height.htm) | 장치의 높이로 요청을 식별 합니다. |
| [해상도 너비](https://docs.vdms.com/cdn/Content/HRE/M/D-Resolution-Width.htm) | 장치의 너비로 요청을 식별 합니다. |

**[맨 위로 이동](#top)**

### <a name="location"></a><a name="location"></a>위치

이 일치 조건은 요청자의 위치에 따라 요청을 식별하도록 설계되었습니다.

| Name       | 목적                                                           |
|------------|-------------------------------------------------------------------|
| [AS 숫자](https://docs.vdms.com/cdn/Content/HRE/M/AS-Number.htm) | 특정 네트워크에서 발생하는 요청을 식별합니다. |
| 도시 이름 | 는 이름이과 (와) 일치 하는 도시에서 시작 되었는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([도시 이름 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/City-Name-Literal.htm)) <br> **-** Regular expression ([City Name Regex](https://docs.vdms.com/cdn/Content/HRE/M/City-Name-Regex.htm)) |
| [Continent](https://docs.vdms.com/cdn/Content/HRE/M/Continent.htm) | 지정 된 대륙에서 시작 되는 요청을 식별 합니다. |
| [국가](https://docs.vdms.com/cdn/Content/HRE/M/Country.htm) | 지정된 국가에서 발생하는 요청을 식별합니다. |
| [DMA 코드](https://docs.vdms.com/cdn/Content/HRE/M/DMA-Code.htm) | 지정 된 metros (지정 된 시장 영역)에서 시작 되는 요청을 식별 합니다. |
| [위도](https://docs.vdms.com/cdn/Content/HRE/M/Latitude.htm) | 지정 된 위도에서 시작 되는 요청을 식별 합니다. |
| [경도](https://docs.vdms.com/cdn/Content/HRE/M/Longitude.htm) | 지정 된 경도에서 시작 되는 요청을 식별 합니다. |
| [Metro 코드](https://docs.vdms.com/cdn/Content/HRE/M/Metro-Code.htm) | 지정 된 metros (지정 된 시장 영역)에서 시작 되는 요청을 식별 합니다. |
| [우편 번호](https://docs.vdms.com/cdn/Content/HRE/M/Postal-Code.htm) | 지정 된 우편 번호에서 시작 되는 요청을 식별 합니다. |
| [지역 코드](https://docs.vdms.com/cdn/Content/HRE/M/Region-Code.htm) | 지정 된 지역에서 시작 되는 요청을 식별 합니다. |

> [!NOTE]
> **Metro 코드 또는 DMA 코드를 사용 해야 하나요?** <br>
이러한 일치 조건 모두 동일한 기능을 제공 합니다. 그러나 Metro 코드 일치 조건을 사용 하 여 DMA에서 요청을 식별 하는 것이 좋습니다.

**[맨 위로 이동](#top)**

### <a name="origin"></a><a name="origin"></a>원본

이 일치 조건은 CDN 스토리지 또는 고객 원본 서버를 가리키는 요청을 식별하도록 설계되었습니다.

| Name       | 목적                                                           |
|------------|-------------------------------------------------------------------|
| [CDN 원본](https://docs.vdms.com/cdn/Content/HRE/M/CDN-Origin.htm) | CDN 스토리지에 저장된 콘텐츠에 대한 요청을 식별합니다. |
| [고객 원본](https://docs.vdms.com/cdn/Content/HRE/M/Customer-Origin.htm) | 특정 고객 원본 서버에 저장된 콘텐츠에 대한 요청을 식별합니다. |

**[맨 위로 이동](#top)**

### <a name="request"></a><a name="request"></a>요청

이 일치 조건은 해당 속성에 따라 요청을 식별하도록 설계되었습니다.

| Name              | 목적                                                                |
|-------------------|------------------------------------------------------------------------|
| [클라이언트 IP 주소](https://docs.vdms.com/cdn/Content/HRE/M/Client-IP-Address.htm) | 특정 IP 주소에서 발생하는 요청을 식별합니다. |
| 쿠키 매개 변수  | 는와 일치 하는 쿠키를 포함 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([쿠키 매개 변수 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/Cookie-Parameter-Literal.htm)) <br> **-** 정규식 ([쿠키 매개 변수 Regex](https://docs.vdms.com/cdn/Content/HRE/M/Cookie-Parameter-Regex.htm) <br> **-** 특정 패턴 ([쿠키 매개 변수 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/Cookie-Parameter-Wildcard.htm)) |
| [에 지 CNAME](https://docs.vdms.com/cdn/Content/HRE/M/Edge-CNAME.htm) | 특정 에지 CNAME을 가리키는 요청을 식별합니다. |
| 참조 도메인 | 와 일치 하는 호스트 이름이 참조 되었는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([도메인 리터럴 참조](https://docs.vdms.com/cdn/Content/HRE/M/Referring-Domain-Literal.htm)) <br> **-** 특정 패턴 ([도메인 와일드 카드 참조](https://docs.vdms.com/cdn/Content/HRE/M/Referring-Domain-Wildcard.htm)) |
| 요청 헤더 | 는와 일치 하는 헤더를 포함 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([요청 헤더 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/Request-Header-Literal.htm)) <br> **-** 정규식 ([요청 헤더 Regex](https://docs.vdms.com/cdn/Content/HRE/M/Request-Header-Regex.htm)) <br> **-** 특정 패턴 ([요청 헤더 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/Request-Header-Wildcard.htm)) |
| [Request 메서드](https://docs.vdms.com/cdn/Content/HRE/M/Request-Method.htm) | 해당 HTTP 메서드로 요청을 식별합니다. |
| [요청 스키마](https://docs.vdms.com/cdn/Content/HRE/M/Request-Scheme.htm) | 해당 HTTP 프로토콜로 요청을 식별합니다. |

**[맨 위로 이동](#top)**

### <a name="url"></a><a name="url"></a>URL

| Name              | 목적                                                                |
|-------------------|------------------------------------------------------------------------|
| 맵의 경로와 | 파일 이름을 포함 하 여 상대 경로가과 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([URL 경로 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/URL-Path-Literal.htm)) <br> **-** 정규식 ([URL 경로 Regex](https://docs.vdms.com/cdn/Content/HRE/M/URL-Path-Regex.htm)) <br> **-** 특정 패턴 ([URL 경로 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/URL-Path-Wildcard.htm)) |
| URL 경로 디렉터리 | 상대 경로가과 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([URL 경로 디렉터리 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/URL-Path-Directory-Literal.htm)) <br> **-** 특정 패턴 ([URL 경로 디렉터리 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/URL-Path-Directory-Wildcard.htm)) |
| URL 경로 확장 | 파일 확장명이와 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([URL 경로 확장 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/URL-Path-Extension-Literal.htm)) <br> **-** 특정 패턴 ([URL 경로 확장 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/URL-Path-Extension-Wildcard.htm)) |
| URL 경로 파일 이름 | 는 해당 파일 이름이과 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([URL 경로 파일 이름 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/URL-Path-Filename-Literal.htm)) <br> **-** 특정 패턴 ([URL 경로 파일 이름 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/URL-Path-Filename-Wildcard.htm)) |
| URL 쿼리 | 쿼리 문자열이와 일치 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([URL 쿼리 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/URL-Query-Literal.htm)) <br> **-** 정규식 ([URL 쿼리 Regex](https://docs.vdms.com/cdn/Content/HRE/M/URL-Query-Regex.htm)) <br> **-** 특정 패턴 ([URL 쿼리 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/URL-Query-Wildcard.htm)) |
| URL 쿼리 매개 변수 | 는와 일치 하는 값으로 설정 된 쿼리 문자열 매개 변수를 포함 하는지 여부에 따라 요청을 식별 합니다. <br> **-** 특정 값 ([URL 쿼리 매개 변수 리터럴](https://docs.vdms.com/cdn/Content/HRE/M/URL-Query-Parameter-Literal.htm)) <br> **-** 특정 패턴 ([URL 쿼리 매개 변수 와일드 카드](https://docs.vdms.com/cdn/Content/HRE/M/URL-Query-Parameter-Wildcard.htm)) |

**[맨 위로 이동](#top)**

가장 최근의 일치 조건은 [Verizon 규칙 엔진 설명서](https://docs.vdms.com/cdn/index.html#Quick_References/HRE_QR.htm#Conditio)를 참조하세요.

## <a name="next-steps"></a>다음 단계

- [Azure Content Delivery Network 개요](cdn-overview.md)
- [규칙 엔진 참조](cdn-verizon-premium-rules-engine-reference.md)
- [규칙 엔진 조건식](cdn-verizon-premium-rules-engine-reference-conditional-expressions.md)
- [규칙 엔진 기능](cdn-verizon-premium-rules-engine-reference-features.md)
- [규칙 엔진을 사용하여 기본 HTTP 동작 재정의](cdn-verizon-premium-rules-engine.md)
