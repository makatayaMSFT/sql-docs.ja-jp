---
description: MSSQLSERVER_1785
title: MSSQLSERVER_1785
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1785 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 0ee5aedf0d0f893552559540e25e18b11b19beac
ms.sourcegitcommit: d819173fb91af6f20ca6ee59686c35c71b060fbc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/28/2020
ms.locfileid: "97797805"
---
# <a name="mssqlserver_1785"></a>MSSQLSERVER_1785
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|1785|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|CRTFKINVTOPO|
|メッセージ テキスト|テーブル '%.ls' に FOREIGN KEY 制約 '%. ls' を設定すると、パスが循環するか、複数のパスに連鎖する可能性があります。 ON DELETE NO ACTION、ON UPDATE NO ACTION、を指定するか、他の FOREIGN KEY 制約を変更してください。|
||

## <a name="explanation"></a>説明

このエラー メッセージが表示されるのは、SQL Server では、`DELETE` または `UPDATE` ステートメントのいずれかによって開始された連鎖参照アクションの全一覧に、1 つのテーブルを複数回表示することはできないためです。 連鎖参照アクションのツリーには、連鎖参照アクション ツリー上の特定のテーブルへのパスが 1 つだけ必要です。

次のようなエラー メッセージがユーザーに報告されます。

> サーバー: メッセージ 1785、レベル 16、状態 1、行 1 テーブル 'table2' に FOREIGN KEY 制約 'fk_two' を設定すると、パスが循環するか、複数のパスに連鎖する可能性があります。 ON DELETE NO ACTION、ON UPDATE NO ACTION、を指定するか、他の FOREIGN KEY 制約を変更してください。 サーバー: メッセージ 1750、レベル 16、状態 1、行 1 制約を作成できませんでした。 以前のエラーを参照してください

## <a name="user-action"></a>ユーザー アクション

この問題を解決するには、連鎖参照アクションの一覧にテーブルへの単一のパスを作成する外部キーを作成します。

参照整合性は、複数の方法で適用できます。 最も基本的な方法は宣言参照整合性 (DRI) ですが、これは最も柔軟性の低い方法でもあります。 より高い柔軟性を必要としつつも、引き続き高レベルの整合性が必要な場合は、代わりにトリガーを使用できます。

## <a name="more-information"></a>説明

次のサンプル コードは、エラー メッセージが生成される外部キー作成の試行の例です。

```sql
USE tempdb
GO

CREATE TABLE table1 (user_ID INTEGER NOT NULL PRIMARY KEY, user_name
CHAR(50) NOT NULL)
GO

CREATE TABLE table2 (author_ID INTEGER NOT NULL PRIMARY KEY, author_name
CHAR(50) NOT NULL, lastModifiedBy INTEGER NOT NULL, addedby INTEGER NOT NULL)
GO

ALTER TABLE table2 ADD CONSTRAINT fk_one FOREIGN KEY (lastModifiedby)
REFERENCES table1 (user_ID) ON DELETE CASCADE ON UPDATE cascade
GO

ALTER TABLE table2 ADD CONSTRAINT fk_two FOREIGN KEY (addedby)
REFERENCES table1(user_ID) ON DELETE NO ACTION ON UPDATE cascade
GO
--this fails with the error because it provides a second cascading path to table2.

ALTER TABLE table2 ADD CONSTRAINT fk_two FOREIGN KEY (addedby)
REFERENCES table1 (user_ID) ON DELETE NO ACTION ON UPDATE NO ACTION
GO
-- this works.
```

### <a name="see-also"></a>関連項目

[連鎖参照整合性](/sql/relational-databases/tables/primary-and-foreign-key-constraints#referential-integrity)
