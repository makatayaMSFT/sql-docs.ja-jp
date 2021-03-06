---
description: sys.filetables (Transact-SQL)
title: sys. filetables (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- filetables
- filetables_TSQL
- sys.filetables
- sys.filetables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetables catalog view
ms.assetid: a740be59-cd52-4707-9ad2-5203669a63ac
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 990965f5f3af485437cd2e97d5eb952a53b157cf
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98093152"
---
# <a name="sysfiletables-transact-sql"></a>sys.filetables (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  内の各 FileTable の行を返し [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ますです。 FileTables について詳しくは、「[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)」をご覧ください。    
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**||オブジェクト ID 番号。 データベース内で一意です。<br /><br /> 詳細については、「 [transact-sql&#41;&#40;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)」を参照してください。|  
|**is_enabled**|**bit**|1 = FileTable は "有効" 状態です。|  
|**directory_name**|**varchar(255)**|FileTable のルートディレクトリの名前。|  
|**filename_collation_id**||FileTable に対して定義されている照合順序識別子を指定します。|  
|**filename_collation_name**||FileTable に対して定義されている照合順序名を指定します。|  
  
## <a name="see-also"></a>参照  
 [Filetable の管理](../../relational-databases/blob/manage-filetables.md)   
 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
  
  
