---
description: sys.dm_hadr_cluster_networks (Transact-sql)
title: sys.dm_hadr_cluster_networks (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_cluster_networks
- sys.dm_hadr_cluster_networks_TSQL
- sys.dm_hadr_cluster_networks
- dm_hadr_cluster_networks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_networks dynamic management view
ms.assetid: ece32b15-d63f-4f93-92b7-e2930333e97a
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: d97862778240fac789f95c00a474df12770f8ef3
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98101607"
---
# <a name="sysdm_hadr_cluster_networks-transact-sql"></a>sys.dm_hadr_cluster_networks (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  可用性グループのサブネット構成に参加している WSFC クラスター メンバーごとに 1 行のデータを返します。 この動的管理ビューを使用して、可用性レプリカごとに構成されているネットワーク仮想 IP を検証できます。  
  
 主キー: **member_name**  +  **network_subnet_IP**  +  **network_subnet_prefix_length**  
  
 > [!TIP]
 > 以降で [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] は、この動的管理ビューは Always On 可用性グループに加えて Always On フェールオーバークラスターインスタンスをサポートしています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|WSFC クラスター内のノードのコンピューター名。|  
|**network_subnet_ip**|**nvarchar (48)**|コンピューターが属するサブネットのネットワーク IP アドレス。 IPv4 または IPv6 アドレスを指定できます。|  
|**network_subnet_ipv4_mask**|**nvarchar (45)**|IP アドレスが属するサブネットを指定するネットワークサブネットマスク。 [CREATE AVAILABILITY group](../../t-sql/statements/create-availability-group-transact-sql.md)または [ALTER availability GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)ステートメントの WITH dhcp 句で dhcp <network_subnet_option> オプションを指定するには、 **network_subnet_ipv4_mask** し [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。<br /><br /> NULL = IPv6 サブネット。|  
||||  
|**network_subnet_prefix_length**|**int**|コンピューターが属するサブネットを指定するネットワーク IP プレフィックス長。|  
|**is_public**|**bit**|ネットワークが WSFC クラスターでプライベートかパブリックかを示します。次のいずれかになります。<br /><br /> 0 = プライベート<br /><br /> 1 = パブリック|  
|**is_ipv4**|**bit**|サブネットの種類。次のいずれかになります。<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [フェールオーバー クラスタリングと Always On 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Transact-sql&#41;&#40;可用性グループの監視 ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_os_cluster_nodes &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [SQL Server システムカタログに対するクエリについてよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
