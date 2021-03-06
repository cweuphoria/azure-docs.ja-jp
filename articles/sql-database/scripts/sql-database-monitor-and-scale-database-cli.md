---
title: "Azure CLI スクリプト - 単一の SQL Database の監視とスケーリング | Microsoft Docs"
description: "Azure CLI のサンプル スクリプト - Azure CLI を使用して単一の SQL データベースを監視およびスケーリングする"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: sample
ms.devlang: CLI
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 03/14/2017
ms.author: janeng
translationtype: Human Translation
ms.sourcegitcommit: 97acd09d223e59fbf4109bc8a20a25a2ed8ea366
ms.openlocfilehash: 4cfc4ab09f7adead289cb949373730bffcfa13ec
ms.lasthandoff: 03/10/2017

---

# <a name="monitor-and-scale-a-single-sql-database-using-the-azure-cli"></a>Azure CLI を使用して&1; つの SQL データベースを監視およびスケーリングする

この CLI のサンプル スクリプトは、単一の Azure SQL データベースのサイズ情報をクエリした後に、そのデータベースを別のパフォーマンス レベルにスケーリングします。 

このスクリプトを実行する前に、`az login` コマンドを使用して Azure との接続が作成されていることを確認してください。 

このサンプルは、bash シェルに対応しています。 Azure CLI スクリプトを Windows で実行する方法については、[Windows での Azure CLI の実行](../../virtual-machines/virtual-machines-windows-cli-options.md)に関する記事を参照してください。


## <a name="sample-script"></a>サンプル スクリプト

[!code-azurecli[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "単一の SQL Database の監視とスケーリング")]

## <a name="clean-up-deployment"></a>デプロイのクリーンアップ

スクリプト サンプルの実行後は、次のコマンドを使用してリソース グループとすべての関連リソースを削除することができます。

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>スクリプトの説明

このスクリプトでは、次のコマンドを使用します。 表内の各コマンドは、それぞれのドキュメントにリンクされています。

| コマンド | メモ |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | すべてのリソースを格納するリソース グループを作成します。 |
| [az sql server create](https://docs.microsoft.com/cli/azure/sql/server#create) | データベースをホストする論理サーバーを作成します。 |
| [az sql db show-usage](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | データベース サイズの使用量に関する情報を表示します。 |
| [az sql db update](https://docs.microsoft.com/cli/azure/sql/db#update) | データベースのプロパティ (サービス層やパフォーマンス レベルなど) を更新するか、エラスティック プールに対して、エラスティック プールから、またはエラスティック プール間でデータベースを移動します。 |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 入れ子になったリソースすべてを含むリソース グループを削除します。 |
|||

## <a name="next-steps"></a>次のステップ

Azure CLI の詳細については、[Azure CLI のドキュメント](https://docs.microsoft.com/cli/azure/overview)のページをご覧ください。

その他の SQL Database 用の CLI サンプル スクリプトは、[Azure SQL Database のドキュメント](../sql-database-cli-samples.md)のページにあります。

