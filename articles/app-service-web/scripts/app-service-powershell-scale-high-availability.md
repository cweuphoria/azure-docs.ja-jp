---
title: "Azure PowerShell のサンプル スクリプト - 高可用性アーキテクチャを使用した世界規模での Web アプリのスケーリング | Microsoft Docs"
description: "Azure PowerShell のサンプル スクリプト - 高可用性アーキテクチャを使用した世界規模での Web アプリのスケーリング"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/08/2017
ms.author: cfowler
translationtype: Human Translation
ms.sourcegitcommit: 97acd09d223e59fbf4109bc8a20a25a2ed8ea366
ms.openlocfilehash: 8e21e2c88578177eb8bc6120ecfcd1222b173ff2
ms.lasthandoff: 03/10/2017

---

# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a>高可用性アーキテクチャを使用して世界規模で Web アプリをスケールする

このシナリオでは、1 つのリソース グループ、2 つの App Service プラン、2 つの Web アプリ、1 つの Traffic Manager プロファイル、および&2; つの Traffic Manager エンドポイントを作成します。 この手順を実施すると、Web アプリを最も短いネットワーク待機時間でグローバルに利用できる高可用性アーキテクチャが完成します。

このスクリプトを実行する前に、`Login-AzureRmAccount` コマンドレットを使用して Azure との接続が作成されていることを確認してください。

## <a name="sample-script"></a>サンプル スクリプト

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "高可用性アーキテクチャを使用して世界規模で Web アプリをスケールする")]

## <a name="clean-up-deployment"></a>デプロイのクリーンアップ 

サンプル スクリプトの実行後、次のコマンドを使用すると、リソース グループ、Web アプリ、およびすべての関連リソースを削除できます。

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>スクリプトの説明

このスクリプトでは、次のコマンドを使用します。 表内の各コマンドは、それぞれのドキュメントにリンクされています。

| コマンド | メモ |
|---|---|
| [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v3.5.0/new-azurermresourcegroup) | すべてのリソースを格納するリソース グループを作成します。 |
| [New-AzureRMTrafficManagerProfile](https://docs.microsoft.com/powershell/resourcemanager/azurerm.trafficmanager/v2.5.0/new-azurermtrafficmanagerprofile) | Traffic Manager プロファイルを作成します。 |
| [New-AzureRmAppServicePlan](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermappserviceplan) | App Service プランを作成します。 |
| [New-AzureRmWebApp](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebapp) | Web アプリを作成します。 |
| [New-AzureRMTrafficManagerEndpoint](https://docs.microsoft.com/powershell/resourcemanager/azurerm.trafficmanager/v2.5.0/new-azurermtrafficmanagerendpoint) | Traffic Manager プロファイルにエンドポイントを作成します。 |

## <a name="next-steps"></a>次のステップ

Azure PowerShell モジュールの詳細については、[Azure PowerShell のドキュメント](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)を参照してください。

その他の Azure App Service Web Apps 用 Azure PowerShell サンプル スクリプトは、[Azure PowerShell サンプル](../app-service-powershell-samples.md)のページにあります。

