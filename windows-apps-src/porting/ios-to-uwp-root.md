---
description: iOS から UWP への移行
Search.SourceType: Video
title: iOS から UWP への移行
ms.assetid: 7a05751d-02df-4240-9ba5-d95f65a7a9c5
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 266a5f147b57e522088dab2ec298b54596ef77b7
ms.sourcegitcommit: b52ddecccb9e68dbb71695af3078005a2eb78af1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74260155"
---
# <a name="move-from-ios-to-uwp"></a>iOS から UWP への移行

ユーザー ベースを Windows 10 とユニバーサル Windows プラットフォーム (UWP) にまで拡大する方法に悩んでいる iOS 開発者向けに、便利なツールが提供されています。そしてその数は日々増え続けています。 どの方法を使うかは、対象のアプリの種類 (ゲーム、ライフ スタイル、エンタープライズなど) と、開発プロセスにどれだけ関与できるかに応じて異なります。 たとえば、OpenGL または Cocos2D に大きく依存している完成済みのゲームまたはほぼ完成しているゲームの場合は、[iOS 用 Windows ブリッジ](https://developer.microsoft.com/windows/bridges/ios)が有力な候補になります。また、スモール ビジネス用のクロスプラットフォーム アプリを計画している場合は、[Xamarin.Forms](https://docs.microsoft.com/xamarin/xamarin-forms/) の使用を検討する必要があります。 Unity などのクロスプラットフォーム ツールでアプリを記述している場合は、[Windows に公開](https://blogs.unity3d.com/2015/09/09/windows-10-universal-apps-in-unity-5-2/)するのが簡単です。

## <a name="why-windows"></a>Windows を選ぶ理由

今日は、Windows は膨大な数のデバイスで実行されています。 UWP は、デスクトップ コンピューター、ゲーム コンソール、ホログラフィック ディスプレイなどのさまざまなデバイス間で美しく応答性に優れたユーザー インターフェイスを作るように設計された最新の API のセットを開発者に提供します。 1 つの Visual Studio ソリューションと、複数のプラットフォームに自動的に最適化されるスマートなユーザー インターフェイス コントロールにより、より少ないコードで記述したアプリをより多くのハードウェア上で実行できます。

> [!VIDEO https://channel9.msdn.com/Blogs/One-Dev-Minute/How-to-Convert-your-iOS-app-to-Windows/player]

| トピック | 説明 |
|-------|-------------|
| [IOS と UWP アプリ開発のアプローチを選択する](selecting-an-approach-to-ios-and-uwp-app-development.md) | クロスプラットフォーム アプリを開発するときの選択肢 |
| [IOS 開発者向け UWP の概要](getting-started-with-uwp-for-ios-developers.md) | この記事は、Windows 10 用の開発を検討している iOS 開発者向けに用意されています。 |
| [Windows 10 を使用して Mac をセットアップする](setting-up-your-mac-with-windows-10.md) | 現在の Mac コンピューターを使用して、Windows 用アプリを開発します。 |

## <a name="related-topics"></a>関連トピック

**デザイナーと開発者向け**
* [すべての Windows デバイス用のユニバーサル Windows アプリの構築](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)
* [UWP アプリ用のデザインアセットをダウンロードする](https://docs.microsoft.com/windows/uwp/design/downloads/index)
