---
title: UWP アプリでの MySQL データベースの使用
description: UWP アプリで MySQL データベースを使用します。
ms.date: 03/28/2019
ms.topic: article
keywords: windows 10, uwp, MySQL, データベース
ms.localizationpriority: medium
ms.openlocfilehash: bfed9c0a0c4198095b9be48fe71832bdfca67718
ms.sourcegitcommit: 76e8b4fb3f76cc162aab80982a441bfc18507fb4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "67713789"
---
# <a name="use-a-mysql-database"></a>MySQL データベースの使用
この記事には、UWP アプリからの MySQL データベースの使用を有効にするのに必要な手順が含まれます。 これには、コードでどのようにデータベースとやりとりできるかを示す小さなコード スニペットも含まれます。

## <a name="set-up-your-solution"></a>ソリューションを設定する

アプリを MySQL データベースに直接接続するために、プロジェクトの最小バージョンが確実に Fall Creators Update (ビルド 16299) を対象にするようにします。  UWP プロジェクトのプロパティ ページにその情報があります。

![Fall Creators Update に設定されたターゲット バージョンと最小バージョンを示す Visual Studio のターゲット設定プロパティ ウィンドウの画像](images/min-version-fall-creators.png)

**パッケージ マネージャー コンソール**を開きます ([表示] -> [その他のウィンドウ] -> [パッケージ マネージャー コンソール])。 **Install-Package MySql.Data** コマンドを使用して、MySQL 用のドライバーをインストールします。 これにより、プログラムを使用して MySQL データベースにアクセスできるようになります。

## <a name="test-your-connection-using-sample-code"></a>サンプル コードを使用して接続をテストする
リモートの MySQL データベースからの接続および読み取りの例は、次のとおりです。 IP アドレス、認証情報、データベース名はカスタマイズする必要があることに注意してください。

```csharp
string M_str_sqlcon = "server=10.xxx.xx.xxx;user id=foo;password=bar;database=baz";
MySqlConnection mysqlcon = new MySqlConnection(M_str_sqlcon);
MySqlCommand mysqlcom = new MySqlCommand("select * from table1", mysqlcon);
mysqlcon.Open();
MySqlDataReader mysqlread = mysqlcom.ExecuteReader(CommandBehavior.CloseConnection);
while (mysqlread.Read())
{
    Debug.WriteLine(mysqlread.GetString(0)+":"+mysqlread.GetString(1));
}
mysqlcon.Close();
```
