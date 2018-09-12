---
title: POST (/titles/{titleId} クラスター/)
assetID: 0977b0b0-872d-f7ad-9ba0-30d56cff4912
permalink: en-us/docs/xboxlive/rest/uri-titlestitleidclusters-post.html
author: KevinAsgari
description: " POST (/titles/{titleId} クラスター/)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 459624ea487c158f3fc92b9c6024b086d49c204e
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882309"
---
# <a name="post-titlestitleidclusters"></a>POST (/titles/{titleId} クラスター/)
Xbox Live Compute server インスタンスを作成するクライアントをできる URI。 これらの Uri のドメインが`gameserverms.xboxlive.com`します。
 
  * [URI パラメーター](#ID4EX)
  * [必要な要求ヘッダー](#ID4EGB)
  * [Authorization](#ID4ELD)
  * [要求本文](#ID4EWD)
  * [必要な応答ヘッダー](#ID4EZE)
  * [応答本文](#ID4E5G)
 
<a id="ID4EX"></a>

 
## <a name="uri-parameters"></a>URI パラメーター
 
| パラメーター| 説明| 
| --- | --- | 
| titleId| 要求の操作をタイトルの ID です。| 
  
<a id="ID5EG"></a>

 
## <a name="host-name"></a>ホスト名

gameserverms.xboxlive.com
 
<a id="ID4EGB"></a>

 
## <a name="required-request-headers"></a>必要な要求ヘッダー
 
要求を作成する場合、次の表に示すように、ヘッダーは必要です。
 
| ヘッダー| 設定値| 説明| 
| --- | --- | --- | --- | --- | 
| ユーザー エージェント|  | 要求を行っているユーザー エージェントについて説明します。| 
| Content-Type| application/json| 提出されたデータの種類です。| 
| Host| gameserverms.xboxlive.com|  | 
| Content-Length|  | 要求のオブジェクトの長さ。| 
| x xbl コントラクト バージョン| 1| API コントラクト バージョン。| 
| Authorization| XBL3.0 x = [ハッシュ]。[トークン]| 認証トークン。| 
  
<a id="ID4ELD"></a>

 
## <a name="authorization"></a>Authorization
 
要求は、Xbox Live の有効な承認ヘッダーを含める必要があります。 呼び出し元がこのリソースへのアクセス許可されていない場合、サービスは応答で 403 Forbidden を返します。 ヘッダーが見つからないか無効な場合は、サービスは応答で 401 Unauthorized を返します。
  
<a id="ID4EWD"></a>

 
## <a name="request-body"></a>要求本文
 
要求は、次のメンバーを含む JSON オブジェクトを含める必要があります。
 
| メンバー| 説明| 
| --- | --- | --- | --- | --- | --- | --- | 
| sessionId| MPSD からセッション識別子です。| 
| abortIfQueued| 省略可能なパラメーターは、いるときにどのように指示場合、すぐにフルフィルメントしないことができますが、リソースのこのセッションをキューに入れいない GSMS を true に設定します。 応答オブジェクトは含まれている場合、この値が true であるため、要求が中止されると、<code>"fulfillmentState" : "Aborted"</code>します。 | 
 
<a id="ID4ERE"></a>

 
### <a name="sample-request"></a>要求の例
 

```cpp
{
  "sessionId" : "/serviceconfigs/00000000-0000-0000-0000-000000000000/sessiontemplates/quick/session/scott1",
  "abortIfQueued" : "true"
}

      
```

   
<a id="ID4EZE"></a>

 
## <a name="required-response-headers"></a>必要な応答ヘッダー
 
応答には常に、次の表に示すように、ヘッダーが含まれます。
 
| ヘッダー| 設定値| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| キャッシュ コントロール|  | ディレクティブ要求/応答のチェーンに沿ったのすべてのキャッシュ メカニズムによって obeyed する必要があります。| 
| Content-Type| application/json| 応答には、データの種類です。| 
| Content-Length|  | 応答本文の長さ。| 
| X コンテンツの種類オプション|  |  | 
| X XblCorrelationId|  | 応答本文の mime タイプ。| 
| Date|  |  | 
  
<a id="ID4E5G"></a>

 
## <a name="response-body"></a>応答本文
 
呼び出しが成功した場合、サービスは、次のメンバーを含む JSON オブジェクトを返します。
 
| メンバー| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| pollIntervalMilliseconds| 完了のポーリングをミリ秒の間隔をお勧めします。 ただし、これはないの推定場合、クラスターは、準備ですがのサブスクリプションと要求とフルフィルメントのレートの現在のプールを指定した状態に更新頻度、呼び出し元のポーリングを行うための推奨事項ではなく。| 
| fulfillmentState| 示します、提供されているセッションは、リソースをすぐに割り当てられたかどうか「フルフィルメント、」リソースの今後の可用性のキューに追加される「キューに入れ」、または中止され、「中止」、要求を処理することができない原因とすぐに、要求"true"と指定した abortIfQueued します。 | 
 
<a id="ID4EWH"></a>

 
### <a name="sample-response"></a>応答の例
 

```cpp
{
  "pollIntervalMilliseconds" : "1000",
  "fulfillmentState" : "Fulfilled" | "Queued" | "Aborted"
}
      
```

   
<a id="remarks"></a>

 
## <a name="remarks"></a>注釈
 
次の応答コードを受信すると、タイトルはサービスに呼び出しを再試行のみする必要があります。
 
   * 408-サーバー タイムアウト
   * 429: too Many Requests
   * 500-サーバー エラー
   * 502-無効なゲートウェイ
   * 503-Service Unavailable
   * 504-ゲートウェイ タイムアウト
   
<a id="ID4EFBAC"></a>

 
## <a name="see-also"></a>関連項目
 [/titles/{titleId} クラスター/](uri-titlestitleidclusters.md)

  