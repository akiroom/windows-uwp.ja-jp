---
ms.assetid: a2751e22-6842-073a-daec-425fb981bafe
title: ビジュアル レイヤー
description: Windows.UI.Composition API を使うと、フレーム ワーク層 (XAML) とグラフィック層 (DirectX) との間のコンポジション層にアクセスできます。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: ac41d461982a39a939e460b7a81b144e5a08fdb3
ms.sourcegitcommit: b52ddecccb9e68dbb71695af3078005a2eb78af1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74255527"
---
# <a name="visual-layer"></a>ビジュアル レイヤー

ビジュアル レイヤーは、グラフィックス、効果、アニメーション用の高パフォーマンスの保持モード API を提供し、Windows デバイス間ですべての UI の基盤となります。 UI は宣言的な方法で定義します。ビジュアル層はグラフィックスハードウェアの高速化に依存しており、アプリの UI スレッドに依存せずに、コンテンツ、効果、およびアニメーションがスムーズにエラーのない方法でレンダリングされるようにします。

主な特長は次のとおりです。

* 使い慣れた WinRT API
* さらに動的な UI と対話式操作を実現する設計
* デザイン ツールとの一貫した概念
* 突然パフォーマンスが低下することがない直線的なスケーラビリティ

Windows UWP アプリは、いずれかの UI フレームワークを介してビジュアル レイヤーを既に使用しています。 非常にわずかな労力で、カスタム レンダリング、効果、アニメーションに直接ビジュアル レイヤーを利用することもできます。

![UI フレームワークの階層: フレームワーク レイヤー (Windows.UI.XAML) はビジュアル レイヤー (Windows.UI.Composition) を基盤とし、ビジュアル レイヤーはさらにグラフィック レイヤー (DirectX) を基盤としている](images/layers-win-ui-composition.png)

## <a name="whats-in-the-visual-layer"></a>ビジュアル レイヤーとは

ビジュアル レイヤーの主な機能は次のとおりです。

1. **コンテンツ**: カスタム描画コンテンツの軽量合成
1. **効果**: 効果をアニメーション化、チェーン化、カスタマイズできる、リアルタイム UI 効果システム
1. **アニメーション**: UI スレッドから独立して実行される、表現力豊かな、フレームワークに依存しないアニメーション

### <a name="content"></a>コンテンツ

コンテンツは、ビジュアルを使用するアニメーションおよび効果システムで使用できるように、ホスト、変換、提供されます。 クラス階層の基底クラスは [**Visual**](https://docs.microsoft.com/uwp/api/Windows.UI.Composition.Visual) クラスで、コンポジターでビジュアル状態を処理するアプリ プロセスにおける、軽量でスレッド アジャイルなプロキシです。 Visual のサブクラスには、子がコンテンツを含むビジュアルと[**SpriteVisual**](https://docs.microsoft.com/uwp/api/Windows.UI.Composition.SpriteVisual)のツリーを作成できるようにするための  [**ContainerVisual**](https://docs.microsoft.com/uwp/api/Windows.UI.Composition.ContainerVisual)が含まれており、純色、カスタム描画コンテンツ、視覚効果のいずれかで描画できます。 また、これらの種類のビジュアルは 2D UI 用のビジュアル ツリー構造を構成し、多くの表示される XAML FrameworkElements を強化します。

詳しくは、[コンポジションのビジュアル](composition-visual-tree.md)の概要をご覧ください。

### <a name="effects"></a>効果

ビジュアル レイヤーの効果システムでは、ビジュアルやビジュアル ツリーにフィルターや透明効果のチェーンを適用できます。 これは UI 効果システムであり、画像やメディアの効果を混同しないでください。 効果はアニメーション システムとの組み合わせで動作し、ユーザーは、UI スレッドから独立してレンダリングされる、スムーズで動的な効果プロパティのアニメーションを実現できます。 ビジュアル レイヤーの効果は、カスタマイズされたと対話型エクスペリエンスを構築するために組み合わせてアニメーション化できる、創造的な構成要素を提供します。

ビジュアル レイヤーは、アニメーション化可能な効果のチェーンに加えて、アニメーション化可能なライトに応答することにより、ビジュアルでマテリアル プロパティを模倣できるようにする照明モデルもサポートします。 ビジュアルによって、シャドウを生じさせることもできます。 照明とシャドウを組み合わせて使うことで、奥行きとリアルさを感じられるようにすることができます。

詳しくは、「[コンポジションの効果](composition-effects.md)」をご覧ください。

### <a name="animations"></a>アニメーション

ビジュアル レイヤーのアニメーション システムによって、移動の視覚効果、効果のアニメーション化、変換、クリップ、その他のプロパティの駆動を実現できます。  これは、パフォーマンスを考慮して最初から設計されたフレームワークに依存しないシステムです。  これは、滑らかさとスケーラビリティを確保するために、UI スレッドとは別に実行されます。  使い慣れたキーフレームアニメーションを使用して、時間の経過と共にプロパティの変更を行うことができますが、ユーザー入力などの異なるプロパティ間に数学的な関係を設定して、シームレスな choreographed エクスペリエンスを直接作成することもできます。

詳しくは、[コンポジションのアニメーション](composition-animation.md)の概要をご覧ください。

### <a name="working-with-your-xaml-uwp-app"></a>XAML UWP アプリの操作

[  **Windows.UI.Xaml.Hosting**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Hosting.ElementCompositionPreview) の [**ElementCompositionPreview**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Hosting) クラスを使用して、XAML フレームワークによってビジュアルを作成できるようになり、表示可能な FrameworkElement を強化することができます。 フレームワークによって作成されたビジュアルには、カスタマイズに関するいくつかの制限があることに注意してください。 これは、フレームワークがオフセット、変換、有効期間を管理するためです。 ただし、独自のビジュアルを作成し、ElementCompositionPreview によって、またはビジュアル ツリー構造内のどこかに既にある ContainerVisual に追加することにより、既存の XAML 要素にアタッチできます。

詳しくは、[XAML でのビジュアル レイヤーの使用](using-the-visual-layer-with-xaml.md)の概要をご覧ください。

### <a name="working-with-your-desktop-app"></a>デスクトップアプリの操作

ビジュアルレイヤーを使用すると、WPF、Windows フォーム、およびC++ Win32 デスクトップアプリの外観、外観、機能を向上させることができます。 コンテンツの孤島を移行して、ビジュアルレイヤーを使用し、残りの UI を既存のフレームワークに保持することができます。 つまり、既存のコードベースに大幅な変更を加えることなく、アプリケーション UI に大幅な更新や拡張を行うことができます。

詳しくは、「[Modernize your desktop app using the Visual layer (ビジュアル レイヤーを使用したデスクトップ アプリの現代化)](/windows/apps/desktop/modernize/visual-layer-in-desktop-apps)」をご覧ください。

## <a name="additional-resources"></a>その他の資料

* [**API の完全なリファレンスドキュメント**](https://docs.microsoft.com/uwp/api/Windows.UI.Composition)
* [WindowsUIDevLabs GitHub](https://github.com/microsoft/WindowsCompositionSamples) にある高度な UI とコンポジションのサンプル
* [Windows. UI. コンポジションのサンプルギャラリー](https://www.microsoft.com/store/apps/9pp1sb5wgnww)
* [@windowsui Twitter フィード](https://twitter.com/windowsui)
* この API に関する Kenny Kerr の MSDN 記事: [Graphics and Animation - Windows Composition Turns 10 (グラフィックとアニメーション - Window コンポジションの 10 年)](https://msdn.microsoft.com/magazine/mt590968)
