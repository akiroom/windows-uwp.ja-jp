---
title: /serviceconfigs/sessiontemplates/{sessionTemplateName}/sessions/{セッション}/メンバー/me
assetID: a6c2fa17-8bed-d0df-d7ff-db1aa60f44b3
permalink: en-us/docs/xboxlive/rest/uri-serviceconfigsscidsessiontemplatessessiontemplatenamesessionssessionnamemembersme.html
author: KevinAsgari
description: " /serviceconfigs/sessiontemplates/{sessionTemplateName}/sessions/{セッション}/メンバー/me"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 0d7e61fe76fc0f322c93d55448d53ee6444ffec5
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882166"
---
# <a name="serviceconfigsscidsessiontemplatessessiontemplatenamesessionssessionnamemembersme"></a>/serviceconfigs/sessiontemplates/{sessionTemplateName}/sessions/{セッション}/メンバー/me
セッション メンバーを削除する削除操作をサポートしています。
<a id="ID4EO"></a>


## <a name="domain"></a>ドメイン
sessiondirectory.xboxlive.com  
<a id="ID4ET"></a>

 
## <a name="remarks"></a>注釈

セッション メンバー リソースのすべての操作では、Xbox ユーザー ID (XUID)、ユーザーの承認を要求する必要があります。

<a id="ID4EAB"></a>


## <a name="uri-parameters"></a>URI パラメーター

| パラメーター| 型| 説明|
| --- | --- | --- |
| scid| GUID| サービス構成 id (SCID)。 セッション識別子のパート 1 です。|
| sessionTemplateName| string| セッション テンプレートの現在のインスタンスの名前です。 セッション識別子のパート 2 です。|
| セッション名| GUID| セッションの一意の ID。 セッション識別子のパート 3 です。|

<a id="ID4EOC"></a>


## <a name="valid-methods"></a>有効なメソッド

[削除 (/serviceconfigs/sessiontemplates/{sessionTemplateName}/sessions/{セッション}/メンバー/me)](uri-serviceconfigsscidsessiontemplatessessiontemplatenamesessionssessionnamemembersmedelete.md)

&nbsp;&nbsp;メンバーをセッションから削除します。

<a id="ID4EYC"></a>


## <a name="see-also"></a>関連項目

<a id="ID4E1C"></a>


##### <a name="parent"></a>Parent

[セッション ディレクトリ Uri](atoc-reference-sessiondirectory.md)