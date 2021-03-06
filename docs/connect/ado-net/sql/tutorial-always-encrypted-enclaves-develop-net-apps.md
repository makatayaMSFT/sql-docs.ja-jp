---
description: チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して .NET アプリケーションを開発する
title: チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して .NET アプリケーションを開発する | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2021
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: 177737bd2927583bdfda1c9b36904faf4ed6023d
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534701"
---
# <a name="tutorial-develop-a-net-application-using-always-encrypted-with-secure-enclaves"></a>チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して .NET アプリケーションを開発する

[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-xxxx-md.md)]

このチュートリアルでは、[セキュリティで保護されたエンクレーブが設定された Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-enclaves.md) に対してサーバー側のセキュリティで保護されたエンクレーブを使用するデータベース クエリを発行する、アプリケーションを開発する方法について説明します。

> [!NOTE]
> セキュア エンクレーブを使用する Always Encrypted は、Windows でのみサポートされています。

## <a name="prerequisites"></a>前提条件

このチュートリアルの次の手順に従う前に、以下のチュートリアルのいずれかを完了していることを確認してください。

- [チュートリアル: SQL Server でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](../../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md)
- [チュートリアル: Azure SQL Database でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)

さらに、Visual Studio (バージョン 2019 を推奨) が必要です。[https://visualstudio.microsoft.com/](https://visualstudio.microsoft.com) からダウンロードできます。 アプリケーション開発環境で、.NET Framework 4.6 以降または .NET Core 2.1 以降が実行されている必要があります。

## <a name="step-1-set-up-your-visual-studio-project"></a>手順 1:Visual Studio プロジェクトを設定する

.NET Framework アプリケーションでセキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するには、お使いのアプリケーションが .NET Framework 4.6 以上をターゲットにしていることを確認する必要があります。 .NET Core アプリケーションでセキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するには、お使いのアプリケーションが .NET Core 2.1 以上をターゲットにしていることを確認する必要があります。

さらに、列マスター キーを Azure Key Vault に格納する場合は、アプリケーションを [Microsoft.Data.SqlClient.AlwaysEncrypted.AzureKeyVaultProvider NuGet](https://www.nuget.org/packages/Microsoft.Data.SqlClient.AlwaysEncrypted.AzureKeyVaultProvider) と統合する必要があります。

1. Visual Studio を開きます。

2. 新しい C\# コンソール アプリ (.NET Framework/Core) プロジェクトを作成します。

3. プロジェクトは必ず .NET Framework 4.6 以降または .NET Core 2.1 以降をターゲットにします。 ソリューション エクスプローラーでプロジェクトを右クリックし、 **[プロパティ]** を選択して、ターゲット フレームワークを設定します。

4. **[ツール]** (メイン メニュー) > **[NuGet パッケージ マネージャー]**  >  **[パッケージ マネージャー コンソール]** に移動して、次の NuGet パッケージをインストールします。 パッケージ マネージャー コンソールで次のコードを実行します。

   ```powershell
   Install-Package Microsoft.Data.SqlClient -Version 1.1.0
   ```

5. Azure Key Vault を使用して列マスター キーを格納する場合は、 **[ツール]** (メイン メニュー) > **[NuGet パッケージ マネージャー]**  >  **[パッケージ マネージャー コンソール]** に移動して、次の NuGet パッケージをインストールします。 パッケージ マネージャー コンソールで次のコードを実行します。

   ```powershell
   Install-Package Microsoft.Data.SqlClient.AlwaysEncrypted.AzureKeyVaultProvider -Version 1.0.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

## <a name="step-2-implement-your-application-logic"></a>手順 2:アプリケーションのロジックを実装する

このアプリケーションでは、**ContosoHR** データベース (「[チュートリアル: SSMS を使用したセキュリティで保護されたエンクレーブを持つ Always Encrypted の概要](../../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md)」または「[チュートリアル: Azure SQL Database でのセキュリティで保護されたエンクレーブを使用する Always Encrypted の概要](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)」) に接続し、**SSN** 列に対する `LIKE` 述語と、**Salary** 列に対する範囲比較が含まれるクエリを実行します。

1. (Visual Studio によって生成された) Program.cs ファイルの内容を、次のコードに置き換えます。 

    ```cs
    using System;
    using Microsoft.Data.SqlClient;
    using System.Data;

    namespace ConsoleApp1
    {
        class Program
        {
            static void Main(string[] args)
            {

                // Connection string for SQL Server
                string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Attestation Protocol = HGS; Enclave Attestation Url = http://hgs.bastion.local/Attestation; Integrated Security = true";

                // Connection string for Azure SQL Database
                //string connectionString = "Data Source = myserver.database.windows.net; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Attestation Protocol = AAS; Enclave Attestation Url = https://myattestationprovider.uks.attest.azure.net/attest/SgxEnclave; User ID=user; Password=password";

                using (SqlConnection connection = new SqlConnection(connectionString))
                {
                    connection.Open();

                    SqlCommand cmd = connection.CreateCommand();
                    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [Salary] FROM [HR].[Employees] WHERE [SSN] LIKE @SSNPattern AND [Salary] > @MinSalary;";

                    SqlParameter paramSSNPattern = cmd.CreateParameter();

                    paramSSNPattern.ParameterName = @"@SSNPattern";
                    paramSSNPattern.DbType = DbType.AnsiStringFixedLength;
                    paramSSNPattern.Direction = ParameterDirection.Input;
                    paramSSNPattern.Value = "%9838";
                    paramSSNPattern.Size = 11;

                    cmd.Parameters.Add(paramSSNPattern);

                    SqlParameter MinSalary = cmd.CreateParameter();

                    MinSalary.ParameterName = @"@MinSalary";
                    MinSalary.DbType = DbType.Currency;
                    MinSalary.Direction = ParameterDirection.Input;
                    MinSalary.Value = 20000;

                    cmd.Parameters.Add(MinSalary);
                    cmd.ExecuteNonQuery();

                    SqlDataReader reader = cmd.ExecuteReader();
                    while (reader.Read())

                    {
                        Console.WriteLine(reader[0] + ", " + reader[1] + ", " + reader[2] + ", " + reader[3]);
                    }
                    Console.ReadKey();
                }
            }
        }
    }
    ```

2. データベース接続文字列を更新します。
    1. 有効なサーバー名とデータベース認証設定を設定します。
    2. `Attestation Protocol` キーワードの値を次のように設定します。
       - `HGS` - [!INCLUDE[ssnoversion-md](../../../includes/ssnoversion-md.md)] とホスト ガーディアン サービス (HGS) を使用している場合。
       - `AAS` - [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] と Microsoft Azure Attestation を使用している場合。
    3. `Enclave Attestation URL` を環境の構成証明 URL に設定します。

3. アプリケーションをビルドして実行します。

## <a name="see-also"></a>こちらもご覧ください

- [Always Encrypted と Microsoft .NET Data Provider for SQL Server を使用する](sqlclient-support-always-encrypted.md)
- [Always Encrypted での Azure Key Vault プロバイダーの使用を示す例](azure-key-vault-example.md)
- [セキュリティで保護されたエンクレーブによって有効になった Always Encrypted での Azure Key Vault プロバイダーの使用を示す例](azure-key-vault-enclave-example.md)
