---
title: /serviceconfigs/sessiontemplates/{sessionTemplateName}/sessions/{セッション}/members
assetID: ae6c6a25-2251-6ffd-ec58-e6c0576a34db
permalink: en-us/docs/xboxlive/rest/uri-serviceconfigsscidsessiontemplatessessiontemplatenamesessionnamemembersindex.html
author: KevinAsgari
description: " /serviceconfigs/sessiontemplates/{sessionTemplateName}/sessions/{セッション}/members"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: e8d56b9d7079e26973595de093b581ef39bd41c0
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881912"
---
# <a name="serviceconfigsscidsessiontemplatessessiontemplatenamesessionssessionnamemembersindex"></a>/serviceconfigs/sessiontemplates/{sessionTemplateName}/sessions/{セッション}/members
指定されたセッション メンバーを削除する削除操作をサポートしています。
<a id="ID4EO"></a>


## <a name="domain"></a>ドメイン
sessiondirectory.xboxlive.com  
<a id="ID4ET"></a>


## <a name="uri-parameters"></a>URI パラメーター

| パラメーター| 型| 説明|
| --- | --- | --- |
| scid| GUID| サービス構成 id (SCID)。 セッション識別子のパート 1 です。|
| sessionTemplateName| string| セッション テンプレートの現在のインスタンスの名前です。 セッション識別子のパート 2 です。|
| セッション名| GUID| セッションの一意の ID。 セッション識別子のパート 3 です。|

<a id="ID4EDC"></a>


## <a name="valid-methods"></a>有効なメソッド

[(/Serviceconfigs/sessiontemplates/{sessionTemplateName}/sessions/{セッション}/members) を削除します。](uri-serviceconfigsscidsessiontemplatessessiontemplatenamesessionnamemembersindexdelete.md)

&nbsp;&nbsp;指定されたメンバーをセッションから削除します。

<a id="ID4ENC"></a>


## <a name="see-also"></a>関連項目

<a id="ID4EPC"></a>


##### <a name="parent"></a>Parent

[セッション ディレクトリ Uri](atoc-reference-sessiondirectory.md)