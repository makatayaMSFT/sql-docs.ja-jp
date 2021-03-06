---
description: Always Encrypted での Azure Key Vault プロバイダーの使用を示す例
title: Always Encrypted での Azure Key Vault プロバイダーの使用を示す例 | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2020
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: 6638144576d56a0225f03021f7cf8226643a45ab
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771584"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted"></a>Always Encrypted での Azure Key Vault プロバイダーの使用を示す例

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

この例は、暗号化された列にアクセスするときの Azure Key Vault プロバイダーの使用を示しています。

[!code-csharp [AKVProvider Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderExample.cs#1)]

> [!NOTE]
> - セキュリティで保護されたエンクレーブを使用しない Always Encrypted 機能を .NET Standard アプリケーションで使用するには、**Microsoft.Data.SqlClient** バージョン 2.1.0 以降が必要です。 サポートされている .NET Standard のバージョンは 2.0 以降です。 
>
> - Linux と macOS で Always Encrypted の機能を使用するには、**Microsoft.Data.SqlClient** バージョン 2.1.0 以降が必要です。

## <a name="see-also"></a>関連項目

- [セキュリティで保護されたエンクレーブによって有効になった Always Encrypted での Azure Key Vault プロバイダーの使用を示す例](azure-key-vault-enclave-example.md)
- [チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する .NET アプリケーションの開発](tutorial-always-encrypted-enclaves-develop-net-apps.md)」をご覧ください。
- [Always Encrypted と Microsoft .NET Data Provider for SQL Server を使用する](sqlclient-support-always-encrypted.md)
