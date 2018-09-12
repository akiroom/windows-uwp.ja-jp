---
title: VerifyStringResult (JSON)
assetID: 272c688e-179e-c7e9-086b-e76d0d4bcb57
permalink: en-us/docs/xboxlive/rest/json-verifystringresult.html
author: KevinAsgari
description: " VerifyStringResult (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: f774f603d89e29f5233fb0866303bab4577ca3d2
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882212"
---
# <a name="verifystringresult-json"></a>VerifyStringResult (JSON)
各文字列に[/system/strings/validate](../uri/stringserver/uri-systemstringsvalidate.md)提出に対応する結果コード。
<a id="ID4ER"></a>


## <a name="verifystringresult"></a>VerifyStringResult

VerifyStringResult オブジェクトには、次の仕様があります。

| メンバー| 種類| 説明|
| --- | --- | --- |
| resultCode| 32 ビットの符号なし整数| 必須。 HResult コードに対応する文字列を送信します。|
| offendingString| string| 必須。 拒否する文字列の原因となった文字列値。|

<a id="ID4EXB"></a>


## <a name="sample-json-syntax"></a>JSON 構文の例


```json
{
    "verifyStringResult":
    [
        {"resultCode": "1", "offendingString": "badword"},
        {"resultCode": "0", "offendingString": ""},
        {"resultCode": "0", "offendingString": ""},
        {"resultCode": "0", "offendingString": ""},
    ]
}

```


#### <a name="common-hresult-values"></a>一般的な HResult 値

| 値| エラーの名前|
| --- | --- | --- | --- | --- |
| 0| 成功|
| 1| 不快感を与える文字列|
| 2| 長い文字列|
| 3| 不明なエラー|

<a id="ID4ELD"></a>


## <a name="see-also"></a>関連項目

<a id="ID4END"></a>


##### <a name="parent"></a>Parent

[JavaScript オブジェクト Notation (JSON) オブジェクト リファレンス](atoc-xboxlivews-reference-json.md)


<a id="ID4EXD"></a>


##### <a name="reference"></a>リファレンス

[POST (/システム/文字列/検証)](../uri/stringserver/uri-systemstringsvalidatepost.md)