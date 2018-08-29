---
author: QuinnRadich
title: 8 月 2018 年に Windows ドキュメントの新しい - UWP アプリの開発
description: 2018年 8 月向けの Windows 10 開発者向けドキュメントには、新しい機能、ビデオ、サンプル、および開発者向けガイダンスが追加されました。
keywords: 新機能, 更新, 機能, 開発者向けガイダンス, Windows 10, 8 月
ms.author: quradic
ms.date: 08/14/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
ms.openlocfilehash: c294dedc8e19605bc2cee0308022bed8624df57e
ms.sourcegitcommit: 3727445c1d6374401b867c78e4ff8b07d92b7adc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2018
ms.locfileid: "2918763"
---
# <a name="whats-new-in-the-windows-developer-docs-in-august-2018"></a>8 月 2018 年に、Windows 開発者向けドキュメントの新しい新機能

Windows 開発者向けドキュメントは、Windows プラットフォームで開発者に提供される新機能の情報を反映して継続的に更新されています。 次の機能の概要、開発者向けガイダンス、およびビデオには 8 月で利用可能ななりました。

Windows 10 の[ツールと SDK をインストール](http://go.microsoft.com/fwlink/?LinkId=821431)すると、[新しいユニバーサル Windows アプリを作成](../get-started/create-uwp-apps.md)したり、[Windows の既存のアプリ コード](../porting/index.md)がどのように使えるかを試したりすることができます。

## <a name="features"></a>機能

### <a name="design"></a>設計

次の機能が Insider Preview ビルドで[Windows Insider](https://insider.windows.com/) program で利用できる、Windows に追加されました。

* [Windows UI のライブラリ](https://aka.ms/winui-docs)は、UWP アプリのコントロールとその他のユーザー interfact 要素を提供する NuGet パッケージのセットです。 これらのパッケージも、以前のバージョンの Windows 10 互換、ユーザーは、最新の OS バージョンがあるない場合でも、アプリが機能するようにします。

* [DropDownButton](../design/controls-and-patterns/buttons.md#create-a-drop-down-button)、 [SplitButton](../design/controls-and-patterns/buttons.md#create-a-split-button)、および[ToggleSplitButton](../design/controls-and-patterns/buttons.md#create-a-toggle-split-button)は、アプリのユーザー インターフェイスを強化するために特殊な機能を備えたボタン コントロールを提供します。

![フォア グラウンドの色を選択するための分割ボタン](../design/controls-and-patterns/images/split-button-rtb.png)

* NavigationView がアプリのナビゲーション オプションの数を減らしてがあり、アプリのコンテンツの空き領域が必要な場合[上部のナビゲーション](../design/controls-and-patterns/navigationview.md)をサポートします。

* ツリー ビューがサポートするために拡張されて[データ バインディング、項目テンプレート、ドラッグ アンド ドロップします](../design/controls-and-patterns/tree-view.md)。

### <a name="package-support-framework"></a>パッケージのサポート フレームワーク

パッケージのサポートのフレームワークでは、修正プログラムの適用、win32 アプリケーションをソース コードにアクセスできない場合、MSIX コンテナーで実行できるようにするために役立つ、オープン ソースのキットです。

詳しくは、[パッケージのサポートのフレームワークを使用して、MSIX パッケージを適用ランタイムの修正プログラム](../porting/package-support-framework.md)をご覧ください。

## <a name="developer-guidance"></a>開発者向けガイダンス

### <a name="web-api-extensions"></a>Web API の拡張機能

複数のブラウザー間の web 開発向け Mozilla Developer Network ドキュメントには、[従来の Microsoft の API の拡張機能](https://developer.mozilla.org/docs/Web/API/Microsoft_API_extensions)の一覧が追加されました。 これらの API の拡張機能は、Internet Explorer または Microsoft Edge に固有のもの MDN web ドキュメント互換性とブラウザーのサポートに関する既存の情報を補足します。従来の Microsoft [CSS 拡張機能](https://developer.mozilla.org/docs/Web/CSS/Microsoft_Extensions)と[JavaScript の拡張機能](https://developer.mozilla.org/docs/Web/JavaScript/Microsoft_JavaScript_extensions)は、利用可能なもとリッチ web MDN から API 情報の表示で直接見つかります[Visual Studio Code](https://code.visualstudio.com/updates/v1_25#_new-css-pseudo-selectors-and-pseudo-elements-from-mdn) 。

### <a name="cwinrt-code-examples"></a>C++/WinRT のコード例

250 が追加されました[、C++/WinRT](../cpp-and-winrt-apis/index.md)コードで、ドキュメントは、既存の C + に付属するトピックへの登録情報/CX コード例を示します。

### <a name="project-rome"></a>Project Rome

["Rome"プロジェクト ドキュメント](https://docs.microsoft.com/windows/project-rome/)サイトは、機能のアプローチに再編成されました。 これは、ため、開発者、求めているを検索して、任意の機能を実装し、複数のプラットフォーム間で簡単にする必要があります。

## <a name="videos"></a>ビデオ

### <a name="xbox-live-unity-plugin"></a>Xbox Live Unity プラグイン

Unity の Xbox Live プラグインには、Xbox Live への署名、統計情報、フレンド リスト、クラウド ストレージ、およびランキングをタイトルに追加するためのサポートが含まれています。 詳しくは、[ビデオを見る](https://youtu.be/fVQZ-YgwNpY)をし、 [GitHub のパッケージをダウンロード](https://aka.ms/UnityPlugin)を開始するします。

### <a name="one-dev-question"></a>1 つのデベロッパー質問

デベロッパー質問の 1 つのビデオ シリーズ長い Microsoft 開発者は一連の Windows の開発、チームのカルチャと履歴に関する質問について説明します。 お答えした最新の質問を以下に示します。

Raymond Chen:

* [カーネルか確認する方法、ビデオ ドライバーを再起動するタイミング](https://youtu.be/3SNAdyO1l5c)

Larry Osterman:

* [Windows で Burgermaster オブジェクトの背後にあるストーリーとは何ですか。](https://youtu.be/0TDSbyAIvX0)