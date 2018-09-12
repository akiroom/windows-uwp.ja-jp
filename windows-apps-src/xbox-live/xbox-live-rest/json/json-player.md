---
title: プレイヤー (JSON)
assetID: eaf6d082-869b-d2d3-d548-5cef65e54541
permalink: en-us/docs/xboxlive/rest/json-player.html
author: KevinAsgari
description: " プレイヤー (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 25d9262ac16eab3d1c2f35960445321fa3872c30
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882134"
---
# <a name="player-json"></a>プレイヤー (JSON)
ゲーム セッションにプレイヤーのデータが含まれています。 
<a id="ID4EN"></a>

 
## <a name="player"></a>プレイヤー
 
プレイヤー オブジェクトでは、次の仕様があります。
 
| メンバー| 種類| 説明| 
| --- | --- | --- | 
| customData| 8 ビットの符号なし整数の配列| Base64 1024 バイトは、ゲーム固有のプレイヤーのデータをエンコードします。 この値は、サーバーに不透明です。| 
| ゲーマータグ| string| ゲーマータグ-は最大 15 文字、プレイヤーのします。 クライアントは、プレイヤーを識別するため、UI でこの値を使用する必要があります。 | 
| isCurrentlyInSession| ブール値| プレイヤーは、セッション内で現在またはセッションを示します。| 
| seatIndex| 32 ビットの符号付き整数| セッションにプレイヤーのインデックス。| 
| xuid| 64 ビットの符号なし整数| Xbox ユーザー ID (XUID)、プレイヤーのします。| 
  
<a id="ID4E3C"></a>

 
## <a name="sample-json-syntax"></a>JSON 構文の例
 

```json
{
    "xuid": 2533274790412952,
    "gamertag":"MyTestUser",
    "seatindex": 3
    "customData":"AIHJ2?iE?/jiKE!l5S=T..."
    "isCurrentlyInSession":"true"
}
    
```

  
<a id="ID4EFD"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4EHD"></a>

 
##### <a name="parent"></a>Parent 

[JavaScript オブジェクト Notation (JSON) オブジェクト リファレンス](atoc-xboxlivews-reference-json.md)

  
<a id="ID4ERD"></a>

 
##### <a name="reference"></a>リファレンス 

[GameSession (JSON)](json-gamesession.md)

   