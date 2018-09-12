---
title: InitialUploadRequest (JSON)
assetID: 8b8bce98-cb5f-bbaf-5564-9be2f58d749b
permalink: en-us/docs/xboxlive/rest/json-initialuploadrequest.html
author: KevinAsgari
description: " InitialUploadRequest (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: eac2405b8668179fa60921ca45012a417e61b352
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882059"
---
# <a name="initialuploadrequest-json"></a>InitialUploadRequest (JSON)
POST ゲーム クリップだったの本文は、要求をアップロードします。 
<a id="ID4EN"></a>

 
## <a name="initialuploadrequest"></a>InitialUploadRequest
 
InitialUploadRequest オブジェクトには、次の仕様があります。
 
| メンバー| 種類| 説明| 
| --- | --- | --- | 
| <b>greatestMomentId</b>| string| クリップの名前として使用するテキストの文字列 ID。 これの管理し、タイトルの開発者によって、タイトルの構成ファイルでローカライズされます。| 
| <b>userCaption</b>| string| 省略可能。 ユーザー入力の代替名最大 250 文字の最大長のゲーム クリップ。| 
| <b>sessionRef</b>| string| 省略可能。 レコーディングの実行中になるゲーム セッションの参照です。| 
| <b>dateRecorded</b>| DateTime| UTC で、レコーディングを開始した時刻。 ISO 8601 の文字列としてマーシャ リング (詳しくは、<a href="http://www.w3.org/TR/NOTE-datetime">日付と時刻の形式</a>を参照) の書式を設定します。| 
| <b>durationInSeconds</b>| 32 ビットの符号なし整数| 秒単位でのクリップの長さ。| 
| <b>expectedBlocks</b>| 32 ビットの符号なし整数| 省略可能。 ファイルを分類するブロックの数。 省略ファイルは、1 つの要求で送信されます。| 
| <b>ファイル サイズ</b>| 32 ビットの符号なし整数| ファイルのアップロードされるビデオのバイト単位のサイズ。| 
| <b>type</b>| [GameClipType 列挙](../enums/gvr-enum-gamecliptypes.md)| 列挙体はコンマ区切りの文字列値としてマーシャ リング、クリップの種類です。| 
| <b>ソース</b>| [GameClipSource 列挙](../enums/gvr-enum-gameclipsource.md)| クリップの元の指定、列挙体の文字列値としてマーシャ リングします。| 
| <b>visibility</b>| [GameClipVisibility 列挙](../enums/gvr-enum-gameclipvisibility.md)| システムが公開されると、ゲーム クリップの可視性を指定します。| 
| <b>titleData</b>| string| 省略可能。 このクリップに関連付けられているタイトルに固有のプロパティのプロパティ バッグです。 格納され、として返されるのです。 タイトル デベロッパーは、クリップに関するメタデータを保持するため、このフィールドを使用できます。| 
| <b>titleData</b>| string| 省略可能。 このクリップに関連付けられているコンソールに固有のプロパティのプロパティ バッグです。 格納され、として返されるのです。 本体のプラットフォームでは、クリップに関するメタデータを保持するため、このフィールドを使用できます。| 
| <b>systemProperties</b>| string| 省略可能。 このクリップに関連付けられているコンソールに固有のプロパティのプロパティ バッグです。 格納され、として返されます。 本体のプラットフォームでは、クリップに関するメタデータを保持するため、このフィールドを使用できます。| 
| <b>usersInSession</b>| 文字列の配列| 省略可能。 現在のセッションでユーザーの一覧です。| 
| <b>thumbnailSource</b>| [ThumbnailSource 列挙](../enums/gvr-enum-thumbnailsource.md)| 省略可能。 サムネイルのソース。| 
| <b>thumbnailOffsetMillseconds</b>| 32 ビットの符号付き整数| 生成されたオフセットのサムネイルを (ミリ秒単位) のオフセットを指定します。 <b>ThumbnailSource</b>をオフセットを設定すると指定だけです。| 
| <b>savedByUser</b>| ブール値| 省略可能。 FIFO 記憶域ではなく、ユーザーのクォータに保存するクリップを設定します。 既定値は false です。| 
  
<a id="ID4ERH"></a>

 
## <a name="sample-json-syntax"></a>JSON 構文の例
 

```json
{
   "greatestMomentId": "123abc",
   "userCaption": "OMG Look at this!",
   "sessionRef": "4587552a-a5ad-4c4c-a787-5bc5af70e4c9",
   "dateRecorded": "2012-12-23T11:08:08Z",
   "durationInSeconds": 27,
   "expectedBlocks": 7,
   "fileSize": 1234567,
   "type": "MagicMoment, Achievement",
   "source": "Console",
   "visibility": "Default",
   "titleData": "{ 'Boss': 'The Invincible' }",
   "systemProperties": "{ 'Id': '123456', 'Location': 'C:\\videos\\123456.mp4' }",
   "thumbnailSource": "Offset",
   "thumbnailOffsetMillseconds": 20000,
   "savedByUser": false
 }
    
```

  
<a id="ID4E1H"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4E3H"></a>

 
##### <a name="parent"></a>Parent 

[JavaScript オブジェクト Notation (JSON) オブジェクト リファレンス](atoc-xboxlivews-reference-json.md)

   