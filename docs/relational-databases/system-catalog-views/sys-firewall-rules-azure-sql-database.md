---
description: sys.firewall_rules (Azure SQL データベース)
title: sys.firewall_rules (Azure SQL Database) |Microsoft Docs
ms.date: 03/26/2019
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.firewall_rules
- firewall_rules
- sys.firewall_rules_TSQL
- firewall_rules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- firewall_rules
- sys.firewall_rules
ms.assetid: 140d2cd8-9aa1-4cc5-870d-e1dbc873b3fe
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: = azuresqldb-current
ms.openlocfilehash: 351ca530c49051b61b6f44b8dc2fbff83623cf8f
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98097993"
---
# <a name="sysfirewall_rules-azure-sql-database"></a>sys.firewall_rules (Azure SQL データベース)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  に関連付けられているサーバーレベルのファイアウォール設定に関する情報を返し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] ます。  
  
 `sys.firewall_rules` ビューには、次の列が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|id|**INT**|サーバー レベルのファイアウォール設定の識別子。|  
|name|**NVARCHAR (128)**|サーバーレベルのファイアウォール設定を説明し、区別するための名前です。|  
|start_ip_address|**VARCHAR (45)**|サーバーレベルのファイアウォール設定の範囲の最下位の IP アドレスです。 この IP アドレス以上の IP アドレスは、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーへの接続を試行できます。 設定できる最下位の IP アドレスは `0.0.0.0` です。|  
|end_ip_address|**VARCHAR (45)**|サーバーレベルのファイアウォール設定の範囲の最上位の IP アドレスです。 これ以下の IP アドレスは、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーへの接続を試みることができます。 設定できる最上位の IP アドレスは `255.255.255.255` です。<br /><br /> 注: このフィールドと **start_ip_address** フィールドの両方がと等しい場合は、Azure の接続試行が許可され `0.0.0.0` ます。|  
|create_date|**/**|サーバーレベルのファイアウォール設定が作成された UTC 日時です。<br /><br /> 注: UTC は、協定世界時の頭字語です。|  
|modify_date|**/**|サーバーレベルのファイアウォール設定が最後に変更された UTC 日時です。|  
  
## <a name="remarks"></a>解説

 Microsoft Azure SQL Database に関連付けられているデータベースレベルのファイアウォール設定に関する情報を返すには、 [sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)を使用します。  
  
## <a name="permissions"></a>アクセス許可

 このビューへの読み取り専用アクセスは、 **master** データベースに接続する権限を持つすべてのユーザーが使用できます。  
  
## <a name="see-also"></a>参照

[sp_set_firewall_rule &#40;Azure SQL データベース&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[sp_set_database_firewall_rule &#40;Azure SQL データベース&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
[データベースエンジンアクセスできるように Windows ファイアウォールを構成する](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[FILESTREAM アクセスのためのファイアウォールの構成](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[レポート サーバー アクセスに対するファイアウォールの構成](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) 
