---
title: "Azure PowerShell のサンプル スクリプト - GitHub からの継続的なデプロイで Web アプリを作成する | Microsoft Docs"
description: "Azure PowerShell のサンプル スクリプト - GitHub からの継続的なデプロイで Web アプリを作成する"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: cephalin
translationtype: Human Translation
ms.sourcegitcommit: 97acd09d223e59fbf4109bc8a20a25a2ed8ea366
ms.openlocfilehash: 9b6429027a0d9f95ddced8b6616693ac2959a014
ms.lasthandoff: 03/10/2017

---

# <a name="create-a-web-app-with-continuous-deployment-from-github"></a>GitHub からの継続的なデプロイで Web アプリを作成する

このサンプル スクリプトでは、App Service で Web アプリを関連リソースと合わせて作成し、GitHub リポジトリからの継続的デプロイを設定します。 継続的なデプロイを使用しない GitHub でのデプロイについては、「[Web アプリを作成して GitHub からコードをデプロイする](app-service-powershell-deploy-github.md)」を参照してください。

このスクリプトを実行する前に、次を確認してください。

- Azure との接続が、`Login-AzureRmAccount` コマンドレットを使用して作成されている。
- アプリケーション コードが、自分が所有するパブリックまたはプライベートの GitHub リポジトリ内にある。
- [GitHub アカウントでアクセス トークンを作成](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)している。

## <a name="sample-script"></a>サンプル スクリプト

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "GitHub からの継続的なデプロイでの Web アプリの作成")]

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
| [New-AzureRmAppServicePlan](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermappserviceplan) | App Service プランを作成します。 |
| [New-AzureRmWebApp](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebapp) | Web アプリを作成します。 |
| [Set-AzureRmResource](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/set-azurermresource) | リソース グループのリソースを変更します。 |

## <a name="next-steps"></a>次のステップ

Azure PowerShell モジュールの詳細については、[Azure PowerShell のドキュメント](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)を参照してください。

その他の Azure App Service Web Apps 用 Azure PowerShell サンプル スクリプトは、[Azure PowerShell サンプル](../app-service-powershell-samples.md)のページにあります。

