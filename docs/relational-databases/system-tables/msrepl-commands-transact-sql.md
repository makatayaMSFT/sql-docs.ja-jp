---
description: MSrepl_commands (Transact-sql)
title: MSrepl_commands (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_commands
- MSrepl_commands_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_commands system table
ms.assetid: 53b9f9cd-9429-47a0-aba2-908fc60e7036
author: cawrites
ms.author: chadam
ms.openlocfilehash: c939e1c5112aee07738ad5d368cb0ef05d804618
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98091127"
---
# <a name="msrepl_commands-transact-sql"></a>MSrepl_commands (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSrepl_commands** テーブルには、レプリケートされたコマンドの行が含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|パブリッシャーデータベースの ID。|  
|**xact_seqno**|**varbinary(16)**|トランザクションのシーケンス番号。|  
|**type**|**int**|コマンドの種類。|  
|**article_id**|**int**|アーティクルの ID です。|  
|**originator_id**|**int**|発信元の ID。|  
|**command_id**|**int**|コマンドの ID。|  
|**partial_command**|**bit**|これが部分コマンドであるかどうかを示します。|  
|**command**|**varbinary (1024)**|コマンドの値。|  
|**hashkey**|**int**|内部使用のみ。|  
|**originator_lsn**|**varbinary(16)**|発生元パブリケーションのコマンドの LSN を識別します。 これは、ピアツーピアトランザクションレプリケーションで使用されます。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)  
  
  
