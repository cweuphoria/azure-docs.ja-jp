---
title: "Azure CLI のサンプル スクリプト - オペレーティング システム ディスクのマウント | Microsoft Docs"
description: "Azure CLI のサンプル スクリプト - オペレーティング システム ディスクのマウント"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
translationtype: Human Translation
ms.sourcegitcommit: e5362b32a0f93433c77c27a6fc116960c45404f9
ms.openlocfilehash: 73bd1f9b018e49ad8a536b80275cbf0faa030b74
ms.lasthandoff: 03/01/2017

---

# <a name="troubleshoot-a-vms-operating-system-disk"></a>VM オペレーティング システム ディスクのトラブルシューティング

このスクリプトでは、障害が発生したかまたは問題のある仮想マシンのオペレーティング システム ディスクを、2 つ目の仮想マシンにデータ ディスクとしてマウントします。 これは、ディスクの問題のトラブルシューティングやデータの復元に役立ちます。 

このスクリプトを実行する前に、`az login` コマンドを使用して Azure との接続が作成されていることを確認してください。 また、既存の仮想マシンも必要です。 サンプル スクリプトに記載されている既存 VM の名前とリソース グループは、環境に合わせて変更してください。

このサンプルは、bash シェルに対応しています。 Azure CLI スクリプトを Windows クライアントで実行する方法については、[Windows での Azure CLI の実行](../virtual-machines-windows-cli-options.md)に関する記事を参照してください。

## <a name="sample-script"></a>サンプル スクリプト

[!code-azurecli[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "VM の簡易作成")]

## <a name="script-explanation"></a>スクリプトの説明

このスクリプトでは、次のコマンドを使用して、リソース グループ、仮想マシン、およびすべての関連リソースを作成します。 表内の各コマンドは、それぞれのドキュメントにリンクされています。

| コマンド | メモ |
|---|---|
| [az vm show](https://docs.microsoft.com/cli/azure/vm#show) | 仮想マシンの一覧を返します。 このサンプルでは、仮想マシンのオペレーティング システム ディスクを返すクエリ オプションを使用しています。 返された値は、変数名 "uri" に追加されます。 |
| [az vm delete](https://docs.microsoft.com/cli/azure/vm#delete) | 仮想マシンを削除します。 |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | 仮想マシンを作成します。  |
| [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) | ディスクを仮想マシンに接続します。 |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | 仮想マシンの IP アドレスを返します。 |

## <a name="next-steps"></a>次のステップ

Azure CLI の詳細については、[Azure CLI のドキュメント](https://docs.microsoft.com/cli/azure/overview)のページをご覧ください。

その他の仮想マシン用の CLI サンプル スクリプトは、[Azure Linux VM のドキュメント](../virtual-machines-linux-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)のページにあります。

