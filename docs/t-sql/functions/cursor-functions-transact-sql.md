---
description: カーソル関数 (Transact-SQL)
title: カーソル関数 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], cursors
- cursor functions
ms.assetid: 7d9daa10-4c50-4212-9400-42120222b2b8
author: cawrites
ms.author: chadam
ms.openlocfilehash: 3433a39caeb0a1e951eba18ccdd3d1658c108252
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98087749"
---
# <a name="cursor-functions-transact-sql"></a>カーソル関数 (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

これらのスカラー関数は、カーソルについての情報を返します。
  
- [@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)
- [@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md)
- [CURSOR_STATUS](../../t-sql/functions/cursor-status-transact-sql.md)
  
すべてのカーソル関数は非決定的です。 つまり、これらの関数は、同じ一連の入力値を使用しても、実行されるたびに常に同じ結果を返すわけではありません。 関数の決定性の詳細については、「[決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。
  
## <a name="see-also"></a>関連項目

[組み込み関数 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)
