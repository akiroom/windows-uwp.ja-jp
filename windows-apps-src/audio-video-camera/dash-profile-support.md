---
ms.assetid: 3E0FBB43-F6A4-4558-AA89-20E7760BA73F
description: この記事では、UWP アプリでサポートされる Dynamic Adaptive Streaming over HTTP (DASH) プロファイルの一覧を示します。
title: Dynamic Adaptive Streaming over HTTP (DASH) プロファイルのサポート
ms.date: 02/15/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: d680f7d4a3510f66cba74d1c8b30d8883b07369a
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57627207"
---
# <a name="dynamic-adaptive-streaming-over-http-dash-profile-support"></a>Dynamic Adaptive Streaming over HTTP (DASH) プロファイルのサポート


## <a name="supported-dash-profiles"></a>サポートされている DASH プロファイル
次の表では、UWP アプリでサポートされている DASH プロファイルを示します。

|Tag | マニフェストの種類 | メモ|7 月にリリースされた Windows 10|Windows 10 バージョン 1511|Windows 10 バージョン 1607 |Windows 10 バージョン 1607 |Windows 10 バージョン 1703|
|----------------|------|-------|-----------|--------------|---------|-------|--------|
|urn:mpeg&#58;dash:profile:isoff-live:2011 | 静的 |     |サポートされている            |  サポート対象              | サポート対象        |サポート対象| サポートされている|
|urn:mpeg&#58;dash:profile:isoff-main:2011 |        | ベスト エフォート | サポートされている            |  サポート対象              | サポート対象        |サポート対象| サポートされている|
|urn:mpeg&#58;dash:profile:isoff-live:2011 | 動的 | セグメント テンプレートで $Time$ はサポートされていますが、$Number$ はサポートされていません。 | サポートされない            | サポートされない              | サポートされない        |サポートされない| サポートされている|


## <a name="unsupported-dash-profiles"></a>サポートされていない DASH プロファイル
上の表に示されていないプロファイルはサポートされていません。これには、次のようなものが含まれますが、これらに限定されません。

* urn:mpeg&#58;dash:profile:full:2011
* urn:mpeg&#58;dash:profile:isoff-on-demand:2011
* urn:mpeg&#58;dash:profile:mp2t-main:2011
* urn:mpeg&#58;dash:profile:mp2t-simple:2011


## <a name="related-topics"></a>関連トピック

* [メディア再生](media-playback.md)
* [アダプティブ ストリーミング](adaptive-streaming.md)
 

 




