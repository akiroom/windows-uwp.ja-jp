---
title: POST (/システム/文字列/検証)
assetID: 6a59bc0b-8edd-87bf-efaf-f16efa3bedf7
permalink: en-us/docs/xboxlive/rest/uri-systemstringsvalidatepost.html
author: KevinAsgari
description: " POST (/システム/文字列/検証)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 4795b1ee19017e5598655117a41617e348986503
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882480"
---
# <a name="post-systemstringsvalidate"></a>POST (/システム/文字列/検証)
検証のための文字列の配列を受け取り、配列のと同じサイズの結果を返します。 これらの Uri のドメインが`client-strings.xboxlive.com`します。
 
  * [注釈](#ID4EV)
  * [必要な要求ヘッダー](#ID4EIB)
  * [要求本文](#ID4ELC)
  * [HTTP ステータス コード](#ID4E4C)
  * [応答本文](#ID4ETF)
 
<a id="ID4EV"></a>

 
## <a name="remarks"></a>注釈
 
各結果は、対応する文字列が Xbox live で許容されると、該当する場合、問題の文字列が含まれて かどうかを示します。
 
同じ文字列には、常に同一の結果が得られます。 非成功の結果が発生した場合、結果を分析し、適宜変更して、文字列。
 
 

> [!NOTE] 
> 結果として得られる<b>VerifyStringResult</b>のみ、文字列の最初の問題のある単語を報告します。 ある可能性があります、文字列内の単語の問題が追加されます。 文字列を使用できるようにする問題のある単語を置換する場合は、問題のある単語または部分文字列を置き換えるし、問題のあるその他の部分文字列を検索する文字列を再検証する必要があります。  

 
  
<a id="ID4EIB"></a>

 
## <a name="required-request-headers"></a>必要な要求ヘッダー
 
| ヘッダー| 説明| 
| --- | --- | --- | 
| Authorization| 認証トークン。 例: XBL3.0 x = [ハッシュ]。[トークン]。| 
| x xbl コントラクト バージョン| 整数 API コントラクト バージョン。 この API を 1 または 2 をする必要があります。| 
  
<a id="ID4ELC"></a>

 
## <a name="request-body"></a>要求本文
 
要求本文は、配列のサイズに制限のない、文字列ごとの 512 文字の文字列の配列です。
 
<a id="ID4ETC"></a>

 
### <a name="sample-request"></a>要求の例
 

```cpp
{
    "stringstoVerify":
    [
        "Poppycock",
        "The quick brown fox jumped over the lazy dog.",
        "Hey, want to hang out?",
        "oh noes"
    ]
}
      
```

   
<a id="ID4E4C"></a>

 
## <a name="http-status-codes"></a>HTTP ステータス コード
 
サービスは、このリソースには、この方法で行った要求に対する応答としてでは、このセクションでステータス コードのいずれかを返します。 Xbox Live サービスで使用される標準の HTTP ステータス コードの一覧は、[標準の HTTP ステータス コード](../../additional/httpstatuscodes.md)を参照してください。
 
| コード| 理由フレーズ| 説明| 
| --- | --- | --- | --- | --- | --- | 
| 200| OK| すべての文字列が正常に処理されます。 これとは限りませんすべての文字列が正の値の Hresult。| 
| 401| 権限がありません| 要求には、ユーザー認証が必要です。| 
| 403| Forbidden| 要求は、ユーザーまたはサービスは許可されません。| 
| 406| 許容できません。| 不足している<b>コンテンツの種類: アプリケーション/json</b>ヘッダー。| 
| 408| 要求のタイムアウト| サービスは、形式が正しくない要求を理解していない可能性があります。 通常、無効なパラメーターです。| 
  
<a id="ID4ETF"></a>

 
## <a name="response-body"></a>応答本文
 
[VerifyStringResult (JSON)](../../json/json-verifystringresult.md)の要求配列と同じサイズの配列を返します。
  
<a id="ID4EAG"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4ECG"></a>

 
##### <a name="parent"></a>Parent 

[/system/strings/validate](uri-systemstringsvalidate.md)

   