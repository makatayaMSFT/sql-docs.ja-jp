---
description: DROP SEQUENCE (Transact-SQL)
title: DROP SEQUENCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP SEQUENCE
- DROP_SEQUENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SEQUENCE statement
- sequence number object, dropping
ms.assetid: c25772d3-61af-4aa7-b58b-a6f67a793e3d
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 0513019d95994607cf3db97c0fe9f72f8c3e44e0
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98171624"
---
# <a name="drop-sequence-transact-sql"></a>DROP SEQUENCE (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  現在のデータベースからシーケンス オブジェクトを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
DROP SEQUENCE [ IF EXISTS ] { database_name.schema_name.sequence_name | schema_name.sequence_name | sequence_name } [ ,...n ]  
 [ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *IF EXISTS*  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql16-md.md)] から [現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。  
  
 条件付きではすでに存在する場合にのみ、シーケンスを削除します。  
  
 *database_name*  
 シーケンス オブジェクトが作成されたデータベースの名前を指定します。  
  
 *schema_name*  
 シーケンス オブジェクトが所属するスキーマの名前を指定します。  
  
 *sequence_name*  
 削除するシーケンスの名前です。 データ型は **sysname** です。  
  
## <a name="remarks"></a>Remarks  
 番号の生成後、その番号とシーケンス オブジェクトは無関係になるため、生成された番号が使用されている場合でも、シーケンス オブジェクトは削除できます。  
  
 シーケンス オブジェクトはスキーマ バインドされないため、ストアド プロシージャまたはトリガーによって参照されているシーケンス オブジェクトは削除できます。 テーブルで既定値として参照されているシーケンス オブジェクトは削除できません。 シーケンスを参照しているオブジェクトの一覧がエラー メッセージに表示されます。  
  
 データベース内のすべてのシーケンス オブジェクトを一覧表示するには、次のステートメントを実行します。  
  
```sql  
SELECT sch.name + '.' + seq.name AS [Sequence schema and name]   
    FROM sys.sequences AS seq  
    JOIN sys.schemas AS sch  
        ON seq.schema_id = sch.schema_id ;  
GO  
```  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 スキーマに対する ALTER または CONTROL 権限が必要です。  
  
### <a name="audit"></a>Audit  
 **DROP SEQUENCE** を監査するには、**SCHEMA_OBJECT_CHANGE_GROUP** を監視します。  
  
## <a name="examples"></a>例  
 次の例では、現在のデータベースから `CountBy1` という名前のシーケンス オブジェクトを削除します。  
  
```sql  
DROP SEQUENCE CountBy1 ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
