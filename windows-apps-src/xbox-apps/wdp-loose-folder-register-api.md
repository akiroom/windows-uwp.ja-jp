---
author: WilliamsJason
title: "Device Portal のルース フォルダー登録 API のリファレンス"
description: "ルース フォルダー登録 API にプログラムでアクセスする方法について説明します。"
ms.sourcegitcommit: ef0f1339b77a8d1f60a677b2ff19a63b68f0d6cd
ms.openlocfilehash: 41e4cc67120b9e32fac34404ca918edcf58ba267

---

# アプリをルース フォルダーに登録する  

**要求**

次の要求形式を使用して、アプリをルース フォルダーに登録できます。

メソッド      | 要求 URI
:------     | :------
POST | /api/app/packagemanager/register
<br />
**URI パラメーター**

次の追加パラメーターを要求 URI に指定できます。

URI パラメーター      | 説明
:------     | :-----
folder (必須) | 登録するパッケージのターゲット フォルダー名です。 このフォルダーは、本体の d:\developmentfiles\LooseApps の下に存在する必要があります。 フォルダーが LooseApps の下のサブフォルダーである場合、フォルダー名にパスの区切り文字が含まれる可能性があるため、このフォルダー名は base64 でエンコードされている必要があります。
<br />

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**

**状態コード**

この API では次の状態コードが返される可能性があります。

HTTP 状態コード      | 説明
:------     | :-----
200 | 展開要求は受け入れられ、処理されています。
4XX | エラー コード
5XX | エラー コード
<br />
**利用可能なデバイス ファミリ**

* Windows Xbox

**コメント**

目的のフォルダーで本体のルース アプリを入手する方法は少なくとも 3 つあります。 最も簡単な方法は、SMB を通じてファイルを \\<IP アドレス>\DevelopmentFiles\LooseApps にコピーする方法です。 これには、[/ext/smb/developerfolder](wdp-smb-api.md) を使って取得できる UWA キットのユーザー名とパスワードが必要です。 

2 つ目の方法は、/api/filesystem/apps/file に対して POST を実行することで、個々のファイルを適切な場所にコピーする方法です。この場合、knownfolderid には DevelopmentFiles を指定し、packagefullname は空にして、ファイル名とパスを適切に提供します (パスは LooseApps で始まっている必要があります)。

3 つ目の方法は、[/api/app/packagemanager/upload](wdp-folder-upload.md) を使ってフォルダー全体を一度にコピーする方法です。この場合、destinationFolder には d:\developmentfiles\looseapps の下に配置されるフォルダーの名前を指定し、ペイロードはディレクトリ コンテンツの原則に従ったマルチパートの http 本文になります。




<!--HONumber=Jun16_HO4-->

