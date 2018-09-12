---
title: 取得する (/users/{ownerId}/概要)
assetID: 754190c9-b15d-f34b-1dca-5c92f6f67d12
permalink: en-us/docs/xboxlive/rest/uri-usersowneridsummaryget.html
author: KevinAsgari
description: " 取得する (/users/{ownerId}/概要)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 73ba0cd060b3432de1cbb641a8991283974da192
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881834"
---
# <a name="get-usersowneridsummary"></a>取得する (/users/{ownerId}/概要)
呼び出し元の観点から、所有者に関する集計データを取得します。

  * [URI パラメーター](#ID4EQ)
  * [Authorization](#ID4E2)
  * [必要な要求ヘッダー](#ID4EBC)
  * [オプションの要求ヘッダー](#ID4EHD)
  * [要求本文](#ID4EXE)
  * [HTTP ステータス コード](#ID4ECF)
  * [必要な応答ヘッダー](#ID4EZG)
  * [応答本文](#ID4EGAAC)

<a id="ID4EQ"></a>


## <a name="uri-parameters"></a>URI パラメーター

| パラメーター| 型| 説明|
| --- | --- | --- |
| ownerId| string| そのリソースにアクセスしているユーザーの識別子。 設定可能な値とは、"me"、だけ、または gt({gamertag}) です。 値の例: <code>me</code>、 <code>xuid(2603643534573581)</code>、 <code>gt(SomeGamertag)</code>|

<a id="ID4E2"></a>


## <a name="authorization"></a>Authorization

| <b>名前</b>| <b>種類</b>| <b>説明</b>|
| --- | --- | --- | --- | --- | --- |
| xuid| 64 ビットの符号なし整数| 必須。 呼び出し元のユーザーの id。 値の例: 2533274790395904|

<a id="ID4EBC"></a>


## <a name="required-request-headers"></a>必要な要求ヘッダー

| ヘッダー| 型| 説明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Authorization| string| 承認のデータです。 これは、通常、暗号化された XSTS トークンです。 値の例: <b>XBL3.0 x = [ハッシュ]、[トークン]</b>します。|

<a id="ID4EHD"></a>


## <a name="optional-request-headers"></a>オプションの要求ヘッダー

| ヘッダー| 型| 説明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| x xbl コントラクト バージョン| string| この要求を送信する必要があります、サービスの名前/数をビルドします。 要求は、ヘッダー、要求に認証トークンなどの妥当性を確認した後、そのサービスにのみルーティングされます。値の例: 1|
| Accept| string| コンテンツの種類の受け入れられる。 すべての返信はされます<code>application/json</code>します。|

<a id="ID4EXE"></a>


## <a name="request-body"></a>要求本文

この要求の本文には、オブジェクトは送信されません。

<a id="ID4ECF"></a>


## <a name="http-status-codes"></a>HTTP ステータス コード

サービスは、このリソースには、この方法で行った要求に対する応答としてでは、このセクションでステータス コードのいずれかを返します。 Xbox Live サービスで使用される標準の HTTP ステータス コードの一覧は、[標準の HTTP ステータス コード](../../additional/httpstatuscodes.md)を参照してください。

| コード| 理由フレーズ| 説明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 200| OK| セッションが正常に取得されます。|
| 400| Bad Request| ユーザー Id が正しくありませんでした。|
| 403| Forbidden| 承認ヘッダーに XUID クレームを解析できませんでした。|

<a id="ID4EZG"></a>


## <a name="required-response-headers"></a>必要な応答ヘッダー

| ヘッダー| 型| 説明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Content-Length| string| 応答に送信されるバイト数。 値の例: 232 します。|
| Content-Type| string| 応答本文の MIME タイプ。 これは、<b>アプリケーション/json</b>でなければなりません。|

<a id="ID4EGAAC"></a>


## <a name="response-body"></a>応答本文

[PersonSummary (JSON)](../../json/json-personsummary.md)を参照してください。

<a id="ID4ESAAC"></a>


### <a name="sample-response"></a>応答の例


```cpp
{
    "targetFollowingCount": 87,
    "targetFollowerCount": 19,
    "isCallerFollowingTarget": true,
    "isTargetFollowingCaller": false,
    "hasCallerMarkedTargetAsFavorite": true,
    "hasCallerMarkedTargetAsKnown": true,
    "legacyFriendStatus": "None",
    "recentChangeCount": 5,
    "watermark": "5246775845000319351"
}

```


<a id="ID4E3AAC"></a>


## <a name="see-also"></a>関連項目

<a id="ID4E5AAC"></a>


##### <a name="parent"></a>Parent

[/users/{ownerId}/概要](uri-usersowneridsummary.md)