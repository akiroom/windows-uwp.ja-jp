---
author: mcleanbyron
description: アプリの申請に関するパッケージのロールアウトを停止するには、Microsoft Store 申請 API の以下のメソッドを使います。
title: アプリの申請に関するロールアウトの停止
ms.author: mcleans
ms.date: 04/17/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, UWP, Microsoft Store 申請 API, パッケージのロールアウト, アプリの申請, 停止
ms.assetid: 4ce79fe3-deda-4d31-b938-d672c3869051
ms.localizationpriority: medium
ms.openlocfilehash: 75575724e93d8abfb79c5527ae97fdec7da6f137
ms.sourcegitcommit: 91511d2d1dc8ab74b566aaeab3ef2139e7ed4945
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2018
ms.locfileid: "1817693"
---
# <a name="halt-the-rollout-for-an-app-submission"></a>アプリの申請に関するロールアウトの停止


アプリの申請に関する[パッケージのロールアウトを停止する](../publish/gradual-package-rollout.md#completing-the-rollout)には、Microsoft Store 申請 API の以下のメソッドを使います。 Microsoft Store 申請 API を使ったアプリの申請の作成プロセスについて詳しくは、「[アプリの申請の管理](manage-app-submissions.md)」をご覧ください。

> [!NOTE]
> アプリの申請に関するロールアウトを停止してから、[新しいアプリの申請を作成する](create-an-app-submission.md)場合、新しい申請は停止した申請を複製したものになります。


## <a name="prerequisites"></a>前提条件

このメソッドを使うには、最初に次の作業を行う必要があります。

* Microsoft Store 申請 API に関するすべての[前提条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら、新しいトークンを取得できます。
* デベロッパー センターのアカウントでアプリの申請を作成します。 この操作は、デベロッパー センター ダッシュボードまたは[アプリ申請の作成](create-an-app-submission.md)メソッドを使って実行できます。
* 申請に関する段階的なパッケージのロールアウトを有効にします。 これは、[デベロッパー センター ダッシュボード](../publish/gradual-package-rollout.md)で行うことも、[Microsoft Store 申請 API](manage-app-submissions.md#manage-gradual-package-rollout) を使って行うこともできます。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求のパラメーターの使用例と説明については、以下のセクションをご覧ください。

| メソッド | 要求 URI                                                      |
|--------|------------------------------------------------------------------|
| POST   | ```https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/haltpackagerollout``` |


### <a name="request-header"></a>要求ヘッダー

| ヘッダー        | 型   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| Authorization | 文字列 | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |


### <a name="request-parameters"></a>要求パラメーター

| 名前        | 種類   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| applicationId | string | 必須。 停止するパッケージのロールアウトの対象となる申請が含まれているアプリのストア ID です。 ストア ID について詳しくは、「[アプリ ID の詳細の表示](https://msdn.microsoft.com/windows/uwp/publish/view-app-identity-details)」をご覧ください。  |
| submissionId | string | 必須。 停止するパッケージのロールアウトの対象となる申請の ID です。 この ID は、[アプリの申請の作成](create-an-app-submission.md)要求に対する応答データで確認できます。 デベロッパー センター ダッシュボードで作成された申請の場合、この ID はダッシュボードの申請ページの URL にも含まれています。  |


### <a name="request-body"></a>要求本文

このメソッドでは要求本文を指定しないでください。

### <a name="request-example"></a>要求の例

アプリの申請に関するパッケージのロールアウトを停止する方法の例を次に示します。

```
POST https://manage.devcenter.microsoft.com/v1.0/my/applications/9NBLGGH4R315/submissions/1152921504621243680/haltpackagerollout HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答

次の例は、このメソッドが正常に呼び出された場合の JSON 応答本文を示しています。 応答本文の値について詳しくは、「[パッケージのロールアウトのリソース](manage-app-submissions.md#package-rollout-object)」をご覧ください。

```json
{
    "isPackageRollout": true,
    "packageRolloutPercentage": 0.0,
    "packageRolloutStatus": "PackageRolloutStopped",
    "fallbackSubmissionId": "1212922684621243058"
}
```

## <a name="error-codes"></a>エラー コード

要求を正常に完了できない場合、次の HTTP エラー コードのいずれかが応答に含まれます。

| エラー コード |  説明   |
|--------|------------------|
| 404  | 申請は見つかりませんでした。 |
| 409  | このコードは、次のエラーのいずれかを示します。<br/><br/><ul><li>申請が、段階的なロールアウト操作に対して有効な状態になっていません (このメソッドを呼び出す前に、申請を公開し、[packageRolloutStatus](manage-app-submissions.md#package-rollout-object) の値を **PackageRolloutInProgress** に設定する必要があります)。</li><li>申請が、指定されたアプリに属していません。</li><li>アプリが、[Microsoft Store 申請 API で現在サポートされていない](create-and-manage-submissions-using-windows-store-services.md#not_supported)デベロッパー センター ダッシュボード機能を使用しています。</li></ul> |   


## <a name="related-topics"></a>関連トピック

* [段階的なパッケージのロールアウト](../publish/gradual-package-rollout.md)
* [Microsoft Store 申請 API を使用したアプリの申請の管理](manage-app-submissions.md)
* [Microsoft Store サービスを使用した申請の作成と管理](create-and-manage-submissions-using-windows-store-services.md)