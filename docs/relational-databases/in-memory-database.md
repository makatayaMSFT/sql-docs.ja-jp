---
title: メモリ内データベース | Microsoft Docs
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- in-memory database
- feature, in-memory database
- in-memory
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: e4e0e6622a2a313b85dfa00df8c88044486f75f5
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65995000"
---
# <a name="in-memory-database"></a>メモリ内データベース

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

メモリ内データベースとは、インメモリ ベースのテクノロジを利用する SQL Server 内の機能の総称です。 インメモリ ベースの新機能が開発されるのに合わせて、このページは継続的に更新されます。

## <a name="hybrid-buffer-pool"></a>ハイブリッド バッファー プール

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[ハイブリッド バッファー プール](../database-engine/configure-windows/hybrid-buffer-pool.md)により、データベース エンジンから永続メモリ (PMEM) デバイスに格納されているデータベース ファイル内のデータ ページに直接アクセスできるようになります。

## <a name="memory-optimized-tempdb-metadata"></a>メモリ最適化 tempdb メタデータ

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では、[メモリ最適化 tempdb メタデータ](./databases/tempdb-database.md#memory-optimized-tempdb-metadata)という新機能が導入されています。この機能により、効果的に一部の競合ボトルネックが除去され、tempdb が多用されるワークロードに対して新たなレベルのスケーラビリティが実現されます。

## <a name="in-memory-oltp"></a>インメモリ OLTP

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[インメモリ OLTP](./in-memory-oltp/in-memory-oltp-in-memory-optimization.md) は、トランザクション処理のパフォーマンスの最適化、データ インジェスト、データの読み込み、および一時的なデータのシナリオに使用できる、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] と [!INCLUDE[ssSDS](../includes/sssds-md.md)] の高度な技術です。

**適用対象:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] から [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。

## <a name="persistent-memory-support-for-linux"></a>Linux に対する永続メモリのサポート

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] では、Linux に対する永続メモリ (PMEM) デバイスのサポートが追加されています。これにより、[永続メモリ](../linux/sql-server-linux-configure-pmem.md)に配置されるデータ ファイルとトランザクション ログ ファイルの完全なエンライトメントが提供されます。

**適用対象:** [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] から [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。