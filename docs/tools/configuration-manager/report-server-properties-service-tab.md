---
title: '[SQL Server Reporting Services のプロパティ] ダイアログ ボックス ([サービス] タブ)'
description: バイナリ パス、ホスト名、開始モードなど、[レポート サーバーのプロパティ] ダイアログ ボックスの [サービス] タブのオプションについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 2a2e1dbf-02b9-4893-aaf0-c0e4a2c9b4f9
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 172c7c8ee64f0555aa6a88e88119246d52deebfd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481613"
---
# <a name="report-server-properties-service-tab"></a>[SQL Server Reporting Services のプロパティ] ダイアログ ボックス ([サービス] タブ)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  このサービスは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のレポート サーバー サービスです。 グレー表示になっているプロパティ値をこのアプリケーションで変更することはできません。  
  
## <a name="options"></a>Options  
 **[バイナリ パス]**  
 このサービスが使用するプログラム ファイルの場所が表示されます。  
  
 **[エラー制御]**  
 1 は、"SERVICE_ERROR_NORMAL" を示します。 コンピューターの起動時にこのサービスが開始しなかった場合は、スタートアップ プログラムによってログにエラーが記録され、ポップアップ メッセージ ボックスが表示されますが、スタートアップ操作は継続します。 この値は変更できません。  
  
 **終了コード**  
 エラーが発生した場合は、エラー番号がこのボックスに表示されます。 その番号を手掛かりにして障害のトラブルシューティングを行ってください。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポート技術情報でその番号を検索することも、技術サポート スタッフにその番号を連絡することも可能です。  
  
 **Host Name**  
 フルテキスト検索を実行しているコンピューターまたはクラスターの名前が表示されます。  
  
 **名前**  
 サービスの表示名が表示されます。  
  
 **プロセス ID**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows プロセス ID が表示されます。  
  
 **[SQL サービスの種類]**  
 呼び出し側プロセスに提供されるサービスの種類です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、いくつかのサービスがインストールされます。  
  
 **[開始モード]**  
 このサービスを以下のいずれかのモードに設定します。  
  
-   手動: このサービスは、コンピューターの起動時に自動的に開始されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーまたは他のツールを使用してこのサービスを開始する必要があります。  
  
-   自動:コンピューターの起動時に、このサービスの開始が試みられます。  
  
-   無効:このサービスを開始できません。  
  
 **State**  
 このサービスが実行中か、停止しているか、無効になっているかが表示されます。  
  
## <a name="see-also"></a>参照  
 [SQL Server のサービス](../../tools/configuration-manager/sql-server-services.md)  
  
  
