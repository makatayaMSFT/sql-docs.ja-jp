---
description: 柔軟なファイルの変換先
title: 柔軟なファイルの変換先 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpextfiledest.f1
- sql14.dts.designer.afpextfiledest.f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d331004e82b155a1c101a31253a82e029ec4a31b
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98091653"
---
# <a name="flexible-file-destination"></a>柔軟なファイルの変換先

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

**柔軟なファイルの変換先** コンポーネントにより、SSIS パッケージがサポートされているさまざまなストレージ サービスにデータを書き込めるようになります。

現在サポートされているストレージ サービスは次のとおりです。

- [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](/azure/storage/blobs/data-lake-storage-introduction)
   
**柔軟なファイルの変換先** をデータ フロー デザイナーにドラッグ アンド ドロップし、ダブルクリックしてエディターを表示します。
  
**柔軟なファイルの変換先** は、[SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。  

次のプロパティは、**柔軟なファイルの変換先エディター** で利用できます。

- **[File Connection Manager Type]\(ファイル接続マネージャーの種類\):** ソース接続マネージャーの種類を指定します。 そして、指定された種類の既存のものを選択するか、新しいものを作成します。
- **[フォルダー パス]:** 送信先フォルダーのパスを指定します。
- **ファイル名:** 送信先ファイル名を指定します。
- **[ファイル形式]:** 送信先のファイル形式を指定します。 サポートされている形式は、**テキスト**、**Avro**、**ORC**、**Parquet** です。 ORC/Parquet の場合は Java が必要です。 詳細については、[こちら](../../integration-services/azure-feature-pack-for-integration-services-ssis.md#dependency-on-java)を参照してください。
- **[列区切り文字]:** 列区切り記号として使用される文字を指定します (複数文字の区切り記号はサポートされていません)。
- **[First row as the column name]\(先頭行を列名にする\):** 先頭行に列名を書き込むかどうかを指定します。
- **[Compress the file]\(ファイルの圧縮\):** ファイルを圧縮するかどうかを指定します。
- **[圧縮の種類]:** 使用する圧縮形式を指定します。 サポートされている形式は **GZIP**、**DEFLATE**、**BZIP2** です。
- **[圧縮レベル]:** 使用する圧縮レベルを指定します。

次のプロパティは、**詳細エディター** で利用できます。

- **rowDelimiter:** ファイルの行を区切るための文字。 許可される文字は 1 つだけです。 **既定** 値は \r\n です。
- **escapeChar:** 入力ファイルの列区切り記号をエスケープするための特殊文字。 escapeChar と quoteChar の両方をテーブルに指定することはできません。 許可される文字は 1 つだけです。 既定値はありません。
- **quoteChar:** 文字列値を引用符で囲むための文字。 引用符文字内の列区切り記号と行区切り記号は文字列値の一部として扱われます。 このプロパティは、入力と出力の両方のデータセットに適用できます。 escapeChar と quoteChar の両方をテーブルに指定することはできません。 許可される文字は 1 つだけです。 既定値はありません。
- **nullValue:** null 値を表すための 1 つまたは複数の文字。 **既定** 値は \N です。
- **encodingName:** エンコーディング名を指定します。 [Encoding.EncodingName](/dotnet/api/system.text.encoding) プロパティを参照してください。
- **skipLineCount:** 入力ファイルからデータを読むとき、スキップする空ではない行の数を示します。 skipLineCount と firstRowAsHeader の両方が指定されている場合、行が最初にスキップされ、次に、入力ファイルからヘッダー情報が読まれます。
- **treatEmptyAsNull:** 入力ファイルからデータを読むとき、null 値として null または空の文字列を扱うことを指定します。 既定値は **True** です。

接続情報を指定した後、 **[列]** ページで、SSIS データ フローのマップ元の列をマップ先の列にマップします。

**サービス プリンシパルのアクセス許可の構成に関する注意事項**

**テスト接続** が機能するためには (BLOB ストレージまたは Data Lake Storage Gen2)、サービス プリンシパルには少なくともストレージ アカウントに対する **ストレージ BLOB データ閲覧者** の役割を割り当てる必要があります。
これは、[RBAC](/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal) を使用して行います。

BLOB ストレージの場合、少なくとも **ストレージ BLOB データ共同作成者** の役割を割り当てることにより、書き込みのアクセス許可が付与されます。

Data Lake Storage Gen2 の場合、アクセス許可は RBAC と [ACL](/azure/storage/blobs/data-lake-storage-how-to-set-permissions-storage-explorer) の両方によって決定されます。
[こちら](/azure/storage/blobs/data-lake-storage-access-control#how-do-i-set-acls-correctly-for-a-service-principal)に説明されているように、アプリ登録に対応するサービス プリンシパルのオブジェクト ID (OID) を使用して ACL を構成することに注意してください。
これは、RBAC 構成で使用されるアプリケーション (クライアント) ID とは異なります。
組み込みロールまたはカスタム ロールを使用してセキュリティ プリンシパルに RBAC データ アクセス許可が付与されると、これらのアクセス許可は、要求の認可時に最初に評価されます。
要求された操作がセキュリティ プリンシパルの RBAC 割り当てによって認可された場合、認可はすぐに解決され、追加の ACL チェックは実行されません。
また、セキュリティ プリンシパルに RBAC 割り当てがない場合、または要求の操作が割り当てられたアクセス許可と一致しない場合、ACL チェックが実行され、要求された操作を実行する権限がセキュリティ プリンシパルに付与されているかどうかが判断されます。
書き込みアクセス許可の場合、少なくともシンク ファイル システムから開始する **実行** アクセス許可を、シンク フォルダーに対する **書き込み** アクセス許可と共に付与します。
または、少なくとも **ストレージ BLOB データ共同作成者** の役割を RBAC を使用して付与します。
詳細については、[この記事](/azure/storage/blobs/data-lake-storage-access-control)を参照してください。