---
title: 'Azure VPN Gateway: 패킷 캡처 구성'
description: VPN 게이트웨이에서 사용할 수 있는 패킷 캡처 기능에 대해 알아봅니다.
services: vpn-gateway
author: radwiv
ms.service: vpn-gateway
ms.topic: how-to
ms.date: 10/15/2019
ms.author: radwiv
ms.openlocfilehash: 3ba3046367ceece6bf0ddf157451025c79977324
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87077201"
---
# <a name="configure-packet-captures-for-vpn-gateways"></a>VPN gateway에 대 한 패킷 캡처 구성

연결 및 성능 관련 문제는 종종 복잡 하며 문제의 원인을 좁히는 데 드는 시간과 노력이 많이 소요 됩니다. 패킷 캡처 기능을 사용 하면 문제 범위를 네트워크의 특정 부분으로 축소 하는 시간을 줄일 수 있습니다. 예를 들어 문제가 네트워크의 고객 측, 네트워크의 Azure 측 또는 그 사이에 있는지 여부 등이 있습니다. 문제를 축소 한 후에는 디버그 하 고 수정 작업을 수행 하는 것이 훨씬 더 효율적입니다.

패킷 캡처에는 일반적으로 사용할 수 있는 몇 가지 도구가 있습니다. 이러한 도구를 사용 하 여 관련 패킷 캡처를 가져오는 작업은 특히 고용량 트래픽 시나리오로 작업할 때 번거로울 수 있습니다. VPN gateway 패킷 캡처에서 제공 하는 필터링 기능은 중요 한 차이점입니다. 일반적으로 사용 가능한 패킷 캡처 도구 외에도 VPN gateway 패킷 캡처를 사용할 수 있습니다.

## <a name="vpn-gateway-packet-capture-filtering-capabilities"></a>VPN gateway 패킷 캡처 필터링 기능

VPN gateway 패킷 캡처는 고객의 요구에 따라 게이트웨이에서 또는 특정 연결에서 실행할 수 있습니다. 동시에 여러 터널에서 패킷 캡처를 실행할 수도 있습니다. VPN 게이트웨이에서 필터링과 함께 단일 또는 양방향 트래픽, IKE 및 ESP 트래픽 및 내부 패킷을 캡처할 수 있습니다.

5 개 튜플 필터 (원본 서브넷, 대상 서브넷, 원본 포트, 대상 포트, 프로토콜) 및 TCP 플래그 (SYN, ACK, FIN, URG, PSH, RST)를 사용 하는 것은 많은 볼륨의 문제를 격리 하는 데 유용 합니다.

각 속성에 대 한 설명이 포함 된 JSON 및 JSON 스키마의 예제는 아래를 참조 하세요. 또한 패킷 캡처를 실행 하는 동안 몇 가지 제한 사항에 유의 하세요.
- 스키마에서 필터는 배열로 표시 되지만 현재는 한 번에 하나의 필터만 사용할 수 있습니다.
- 여러 게이트웨이 차원의 패킷 캡처는 동시에 허용 되지 않습니다.
- 동일한 연결에서 동시에 여러 패킷 캡처가 허용 되지 않습니다. 서로 다른 연결에서 패킷 캡처를 동시에 실행할 수 있습니다.
- 게이트웨이 당 최대 5 개의 패킷 캡처를 병렬로 실행할 수 있습니다. 이러한 패킷 캡처는 게이트웨이 전체의 패킷 캡처 또는 연결 패킷 캡처의 조합일 수 있습니다.

### <a name="example-json"></a>예제 JSON
```JSON-interactive
{
  "TracingFlags": 11,
  "MaxPacketBufferSize": 120,
  "MaxFileSize": 200,
  "Filters": [
    {
      "SourceSubnets": [
        "20.1.1.0/24"
      ],
      "DestinationSubnets": [
        "10.1.1.0/24"
      ],
      "SourcePort": [
        500
      ],
      "DestinationPort": [
        4500
      ],
      "Protocol": [
        6
      ],
      "TcpFlags": 16,
      "CaptureSingleDirectionTrafficOnly": true
    }
  ]
}
```
### <a name="json-schema"></a>JSON 스키마
```JSON-interactive
{
    "type": "object",
    "title": "The Root Schema",
    "description": "The root schema input JSON filter for packet capture",
    "default": {},
    "additionalProperties": true,
    "required": [
        "TracingFlags",
        "MaxPacketBufferSize",
        "MaxFileSize",
        "Filters"
    ],
    "properties": {
        "TracingFlags": {
            "$id": "#/properties/TracingFlags",
            "type": "integer",
            "title": "The Tracingflags Schema",
            "description": "Tracing flags that customer can pass to define which packets are to be captured. Supported values are CaptureESP = 1, CaptureIKE = 2, CaptureOVPN = 8. The final value is OR of the bits.",
            "default": 11,
            "examples": [
                11
            ]
        },
        "MaxPacketBufferSize": {
            "$id": "#/properties/MaxPacketBufferSize",
            "type": "integer",
            "title": "The Maxpacketbuffersize Schema",
            "description": "Maximum buffer size of each packet. The capture will only contain contents of each packet truncated to this size.",
            "default": 120,
            "examples": [
                120
            ]
        },
        "MaxFileSize": {
            "$id": "#/properties/MaxFileSize",
            "type": "integer",
            "title": "The Maxfilesize Schema",
            "description": "Maximum file size of the packet capture file. It is a circular buffer.",
            "default": 100,
            "examples": [
                100
            ]
        },
        "Filters": {
            "$id": "#/properties/Filters",
            "type": "array",
            "title": "The Filters Schema",
            "description": "An array of filters that can be passed to filter inner ESP traffic.",
            "default": [],
            "examples": [
                [
                    {
                        "Protocol": [
                            6
                        ],
                        "CaptureSingleDirectionTrafficOnly": true,
                        "SourcePort": [
                            500
                        ],
                        "DestinationPort": [
                            4500
                        ],
                        "TcpFlags": 16,
                        "SourceSubnets": [
                            "20.1.1.0/24"
                        ],
                        "DestinationSubnets": [
                            "10.1.1.0/24"
                        ]
                    }
                ]
            ],
            "additionalItems": true,
            "items": {
                "$id": "#/properties/Filters/items",
                "type": "object",
                "title": "The Items Schema",
                "description": "An explanation about the purpose of this instance.",
                "default": {},
                "examples": [
                    {
                        "SourcePort": [
                            500
                        ],
                        "DestinationPort": [
                            4500
                        ],
                        "TcpFlags": 16,
                        "SourceSubnets": [
                            "20.1.1.0/24"
                        ],
                        "DestinationSubnets": [
                            "10.1.1.0/24"
                        ],
                        "Protocol": [
                            6
                        ],
                        "CaptureSingleDirectionTrafficOnly": true
                    }
                ],
                "additionalProperties": true,
                "required": [
                    "SourceSubnets",
                    "DestinationSubnets",
                    "SourcePort",
                    "DestinationPort",
                    "Protocol",
                    "TcpFlags",
                    "CaptureSingleDirectionTrafficOnly"
                ],
                "properties": {
                    "SourceSubnets": {
                        "$id": "#/properties/Filters/items/properties/SourceSubnets",
                        "type": "array",
                        "title": "The Sourcesubnets Schema",
                        "description": "An array of source subnets that need to match the Source IP address of a packet. Packet can match any one value in the array of inputs.",
                        "default": [],
                        "examples": [
                            [
                                "20.1.1.0/24"
                            ]
                        ],
                        "additionalItems": true,
                        "items": {
                            "$id": "#/properties/Filters/items/properties/SourceSubnets/items",
                            "type": "string",
                            "title": "The Items Schema",
                            "description": "An explanation about the purpose of this instance.",
                            "default": "",
                            "examples": [
                                "20.1.1.0/24"
                            ]
                        }
                    },
                    "DestinationSubnets": {
                        "$id": "#/properties/Filters/items/properties/DestinationSubnets",
                        "type": "array",
                        "title": "The Destinationsubnets Schema",
                        "description": "An array of destination subnets that need to match the Destination IP address of a packet. Packet can match any one value in the array of inputs.",
                        "default": [],
                        "examples": [
                            [
                                "10.1.1.0/24"
                            ]
                        ],
                        "additionalItems": true,
                        "items": {
                            "$id": "#/properties/Filters/items/properties/DestinationSubnets/items",
                            "type": "string",
                            "title": "The Items Schema",
                            "description": "An explanation about the purpose of this instance.",
                            "default": "",
                            "examples": [
                                "10.1.1.0/24"
                            ]
                        }
                    },
                    "SourcePort": {
                        "$id": "#/properties/Filters/items/properties/SourcePort",
                        "type": "array",
                        "title": "The Sourceport Schema",
                        "description": "An array of source ports that need to match the Source port of a packet. Packet can match any one value in the array of inputs.",
                        "default": [],
                        "examples": [
                            [
                                500
                            ]
                        ],
                        "additionalItems": true,
                        "items": {
                            "$id": "#/properties/Filters/items/properties/SourcePort/items",
                            "type": "integer",
                            "title": "The Items Schema",
                            "description": "An explanation about the purpose of this instance.",
                            "default": 0,
                            "examples": [
                                500
                            ]
                        }
                    },
                    "DestinationPort": {
                        "$id": "#/properties/Filters/items/properties/DestinationPort",
                        "type": "array",
                        "title": "The Destinationport Schema",
                        "description": "An array of destination ports that need to match the Destination port of a packet. Packet can match any one value in the array of inputs.",
                        "default": [],
                        "examples": [
                            [
                                4500
                            ]
                        ],
                        "additionalItems": true,
                        "items": {
                            "$id": "#/properties/Filters/items/properties/DestinationPort/items",
                            "type": "integer",
                            "title": "The Items Schema",
                            "description": "An explanation about the purpose of this instance.",
                            "default": 0,
                            "examples": [
                                4500
                            ]
                        }
                    },
                    "Protocol": {
                        "$id": "#/properties/Filters/items/properties/Protocol",
                        "type": "array",
                        "title": "The Protocol Schema",
                        "description": "An array of protocols that need to match the Protocol of a packet. Packet can match any one value in the array of inputs.",
                        "default": [],
                        "examples": [
                            [
                                6
                            ]
                        ],
                        "additionalItems": true,
                        "items": {
                            "$id": "#/properties/Filters/items/properties/Protocol/items",
                            "type": "integer",
                            "title": "The Items Schema",
                            "description": "An explanation about the purpose of this instance.",
                            "default": 0,
                            "examples": [
                                6
                            ]
                        }
                    },
                    "TcpFlags": {
                        "$id": "#/properties/Filters/items/properties/TcpFlags",
                        "type": "integer",
                        "title": "The Tcpflags Schema",
                        "description": "A list of TCP flags. The TCP flags set on the packet must match any flag in the list of flags provided. FIN = 0x01,SYN = 0x02,RST = 0x04,PSH = 0x08,ACK = 0x10,URG = 0x20,ECE = 0x40,CWR = 0x80. An OR of flags can be provided.",
                        "default": 0,
                        "examples": [
                            16
                        ]
                    },
                    "CaptureSingleDirectionTrafficOnly": {
                        "$id": "#/properties/Filters/items/properties/CaptureSingleDirectionTrafficOnly",
                        "type": "boolean",
                        "title": "The Capturesingledirectiontrafficonly Schema",
                        "description": "A flags which when set captures reverse traffic also.",
                        "default": false,
                        "examples": [
                            true
                        ]
                    }
                }
            }
        }
    }
}
```

## <a name="setup-packet-capture-using-powershell"></a>PowerShell을 사용 하 여 패킷 캡처 설정

패킷 캡처를 시작 하 고 중지 하는 PowerShell 명령은 아래 예제를 참조 하세요. 매개 변수 옵션에 대 한 자세한 내용은이 PowerShell [문서](https://docs.microsoft.com/powershell/module/az.network/start-azvirtualnetworkgatewaypacketcapture)를 참조 하세요.

### <a name="start-packet-capture-for-a-vpn-gateway"></a>VPN gateway에 대 한 패킷 캡처 시작

```azurepowershell-interactive
Start-AzVirtualnetworkGatewayPacketCapture -ResourceGroupName "YourResourceGroupName" -Name "YourVPNGatewayName"
```

선택적 매개 변수 **-filterdata** 는 필터를 적용 하는 데 사용할 수 있습니다.

### <a name="stop-packet-capture-for-a-vpn-gateway"></a>VPN gateway에 대 한 패킷 캡처 중지

```azurepowershell-interactive
Stop-AzVirtualNetworkGatewayPacketCapture -ResourceGroupName "YourResourceGroupName" -Name "YourVPNGatewayName" -SasUrl "YourSASURL"
```

### <a name="start-packet-capture-for-a-vpn-gateway-connection"></a>VPN gateway 연결에 대 한 패킷 캡처 시작

```azurepowershell-interactive
Start-AzVirtualNetworkGatewayConnectionPacketCapture -ResourceGroupName "YourResourceGroupName" -Name "YourVPNGatewayConnectionName"
```

선택적 매개 변수 **-filterdata** 는 필터를 적용 하는 데 사용할 수 있습니다.

### <a name="stop-packet-capture-on-a-vpn-gateway-connection"></a>VPN gateway 연결에서 패킷 캡처 중지

```azurepowershell-interactive
Stop-AzVirtualNetworkGatewayConnectionPacketCapture -ResourceGroupName "YourResourceGroupName" -Name "YourVPNGatewayConnectionName" -SasUrl "YourSASURL"
```

## <a name="key-considerations"></a>주요 고려 사항

- 패킷 캡처 실행은 성능에 영향을 줄 수 있습니다. 필요 하지 않은 경우 패킷 캡처를 중지 해야 합니다.
- 제안 된 최소 패킷 캡처 기간은 600 초입니다. 패킷 캡처 기간이 짧으면 경로에 있는 여러 구성 요소 간의 문제를 동기화 하기 때문에 전체 데이터를 제공 하지 못할 수 있습니다.
- 패킷 캡처 데이터 파일은 PCAP 형식으로 생성 됩니다. Wireshark 또는 기타 일반적으로 사용할 수 있는 응용 프로그램을 사용 하 여 PCAP 파일을 엽니다.

## <a name="next-steps"></a>다음 단계

VPN Gateway에 대 한 자세한 내용은 정보 [VPN Gateway](vpn-gateway-about-vpngateways.md) 를 참조 하세요.
