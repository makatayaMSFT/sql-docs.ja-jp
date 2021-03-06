---
description: SQL Server への接続 (DB2ToSQL)
title: SQL Server への接続 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: bc14a072-8949-4ee0-a4b4-ada55fe8df5c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 8b9d2fc6610ad7a0af9518bd91b270d914e9e622
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88373008"
---
# <a name="connect-to-sql-server-db2tosql"></a>SQL Server への接続 (DB2ToSQL)
[ **SQL Server への接続** ] ダイアログボックスを使用すると、に移行するのインスタンスに接続 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] できます。 [ **SQL Server への接続** ] ダイアログボックスにアクセスするには、[ **ファイル** ] メニューの [ **SQL Server に接続**] をクリックします。  
  
## <a name="options"></a>Options  
**サーバー名**  
接続する SQL Server のインスタンスを入力または選択します。 既定では、最近接続したインスタンスが表示されます。  
  
-   ローカルコンピューター上の既定のインスタンスに接続している場合は、 **localhost** またはドット (**.**) のいずれかを入力できます。  
  
-   別のコンピューター上の既定のインスタンスに接続している場合は、コンピューターの名前を入力します。  
  
-   別のコンピューター上の名前付きインスタンスに接続する場合は、コンピューター名、円記号、インスタンス名 ( *MyServer* \\ *myinstance*など) を入力します。  
  
**サーバーポート**  
のインスタンス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が既定のポート (1433) で接続を受け入れるように構成されていない場合は、ポート番号を入力します。 それ以外の場合は、この値を空白のままにします。  
  
**[データベース]**  
オブジェクトとデータを移行するデータベースを指定します。 このオプションは、に再接続するときには使用できません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
**認証**  
への接続に使用する認証方法を選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 現在の Windows アカウントを使用するには、[Windows 認証] を選択します。 ログインとパスワードを指定するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、[認証] を選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
**ユーザー名**  
認証を使用している場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、のインスタンスのログインを入力し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 Windows 認証を使用している場合、このオプションは使用できません。  
  
**パスワード**  
認証を使用している場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、のインスタンスにログインするためのパスワードを入力し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 Windows 認証を使用している場合、このオプションは使用できません。  
  
**暗号化接続**  
SQL Server に安全に接続する場合は、[ **暗号化接続** ] チェックボックスをオンにして、暗号化接続を使用します。  
  
**[Trust Server Certificate]**  
このオプションを使用する場合は、[ **サーバー証明書を信頼** する] チェックボックスをオンにします。  
  
> [!NOTE]  
> 信頼された **サーバー証明書**を有効にするには、"Encrypt" を **True**に設定する必要があります。  
  
