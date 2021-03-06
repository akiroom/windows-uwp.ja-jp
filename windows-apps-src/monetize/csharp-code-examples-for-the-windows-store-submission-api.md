---
ms.assetid: FABA802F-9CB2-4894-9848-9BB040F9851F
description: このセクションの C# コード例を使用して、Microsoft Store 申請 API を使用する方法をご確認ください。
title: C# のコード例 - アプリ、アドオン、およびフライトの申請
ms.date: 08/03/2017
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store 申請 API, コード例, C#
ms.localizationpriority: medium
ms.openlocfilehash: b3073e2a5ffa445a39bdf6d54dd288be97c88207
ms.sourcegitcommit: 6a7dd4da2fc31ced7d1cdc6f7cf79c2e55dc5833
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2019
ms.locfileid: "58334970"
---
# <a name="c-sample-submissions-for-apps-add-ons-and-flights"></a>C\#サンプル: アプリ、アドオン、および便の送信

この記事では、次のタスクで [Microsoft Store 申請 API](create-and-manage-submissions-using-windows-store-services.md) を使用する方法を示す C# コード例を提供します。

* [アプリの提出を作成します。](#create-app-submission)
* [アドオンを提出を作成します。](#create-add-on-submission)
* [アドオンを申請を更新します。](#update-add-on-submission)
* [パッケージのフライトの提出を作成します。](#create-flight-submission)

各例を確認して、それぞれが対応するタスクについて詳しく知ることができます。また、この記事のすべてのコード例を使って、コンソール アプリケーションをビルドすることもできます。 サンプルをビルドするには、Visual Studio で**DeveloperApiCSharpSample** という名前の C# コンソール アプリケーションを作成し、各サンプルをプロジェクトの別のコード ファイルにコピーして、プロジェクトをビルドします。

## <a name="prerequisites"></a>前提条件

以下の例では、次のライブラリを使用します。

* Microsoft.WindowsAzure.Storage.dll。 このライブラリは、[Azure SDK for .NET](https://azure.microsoft.com/downloads/) に含まれています。または [WindowsAzure.Storage NuGet パッケージ](https://www.nuget.org/packages/WindowsAzure.Storage)をインストールすると入手できます。
* Newtonsoft の [Newtonsoft.Json](https://www.newtonsoft.com/json) NuGet パッケージ。

## <a name="main-program"></a>メイン プログラム

次の例では、コマンド ライン プログラムを実装し、この記事の他のサンプル メソッドを呼び出して、Microsoft Store 申請 API のさまざまな使用方法を示します。 このプログラムを採用するには、次の手順を実行してください。

* ```ApplicationId```、```InAppProductId```、および ```FlightId``` プロパティを、管理するアプリ、アドオン、およびパッケージ フライトの ID に割り当てます。
* ```ClientId``` および ```ClientSecret``` プロパティをアプリのクライアント ID とキーに割り当て、```TokenEndpoint``` URL 内の文字列 *tenantid* をアプリのテナント ID に置き換えます。 詳細については、次を参照してください[に Azure AD アプリケーションを、パートナー センター アカウントに関連付ける方法。](create-and-manage-submissions-using-windows-store-services.md#how-to-associate-an-azure-ad-application-with-your-partner-center-account)

> [!div class="tabbedCodeSnippets"]
[!code-csharp[SubmissionApi](./code/StoreServicesExamples_Submission/cs/Program.cs#Main)]

<span id="clientconfiguration" />

## <a name="clientconfiguration-helper-class"></a>ClientConfiguration ヘルパー クラス

サンプル アプリでは、Microsoft Store 申請 API を使用する各サンプル メソッドに Azure Active Directory データとアプリ データを渡すために、```ClientConfiguration``` ヘルパー クラスが使われています。

> [!div class="tabbedCodeSnippets"]
[!code-csharp[SubmissionApi](./code/StoreServicesExamples_Submission/cs/ClientConfiguration.cs#ClientConfiguration)]

<span id="create-app-submission" />

## <a name="create-an-app-submission"></a>アプリの申請の作成

次の例では、Microsoft Store 申請 API のいくつかのメソッドを使ってアプリの申請を更新するクラスを実装します。 ```RunAppSubmissionUpdateSample```クラスのメソッドは、パブリッシュされた最後の送信の複製として新しい送信を作成し、更新し、パートナー センターに複製された送信をコミットします。 具体的には、```RunAppSubmissionUpdateSample``` メソッドは次のタスクを実行します。

1. まず、メソッドは[指定されたアプリのデータを取得](get-an-app.md)します。
2. 次に、[アプリの保留中の申請を削除](delete-an-app-submission.md)します (存在する場合)。
3. その後、[アプリの新しい申請を作成](create-an-app-submission.md)します (新しい申請は、最後に公開された申請のコピーです)。
4. 新しい申請の詳細を変更し、申請の新しいパッケージを Azure Blob Storage にアップロードします。
5. 次に、その[更新](update-an-app-submission.md)し[コミット](commit-an-app-submission.md)パートナー センターに新しい送信します。
6. 最後に、申請が正常にコミットされるまで、定期的に[新しい申請の状態をチェック](get-status-for-an-app-submission.md)します。

> [!div class="tabbedCodeSnippets"]
[!code-csharp[SubmissionApi](./code/StoreServicesExamples_Submission/cs/AppSubmissionUpdateSample.cs#AppSubmissionUpdateSample)]

<span id="create-add-on-submission" />

## <a name="create-an-add-on-submission"></a>アドオンの申請の作成

次の例では、Microsoft Store 申請 API のいくつかのメソッドを使って新しいアドオンの申請を作成するクラスを実装します。 クラスの ```RunInAppProductSubmissionCreateSample``` メソッドは、次のタスクを実行します。

1. まず、メソッドは[新しアドオンを作成](create-an-add-on.md)します。
2. 次に、その[アドオンの新しい申請を作成](create-an-add-on-submission.md)します。
3. 申請のアイコンが含まれた ZIP アーカイブを Azure Blob Storage にアップロードします。
4. 次に、その[パートナー センターに新しい送信コミット](commit-an-add-on-submission.md)します。
5. 最後に、申請が正常にコミットされるまで、定期的に[新しい申請の状態をチェック](get-status-for-an-add-on-submission.md)します。

> [!div class="tabbedCodeSnippets"]
[!code-csharp[SubmissionApi](./code/StoreServicesExamples_Submission/cs/InAppProductSubmissionCreateSample.cs#InAppProductSubmissionCreateSample)]

<span id="update-add-on-submission" />

## <a name="update-an-add-on-submission"></a>アドオンの申請の更新

次の例では、Microsoft Store 申請 API のいくつかのメソッドを使って既存のアドオンの申請を更新するクラスを実装します。 ```RunInAppProductSubmissionUpdateSample```クラスのメソッドは、パブリッシュされた最後の送信の複製として新しい送信を作成し、更新し、パートナー センターに複製された送信をコミットします。 具体的には、```RunInAppProductSubmissionUpdateSample``` メソッドは次のタスクを実行します。

1. まず、メソッドは[指定されたアドオンのデータを取得](get-an-add-on.md)します。
2. 次に、[アドオンの保留中の申請を削除](delete-an-add-on-submission.md)します (存在する場合)。
3. その後、[アドオンの新しい申請を作成](create-an-add-on-submission.md)します (新しい申請は、最後に公開された申請のコピーです)。
5. 次に、その[更新](update-an-add-on-submission.md)し[コミット](commit-an-add-on-submission.md)パートナー センターに新しい送信します。
6. 最後に、申請が正常にコミットされるまで、定期的に[新しい申請の状態をチェック](get-status-for-an-add-on-submission.md)します。

> [!div class="tabbedCodeSnippets"]
[!code-csharp[SubmissionApi](./code/StoreServicesExamples_Submission/cs/InAppProductSubmissionUpdateSample.cs#InAppProductSubmissionUpdateSample)]

<span id="create-flight-submission" />

## <a name="create-a-package-flight-submission"></a>パッケージ フライトの申請の作成

次の例では、Microsoft Store 申請 API のいくつかのメソッドを使ってパッケージ フライトの申請を更新するクラスを実装します。 ```RunFlightSubmissionUpdateSample```クラスのメソッドは、パブリッシュされた最後の送信の複製として新しい送信を作成し、更新し、パートナー センターに複製された送信をコミットします。 具体的には、```RunFlightSubmissionUpdateSample``` メソッドは次のタスクを実行します。

1. まず、メソッドは[指定されたパッケージ フライトのデータを取得](get-a-flight.md)します。
2. 次に、[パッケージ フライトの保留中の申請を削除](delete-a-flight-submission.md)します (存在する場合)。
3. その後、[パッケージ フライトの新しい申請を作成](create-a-flight-submission.md)します (新しい申請は、最後に公開された申請のコピーです)。
4. 申請の新しいパッケージを Azure Blob Storage にアップロードします。
5. 次に、その[更新](update-a-flight-submission.md)し[コミット](commit-a-flight-submission.md)パートナー センターに新しい送信します。
6. 最後に、申請が正常にコミットされるまで、定期的に[新しい申請の状態をチェック](get-status-for-a-flight-submission.md)します。

> [!div class="tabbedCodeSnippets"]
[!code-csharp[SubmissionApi](./code/StoreServicesExamples_Submission/cs/FlightSubmissionUpdateSample.cs#FlightSubmissionUpdateSample)]

<span id="ingestionclient" />

## <a name="ingestionclient-helper-class"></a>IngestionClient ヘルパー クラス

```IngestionClient``` クラスは、サンプル アプリのその他のメソッドが使用して、次のタスクを実行するヘルパー メソッドを提供します。

* Microsoft Store 申請 API のメソッドの呼び出しに使用できる [Azure AD アクセス トークンを取得](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 トークンを取得した後、Microsoft Store 申請 API の呼び出しでこのトークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れた後は、新しいトークンを生成できます。
* アプリまたはアドオンの申請の新しいアセットが含まれた ZIP アーカイブを Azure Blob Storage にアップロードします。 アプリとアドオンの申請のために Azure Blob Storage に ZIP アーカイブをアップロードする方法について詳しくは、「[アプリの申請の作成](manage-app-submissions.md#create-an-app-submission)」と「[アドオンの申請の作成](manage-add-on-submissions.md#create-an-add-on-submission)」の関連する手順をご覧ください。
* Microsoft Store 申請 API の HTTP 要求を処理します。

> [!div class="tabbedCodeSnippets"]
[!code-csharp[SubmissionApi](./code/StoreServicesExamples_Submission/cs/IngestionClient.cs#IngestionClient)]

## <a name="related-topics"></a>関連トピック

* [作成し、Microsoft Store サービスを使用して送信の管理](create-and-manage-submissions-using-windows-store-services.md)
