---
title: 확장 된 GeoJSON 기 하 도형 | Microsoft Azure 맵
description: 추가 기하학 셰이프를 포함 하도록 Azure Maps GeoJSON 사양을 확장 하는 방법에 대해 알아봅니다. 지도에서 사용할 원과 사각형을 설정 하는 예제를 봅니다.
author: sataneja
ms.author: sataneja
ms.date: 05/17/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.openlocfilehash: e6cfbef3751a7b4256f689af0e5b3524ae6fa878
ms.sourcegitcommit: bfeae16fa5db56c1ec1fe75e0597d8194522b396
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/10/2020
ms.locfileid: "88037459"
---
# <a name="extended-geojson-geometries"></a>확장 된 GeoJSON 기 하 도형

Azure Maps는 내부 및 지역별 기능을 검색할 수 있는 강력한 Api 목록을 제공 합니다. 이러한 Api는 지리적 기능을 나타내는 표준 [GeoJSON 사양을][1] 준수 합니다.  

[GeoJSON spec][1] 은 다음 기 하 도형만 지원 합니다.

* GeometryCollection
* LineString
* MultiLineString
* MultiPoint
* MultiPolygon
* 요소
* 다각형

일부 Azure Maps Api는 [GeoJSON 사양의][1]일부가 아닌 기 하 도형을 허용 합니다. 예를 들어 [Geometry API 내에서 검색](https://docs.microsoft.com/rest/api/maps/search/postsearchinsidegeometry) 은 원과 다각형을 허용 합니다.

이 문서에서는 Azure Maps가 [GeoJSON 사양][1]을 확장하여 특정 기하 도형을 나타내는 방법에 대한 자세한 설명을 제공합니다.

## <a name="circle"></a>Circle

`Circle` [GeoJSON 사양][1]에서 기 하 도형을 지원 하지 않습니다. 개체를 사용 `GeoJSON Point Feature` 하 여 원을 나타냅니다.

`Circle`개체를 사용 하 여 표현 된 기 하 도형에는 `GeoJSON Feature` 다음 좌표와 속성이 포함 __되어야 합니다__ .

- Center

    원 중심은 개체를 사용 하 여 표현 됩니다 `GeoJSON Point` .

- 반지름

    원의 `radius`는 `GeoJSON Feature`의 속성을 사용하여 표현됩니다. 반지름 값은 미터(_meters_) 단위이고 `double` 형식이어야 합니다.

- 하위 유형

    원 기하 도형에는 `subType` 속성도 포함되어야 합니다. 이 속성은의 속성에 포함 되 `GeoJSON Feature` 고 해당 값은 _원_ 이어야 합니다.

#### <a name="example"></a>예제

개체를 사용 하 여 원을 표시 하는 방법은 다음과 같습니다 `GeoJSON Feature` . 위도: 47.639754 및 경도:-122.126986를 중심으로 원을 중심으로 지정 하 고 100 미터와 같은 반지름을 할당 하겠습니다.

```json            
{
    "type": "Feature",
    "geometry": {
        "type": "Point",
        "coordinates": [-122.126986, 47.639754]
    },
    "properties": {
        "subType": "Circle",
        "radius": 100
    }
}          
```

## <a name="rectangle"></a>사각형

`Rectangle` [GeoJSON 사양][1]에서 기 하 도형을 지원 하지 않습니다. 개체를 사용 `GeoJSON Polygon Feature` 하 여 사각형을 나타냅니다. 사각형 확장은 웹 SDK의 그리기 도구 모듈에서 주로 사용 됩니다.

`Rectangle`개체를 사용 하 여 표현 된 기 하 도형에는 `GeoJSON Polygon Feature` 다음 좌표와 속성이 포함 __되어야 합니다__ .

- 방향

    사각형의 모퉁이는 개체의 좌표를 사용 하 여 표시 됩니다 `GeoJSON Polygon` . 각 모퉁이 마다 하나씩 5 개의 좌표가 있어야 합니다. 그리고 첫 번째 좌표와 동일한 다섯 번째 좌표로 다각형 링을 닫습니다. 이러한 좌표가 정렬 되며 개발자가 원하는 대로 회전할 수 있습니다.

- 하위 유형

    사각형 기 하 도형에도 속성이 포함 되어야 합니다 `subType` . 이 속성은의 속성에 포함 되어야 하며 `GeoJSON Feature` , 해당 값은 _사각형_ 이어야 합니다.

### <a name="example"></a>예제

```json
{
    "type": "Feature",
    "geometry": {
        "type": "Polygon",
        "coordinates": [[[5,25],[14,25],[14,29],[5,29],[5,25]]]
    },
    "properties": {
        "subType": "Rectangle"
    }
}

```
## <a name="next-steps"></a>다음 단계

Azure Maps에서 데이터 GeoJSON에 대해 자세히 알아보세요.

> [!div class="nextstepaction"]
> [지 오 GeoJSON 형식](geofence-geojson.md)

Azure Maps 및 위치 인텔리전스 응용 프로그램과 관련 된 일반적인 기술 용어를 검토 합니다.

> [!div class="nextstepaction"]
> [Azure Maps 용어집](glossary.md)

[1]: https://tools.ietf.org/html/rfc7946
