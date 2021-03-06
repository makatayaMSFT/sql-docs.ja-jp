---
title: lightweight pooling サーバー構成オプション | Microsoft Docs
description: "\"lightweight pooling\" オプションについて説明します。 これを使用することにより、過度のコンテキスト切り替えが発生する対称型マルチプロセッシング環境でスループットが向上するしくみについて説明します。"
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default lightweight pooling
- decreasing overhead
- lightweight pooling option
- system overhead [SQL Server]
- performance [SQL Server], lightweight pooling
- context switching [SQL Server], lightweight pooling option
- excessive context switching [SQL Server]
- reducing overhead
- overhead [SQL Server]
ms.assetid: 2dc11b61-d065-4126-8e00-acf40390f9fb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 13efd00252dac50756a243475816a5a2e4119110
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772441"
---
# <a name="lightweight-pooling-server-configuration-option"></a>lightweight pooling サーバー構成オプション
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **lightweight pooling** オプションは、SMP (symmetric multiprocessing) 環境で発生するコンテキストの過度の切り替えによるシステムのオーバーヘッドを削減する手段を提供する場合に使用します。 コンテキストの過度の切り替えが発生した場合、簡易プーリングを使用してコンテキストの切り替えをインラインで行い、ユーザーまたはカーネルのリング遷移を削減することによって、スループットを向上できます。  
  
 ファイバー モードは、UMS ワーカーのコンテキスト切り替えがパフォーマンスの重大なボトルネックになる状況を対象としています。 この状況はまれであるため、一般的なシステムのパフォーマンスやスケーラビリティがファイバー モードで向上することはほとんどありません。 また、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] ではコンテキストの切り替えが改良されているため、ファイバー モードの必要性も少なくなっています。 ルーチン処理にファイバー モード スケジューリングを使用することはお勧めしません。 これは、コンテキストの切り替えがもたらす本来の利点が損なわれることでパフォーマンスが低下する場合があるためと、スレッド ローカル ストレージ (TLS) やスレッド所有オブジェクト (ミューテックス (Win32 カーネル オブジェクトの一種) など) を使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の一部のコンポーネントがファイバー モードでは正常に機能しない場合があるためです。  
  
 **lightweight pooling** を 1 に設定すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はファイバー モード スケジューリングに切り替わります。 このオプションの既定値は 0 です。  
  
 **lightweight pooling** オプションは拡張オプションです。 **sp_configure** システム ストアド プロシージャを使用して **lightweight pooling** の設定を変更するには、 **show advanced options** を 1 に設定する必要があります。 この設定は、サーバーを再起動した後に有効になります。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 および [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows XP では、簡易プーリングはサポートされていません。 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] では、簡易プーリングが完全にサポートされています。  
  
> [!NOTE]  
>  簡易プーリングでは、共通言語ランタイム (CLR) の実行はサポートされていません。 "clr enabled" オプションまたは "lightweight pooling" オプションのいずれかを無効にしてください。 CLR に依存していてファイバー モードで正しく動作しない機能には、Hierarchy データ型、レプリケーション、およびポリシー ベースの管理があります。  
  
## <a name="see-also"></a>参照  
 [clr enabled サーバー構成オプション](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [clr enabled サーバー構成オプション](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)  
  
  
