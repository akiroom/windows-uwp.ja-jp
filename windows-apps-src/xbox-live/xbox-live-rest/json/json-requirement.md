---
title: 要件 (JSON)
assetID: 74faee8d-42e3-cfcf-22b3-9dcd9227de6b
permalink: en-us/docs/xboxlive/rest/json-requirement.html
author: KevinAsgari
description: " 要件 (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: f13edfbe5858a5fc3c4f24d22b31eb25f8386e25
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881973"
---
# <a name="requirement-json"></a>要件 (JSON)
実績とそれらに対応するための距離、ユーザーがロック解除の条件。 
<a id="ID4EN"></a>

 
## <a name="requirement"></a>要件
 
要件のオブジェクトには、次の仕様があります。
 
| メンバー| 種類| 説明| 
| --- | --- | --- | 
| id| string| 要件の ID です。| 
| 現在の| string| 要件と進行状況の現在の値。| 
| ターゲット| string| 要件のターゲット値。| 
| 入力| string| 要件の操作の種類。 有効な値は、合計、最小、最大値はします。| 
| ruleParticipationType| string| 要件の参加の種類。 有効な値は、個人のグループです。| 
  
<a id="ID4ETC"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4EVC"></a>

 
##### <a name="parent"></a>Parent 

[JavaScript オブジェクト Notation (JSON) オブジェクト リファレンス](atoc-xboxlivews-reference-json.md)

   