---
title: バイナリ BLOB の読み取り
author: KevinAsgari
description: Xbox Live タイトル ストレージ内のバイナリ BLOB の読み取りについて説明します。
ms.assetid: 9b8e0c35-0cea-4491-bf30-22fad224f11b
ms.author: kevinasg
ms.date: 04/04/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, ゲーム, uwp, windows 10, xbox one, タイトル ストレージ
ms.localizationpriority: low
ms.openlocfilehash: 604793be3e08c755169fc4cd07a2432a8c6829ea
ms.sourcegitcommit: 01760b73fa8cdb423a9aa1f63e72e70647d8f6ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/24/2018
---
# <a name="reading-a-binary-blob-in-xbox-live-title-storage"></a>Xbox Live タイトル ストレージ内のバイナリ BLOB の読み取り

1.  タイトル ストレージからデータを読み取るには、*GET* メソッドを使用して要求を送信します。 次の例ではグローバル タイトル ストレージを使用します。

        GET https://titlestorage.xboxlive.com/global/scids/{scid}/data/userinfo.bin,binary
        Content-Type: application/octet-stream
        x-xbl-contract-version: 1
        Authorization: XBL3.0 x=<userHash>;<STSTokenString>
        Connection: Keep-Alive



-   更新するには、ユーザーはそのセッション内にいなければなりません。

-   STSTokenString は、簡潔にするためのプレースホルダーであり、認証要求から返されるトークンで置き換える必要があります。

#### <a name="reference"></a>参照先

**/global/scids/{scid}/data/{pathAndFileName},{type}**