---
title: sqlmlutils を使用した Python パッケージのインストール
description: Python pip を使用して SQL Server Machine Learning Services のインスタンスに新しい Python パッケージをインストールする方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/26/2020
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: dcb3806c4ac165080e791db01d829272b3297e8a
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98091562"
---
# <a name="install-python-packages-with-sqlmlutils"></a>sqlmlutils を使用した Python パッケージのインストール

[!INCLUDE [SQL Server 2019 SQL MI](../../includes/applies-to-version/sqlserver2019-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
この記事では、[**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) パッケージの関数を使用して、[SQL Server](../sql-server-machine-learning-services.md) および [ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)上の Machine Learning Services のインスタンスに新しい Python パッケージをインストールする方法について説明します。 インストールするパッケージは、[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) T-SQL ステートメントを使用してデータベース内で実行されている Python スクリプトで使用できます。
::: moniker-end

::: moniker range="=azuresqldb-mi-current"
この記事では、[**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) パッケージの関数を使用して、[Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) のインスタンスに新しい Python パッケージをインストールする方法について説明します。 インストールするパッケージは、[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) T-SQL ステートメントを使用してデータベース内で実行されている Python スクリプトで使用できます。
::: moniker-end

パッケージの場所とインストール パスの詳細については、「[Get Python package information](../package-management/python-package-information.md)」(Python パッケージ情報の取得) を参照してください。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
> [!NOTE]
> この記事で説明されている **sqlmlutils** パッケージは SQL Server 2019 以降で Python パッケージを追加するために使用されます。 SQL Server 2017 以前の場合は、[Python ツールを使用したパッケージのインストール](./install-python-packages-standard-tools.md?view=sql-server-2017&preserve-view=true)に関する記事を参照してください。
::: moniker-end

## <a name="prerequisites"></a>前提条件

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
+ Python 言語オプションと共に [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) がインストールされている必要があります。
::: moniker-end

+ SQL Server への接続に使用するクライアント コンピューターに [Azure Data Studio](../../azure-data-studio/what-is-azure-data-studio.md) をインストールします。 他のデータベース管理ツールまたはクエリ ツールも使用できますが、この記事では Azure Data Studio を想定しています。

+ Azure Data Studio に Python カーネルをインストールします。 また、コマンドラインから Python をインストールして使用することもできます。また、[Python の拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-python.python)と共に [Visual Studio Code](https://code.visualstudio.com/download) などの代替 Python 開発環境を使用できます。

  クライアント コンピューター上の Python バージョンは、サーバー上の Python バージョンと一致する必要があります。また、インストールするパッケージは、お持ちの Python のバージョンに準拠している必要があります。
  SQL Server バージョンごとに含まれている Python のバージョンの詳細については、「[Python および R のバージョン](../sql-server-machine-learning-services.md#versions)」を参照してください。
  
  特定の SQL Server インスタンスの Python バージョンを確認するには、次の T-SQL コマンドを使用します。

  ```sql
  EXECUTE sp_execute_external_script
    @language = N'Python',
    @script = N'
  import sys
  print(sys.version)
  '
  ```

### <a name="other-considerations"></a>その他の考慮事項

+ Python パッケージ ライブラリは SQL Server インスタンスの Program Files フォルダー内にあります。既定では、このフォルダーにインストールするには管理者権限が必要です。 詳細については、[パッケージ ライブラリの場所](../package-management/python-package-information.md#default-python-library-location)に関するページを参照してください。

+ パッケージのインストールは、**sqlmlutils** に渡す接続情報で指定する SQL インスタンス、データベース、ユーザーに固有のものです。 パッケージを複数の SQL インスタンスまたはデータベースで使用する場合や、別のユーザーに対してパッケージを使用する場合は、それぞれにパッケージをインストールする必要があります。 例外として、`dbo` のメンバーによってパッケージがインストールされた場合、そのパッケージは *パブリック* であり、すべてのユーザーと共有することができます。 ユーザーがパブリック パッケージの新しいバージョンをインストールした場合、パブリック パッケージは影響を受けませんが、そのユーザーは新しいバージョンにアクセスできます。

+ パッケージを追加する前に、パッケージが SQL Server 環境に適しているかどうかを検討してください。

  + データベースをクエリするだけのタスクではなく、データベース エンジンとの緊密な統合からメリットが得られるタスク (機械学習など) には、データベース内の Python を使用することをお勧めします。

  + サーバーに対して計算の負荷が大きくなるパッケージを追加すると、パフォーマンスが低下します。

  + 強化された SQL Server 環境では、次のパッケージを避けることをお勧めします。
    + ネットワーク アクセスを必要とするパッケージ
    + 管理者特権でのファイル システム アクセスが必要なパッケージ
    + Web 開発、または SQL Server 内で実行しても効果のないタスクに使用されるパッケージ

  + Python パッケージ **tensorflow** は、sqlmlutils を使用してインストールすることはできません。 詳細と回避策については、[SQL Server Machine Learning Services の既知の問題](../troubleshooting/known-issues-for-sql-server-machine-learning-services.md#9-cannot-install-tensorflow-package-using-sqlmlutils)に関するページを参照してください。

## <a name="install-sqlmlutils-on-the-client-computer"></a>sqlmlutils をクライアント コンピューターにインストールする

**sqlmlutils** を使用するには、まず、SQL Server への接続に使用するクライアント コンピューターにインストールする必要があります。

### <a name="in-azure-data-studio"></a>Azure Data Studio で

Azure Data Studio で **sqlmlutils** を使用する場合は、Python カーネル ノートブックの [パッケージの管理] 機能を使用して、それをインストールできます。

1. [Azure Data Studio の Python カーネル ノートブック](../../azure-data-studio/notebooks/notebooks-python-kernel.md)で、 **[パッケージの管理]** をクリックします。
1. **[新規追加]** をクリックします。
1. **[Search Pip packages]\(Pip パッケージの検索\)** フィールドに「sqlmlutils」と入力し、 **[検索]** をクリックします。
1. インストールする **[パッケージ バージョン]** を選択します (最新バージョンが推奨されます)。
1. **[インストール]** をクリックし、次に **[閉じる]** をクリックします。

### <a name="from-python-command-line"></a>Python コマンド ラインから

Python コマンド プロンプトまたは IDE から **sqlmlutils** を使用する場合は、単純な **pip** コマンドを使用して sqlmlutils をインストールできます。

```console
pip install sqlmlutils
```

または zip ファイルから **sqlmlutils** をインストールすることもできます。

1. **pip** がインストールされていることを確認します。 詳細については [pip のインストール](https://pip.pypa.io/en/stable/installing/)に関するページを参照してください。
1. 最新の **sqlmlutils** zip ファイルを、 https://github.com/Microsoft/sqlmlutils/tree/master/Python/dist からクライアント コンピューターにダウンロードします。 ファイルは解凍しないでください。
1. **コマンド プロンプト** を開き、次のコマンドを実行して **sqlmlutils** パッケージをインストールします。 ダウンロードした **sqlmlutils** zip ファイルの完全なパスに置き換えます。この例では、ダウンロードしたファイルが `c:\temp\sqlmlutils-1.0.0.zip` であることを想定しています。
   ```console
   pip install --upgrade --upgrade-strategy only-if-needed c:\temp\sqlmlutils-1.0.0.zip
   ```

## <a name="add-a-python-package-on-sql-server"></a>SQL Server への Python パッケージのインストール

**sqlmlutils** を使用すると、SQL インスタンスに Python パッケージを追加できます。 その後、SQL インスタンスで実行されている Python コードでこれらのパッケージを使用できます。 **sqlmlutils** では、[CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md) を使用してパッケージとその依存関係がインストールされます。

次の例では、SQL Server に[テキスト ツール](https://pypi.org/project/text-tools/) パッケージを追加します。

### <a name="add-the-package-online"></a>パッケージをオンラインで追加する

SQL Server への接続に使用するクライアント コンピューターがインターネットにアクセスできる場合は、**sqlmlutils** を使用して、**テキスト ツール** パッケージ、およびインターネット経由のすべての依存関係を検索し、SQL Server インスタンスにパッケージをリモートでインストールすることができます。

::: moniker range=">=sql-server-ver15"

1. クライアント コンピューターで、**Python** または Python 環境を開きます。

1. 次のコマンドを使用して、**テキスト ツール** パッケージをインストールします。 独自の SQL Server データベース接続情報に置き換えます (Windows 認証を使用する場合は、`uid` パラメーターと `pwd` パラメーターは必要ありません)。

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=azuresqldb-mi-current"

1. クライアント コンピューターで、**Python** または Python 環境を開きます。

1. 次のコマンドを使用して、**テキスト ツール** パッケージをインストールします。 実際の SQL Server データベースの接続情報に置き換えてください。

::: moniker-end

   ```python
   import sqlmlutils
   connection = sqlmlutils.ConnectionInfo(server="server", database="database", uid="username", pwd="password")
   sqlmlutils.SQLPackageManager(connection).install("text-tools")
   ```

### <a name="add-the-package-offline"></a>パッケージをオフラインで追加する

SQL Server への接続に使用するクライアント コンピューターにインターネット接続がない場合は、インターネットにアクセスできるコンピューターで **pip** を使用して、パッケージとそのすべての依存パッケージをローカル フォルダーにダウンロードできます。 次に、パッケージをオフラインでインストールできるクライアント コンピューターにフォルダーをコピーします。

#### <a name="on-a-computer-with-internet-access"></a>インターネットに接続されているコンピューター

1. **コマンド プロンプト** を開き、次のコマンドを実行して、**テキスト ツール** パッケージを含むローカル フォルダーを作成します。 この例では、フォルダー `c:\temp\text-tools` を作成します。

   ```console
   pip download text-tools -d c:\temp\text-tools
   ```

1. `text-tools` フォルダーをクライアント コンピューターにコピーします。 次の例では、`c:\temp\packages\text-tools` にコピーしたことを想定しています。

#### <a name="on-the-client-computer"></a>クライアント コンピューター上

**sqlmlutils** を使用して、**pip** で作成した、ローカル フォルダー内にある各パッケージ (WHL ファイル) をインストールします。 パッケージはどのような順序でインストールしてもかまいません。

この例では、**テキスト ツール** に依存関係がないので、インストールする `text-tools` フォルダー内のファイルは 1 つのみです。 これに対し、**scikit-plot** のようなパッケージには 11 個の依存関係があるため、フォルダー内に 12 個のファイル (**scikit-plot** パッケージと 11 個の依存パッケージ) があり、それぞれをインストールします。

::: moniker range=">=sql-server-ver15"

次の Python スクリプトを実行します。 パッケージの実際のファイル パスと名前、独自の SQL Server データベース接続情報に置き換えます (Windows 認証を使用する場合は、`uid` パラメーターと `pwd` パラメーターは必要ありません)。 フォルダー内のパッケージ ファイルごとに `sqlmlutils.SQLPackageManager` ステートメントを繰り返します。

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=azuresqldb-mi-current"

次の Python スクリプトを実行します。 パッケージの実際のファイル パスと名前、独自の SQL Server データベース接続情報に置き換えます。 フォルダー内のパッケージ ファイルごとに `sqlmlutils.SQLPackageManager` ステートメントを繰り返します。

::: moniker-end

```python
import sqlmlutils
connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="username", pwd="password"))
sqlmlutils.SQLPackageManager(connection).install("text_tools-1.0.0-py3-none-any.whl")
```

## <a name="use-the-package"></a>パッケージを使用する

これで、SQL Server の Python スクリプトでパッケージを使用できるようになりました。 次に例を示します。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
from text_tools.finders import find_best_string
corpus = "Lorem Ipsum text"
query = "Ipsum"
first_match = find_best_string(query, corpus)
print(first_match)
  '
```

## <a name="remove-the-package-from-sql-server"></a>SQL Server からのパッケージの削除

**テキスト ツール** パッケージを削除する場合は、前に定義したのと同じ接続変数を使用して、クライアント コンピューターで次の Python コマンドを使用します。

```python
sqlmlutils.SQLPackageManager(connection).uninstall("text-tools")
```

## <a name="more-sqlmlutils-functions"></a>その他の sqlmlutils 関数

**sqlmlutils** パッケージには、Python パッケージを管理するためと、SQL Server でストアド プロシージャやクエリを作成、管理、実行するための関数が多数含まれています。 詳細については、[sqlmlutils Python の README ファイル](https://github.com/microsoft/sqlmlutils/tree/master/Python)を参照してください。

**sqlmlutils** 関数の詳細については、Python の **help** 関数を使用してださい。 次に例を示します。

```Python
import sqlmlutils
help(SQLPackageManager.install)
```

## <a name="next-steps"></a>次のステップ

+ SQL Server Machine Learning Services にインストールされている Python パッケージに関する情報については、「[Python パッケージ情報の取得](../package-management/python-package-information.md)」を参照してください。

+ SQL Server Machine Learning Services への R パッケージのインストールについては、[SQL Server への新しい R パッケージのインストール](install-additional-r-packages-on-sql-server.md)に関するページを参照してください。
