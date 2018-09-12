---
title: 取得する (/serviceconfigs//hoppers/name {/統計)
assetID: 4de5b07d-93e1-8ff0-05dd-1d3bb1802088
permalink: en-us/docs/xboxlive/rest/uri-serviceconfigsscidhoppershoppernamestatsget.html
author: KevinAsgari
description: " 取得する (/serviceconfigs//hoppers/name {/統計)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 242a3bd3a2e6112436ec3f7aa3dad60c05619314
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881480"
---
# <a name="get-serviceconfigsscidhoppersnamestats"></a>取得する (/serviceconfigs//hoppers/name {/統計)

ホッパーの統計情報を取得します。

> [!IMPORTANT]
> このメソッドは、コントラクト 103 以降で使用するものでは、X Xbl コントラクト バージョンのヘッダーの要素が必要です。 103 または後ですべての要求します。

  * [注釈](#ID4ET)
  * [URI パラメーター](#ID4E5)
  * [Authorization](#ID4EJB)
  * [HTTP ステータス コード](#ID4E3C)
  * [要求本文](#ID4EFD)
  * [応答本文](#ID4EQD)

<a id="ID4ET"></a>


## <a name="remarks"></a>注釈
この HTTP/REST メソッドは、サービス構成 ID (SCID) レベルで名前付きのホッパーからの統計情報を取得します。 **Microsoft.Xbox.Services.Matchmaking.MatchmakingService.GetHopperStatisticsAsync** API では、以下のメソッドをラップすることができます。  
<a id="ID4E5"></a>


## <a name="uri-parameters"></a>URI パラメーター

| パラメーター| 型| 説明|
| --- | --- | --- | --- |
| scid| GUID| セッションのサービス構成 id (SCID)。|
| name| string| ホッパーの名前です。|

<a id="ID4EJB"></a>


## <a name="authorization"></a>Authorization

| 型| 必須かどうか| 説明| 不足している場合、応答|
| --- | --- | --- | --- | --- | --- | --- | --- |
| XUID (ユーザーの ID)| 必須| 要求を行っているユーザーは、チケットによって参照される、チケット セッションのメンバーである必要があります。 | 403|
| 特権とデバイスの種類| 必須| ユーザーの deviceType がコンソールに設定されているとき、マッチメイ キング サービスへの呼び出しには、要求のマルチプレイヤー権限を持つユーザーのみが許可されています。 | 403|
| タイトル ID/実証購入/デバイスの種類| 必須| タイトルに一致するには、指定されたタイトルの要求、デバイスの種類の組み合わせのマッチメイ キングを許可する必要があります。 | 403|

<a id="ID4E3C"></a>


## <a name="http-status-codes"></a>HTTP ステータス コード
サービスは、MPSD に適用される、HTTP ステータス コードを返します。  
<a id="ID4EFD"></a>


## <a name="request-body"></a>要求本文

この要求の本文には、オブジェクトは送信されません。

<a id="ID4EQD"></a>


## <a name="response-body"></a>応答本文

| メンバー| 種類| 説明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 呼び出します| string| 選択したホッパーの名前です。|
| 待機時間| 32 ビットの符号付き整数| 照合時間 (秒の整数)、ホッパーの平均です。 |
| 高コスト| 32 ビットの符号付き整数| ホッパーでマッチを待っているユーザーの数。|

<a id="ID4E1D"></a>


### <a name="sample-response"></a>応答の例


```cpp
{
      "hopperName":"contosoawesome2",
      "waitTime":30,
      "population":1
    }


```


<a id="ID4EJE"></a>


## <a name="see-also"></a>関連項目

<a id="ID4ELE"></a>


##### <a name="parent"></a>Parent  

[/serviceconfigs//hoppers/name {/統計](uri-serviceconfigsscidhoppershoppernamestats.md)