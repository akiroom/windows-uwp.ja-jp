---
title: 配置 (/{uri})
assetID: 24a24c93-f43b-017e-91e0-29e190fec8a8
permalink: en-us/docs/xboxlive/rest/uri-uriput.html
author: KevinAsgari
description: " 配置 (/{uri})"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 61eecfbc6d5ebeda4825b8a3d29e90347b9988af
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882374"
---
# <a name="put-uri"></a>配置 (/{uri})
ゲーム クリップのデータをアップロードします。
これらの Uri のドメイン`gameclipsmetadata.xboxlive.com`と`gameclipstransfer.xboxlive.com`対象の URI の機能に応じて、します。

  * [注釈](#ID4EX)
  * [URI パラメーター](#ID4EQB)
  * [クエリ文字列パラメーター](#ID4ERC)
  * [必要な要求ヘッダー](#ID4EBE)
  * [オプションの要求ヘッダー](#ID4ENG)
  * [要求本文](#ID4EWH)
  * [HTTP ステータス コード](#ID4ECAAC)
  * [必要な応答ヘッダー](#ID4EYEAC)
  * [省略可能な応答ヘッダー](#ID4ELHAC)
  * [応答本文](#ID4ELIAC)

<a id="ID4EX"></a>


## <a name="remarks"></a>注釈

**InitialUploadResponse**が返された後は、そのオブジェクトで返される**uploadUri**を通じて、アップロードが実行されます。 クライアントする必要があります、ファイルに分割**expectedBlocks**連番のブロックで各 2 MB を超える。 これらは、並列にアップロードできます。

ブロック内のファイルをアップロードする場合、サーバー (202) を承諾済みの各要求の HTTP ステータス コードが返されます、Created (201) を返す、1 つのファイルとすべてのブロックをコミットを受け取るまで、予期されるすべてのブロックの場合はします。 このような場合は、応答には、オブジェクトが含まれていないと、サーバーは、追加の処理をスケジュール可能性があります。 エラーが発生した**ServiceErrorResponse**オブジェクトを適切な HTTP ステータス コードと共に返される可能性があります。

、回復不可能なエラー コード バックオフ再試行の標準的なメカニズムを使用して、クライアントを再試行する必要があります。

> [!NOTE] 
> 場合でも、アップロードが正常に完了すると、それ以降の処理が発生する可能性があります上の理由から、クリップがアップロードまたはメタデータに関連しない拒否を進めますプロセスします。


<a id="ID4EQB"></a>


## <a name="uri-parameters"></a>URI パラメーター

| パラメーター| 型| 説明|
| --- | --- | --- | --- |
| <b>uri</b>| string| <b>InitialUploadResponse</b>オブジェクト内で<b>uploadUri</b>フィールド。|

<a id="ID4ERC"></a>


## <a name="query-string-parameters"></a>クエリ文字列パラメーター

| パラメーター| 型| 説明|
| --- | --- | --- | --- | --- | --- | --- |
| <b>blockNum</b>| 32 ビットの符号なし整数| <b>ExpectedBlocks</b>が設定されているかどうかに必要です。 ファイルのブロックの順序を決定するインデックス 0 で始まるブロックの数です。 たとえば、 <b>expectedBlocks</b>が 7 の場合は、し<b>blockNum</b>は、0 から 6 にします。 |
| <b>uploadId</b>| string| 必須。 <b>GameClipsServiceUploadResponse</b>オブジェクトの不透明な ID です。|

<a id="ID4EBE"></a>


## <a name="required-request-headers"></a>必要な要求ヘッダー

| ヘッダー| 型| 説明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Authorization| string| HTTP の認証の資格情報を認証します。 値の例: <b>Xauth =&lt;authtoken ></b>|
| X RequestedServiceVersion| string| この要求を送信する必要があります、Xbox LIVE サービスの名前/数をビルドします。 要求は、ヘッダー、要求に認証トークンなどの妥当性を確認した後、そのサービスにのみルーティングされます。例: 1、vnext します。|
| Content-Type| string| 応答本文の MIME タイプ。 例:<b>アプリケーション/json</b>します。|
| Accept| string| コンテンツの種類の利用可能な値です。 例:<b>アプリケーション/json</b>します。|
| キャッシュ コントロール| string| キャッシュ動作を指定するていねい要求します。|

<a id="ID4ENG"></a>


## <a name="optional-request-headers"></a>オプションの要求ヘッダー

| ヘッダー| 型| 説明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Accept-Encoding| string| 受け入れ可能な圧縮エンコードします。 値の例: gzip、圧縮の id。|
| ETag| string| キャッシュの最適化のために使用します。 値の例:"686897696a7c876b7e"。|

<a id="ID4EWH"></a>


## <a name="request-body"></a>要求本文

この要求の本文には、オブジェクトは送信されません。

<a id="ID4ECAAC"></a>


## <a name="http-status-codes"></a>HTTP ステータス コード

サービスは、このリソースには、この方法で行った要求に対する応答としてでは、このセクションでステータス コードのいずれかを返します。 Xbox Live サービスで使用される標準の HTTP ステータス コードの一覧は、[標準の HTTP ステータス コード](../../additional/httpstatuscodes.md)を参照してください。

| コード| 理由フレーズ| 説明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 200| OK| セッションが正常に取得されます。|
| 301| 完全に移動| サービスについては、さまざまな URI に移動します。|
| 307| 一時的なリダイレクト| サービスについては、さまざまな URI に移動します。|
| 400| Bad Request| サービスは、形式が正しくない要求を理解していない可能性があります。 通常、無効なパラメーターです。|
| 401| 権限がありません| 要求には、ユーザー認証が必要です。|
| 403| Forbidden| 要求は、ユーザーまたはサービスは許可されません。|
| 404| Not Found します。| 指定されたリソースは見つかりませんでした。|
| 406| 許容できません。| リソースのバージョンがサポートされていません。|
| 408| 要求のタイムアウト| 要求にかかった時間が長すぎます。|
| 410| 無効| 要求されたリソースが利用可能ではなくなりました。|

<a id="ID4EYEAC"></a>


## <a name="required-response-headers"></a>必要な応答ヘッダー

| ヘッダー| 型| 説明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| X RequestedServiceVersion| string| この要求を送信する必要があります、Xbox LIVE サービスの名前/数をビルドします。 要求は、ヘッダー、要求に認証トークンなどの妥当性を確認した後、そのサービスにのみルーティングされます。例: 1、vnext します。|
| Content-Type| string| 応答本文の MIME タイプ。 例:<b>アプリケーション/json</b>します。|
| キャッシュ コントロール| string| キャッシュ動作を指定するていねい要求します。|
| Accept| string| コンテンツの種類の利用可能な値です。 例:<b>アプリケーション/json</b>します。|
| Retry-after| string| クライアントが利用できないサーバーの場合、後で再試行するように指示します。|
| 異なる| string| 下位のプロキシの応答をキャッシュする方法を指示します。|

<a id="ID4ELHAC"></a>


## <a name="optional-response-headers"></a>省略可能な応答ヘッダー

| ヘッダー| 型| 説明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Etag| string| キャッシュの最適化のために使用します。 例:"686897696a7c876b7e"。|

<a id="ID4ELIAC"></a>


## <a name="response-body"></a>応答本文

応答の本文には、オブジェクトは送信されません。

<a id="ID4EWIAC"></a>


## <a name="see-also"></a>関連項目

<a id="ID4EYIAC"></a>


##### <a name="parent"></a>Parent

[/{uri}](uri-uri.md)