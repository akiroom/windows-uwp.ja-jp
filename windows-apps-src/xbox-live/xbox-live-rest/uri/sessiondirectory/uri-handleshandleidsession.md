---
title: /handles/{ハンドル id を使用}/セッション
assetID: 4ed2dcf5-5d1f-91ce-4a3f-eb3ba68727bf
permalink: en-us/docs/xboxlive/rest/uri-handleshandleidsession.html
author: KevinAsgari
description: " /handles/{ハンドル id を使用}/セッション"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: eb7ca17500f571ed72cf0bcd6ececbcde17ce717
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881835"
---
# <a name="handleshandleidsession"></a>/handles/{ハンドル id を使用}/セッション
PUT を取得する操作セッションでは、ハンドルを逆参照を使用してをサポートしています。 

> [!NOTE] 
> この URI は、2015年マルチプレイヤーでは使用され、以降そのマルチプレイヤーのバージョンにのみ適用されます。 テンプレート コントラクト 104/105 以降で使用して設計されています。  

 

> [!NOTE] 
> この URI は、現在 Xbox One 本体とサーバーのサービスの識別子を使用してアクセスできる外部のみです。  

 
<a id="ID4ES"></a>

 
## <a name="domain"></a>ドメイン
sessiondirectory.xboxlive.com  
<a id="ID4EX"></a>

 
## <a name="uri-parameters"></a>URI パラメーター
 
| パラメーター| 型| 説明| 
| --- | --- | --- | --- | --- | 
| ハンドル id を使用| GUID| セッションのハンドルを一意の ID。| 
  
<a id="ID4ESB"></a>

 
## <a name="valid-methods"></a>有効なメソッド

[取得する (/handles/{ハンドル id を使用}/セッション)](uri-handleshandleidsessionget.md)

&nbsp;&nbsp;指定したハンドル識別子セッション オブジェクトを取得します。 

[配置 (/handles/{ハンドル id}/セッション)](uri-handleshandleidsessionput.md)

&nbsp;&nbsp;作成またはハンドルを逆参照によって、セッションを更新します。
 
<a id="ID4E6B"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4EBC"></a>

 
##### <a name="parent"></a>Parent 

[セッション ディレクトリ Uri](atoc-reference-sessiondirectory.md)

   