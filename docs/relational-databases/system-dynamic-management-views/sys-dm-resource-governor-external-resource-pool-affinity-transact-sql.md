---
description: sys.dm_resource_governor_external_resource_pool_affinity (Transact-sql)
title: sys.dm_resource_governor_external_resource_pool_affinity (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- sys.dm_resource_governor_external_resource_pool_affinity_TSQL
- dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity
ms.assetid: e32fac49-5161-47c0-8540-af3fe730c00c
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: c93e9c33174172311a7378219440b7c60b7ab4b8
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98172484"
---
# <a name="sysdm_resource_governor_external_resource_pool_affinity-transact-sql"></a>sys.dm_resource_governor_external_resource_pool_affinity (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]
**適用対象:** [!INCLUDE[sssql15-md](../../includes/sssql16-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]および [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

現在の外部リソースプールの構成に関する CPU アフィニティ情報を返します。
  
|列名|データ型|説明|
|----------------|---------------|-----------------|
|pool_id|**int**|外部リソースプールの ID。 NULL 値は許可されません。|
|processor_group|**smallint**|Windows 論理プロセッサグループの ID。 NULL 値は許可されません。|
|cpu_mask|**bigint**|このプールに関連付けられている Cpu を表すバイナリマスク。 NULL 値は許可されません。|
  
## <a name="remarks"></a>Remarks

アフィニティを使用して作成されたプールは、アフィニティがない `AUTO` ため、このビューに表示されません。 詳細については、「 [CREATE EXTERNAL RESOURCE pool &#40;transact-sql&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md) 」および「 [ALTER external Resource pool &#40;transact-sql&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md) ステートメント」を参照してください。

## <a name="permissions"></a>アクセス許可

`VIEW SERVER STATE` 権限が必要です。

## <a name="see-also"></a>関連項目

[SQL Server での Machine Learning のリソース管理](../../machine-learning/administration/resource-governor.md)

[sys.dm_resource_governor_resource_pool_affinity &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[external scripts enabled サーバー構成オプション](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
