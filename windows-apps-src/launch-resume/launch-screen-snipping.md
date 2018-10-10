---
author: QuinnRadich
title: 起動画面 snipping
description: このトピックでは、ms screenclip と ms screensketch URI スキームについて説明します。 アプリは、これらの URI スキームを使用して、切り取り領域とスケッチ アプリを起動する、または新しい切り取り領域を開くことができます。
ms.author: quradic
ms.date: 8/1/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10、uwp、uri、切り取り領域、スケッチ
ms.localizationpriority: medium
ms.openlocfilehash: e18662125ef72051a289b3f1d0f3dc09b452d256
ms.sourcegitcommit: 49aab071aa2bd88f1c165438ee7e5c854b3e4f61
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2018
ms.locfileid: "4469708"
---
# <a name="launch-screen-snipping"></a>起動画面 snipping

**Ms screenclip:** と**ms screensketch:** URI スキームでは、snipping やスクリーン ショットの編集を開始することができます。

## <a name="open-a-new-snip-from-your-app"></a>アプリから新しい切り取り領域を開く

**Ms screenclip:** URI が自動的開き、新しい切り取り領域を開始するアプリを使用します。 結果として得られるの切り取り領域は、ユーザーのクリップボードにコピーされますが、開いたアプリに戻るに自動的に渡されません。

**ms screenclip:** は次のパラメーターを受け取ります。

| パラメーター | 型 | 必須かどうか | 説明 |
| --- | --- | --- | --- |
| ソース | string | いいえ | URI を起動したソースを示す自由形式の文字列です。 |
| delayInSeconds | int | × | 1 ~ 30 の整数値。 URI の呼び出しと snipping の開始時の間の完全な秒の遅延を指定します。 |

## <a name="launching-the-snip--sketch-app"></a>切り取り領域 & スケッチ アプリを起動します。

**Ms screensketch:** URI では、プログラムで切り取り領域とスケッチ アプリを起動し、注釈をそのアプリで特定のイメージを開くことができます。

**ms screensketch:** は次のパラメーターを受け取ります。

| パラメーター | 型 | 必須かどうか | 説明 |
| --- | --- | --- | --- |
| sharedAccessToken | string | いいえ | 切り取り領域とスケッチ アプリで開くには、ファイルを識別するトークンです。 [SharedStorageAccessManager.AddFile](https://docs.microsoft.com/uwp/api/windows.applicationmodel.datatransfer.sharedstorageaccessmanager.addfile)から取得されます。 このパラメーターを省略すると、ファイルを開くことがなく、アプリが起動します。 |
| ソース | string | いいえ | URI を起動したソースを示す自由形式の文字列です。 |
| isTemporary | bool | × | 場合は、画面スケッチが True に設定は、開いた後、ファイルを削除しようとしています。 |

次の例では、ユーザーのアプリからの切り取り領域とスケッチに画像を送信する[LaunchUriAsync](https://docs.microsoft.com/uwp/api/Windows.System.Launcher#Windows_System_Launcher_LaunchUriAsync_Windows_Foundation_Uri_)メソッドを呼び出します。

```csharp

bool result = await Windows.System.Launcher.LaunchUriAsync(new Uri("ms-screensketch:edit?source=MyApp&isTemporary=false&sharedAccessToken=2C37ADDA-B054-40B5-8B38-11CED1E1A2D"));

```