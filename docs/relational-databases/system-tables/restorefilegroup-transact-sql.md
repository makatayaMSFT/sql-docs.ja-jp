---
description: restorefilegroup (Transact-sql)
title: restorefilegroup (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- restorefilegroup_TSQL
- restorefilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], restorefilegroup system table
- restorefilegroup system table
ms.assetid: 3aa15c55-6b72-4f76-97d7-bd88391d105c
author: cawrites
ms.author: chadam
ms.openlocfilehash: b4be126afb404fcff25dfa5ce036a70189d7b640
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98096172"
---
# <a name="restorefilegroup-transact-sql"></a>restorefilegroup (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  復元されたファイル グループごとに 1 行のデータを格納します。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|対応する復元操作を特定するための一意な識別番号。 **Restorehistory (restore_history_id)** を参照します。|  
|**filegroup_name**|**nvarchar(128)**|復元されるファイル グループの名前。 NULL にすることができます。<br /><br /> データベースをデータベーススナップショットに戻すと、完全復元の場合と同じ方法でこの値が設定されます。|  
  
## <a name="remarks"></a>解説  
 このテーブルおよびその他のバックアップテーブルと履歴テーブルの行の数を減らすには、 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) ストアドプロシージャを実行します。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のテーブルのバックアップと復元 ](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefile &#40;Transact-sql&#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [restorehistory &#40;Transact-sql&#41;](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
