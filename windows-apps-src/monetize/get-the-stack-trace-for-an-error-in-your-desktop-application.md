---
description: デスクトップ アプリケーションのエラーに関するスタック トレースを取得するには、Microsoft Store 分析 API の以下のメソッドを使います。
title: デスクトップ アプリケーションのエラーに関するスタック トレースの取得
ms.date: 06/05/2018
ms.topic: article
keywords: Windows 10, UWP, Store サービス, Microsoft Store 分析 API, スタック トレース, エラー, デスクトップ アプリケーション
ms.localizationpriority: medium
ms.openlocfilehash: 4aaa71c431a9dac6ad6650d05f71df897f0884fa
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372684"
---
# <a name="get-the-stack-trace-for-an-error-in-your-desktop-application"></a>デスクトップ アプリケーションのエラーに関するスタック トレースの取得

[Windows デスクトップ アプリケーション プログラム](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)に追加したデスクトップ アプリケーションのエラーに関するスタック トレースを取得するには、Microsoft Store 分析 API の以下のメソッドを使います。 このメソッドでダウンロードできるのは、過去 30 日以内に発生したエラーに関するスタック トレースのみです。 スタック トレースがでも利用できる、[正常性レポート](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)パートナー センターでのデスクトップ アプリケーションです。

このメソッドを使うには、その前にまず「[デスクトップ アプリケーションのエラーに関する詳細情報の取得](get-details-for-an-error-in-your-desktop-application.md)」のメソッドを使って、スタック トレースを取得するエラーに関連付けられた CAB ファイルの ID ハッシュを取得する必要があります。

## <a name="prerequisites"></a>前提条件


このメソッドを使うには、最初に次の作業を行う必要があります。

* Microsoft Store 分析 API に関するすべての[前提条件](access-analytics-data-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。
* スタック トレースを取得するエラーに関連付けられた CAB ファイルの ID ハッシュを取得します。 この値を取得するには、「[デスクトップ アプリケーションのエラーに関する詳細情報の取得](get-details-for-an-error-in-your-desktop-application.md)」のメソッドを使ってアプリの特定のエラーに関する詳細情報を取得し、そのメソッドの応答本文に含まれる **cabIdHash** 値を使用します。

## <a name="request"></a>要求


### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                          |
|--------|----------------------------------------------------------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/desktop/stacktrace``` |


### <a name="request-header"></a>要求ヘッダー

| Header        | 種類   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| Authorization | string | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |
 

### <a name="request-parameters"></a>要求パラメーター

| パラメーター        | 種類   |  説明      |  必須  |
|---------------|--------|---------------|------|
| applicationId | string | スタック トレースを取得するデスクトップ アプリケーションの製品 ID です。 デスクトップ アプリケーションの製品 ID を取得するには、いずれかを開く[analytics は、パートナー センターでデスクトップ アプリケーションのレポート](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)(など、**正常性レポート**) し、URL から、製品 ID を取得します。 |  〇  |
| cabIdHash | string | スタック トレースを取得するエラーに関連付けられた CAB ファイルの一意の ID ハッシュです。 この値を取得するには、「[デスクトップ アプリケーションのエラーに関する詳細情報の取得](get-details-for-an-error-in-your-desktop-application.md)」のメソッドを使ってアプリケーションの特定のエラーに関する詳細情報を取得し、そのメソッドの応答本文に含まれる **cabIdHash** 値を使用します。 |  〇  |

 
### <a name="request-example"></a>要求の例

次の例は、このメソッドを使ってスタック トレースを取得する方法を示しています。 *applicationId* パラメーターと *cabIdHash* パラメーターは、デスクトップ アプリケーションに合わせて適切な値に置き換えてください。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/desktop/stacktrace?applicationId=10238467886765136388&cabIdHash=54ffb83a-e159-41d2-8158-f36f306cc01e HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答


### <a name="response-body"></a>応答本文

| Value      | 種類    | 説明                  |
|------------|---------|--------------------------------|
| Value      | array   | 各オブジェクトにスタック トレース データの 1 つのフレームが格納されたオブジェクトの配列です。 各オブジェクトのデータについて詳しくは、次の「[スタック トレースの値](#stack-trace-values)」セクションをご覧ください。 |
| @nextLink  | string  | データの追加ページがある場合、この文字列には、データの次のページを要求するために使用できる URI が含まれます。 たとえば、要求の **top** パラメーターを 10 に設定した場合、クエリに適合するエラーが 10 行を超えると、この値が返されます。 |
| TotalCount | 整数 | クエリの結果データ内の行の総数です。          |


### <a name="stack-trace-values"></a>スタック トレースの値

*Value* 配列の要素には、次の値が含まれます。

| Value           | 種類    | 説明      |
|-----------------|---------|----------------|
| レベル (level)            | string  |  コール スタックでこの要素が表すフレーム番号です。  |
| image   | string  |   このスタック フレームで呼び出される関数が含まれている実行可能ファイルまたはライブラリ イメージの名前です。           |
| 関数 (function) | string  |  このスタック フレームで呼び出される関数の名前。 これは、アプリが実行可能ファイルまたはライブラリのシンボルを含んでいる場合のみ使用可能です。              |
| offset     | string  |  関数の先頭を基準とした現在の命令のバイト オフセットです。      |


### <a name="response-example"></a>応答の例

この要求の JSON 返信の本文の例を次に示します。

```json
{
  "Value": [
    {
      "level": "0",
      "image": "Contoso.ContosoApp",
      "function": "Contoso.ContosoApp.MainPage.DoWork",
      "offset": "0x25C"
    }
    {
      "level": "1",
      "image": "Contoso.ContosoApp",
      "function": "Contoso.ContosoApp.MainPage.Initialize",
      "offset": "0x26"
    }
    {
      "level": "2",
      "image": "Contoso.ContosoApp",
      "function": "Contoso.ContosoApp.Start",
      "offset": "0x66"
    }
  ],
  "@nextLink": null,
  "TotalCount": 3
}

```

## <a name="related-topics"></a>関連トピック

* [正常性レポート](../publish/health-report.md)
* [Microsoft Store サービスを使用して分析データにアクセス](access-analytics-data-using-windows-store-services.md)
* [エラー報告、デスクトップ アプリケーションのデータを取得します。](get-desktop-application-error-reporting-data.md)
* [お客様のデスクトップ アプリケーションでエラーの詳細を取得します。](get-details-for-an-error-in-your-desktop-application.md)
* [お客様のデスクトップ アプリケーションでエラー用の CAB ファイルをダウンロードします。](download-the-cab-file-for-an-error-in-your-desktop-application.md)
