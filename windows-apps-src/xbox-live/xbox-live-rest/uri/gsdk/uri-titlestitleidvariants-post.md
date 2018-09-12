---
title: POST (/titles/{titleId}/バリアント)
assetID: 84303448-5a11-d96f-907d-77f57f859741
permalink: en-us/docs/xboxlive/rest/uri-titlestitleidvariants-post.html
author: KevinAsgari
description: " POST (/titles/{titleId}/バリアント)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 246427b772403ca07adac2a4b1b07ec159142049
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882214"
---
# <a name="post-titlestitleidvariants"></a>POST (/titles/{titleId}/バリアント)
指定されたタイトル id。 用のバリアントをゲームの一覧を取得するクライアントによって呼び出される URIこれらの Uri のドメイン`gameserverds.xboxlive.com`と`gameserverms.xboxlive.com`します。
 
  * [URI パラメーター](#ID4EZ)
  * [必要な要求ヘッダー](#ID4EIB)
  * [オプションの要求ヘッダー](#ID4EED)
  * [Authorization](#ID4E3D)
  * [要求本文](#ID4EEE)
  * [必要な応答ヘッダー](#ID4ELF)
  * [省略可能な応答ヘッダー](#ID4EMG)
  * [応答本文](#ID4EEH)
 
<a id="ID4EZ"></a>

 
## <a name="uri-parameters"></a>URI パラメーター
 
| パラメーター| 説明| 
| --- | --- | 
| タイトル id| 要求の操作をタイトルの ID です。| 
  
<a id="ID5EG"></a>

 
## <a name="host-name"></a>ホスト名

gameserverds.xboxlive.com
 
<a id="ID4EIB"></a>

 
## <a name="required-request-headers"></a>必要な要求ヘッダー
 
要求を作成する場合、次の表に示すように、ヘッダーは必要です。
 
| ヘッダー| 設定値| 説明| 
| --- | --- | --- | --- | --- | 
| Content-Type| application/json| 提出されたデータの種類です。| 
| Host| gameserverds.xboxlive.com|  | 
| Content-Length|  | 要求のオブジェクトの長さ。| 
| x xbl コントラクト バージョン| 1| API コントラクト バージョン。| 
| Authorization| XBL3.0 x = [ハッシュ]。[トークン]| 認証トークン。| 
  
<a id="ID4EED"></a>

 
## <a name="optional-request-headers"></a>オプションの要求ヘッダー
 
要求を作成する場合は、次の表に示すように、ヘッダーはオプションです。
 
| ヘッダー| 設定値| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | 
| X XblCorrelationId|  | 要求の本文の mime タイプ。| 
  
<a id="ID4E3D"></a>

 
## <a name="authorization"></a>Authorization

要求は、Xbox Live の有効な承認ヘッダーを含める必要があります。 呼び出し元がこのリソースへのアクセス許可されていない場合、サービスは応答で 403 Forbidden を返します。 ヘッダーが見つからないか無効な場合は、サービスは応答で 401 Unauthorized を返します。
 
<a id="ID4EEE"></a>

 
## <a name="request-body"></a>要求本文
 
要求は、次のメンバーを含む JSON オブジェクトを含める必要があります。
 
| メンバー| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| locale| ローカルのバリアントを返します。| 
| maxVariants| バリエーションを返すの最大数。| 
| publisherOnly|  | 
| 制限|  | 
 
<a id="ID4EDF"></a>

 
### <a name="sample-request"></a>要求の例
 

```cpp
{
  "locale": "en-us",
  "maxVariants": "100",
  "publisherOnly": "false",
  "restriction": null
}

```

   
<a id="ID4ELF"></a>

 
## <a name="required-response-headers"></a>必要な応答ヘッダー
 
応答には常に、次の表に示すように、ヘッダーが含まれます。
 
| ヘッダー| 設定値| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| Content-Type| application/json| 応答本文内のデータの種類です。| 
| Content-Length|  | 応答本文の長さ。| 
  
<a id="ID4EMG"></a>

 
## <a name="optional-response-headers"></a>省略可能な応答ヘッダー
 
応答には、次に示すように、ヘッダーの各自が可能性があります。
 
| ヘッダー| 設定値| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| X XblCorrelationId|  | 応答本文の mime タイプ。| 
  
<a id="ID4EEH"></a>

 
## <a name="response-body"></a>応答本文
 
呼び出しが成功した場合、サービスは、次のメンバーを含む JSON オブジェクトを返します。
 
| メンバー| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| バリエーション| バリアントの配列です。| 
| バリエーション| バリアントの Id です。| 
| name| バリアントの名前です。| 
| isPublisher|  | 
| ランク|  | 
| gameVariantSchemaId|  | 
| variantSchemas| バリアントのスキーマの配列です。| 
| variantSchemaId| スキーマの Id です。| 
| schemaContent| スキーマの内容| 
| name| スキーマの名前| 
| gsiSets| GSI セットの配列です。| 
| minRequiredPlayers| バリアントのプレイヤーの最小数。| 
| maxAllowedPlayers| バリアントのプレイヤーの最大数。| 
| は| GSI セットの Id です。| 
| gsiSetName| GSI セットの名前です。| 
| selectionOrder|  | 
| variantSchemaId| GSI で使われる varaint スキーマの id を設定します。| 
 
<a id="ID4EYBAC"></a>

 
### <a name="sample-response"></a>応答の例
 

```cpp
{
 "variants": [
     { 
       "variantId": "8B6EF8A0-7807-42C4-9CB0-1D9B8B8CE742", 
       "name": "tankWarsV2.0",
       "isPublisher": "true",
       "rank": "1",
       "gameVariantSchemaId": "9742DBA5-23FD-4760-9D74-6CFA211B9CFB"
     }],
  "variantSchemas": [
     {
        "variantSchemaId": "9742DBA5-23FD-4760-9D74-6CFA211B9CFB",
        "schemaContent": "&lt;?xml version=\"1.0\" encoding=\"UTF-8\" ?>&lt;xs:schema xmlns:xs=\"http://www.w3.org/2001/XMLSchema\">&lt;xs:element name=\"root\">&lt;/xs:element>&lt;/xs:schema>"
        "name": "tanksSchema"
     }],
     "gsiSets":
     [{ 
          "minRequiredPlayers": "5", 
          "maxAllowedPlayers": "10", 
          "gsiSetId": "B28047F5-B52F-477E-97C2-4C1C39E31D42",
          "gsiSetName": "TanksGSISet",
          "selectionOrder": "1",
          "variantSchemaId": "9742DBA5-23FD-4760-9D74-6CFA211B9CFB"
     }]
 }

  

```

   
<a id="ID4ERCAC"></a>

 
## <a name="see-also"></a>関連項目
 [/titles/{titleId}/バリエーション](uri-titlestitleidvariants.md)

  