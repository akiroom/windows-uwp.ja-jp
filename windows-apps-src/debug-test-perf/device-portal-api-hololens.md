---
ms.assetid: 41ac0142-4d86-4bb3-b580-36d0d6956091
title: HoloLens 用 Device Portal API リファレンス
description: HoloLens 用の Windows Device Portal REST API について説明します。これらの API を使うと、プログラムからデータにアクセスしてデバイスを制御できます。
ms.date: 03/22/2018
ms.topic: article
keywords: windows 10, uwp, デバイス ポータル
ms.localizationpriority: medium
ms.openlocfilehash: 3aeb068908adf6d6c40a50cee3aececba1861ee8
ms.sourcegitcommit: 76e8b4fb3f76cc162aab80982a441bfc18507fb4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "63801383"
---
# <a name="device-portal-api-reference-for-hololens"></a>HoloLens 用 Device Portal API リファレンス

Windows Device Portal の機能はすべて、REST API の上に構築されています。REST API は、プログラムからデータにアクセスしてデバイスを制御するために使用できます。

## <a name="holographic-os"></a>ホログラフィック OS

### <a name="get-https-requirements-for-the-device-portal"></a>Device Portal の HTTPS 要件を取得する

**要求**

次の要求型式を使用して、Device Portal の HTTPS 要件を取得できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/os/webmanagement/settings/https |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="get-the-stored-interpupillary-distance-ipd"></a>保存されている瞳孔間距離 (IPD) を取得する

**要求**

次の要求型式を使用して、保存されている IPD の値を取得できます。 値はミリメートル単位で返されます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/os/settings/ipd |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="get-a-list-of-hololens-specific-etw-providers"></a>HoloLens 固有の ETW プロバイダーの一覧を取得する

**要求**

次の要求型式を使用して、システムには登録されていない HoloLens 固有の ETW プロバイダーの一覧を取得できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/os/etw/customproviders |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。


### <a name="return-the-state-for-all-active-services"></a>アクティブなすべてのサービスの状態を返す

**要求**

次の要求形式を使用して、現在実行されているすべてのサービスの状態を取得できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/os/services |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。


### <a name="set-the-https-requirement-for-the-device-portal"></a>Device Portal の HTTPS 要件を設定する

**要求**

次の要求形式を使用して、Device Portal の HTTPS 要件を設定できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/management/settings/https |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| 必須   | (**必須**) Device Portal で HTTPS を必要とするかどうかを決定します。 指定できる値は、**yes**、**no**、**default** です。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。


### <a name="set-the-interpupillary-distance-ipd"></a>瞳孔間距離 (IPD) を設定する

**要求**

次の要求形式を使用して、保存されている IPD を設定できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/os/settings/ipd |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| ipd   | (**必須**) 保存する新しい IPD 値。 この値はミリメートル単位で指定します。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。


## <a name="holographic-perception"></a>ホログラフィックの認識

### <a name="accept-websocket-upgrades-and-run-a-mirage-client-that-sends-updates"></a>WebSocket のアップグレードを受け入れ、ミラージュ クライアントを実行する

**要求**

次の要求型式を使用して、WebSocket のアップグレードを受け入れ、30fps で更新を送信するミラージュ クライアントを実行できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET/WebSocket | /api/holographic/perception/client |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| clientmode   | (**必須**) 追跡モードを決定します。 値を **active** に設定すると、パッシブに確立できない場合は視覚追跡モードが強制されます。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。


## <a name="holographic-thermal"></a>ホログラフィックの温度

### <a name="get-the-thermal-stage-of-the-device"></a>デバイスの温度ステージを取得する

**要求**

次の要求形式を使用して、デバイスの温度ステージを取得できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/ |

**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

返される可能性のある値を次の表に示します。

| Value | 説明 |
| --- | --- |
| 1 | Normal |
| 2 で保護されたプロセスとして起動されました | 中 |
| 3 で保護されたプロセスとして起動されました | ［重大］ |

**状態コード**

- 標準の状態コード。

## <a name="hsimulation-control"></a>HSimulation の制御
### <a name="create-a-control-stream-or-post-data-to-a-created-stream"></a>制御ストリームを作成する、または作成されたストリームにデータをポストする

**要求**

次の要求形式を使用して、制御ストリームを作成したり、作成されたストリームにデータをポストしたりできます。 ポストされるデータの種類は **application/octet-stream** と想定されます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/simulation/control/stream |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| priority   | (**制御ストリームを作成する場合は必須**) ストリームの優先度を示します。 |
| streamid   | (**作成されたストリームにポストする場合は必須**) ポスト先のストリームの識別子。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="delete-a-control-stream"></a>制御ストリームを削除する

**要求**

次の要求形式を使用して、制御ストリームを削除できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| DELETE | /api/holographic/simulation/control/stream |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="get-a-control-stream"></a>制御ストリームを取得する

**要求**

次の要求形式を使用して、制御ストリームの Web ソケット接続を開くことができます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET/WebSocket | /api/holographic/simulation/control/stream |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="get-the-simulation-mode"></a>シミュレーション モードを取得する

**要求**

次の要求形式を使用して、シミュレーション モードを取得できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/simulation/control/mode |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="set-the-simulation-mode"></a>シミュレーション モードを設定する

**要求**

次の要求型式を使用して、シミュレーション モードを設定できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/simluation/control/mode |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| mode   | (**必須**) シミュレーション モードを示します。 指定できる値は、**default**、**simulation**、**remote**、**legacy** です。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

## <a name="hsimulation-playback"></a>HSimulation の再生

### <a name="delete-a-recording"></a>レコーディングを削除する

**要求**

次の要求型式を使用して、レコーディングを削除できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| DELETE | /api/holographic/simulation/playback/file |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| recording   | (**必須**) 削除するレコーディングの名前。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="get-all-recordings"></a>すべてのレコーディングを取得する

**要求**

次の要求形式を使用して、利用可能なすべてのレコーディングを取得できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/simulation/playback/files |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="get-the-types-of-data-in-a-loaded-recording"></a>読み込まれたレコーディング内のデータの種類を取得する

**要求**

次の要求形式を使用して、読み込まれたレコーディング内のデータの種類を取得できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/simulation/playback/session/types |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| recording   | (**必須**) 対象とするレコーディングの名前。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="get-all-the-loaded-recordings"></a>読み込まれたすべてのレコーディングを取得する

**要求**

次の要求形式を使用して、読み込まれたすべてのレコーディングを取得できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/simulation/playback/session/files |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="get-the-current-playback-state-of-a-recording"></a>レコーディングの現在の再生状態を取得する 

**要求**

次の要求形式を使用して、レコーディングの現在の再生状態を取得できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/simulation/playback/session |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| recording   | (**必須**) 対象とするレコーディングの名前。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="load-a-recording"></a>レコーディングを読み込む

**要求**

次の要求形式を使用して、レコーディングを読み込むことができます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/simulation/playback/session/file |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| recording   | (**必須**) 読み込むレコーディングの名前。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="pause-a-recording"></a>レコーディングを一時停止する

**要求**

次の要求形式を使用して、レコーディングを一時停止できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/simulation/playback/session/pause |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| recording   | (**必須**) 一時停止するレコーディングの名前。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="play-a-recording"></a>レコーディングを再生する

**要求**

次の要求形式を使用して、レコーディングを再生できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/simulation/playback/session/play |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| recording   | (**必須**) 再生するレコーディングの名前。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="stop-a-recording"></a>レコーディングを停止する

**要求**

次の要求形式を使用して、レコーディングを停止できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/simulation/playback/session/stop |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| recording   | (**必須**) 停止するレコーディングの名前。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="unload-a-recording"></a>レコーディングをアンロードする

**要求**

次の要求形式を使用して、レコーディングをダウンロードできます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| DELETE | /api/holographic/simulation/playback/session/file |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| recording   | (**必須**) アンロードするレコーディングの名前。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="upload-a-recording"></a>レコーディングをアップロードする

**要求**

次の要求形式を使用して、レコーディングをアップロードできます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/simulation/playback/file |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

## <a name="hsimulation-recording"></a>HSimulation のレコーディング

### <a name="get-the-recording-state"></a>レコーディングの状態を取得する

**要求**

次の要求形式を使用して、現在のレコーディングの状態を取得できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/simulation/recording/status |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="start-a-recording"></a>レコーディングを開始する

**要求**

次の要求形式を使用して、レコーディングを開始できます。 アクティブにできるレコーディングは一度に 1 つだけです。 
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/simulation/recording/start |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| head   | (**下記参照**) システムで頭部のデータを記録する必要があることを示すには、この値を 1 に設定します。 |
| hands   | (**下記参照**) システムで手のデータを記録する必要があることを示すには、この値を 1 に設定します。 |
| spatialMapping   | (**下記参照**) システムで空間マッピング データを記録する必要があることを示すには、この値を 1 に設定します。 |
| environment   | (**下記参照**) システムで環境データを記録する必要があることを示すには、この値を 1 に設定します。 |
| name   | (**必須**) レコーディングの名前。 |
| singleSpatialMappingFrame   | (**省略可能**) 単一の空間マッピング フレームのみを記録する必要があることを示すには、この値を 1 に設定します。 |

これらのパラメーターについては、*head*、*hands*、*spatialMapping*、*environment* のいずれか 1 つだけを 1 に設定する必要があります。

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="stop-the-current-recording"></a>現在のレコーディングを停止する

**要求**

次の要求形式を使用して、現在のレコーディングを停止できます。 レコーディングはファイルとして返されます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/simulation/recording/stop |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

## <a name="mixed-reality-capture"></a>複合現実キャプチャ

### <a name="delete-a-mixed-reality-capture-mrc-recording-from-the-device"></a>デバイスから Mixed Reality キャプチャ (MRC) レコーディングを削除する

**要求**

次の要求形式を使用して、MRC レコーディングを削除できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
DELETE | /api/holographic/mrc/file |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| &lt;ファイル名&gt;   | (**必須**) 削除するビデオ ファイルの名前。 この名前は hex64 エンコードされている必要があります。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="download-a-mixed-reality-capture-mrc-file"></a>Mixed Reality キャプチャ (MRC) ファイルをダウンロードする

**要求**

次の要求形式を使用して、デバイスから MRC ファイルをダウンロードできます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/mrc/file |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| &lt;ファイル名&gt;   | (**必須**) 取得するビデオ ファイルの名前。 この名前は hex64 エンコードされている必要があります。 |
| op   | (**省略可能**) ストリームをダウンロードする場合は、この値を **stream** に設定します。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="get-the-mixed-reality-capture-mrc-settings"></a>Mixed Reality キャプチャ (MRC) の設定を取得する

**要求**

次の要求形式を使用して、MRC の設定を取得できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/mrc/settings |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="get-the-status-of-the-mixed-reality-capture-mrc-recording"></a>Mixed Reality キャプチャ (MRC) レコーディングの状態を取得する

**要求**

次の要求形式を使用して、MRC レコーディングの状態を取得できます。 返される可能性のある値は、**running** と **stopped** です。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/mrc/status |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="get-the-list-of-mixed-reality-capture-mrc-files"></a>Mixed Reality キャプチャ (MRC) ファイルのリストを取得する

**要求**

次の要求形式を使用して、デバイスに保存されている MRC ファイルを取得できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/mrc/files |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="set-the-mixed-reality-capture-mrc-settings"></a>Mixed Reality キャプチャ (MRC) の設定を行う

**要求**

次の要求形式を使用して、MRC の設定を行うことができます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/mrc/settings |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="starts-a-mixed-reality-capture-mrc-recording"></a>Mixed Reality キャプチャ (MRC) レコーディングを開始する

**要求**

次の要求形式を使用して、MRC レコーディングを開始できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/mrc/video/control/start |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="stop-the-current-mixed-reality-capture-mrc-recording"></a>現在の Mixed Reality キャプチャ (MRC) レコーディングを停止する

**要求**

次の要求形式を使用して、現在の MRC レコーディングを停止できます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| POST | /api/holographic/mrc/video/control/stop |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="take-a-mixed-reality-capture-mrc-photo"></a>Mixed Reality キャプチャ (MRC) の写真を撮る

**要求**

次の要求形式を使用して、MRC の写真を撮ることができます。 写真は JPEG 形式で返されます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/mrc/photo |


**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

## <a name="mixed-reality-streaming"></a>複合現実のストリーミング

### <a name="initiates-a-chunked-download-of-a-fragmented-mp4"></a>フラグメント化 mp4 のチャンク ダウンロードを開始する

**要求**

次の要求型式を使用して、フラグメント化 mp4 のチャンク ダウンロードを開始できます。 この API では既定の品質が使われます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/stream/live.mp4 |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| pv   | (**省略可能**) PV カメラをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |
| holo   | (**省略可能**) ホログラムをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |
| mic   | (**省略可能**) マイクをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |
| loopback   | (**省略可能**) アプリケーション オーディオをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="initiates-a-chunked-download-of-a-fragmented-mp4"></a>フラグメント化 mp4 のチャンク ダウンロードを開始する

**要求**

次の要求型式を使用して、フラグメント化 mp4 のチャンク ダウンロードを開始できます。 この API では高品質が使われます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/stream/live_high.mp4 |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| pv   | (**省略可能**) PV カメラをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |
| holo   | (**省略可能**) ホログラムをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |
| mic   | (**省略可能**) マイクをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |
| loopback   | (**省略可能**) アプリケーション オーディオをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="initiates-a-chunked-download-of-a-fragmented-mp4"></a>フラグメント化 mp4 のチャンク ダウンロードを開始する

**要求**

次の要求型式を使用して、フラグメント化 mp4 のチャンク ダウンロードを開始できます。 この API では低品質が使われます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/stream/live_low.mp4 |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| pv   | (**省略可能**) PV カメラをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |
| holo   | (**省略可能**) ホログラムをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |
| mic   | (**省略可能**) マイクをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |
| loopback   | (**省略可能**) アプリケーション オーディオをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。

### <a name="initiates-a-chunked-download-of-a-fragmented-mp4"></a>フラグメント化 mp4 のチャンク ダウンロードを開始する

**要求**

次の要求型式を使用して、フラグメント化 mp4 のチャンク ダウンロードを開始できます。 この API では中品質が使われます。
 
| 認証方法      | 要求 URI |
| :------     | :----- |
| GET | /api/holographic/stream/live_med.mp4 |


**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

| URI パラメーター | 説明 |
| :---          | :--- |
| pv   | (**省略可能**) PV カメラをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |
| holo   | (**省略可能**) ホログラムをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |
| mic   | (**省略可能**) マイクをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |
| loopback   | (**省略可能**) アプリケーション オーディオをキャプチャするかどうかを示します。 **true** または **false** を指定する必要があります。 |

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

- なし

**状態コード**

- 標準の状態コード。
