---
title: Xbox Live テスト ユーザー管理 API のリファレンス
description: ユーザー管理 API にプログラムでアクセスする方法について説明します。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.assetid: 70876ab6-8222-4940-b4fb-65b581a77d6a
ms.openlocfilehash: 71c47767cf026b962f682fb30ca93758dbd5e227
ms.sourcegitcommit: bad7ed6def79acbb4569de5a92c0717364e771d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59244078"
---
#<a name="xbox-live-user-management"></a>Xbox Live ユーザー管理 #

## <a name="request"></a>要求

本体のユーザーの一覧を取得したり、一覧を更新したりできます。更新では、既存のユーザーの追加、削除、サインイン、サインアウト、または変更を行うことができます。

| メソッド        | 要求 URI     | 
| ------------- |-----------------|
| GET           | /ext/user |
| PUT           | /ext/user |


**URI パラメーター**

* なし

**要求ヘッダー**

* なし

**要求本文**

PUT メソッドの呼び出しには、次の構造の JSON 配列を含める必要があります。

* Users
  * AutoSignIn (省略可能): EmailAddress や UserId で指定されたアカウントの自動サインインを無効または有効にするブール値。
  * EmailAddress (省略可能 - スポンサーが付いたユーザーをサインインしない限り、ユーザー Id は指定しないかどうかを指定する必要があります)。電子メール アドレスを変更/追加/削除するユーザーを指定します。
  * パスワード (省略可能 - ユーザーがコンソールに現在がないかどうかを指定する必要があります)。コンソールに新しいユーザーを追加するために使用するパスワード。
  * SignedIn (省略可能): 指定されたアカウントでサインインまたはサインアウトする必要があるかどうかを指定するブール値。
  * ユーザー Id (省略可能 - EmailAddress が付属しており、ユーザーをサインインしない限り、指定しないかどうかを指定する必要があります)。ユーザー Id の変更/追加/削除するユーザーを指定します。
  * SponsoredUser (省略可能): スポンサー ユーザーを追加するかどうかを指定するブール値。
  * (省略可能) の削除: コンソールからこのユーザーの削除を指定するブール値

## <a name="response"></a>応答

**応答本文**

GET メソッドの呼び出しでは、次のプロパティが指定された JSON 配列を返します。

* Users
  * AutoSignIn (省略可能)
  * EmailAddress (省略可能)
  * Gamertag
  * SignedIn
  * UserId
  * XboxUserId
  * SponsoredUser (省略可能)
  
**状態コード**

この API では次の状態コードが返される可能性があります。

| HTTP 状態コード   | 説明     | 
| ------------------ |-----------------|
| 200                | GET メソッドの呼び出しが成功し、ユーザーの JSON 配列が応答本文で返されました |
| 204                | PUT メソッドの呼び出しが成功し、本体のユーザーが更新されました |
| 4XX                | 無効な要求データまたは形式を示すさまざまなエラー |
| 5XX                | 予期しないエラーのエラー コード |
