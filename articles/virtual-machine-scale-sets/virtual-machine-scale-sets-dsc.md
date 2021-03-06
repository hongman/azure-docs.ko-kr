---
title: Virtual Machine Scale Sets에서 필요한 상태 구성 사용
description: Azure 필요한 상태 구성 확장과 함께 Virtual Machine Scale Sets를 사용 하 여 가상 컴퓨터를 구성 합니다.
author: ju-shim
ms.author: jushiman
ms.topic: how-to
ms.service: virtual-machine-scale-sets
ms.subservice: extensions
ms.date: 6/25/2020
ms.reviewer: mimckitt
ms.custom: mimckitt
ms.openlocfilehash: 20e5bff87d5cd0d6e0a35a558462bb5598bfe3f4
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87080491"
---
# <a name="using-virtual-machine-scale-sets-with-the-azure-dsc-extension"></a>Azure DSC 확장에 Virtual Machine Scale Sets 사용
[Azure DSC(필요한 상태 구성)](../virtual-machines/extensions/dsc-overview.md?toc=/azure/virtual-machines/windows/toc.json) 확장 처리기에 [Virtual Machine Scale Sets](./overview.md)를 사용할 수 있습니다. 가상 머신 확장 집합은 많은 수의 가상 머신을 배포 및 관리하는 방법을 제공하며 부하에 따라 탄력적으로 확장 및 축소될 수 있습니다. DSC는 VM이 온라인으로 전환되어 프로덕션 소프트웨어를 실행하도록 VM을 구성하는 데 사용합니다.

## <a name="differences-between-deploying-to-virtual-machines-and-virtual-machine-scale-sets"></a>Virtual Machines 및 Virtual Machine Scale Sets에 대한 배포 간의 차이점
가상 머신 확장 집합에 대한 기본 템플릿 구조는 단일 VM과 약간 다릅니다. 특히, 단일 VM은 확장을 "virtualMachines" 노드 아래에 배포합니다. DSC가 템플릿에 추가된 "extensions" 유형의 항목이 있습니다.

```
"resources": [
          {
              "name": "Microsoft.Powershell.DSC",
              "type": "extensions",
              "location": "[resourceGroup().location]",
              "apiVersion": "2015-06-15",
              "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "tags": {
                  "displayName": "dscExtension"
              },
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": false,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "DscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }
          }
      ]
```

가상 머신 확장 집합 노드에는 "VirtualMachineProfile", "extensionProfile" 특성을 포함하는 "properties" 섹션이 있습니다. "extensions" 아래에 DSC가 추가됩니다.

```
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": false,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
```

## <a name="behavior-for-a-virtual-machine-scale-set"></a>Virtual Machine Scale Set의 동작
가상 머신 확장 집합의 동작은 단일 VM의 동작과 동일합니다. 새 VM을 만들 때 DSC 확장으로 자동으로 프로비전됩니다. 확장에 최신 버전의 WMF가 필요한 경우 확장을 온라인으로 전환하려면 VM을 다시 부팅합니다. 온라인 상태이면 DSC 구성.zip을 다운로드하고 VM에 프로비전합니다. 자세한 내용은 [Azure DSC 확장 개요](../virtual-machines/extensions/dsc-overview.md?toc=/azure/virtual-machines/windows/toc.json)에서 확인할 수 있습니다.

## <a name="next-steps"></a>다음 단계
[DSC 확장에 대한 Azure Resource Manager 템플릿](../virtual-machines/extensions/dsc-template.md?toc=/azure/virtual-machines/windows/toc.json)을 검토합니다.

[DSC 확장이 자격 증명을 안전하게 처리](../virtual-machines/extensions/dsc-credentials.md?toc=/azure/virtual-machines/windows/toc.json)하는 방법을 알아봅니다. 

Azure DSC 확장 처리기에 대한 자세한 내용은 [Azure 필요한 상태 구성 확장 처리기 소개](../virtual-machines/extensions/dsc-overview.md?toc=/azure/virtual-machines/windows/toc.json)를 참조하세요. 

PowerShell DSC에 대한 자세한 내용은 [PowerShell 설명서 센터를 방문하세요](/powershell/scripting/dsc/overview/overview). 
