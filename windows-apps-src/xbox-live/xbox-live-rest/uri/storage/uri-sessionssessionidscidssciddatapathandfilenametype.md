---
title: /sessions/{sessionId}/scids/{scid}/data {{pathandfilename}, {type}
assetID: f5e91763-0704-8526-77d4-c55dfec3b5a5
permalink: en-us/docs/xboxlive/rest/uri-sessionssessionidscidssciddatapathandfilenametype.html
author: KevinAsgari
description: " /sessions/{sessionId}/scids/{scid}/data {{pathandfilename}, {type}"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: f0ce084fed46cce407c712ee42b782565c1174d4
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881925"
---
# <a name="sessionssessionidscidssciddatapathandfilenametype"></a>/sessions/{sessionId}/scids/{scid}/data {{pathandfilename}, {type}
ファイルをダウンロードします。 これらの Uri のドメインが`titlestorage.xboxlive.com`します。
 
  * [URI パラメーター](#ID4EV)
 
<a id="ID4EV"></a>

 
## <a name="uri-parameters"></a>URI パラメーター
 
| パラメーター| 型| 説明| 
| --- | --- | --- | 
| sessionId| string| 検索するセッションの ID です。| 
| scid| guid| ルックアップ サービス構成の ID です。| 
| pathAndFileName| string| アクセスする項目のパスとファイル名。 パス部分 (となどを含む最終的なスラッシュ) の有効な文字が大文字 (A ~ Z)、(a ~ z) 小文字の英字、数字 (0 ~ 9)、アンダー スコア (_) を含めるし、スラッシュ (/)。パス部分を空にすることがあります。有効な文字 (すべての最終的なスラッシュ後) ファイル名の部分には、大文字 (A ~ Z)、(a ~ z) 小文字の英字、数字 (0 ~ 9) が含まれているアンダー スコア (_)、ピリオド (.)、およびハイフン (-)。 ファイル名を空にする場合がありますはいない期間の終了または 2 つの連続するピリオドが含まれては。| 
| type| 文字列| データの形式です。 値はバイナリまたは json です。| 
  
<a id="ID4EOC"></a>

 
## <a name="valid-methods"></a>有効なメソッド

[(/Sessions/{sessionId}/scids/{scid}/data {{pathandfilename}, {type}) を削除します。](uri-sessionssessionidscidssciddatapathandfilenametype-delete.md)

&nbsp;&nbsp;ファイルを削除します。 

[(/Sessions/{sessionId}/scids/{scid}/data {{pathandfilename}, {type}) を取得します。](uri-sessionssessionidscidssciddatapathandfilenametype-get.md)

&nbsp;&nbsp;ファイルをダウンロードします。

[PUT (/sessions/{sessionId}/scids/{scid}/data {{pathandfilename}, {type})](uri-sessionssessionidscidssciddatapathandfilenametype-put.md)

&nbsp;&nbsp;ファイルをアップロードします。 メタデータとデータが送信される 1 つのメッセージで、または一連の小さいブロックのデータやメタデータが送信される複数のブロック アップロードとして完全なアップロードでは、データをアップロードできます。 1 つのメッセージとしては 4 つのメガバイト数よりも小さいファイルのみを送信できます。 複数のブロックのアップロードの種類の json データはサポートされていません。 
 
<a id="ID4E5C"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4EAD"></a>

 
##### <a name="parent"></a>Parent 

[タイトル ストレージ Uri](atoc-reference-storagev2.md)

   