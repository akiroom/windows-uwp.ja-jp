---
title: 暗号化に関する輸出制限の順守
description: アプリでの暗号化が、Microsoft Store に登録されない可能性がある方法で使われていないかどうかを判断する場合に、この情報を利用してください。
ms.assetid: 204C7D1D-6F08-4AEE-A333-434D715E7617
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp, セキュリティ
ms.localizationpriority: medium
ms.openlocfilehash: c647d91213ddf1fd8a3dafd80c6888a026cda576
ms.sourcegitcommit: b52ddecccb9e68dbb71695af3078005a2eb78af1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74258937"
---
# <a name="export-restrictions-on-cryptography"></a>暗号化に関する輸出制限の順守



アプリでの暗号化が、Microsoft Store に登録されない可能性がある方法で使われていないかどうかを判断する場合に、この情報を利用してください。

米国商務省産業安全保障局は、一部の種類の暗号化を使う技術の輸出を規制しています。 アプリ ファイルは米国内に保存することができるため、Microsoft Store に登録されているすべてのアプリはこれらの法律と規制に従う必要があります。 米国以外の国で配布することを目的として他の国からアプリ開発者によってアップロードされたアプリについても、これらの規制に従う必要があります。 このため、アプリを Microsoft Store に提出する場合、すべてのアプリ開発者はこれらの規制で制限されている技術がアプリに含まれていないことを確認する必要があります。

> ここに記載されている情報にはいくつかのガイダンスがありますが、アプリが適用されるすべての法律および規制に準拠していることを確認するために、Microsoft Store でアプリを発行しているアプリ開発者としての責任があります **。  **

 

米国商務省と産業安全保障局の詳しい情報については、[産業安全保障局の Web サイト](https://www.bis.doc.gov/about/index.htm)をご覧ください。

暗号化を含む技術の輸出を管理する輸出管理規制 (EAR) の情報については、[暗号化技術を使う品目に対する輸出管理規制に関する Web ページ](https://www.bis.doc.gov/index.php/policy-guidance/encryption)をご覧ください。

## <a name="governed-uses"></a>管理対象の使用

まず、輸出管理規制の対象となる暗号化の種類をアプリが使っているかどうかを判断します。 この質問には、ここで一覧に示している例も含まれていますが、この一覧が暗号化の応用のすべてではないことに注意してください。

> **重要**  アプリ用に記述したコードだけでなく、アプリに含まれている、またはリンク先のすべてのソフトウェアライブラリ、ユーティリティ、およびオペレーティングシステムコンポーネントも考慮してください。

-   認証、整合性チェックなどの、デジタル署名の使用
-   アプリが使ったりアクセスしたりするデータまたはファイルの暗号化
-   キー管理、証明書管理、または公開キー インフラストラクチャとやり取りのある操作
-   NTLM、Kerberos、Secure Sockets Layer (SSL)、トランスポート層セキュリティ (TLS) などの、セキュリティで保護された通信チャネルの使用
-   暗号化パスワードなどによる情報セキュリティ
-   コピー防止やデジタル著作権管理 (DRM)
-   ウイルス対策機能

暗号化の適用に関する最新の一覧については、[暗号化技術を使う品目に対する輸出管理規制に関する Web ページ](https://www.bis.doc.gov/index.php/policy-guidance/encryption)をご覧ください。

## <a name="non-restricted-uses"></a>制限なしの使用

一部の暗号化の適用は制限されていません。 次のタスクは、制限を受けません。

-   パスワードの暗号化
-   コピー防止
-   認証
-   デジタル著作権管理
-   デジタル署名の使用

暗号化の適用に関する最新の一覧については、[暗号化技術を使う品目に対する輸出管理規制に関する Web ページ](https://www.bis.doc.gov/index.php/policy-guidance/encryption)をご覧ください。

アプリがこの一覧に含まれないタスクについて暗号化を呼び出す、サポートする、組み込む、または使う場合は、輸出規制品目番号 (ECCN) が必要です。

ECCN を持っていない場合は、[ECCN についての質問とその回答が掲載された Web ページ](https://www.bis.doc.gov/licensing/do_i_needaneccn.html)をご覧ください。
