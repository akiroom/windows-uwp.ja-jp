---
ms.assetid: 252C44DF-A2B8-4F4F-9D47-33E423F48584
description: 日付範囲やその他のオプション フィルターを指定して集計エラー報告データを取得するには、Microsoft Store 分析 API の以下のメソッドを使います。
title: アプリのエラー報告データの取得
ms.date: 09/04/2018
ms.topic: article
keywords: Windows 10, UWP, Store サービス, Microsoft Store 分析 API, エラー
ms.localizationpriority: medium
ms.openlocfilehash: 69504fd8d670158a35e5afd5dcd035acd296f084
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57590597"
---
# <a name="get-error-reporting-data-for-your-app"></a>アプリのエラー報告データの取得

日付範囲やその他のオプション フィルターを指定して、アプリの集計エラー報告データを JSON 形式で取得するには、Microsoft Store 分析 API の以下のメソッドを使います。 このメソッドは、過去 30 日以内に発生したエラーのみを取得できます。 この情報も記載されて、**エラー**のセクション、[正常性レポート](../publish/health-report.md)パートナー センターでします。

[エラーの詳細を取得する](get-details-for-an-error-in-your-app.md)、[スタック トレースを取得する](get-the-stack-trace-for-an-error-in-your-app.md)、および [CAB ファイルをダウンロードする](download-the-cab-file-for-an-error-in-your-app.md)メソッドを利用すれば、追加のエラー情報を取得することもできます。

## <a name="prerequisites"></a>前提条件


このメソッドを使うには、最初に次の作業を行う必要があります。

* Microsoft Store 分析 API に関するすべての[前提条件](access-analytics-data-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。

## <a name="request"></a>要求


### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                          |
|--------|----------------------------------------------------------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/failurehits``` |


### <a name="request-header"></a>要求ヘッダー

| Header        | 種類   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| Authorization | string | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |


### <a name="request-parameters"></a>要求パラメーター

| パラメーター        | 種類   |  説明      |  必須  
|---------------|--------|---------------|------|
| applicationId | string | エラー報告データを取得するアプリのストア ID です。 Store ID は、[アプリ id のページ](../publish/view-app-identity-details.md)パートナー センターでします。 ストア ID は、たとえば 9WZDNCRFJ3Q8 のような文字列です。 |  〇  |
| startDate | date | 取得するエラー報告データの日付範囲の開始日です。 既定値は現在の日付です。 *aggregationLevel* が **day**、**week**、または **month** の場合、このパラメーターには日付を ```mm/dd/yyyy``` の形式で指定する必要があります。 *aggregationLevel* が **hour** の場合、このパラメーターには日付を ```mm/dd/yyyy``` の形式で指定するか、日付と時刻を ```yyyy-mm-dd hh:mm:ss``` の形式で指定できます。<p/><p/>**注:**&nbsp;&nbsp;このメソッドは過去 30 日以内に発生したエラーのみを取得できます。  |  いいえ  |
| endDate | date | 取得するエラー報告データの日付範囲の終了日です。 既定値は現在の日付です。 *aggregationLevel* が **day**、**week**、または **month** の場合、このパラメーターには日付を ```mm/dd/yyyy``` の形式で指定する必要があります。 *aggregationLevel* が **hour** の場合、このパラメーターには日付を ```mm/dd/yyyy``` の形式で指定するか、日付と時刻を ```yyyy-mm-dd hh:mm:ss``` の形式で指定できます。 |  X  |
| top | int | 要求で返すデータの行数です。 最大値および指定しない場合の既定値は 10000 です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。 |  X  |
| skip | int | クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、top=10000 と skip=0 を指定すると、データの最初の 10,000 行が取得され、top=10000 と skip=10000 を指定すると、データの次の 10,000 行が取得されます。 |  X  |
| filter |string  | 応答内の行をフィルター処理する 1 つまたは複数のステートメントです。 各ステートメントには、応答本文からのフィールド名、および **eq** 演算子または **ne** 演算子と関連付けられる値が含まれており、**and** や **or** を使用してステートメントを組み合わせることができます。 *filter* パラメーターでは、文字列値を単一引用符で囲む必要があります。 応答本文から次のフィールドを指定することができます。<p/><ul><li>**ApplicationName**</li><li>**failureName**</li><li>**failureHash**</li><li>**symbol**</li><li>**osVersion**</li><li>**osRelease**</li><li>**eventType**</li><li>**market**</li><li>**deviceType**</li><li>**パッケージ名**</li><li>**packageVersion**</li><li>**date**</li></ul> | X   |
| aggregationLevel | string | 集計データを取得する時間範囲を指定します。 **hour**、**day**、**week**、**month** のいずれかの文字列を指定できます。 指定しない場合、既定値は **day** です。 **week** または **month** を指定した場合、*failureName* と *failureHash* の値は 1,000 バケットに制限されます。<p/><p/>**注:**&nbsp;&nbsp;**hour** を指定した場合は、過去 72 時間以内のエラー データしか取得できません。 72 時間よりも前のエラー データを取得するには、**day** または他のいずれかの集計レベルを指定してください。  | X |
| orderby | string | 結果データ値の順序を指定するステートメントです。 構文は *orderby=field [order],field [order],...* です。*field* パラメーターには、次のいずれかの文字列を指定できます。<ul><li>**ApplicationName**</li><li>**failureName**</li><li>**failureHash**</li><li>**symbol**</li><li>**osVersion**</li><li>**osRelease**</li><li>**eventType**</li><li>**market**</li><li>**deviceType**</li><li>**パッケージ名**</li><li>**packageVersion**</li><li>**date**</li></ul><p>*order* パラメーターは省略可能であり、**asc** または **desc** を指定して、各フィールドを昇順または降順にすることができます。 既定値は **asc** です。</p><p>*orderby* 文字列の例: *orderby=date,market*</p> |  X  |
| groupby | string | 指定したフィールドのみにデータ集計を適用するステートメントです。 次のフィールドを指定できます。<ul><li>**failureName**</li><li>**failureHash**</li><li>**symbol**</li><li>**osVersion**</li><li>**eventType**</li><li>**market**</li><li>**deviceType**</li><li>**パッケージ名**</li><li>**packageVersion**</li></ul><p>返されるデータ行には、*groupby* パラメーターに指定したフィールドと次の値が含まれます。</p><ul><li>**date**</li><li>**applicationId**</li><li>**ApplicationName**</li><li>**deviceCount**</li><li>**eventCount**</li></ul><p>*groupby* パラメーターは、*aggregationLevel* パラメーターと同時に使用できます。 例: *&amp;groupby=failureName,market&amp;aggregationLevel=week*</p></p> |  X  |


### <a name="request-example"></a>要求の例

エラー報告データを取得するためのいくつかの要求の例を次に示します。 *applicationId* 値を、目的のアプリのストア ID に置き換えてください。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/failurehits?applicationId=9NBLGGGZ5QDR&startDate=1/1/2015&endDate=2/1/2015&top=10&skip=0 HTTP/1.1
Authorization: Bearer <your access token>

GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/failurehits?applicationId=9NBLGGGZ5QDR&startDate=8/1/2015&endDate=8/31/2015&skip=0&filter=market eq 'US' and deviceType eq 'phone' HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答


### <a name="response-body"></a>応答本文

| Value      | 種類    | 説明     |
|------------|---------|--------------|
| Value      | array   | 集計エラー報告データが含まれるオブジェクトの配列です。 各オブジェクトのデータについて詳しくは、次の「[エラー値](#error-values)」セクションをご覧ください。     |
| @nextLink  | string  | データの追加ページがある場合、この文字列には、データの次のページを要求するために使用できる URI が含まれます。 たとえば、要求の **top** パラメーターが 10000 に設定されたが、クエリの入手データに 10,000 を超えるエラー行が含まれている場合に、この値が返されます。 |
| TotalCount | 整数 | クエリの結果データ内の行の総数です。     |


### <a name="error-values"></a>エラー値

*Value* 配列の要素には、次の値が含まれます。

| Value           | 種類    | 説明        |
|-----------------|---------|---------------------|
| date            | string  | エラー データの日付範囲の最初の日付を ```yyyy-mm-dd``` の形式で示します。 要求に単一の日付を指定した場合、この値はその日付になります。 要求に日付範囲を指定した場合、この値はその日付範囲の最初の日付になります。 *aggregationLevel* 値に **hour** が指定されている要求の場合、この値には ```hh:mm:ss``` 形式の時刻値も含まれます。  |
| applicationId   | string  | エラー データを取得するアプリのストア ID です。   |
| applicationName | string  | アプリの表示名です。   |
| failureName     | string  | 4 つの部分から成るエラーの名前です。問題が発生した 1 つ以上のクラス、例外/バグ チェック コード、障害が発生したイメージの名前、関連する関数の名前で構成されます。  |
| failureHash     | string  | エラーの一意の識別子です。   |
| symbol          | string  | このエラーに割り当てられた記号です。 |
| osVersion       | string  | エラーが発生した OS のバージョンを指定する、以下のいずれかの文字列です。<ul><li>**Windows Phone 7.5**</li><li>**Windows Phone 8**</li><li>**Windows Phone 8.1**</li><li>**Windows Phone 10**</li><li>**Windows 8**</li><li>**Windows 8.1**</li><li>**Windows 10**</li><li>**Unknown**</li></ul>  |
| osRelease       | string  |  エラーが発生した OS リリースまたはフライティング リングを (OS バージョン内のサブグループとして) 指定する、以下のいずれかの文字列です。<p/><p>Windows 10 の場合:</p><ul><li><strong>バージョン 1507</strong></li><li><strong>バージョン 1511</strong></li><li><strong>バージョン 1607</strong></li><li><strong>バージョン 1703</strong></li><li><strong>バージョン 1709</strong></li><li><strong>バージョン 1803</strong></li><li><strong>Release Preview</strong></li><li><strong>Insider Fast</strong></li><li><strong>低速 insider</strong></li></ul><p/><p>Windows Server 1709 の場合:</p><ul><li><strong>RTM</strong></li></ul><p>Windows Server 2016 の場合:</p><ul><li><strong>バージョン 1607</strong></li></ul><p>Windows 8.1 の場合:</p><ul><li><strong>更新プログラム 1</strong></li></ul><p>Windows 7 の場合:</p><ul><li><strong>Service Pack 1</strong></li></ul><p>OS リリースまたはフライティング リングが不明な場合、このフィールドは値 <strong>Unknown</strong> になります。</p>    |
| eventType       | string  | 次のいずれかの文字列です。<ul><li>**クラッシュ**</li><li>**ハング**</li><li>**メモリ**</li><li>**jse**</li></ul>      |
| market          | string  | デバイス市場の ISO 3166 国コードです。   |
| deviceType      | string  | エラーが発生したデバイスの種類を示す、以下のいずれかの文字列です。<ul><li>**PC**</li><li>**Phone**</li><li>**Console**</li><li>**IoT**</li><li>**Holographic**</li><li>**Unknown**</li></ul>    |
| packageName     | string  | このエラーに関連付けられているアプリ パッケージの一意の名前です。      |
| packageVersion  | string  | このエラーに関連付けられているアプリ パッケージのバージョンです。   |
| deviceCount     | number | 指定した集計レベルでこのエラーに対応する一意のデバイスの数です。  |
| eventCount      | number | 指定した集計レベルでこのエラーに起因すると考えられるイベントの数です。      |


### <a name="response-example"></a>応答の例

この要求の JSON 返信の本文の例を次に示します。

```json
{
  "Value": [
    {
      "date": "2017-03-09",
      "applicationId": "9NBLGGGZ5QDR",
      "applicationName": "Contoso Demo",
      "failureName": "APPLICATION_FAULT_8013150a_StoreWrapper.ni.DLL!70475e55",
      "failureHash": "5a6b2170-1661-ed47-24d7-230fed0077af",
      "symbol": "storewrapper_ni!70475e55",
      "osVersion": "Windows 10",
      "osRelease": "Version 1507",
      "eventType": "crash",
      "market": "US",
      "deviceType": "PC",
      "packageName": "",
      "packageVersion": "0.0.0.0",
      "deviceCount": 0.0,
      "eventCount": 1.0
    }
  ],
  "@nextLink": "failurehits?applicationId=9NBLGGGZ5QDR&aggregationLevel=week&startDate=2017/03/01&endDate=2016/02/01&top=1&skip=1",
  "TotalCount": 21
}

```

## <a name="related-topics"></a>関連トピック

* [正常性レポート](../publish/health-report.md)
* [アプリでエラーの詳細を取得します。](get-details-for-an-error-in-your-app.md)
* [アプリでエラーのスタック トレースを取得します。](get-the-stack-trace-for-an-error-in-your-app.md)
* [アプリでエラー用の CAB ファイルをダウンロードします。](download-the-cab-file-for-an-error-in-your-app.md)
* [Microsoft Store サービスを使用して分析データにアクセス](access-analytics-data-using-windows-store-services.md)
* [アプリの取得数を取得します。](get-app-acquisitions.md)
* [アドオンの取得数を取得します。](get-in-app-acquisitions.md)
* [アプリのレーティングを取得します。](get-app-ratings.md)
* [アプリのレビューを取得します。](get-app-reviews.md)
