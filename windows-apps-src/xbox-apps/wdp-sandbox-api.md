---
title: Device Portal の Xbox Live サンド ボックス API のリファレンス
description: Xbox Live サンド ボックスにプログラムでアクセスする方法について説明します。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.assetid: 72c7459c-420a-4da9-8afa-191a846185a5
ms.localizationpriority: medium
ms.openlocfilehash: 8f04514962cf0684daa99ee75d4c4da73c785735
ms.sourcegitcommit: bad7ed6def79acbb4569de5a92c0717364e771d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59244088"
---
# <a name="xbox-live-sandbox-api-reference"></a>Xbox Live サンド ボックス API のリファレンス   
この REST API を使用して、Xbox Live サンド ボックスを取得および設定できます。

## <a name="get-the-xbox-live-sandbox"></a>Xbox Live サンド ボックスを取得する

**要求**

次の要求を使用して、デバイスの Xbox Live サンド ボックスの現在の値を読み取ることができます。

メソッド      | 要求 URI
:------     | :-----
GET | /ext/xboxlive/sandbox

**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**   
Sandbox: (文字列) デバイスに適用されている現在のサンド ボックス。   

**状態コード**

この API では次の状態コードが返される可能性があります。

HTTP 状態コード      | 説明
:------     | :-----
200 | ファイル共有の資格情報にアクセスする要求が許可されました。
4XX | エラー コード
5XX | エラー コード

## <a name="set-the-xbox-live-sandbox"></a>Xbox Live サンド ボックスを設定する
次の要求を使用して、デバイスの Xbox Live サンド ボックスを変更できます。 Xbox One では、設定を有効にするためにデバイスを再起動する必要があることに注意してください。

**要求**

次の要求を使用して、デバイスの Xbox Live サンド ボックスの現在の値を設定できます。

メソッド      | 要求 URI
:------     | :-----
PUT | /ext/xboxlive/sandbox

**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**   
要求本文は、次のフィールドを含む JSON オブジェクトです。   
Sandbox: (文字列) デバイスのサンド ボックスに設定する新しい値。

**応答**   
Sandbox: (文字列) デバイスに適用されている現在のサンド ボックス。   

**状態コード**

この API では次の状態コードが返される可能性があります。

HTTP 状態コード      | 説明
:------     | :-----
200 | ファイル共有の資格情報にアクセスする要求が許可されました。
4XX | エラー コード
5XX | エラー コード

**利用可能なデバイス ファミリ**

* Windows Xbox

