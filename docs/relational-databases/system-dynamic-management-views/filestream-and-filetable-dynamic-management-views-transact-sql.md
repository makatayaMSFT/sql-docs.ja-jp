---
description: Filestream および FileTable の動的管理ビュー (Transact-SQL)
title: Filestream および FileTable の動的管理ビュー (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], dynamic management views
ms.assetid: e50a135d-6644-42a4-a0df-1c7a2b722051
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 3af7a4d72a93d2c44f470f83f6a0010737d3adcc
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98099032"
---
# <a name="filestream-and-filetable-dynamic-management-views-transact-sql"></a>Filestream および FileTable の動的管理ビュー (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ここでは、FILESTREAM 機能および FileTable 機能に関連する動的管理ビューについて説明します。  
  
## <a name="filestream-dynamic-management-views-and-functions"></a>Filestream 動的管理ビューおよび関数  
 [sys.dm_filestream_file_io_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-handles-transact-sql.md)  
 現在開いているトランザクション ファイル ハンドルを表示します。  
  
 [sys.dm_filestream_file_io_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-requests-transact-sql.md)  
 現在のファイル入力とファイル出力の要求を表示します。  
  
## <a name="filetable-dynamic-management-views-and-functions"></a>FileTable 動的管理ビューおよび関数  
 [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)  
 現在開いている、FileTable データに対する非トランザクション ファイル ハンドルを表示します。  

## <a name="see-also"></a>参照
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream および FileTable のカタログ ビュー (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[Filestream および FileTable システム ストアド プロシージャ (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)
  
