---
title: Windows ランタイム 8.x から UWP へのケース スタディ - Bookstore1
ms.assetid: e4582717-afb5-4cde-86bb-31fb1c5fc8f3
description: このトピックでは、非常に単純なユニバーサル8.1 アプリを Windows 10 ユニバーサル Windows プラットフォーム (UWP) アプリに移植するケーススタディについて説明します。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: ecbc4d3fcdff9d06469e7a274fd56ef453a81e02
ms.sourcegitcommit: b52ddecccb9e68dbb71695af3078005a2eb78af1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74260130"
---
# <a name="windows-runtime-8x-to-uwp-case-study-bookstore1"></a>Windows ランタイム 8.x から UWP へのケース スタディ - Bookstore1


このトピックでは、非常に単純なユニバーサル8.1 アプリを Windows 10 ユニバーサル Windows プラットフォーム (UWP) アプリに移植するケーススタディについて説明します。 ユニバーサル8.1 アプリとは、Windows 8.1 用の1つのアプリパッケージと Windows Phone 8.1 用の別のアプリケーションパッケージを作成するアプリです。 Windows 10 では、顧客がさまざまなデバイスにインストールできる1つのアプリパッケージを作成できます。これは、このケーススタディで実行します。 「[UWP アプリのガイド](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)」をご覧ください。

移植するアプリは、ビュー モデルにバインドされた **ListBox** で構成されます。 ビュー モデルにはタイトル、著者、表紙を示す書籍の一覧が含まれます。 表紙画像では、 **[ビルド アクション]** が **[コンテンツ]** に設定され、 **[出力ディレクトリにコピー]** が **[コピーしない]** に設定されています。

このセクションの前のトピックでは、プラットフォーム間の違いについて説明し、ビュー モデルへのバインドを通じて、データへのアクセスに至るまで、XAML マークアップからのアプリのさまざまな要素に対する移植プロセスの詳細とガイダンスを提供しました。 ケース スタディでは、実際の例が動作するようすを示すことにより、このガイダンスを補足することを目的としています。 ケース スタディは、ガイダンスを読み終わっていることを前提としているため、繰り返し説明することはありません。

Visual Studio で Bookstore1Universal\_10 を開いたときに、"Visual Studio 更新プログラムが必要です" というメッセージが表示された場合は、 [Targetplatformversion](w8x-to-uwp-troubleshooting.md)の手順に従っ**て   ます**。

## <a name="downloads"></a>ダウンロード

[Bookstore1\_81 Universal 8.1 アプリをダウンロード](https://codeload.github.com/MicrosoftDocs/windows-topic-specific-samples/zip/Bookstore1_81)します。

[Bookstore1Universal\_10 Windows 10 アプリをダウンロード](https://codeload.github.com/MicrosoftDocs/windows-topic-specific-samples/zip/Bookstore1Universal_10)します。

## <a name="the-universal-81-app"></a>ユニバーサル 8.1 アプリ

ここでは、Bookstore1\_81 (ポートに送信されるアプリ) を示します。 これは、アプリ名とページ タイトルの見出しの下に、縦方向にスクロールする書籍のリスト ボックスを示すシンプルなアプリです。

![bookstore1\-81 が windows 上でどのように見えるか](images/w8x-to-uwp-case-studies/c01-01-win81-how-the-app-looks.png)

Windows 上の Bookstore1\_81

![windows phone での bookstore1\-81 の検索方法](images/w8x-to-uwp-case-studies/c01-02-wp81-how-the-app-looks.png)

Windows Phone での Bookstore1\_81

##  <a name="porting-to-a-windows10-project"></a>Windows 10 プロジェクトへの移植

Bookstore1\_81 ソリューションは、8.1 ユニバーサルアプリプロジェクトであり、これらのプロジェクトが含まれています。

-   Bookstore1\_81. Windows。 これは、Windows 8.1 用のアプリケーションパッケージをビルドするプロジェクトです。
-   Bookstore1\_81. Appname.windowsphone。 これは、Windows Phone 8.1 用アプリ パッケージを構築するプロジェクトです。
-   Bookstore1\_81。 これは、他の 2 つのプロジェクトの両方で使われるソース コード、マークアップ ファイル、および他のアセットやリソースを含むプロジェクトです。

このケース スタディでは、サポートするデバイスに関して、「[ユニバーサル 8.1 アプリがある場合](w8x-to-uwp-root.md)」で説明した通常のオプションを使います。 ここでの決定は単純なものです。このアプリには同じ機能があり、ほとんどの場合、Windows 8.1 と Windows Phone 8.1 の両方の形式で同じコードが使用されます。 そのため、共有プロジェクト (および他のプロジェクトから必要な他のプロジェクト) の内容を、ユニバーサルデバイスファミリを対象とする Windows 10 (最も広範なデバイスにインストール可能) に移植します。

これは、Visual Studio で新しいプロジェクトを作成し、Bookstore1\_81 からファイルをコピーし、コピーしたファイルを新しいプロジェクトに含める、非常に簡単なタスクです。 最初に、"新しいアプリケーション (Windows ユニバーサル)" プロジェクトを新規作成します。 「Bookstore1Universal\_10」という名前を指定します。 これらは、Bookstore1\_81 から Bookstore1Universal\_10 にコピーするファイルです。

**共有プロジェクトから**

-   ブックのカバー画像 PNG ファイルが格納されているフォルダーをコピーします (このフォルダーは \\アセット\\カバーイメージ)。 フォルダーをコピーしたら、**ソリューション エクスプローラー**で **[すべてのファイルを表示]** がオンであることを確認します。 コピーしたフォルダーを右クリックし、 **[プロジェクトに含める]** をクリックします。 このコマンドは、ファイルまたはフォルダーをプロジェクトに "含める" ことを意味します。 ファイルやフォルダーをコピーするたびに、**ソリューション エクスプローラー**で **[更新]** をクリックしてから、ファイルまたはフォルダーをプロジェクトに含めます。 コピー先で置き換えるファイルについては、この手順を実行する必要はありません。
-   ビューモデルのソースファイルが格納されているフォルダーをコピーします (このフォルダーは \\ビューモデルです)。
-   MainPage.xaml をコピーして、コピー先のファイルを置き換えます。

**Windows プロジェクトから**

-   BookstoreStyles.xaml をコピーします。 このファイル内のすべてのリソースキーは Windows 10 アプリで解決されるため、この方法をお勧めします。同等の Appname.windowsphone ファイルには含まれません。

コピーしたソースコードとマークアップファイルを編集し、Bookstore1\_81 名前空間への参照を Bookstore1Universal\_10 に変更します。 これをすばやく行うには、 **[フォルダーを指定して置換]** 機能を使います。 ビュー モデルでも、その他の命令型コードでも、コードを変更する必要はありません。 しかし、どのバージョンのアプリが実行されているかを簡単に確認できるように、 **Bookstore1Universal\_10. BookstoreViewModel. AppName** 81\_プロパティによって返される値を "Bookstore1Universal\_10" に変更します。

これで、ビルドして実行することができます。 ここでは、Windows 10 に移植するための明示的な作業がまだ行われていない場合の新しい UWP アプリの外観について説明します。

![最初のソース コードの変更を加えた Windows 10 アプリ](images/w8x-to-uwp-case-studies/c01-03-desk10-initial-source-code-changes.png)

デスクトップデバイスで実行されている最初のソースコードの変更を含む Windows 10 アプリ

![最初のソース コードの変更を加えた Windows 10 アプリ](images/w8x-to-uwp-case-studies/c01-04-mob10-initial-source-code-changes.png)

モバイルデバイスで実行されている最初のソースコードの変更を含む Windows 10 アプリ

ビューおよびビュー モデルは、適切に連携しており、**ListBox** が機能しています。 修正が必要なのは、スタイル設定だけです。 淡色テーマのモバイル デバイスでは、リスト ボックスの境界線が表示されますが、これは、簡単に非表示にすることができます。 そして、文字体裁が大きすぎるため、ここで使うスタイルを変更します。 また、既定のような外観にしたい場合は、デスクトップ デバイスでの実行時のアプリの色を淡色にする必要があります。 では、それを変更しましょう。

## <a name="universal-styling"></a>ユニバーサル スタイル設定

Bookstore1\_81 アプリでは、2つの異なるリソースディクショナリ (BookstoreStyles .xaml) を使用して、そのスタイルを Windows 8.1 と Windows Phone 8.1 オペレーティングシステムに合わせて調整しています。 これら2つの BookstoreStyles .xaml ファイルには、Windows 10 アプリに必要なスタイルが完全に含まれていません。 ただし、さいわいなことに、目的としているのは、そのどちらよりもはるかに単純なスタイルです。 したがって、以降の手順で行うのはほとんど、プロジェクト ファイルとマークアップの削除と簡素化の作業です。 手順は次のとおりです。 このトピックの上部にあるリンクを使用して、プロジェクトをダウンロードし、この時点とケース スタディの終了時の間のすべての変更の結果を参照できます。

-   項目間のスペースを縮めるために、MainPage.xaml で `BookTemplate` データ テンプレートを探し、`Margin="0,0,0,8"` をルートの **Grid** から削除します。
-   また、`BookTemplate` には、`BookTemplateTitleTextBlockStyle` と `BookTemplateAuthorTextBlockStyle` への参照があります。 Bookstore1\_81 では、これらのキーを間接参照として使用して、1つのキーが2つのアプリで異なる実装を持つようにしました。 その間接参照は、必要ではなくなりました。システム スタイルを直接参照できます。 そこで、これらの参照をそれぞれ、`TitleTextBlockStyle` と `SubtitleTextBlockStyle` で置き換えます。
-   ここで、`LayoutRoot` の Background を適切な既定値に設定して、テーマが何であるかに関係なく、すべてのデバイスでの実行時にアプリが適切に表示されるようにする必要があります。 これを、`"Transparent"` から `"{ThemeResource ApplicationPageBackgroundThemeBrush}"` に変更します。
-   `TitlePanel` で、`TitleTextBlockStyle` (今では少し大きすぎる) への参照を `CaptionTextBlockStyle` への参照に変更します。 `PageTitleTextBlockStyle` はもう1つの Bookstore1\_81 を間接的に必要としません。 これは、代わりに `HeaderTextBlockStyle` を参照するように変更します。
-   **ListBox** で特別な Background、Style、ItemContainerStyle を設定する必要はなくなったので、この 3 つの属性とその値をマークアップから削除します。 ただし、**ListBox** の境界線を非表示にする必要があるため、これに `BorderBrush="{x:Null}"` を追加します。
-   BookstoreStyles.xaml (**ResourceDictionary** ファイル) 内のリソースはすべて、参照されなくなります。 これらのリソースはすべて削除できます。 ただし、BookstoreStyles.xaml ファイル自体を削除しないでください。次のセクションで示すように、まだ、最後の用途があります。

スタイル設定操作の最後のシーケンスで、アプリの外観は次のようになります。

![ほとんどの移植が行われた Windows 10 アプリ](images/w8x-to-uwp-case-studies/c01-05-desk10-almost-ported.png)

デスクトップデバイスで実行されているほぼ移植された Windows 10 アプリ

![ほとんどの移植が行われた Windows 10 アプリ](images/w8x-to-uwp-case-studies/c01-06-mob10-almost-ported.png)

モバイルデバイスで実行されているほぼ移植された Windows 10 アプリ

## <a name="an-optional-adjustment-to-the-list-box-for-mobile-devices"></a>モバイル デバイス向けのリスト ボックスの調整 (オプション)

モバイル デバイスでのアプリの実行中には、両方のテーマで既定で、リスト ボックスの背景は淡色です。 このスタイルを使うことができます。使う場合は、整理以外の作業はありません。つまり、BookstoreStyles.xaml リソース ディクショナリ ファイルと、それを MainPage.xaml にマージするマークアップをプロジェクトから削除するだけです。

コントロールは、動作に影響を及ぼすことなく、表示形式をカスタマイズできるように設計されています。 元のアプリの外観のように、濃色のテーマでリスト ボックスを濃色にする場合は、次のセクションで説明する方法をご覧ください。

変更をアプリに反映させる必要があるのは、モバイル デバイスでアプリを実行するときだけです。 したがって、モバイル デバイス ファミリで実行するときには、わずかにカスタマイズしたリスト ボックスのスタイルを使い、それ以外のすべてのデバイスで実行するときには、既定のスタイルを引き続き使います。 これを行うには、BookstoreStyles.xaml のコピーを作成し、それに、特別な MRT 修飾名を付けて、モバイル デバイスでのみ読み込まれるようにします。

新しい **ResourceDictionary** プロジェクト項目を追加し、BookstoreStyles.DeviceFamily-Mobile.xaml という名前を付けます。 これで、両方の論理名が BookstoreStyles.xaml (これが、マークアップとコードで使用する名前です) である 2 つのファイルができました。 ただし、これらのファイルの物理名は異なっているため、異なるマークアップを含めることができます。 この MRT 修飾名の名前付けスキームは、どの xaml ファイルでも使用できますが、同じ論理名を持つすべての xaml ファイルは、1 つの xaml.cs 分離コード ファイルを共有することに注意してください (この場合、適用されるのは 1 つです)。

リスト ボックスのコントロール テンプレートのコピーを編集し、新しいリソース ディクショナリである BookstoreStyles.DeviceFamily Mobile.xaml 内の `BookstoreListBoxStyle` キーで保存します。 今度は、setter のうち、3 つに単純な変更を加えます。

-   Foreground setter で、値を `"{x:Null}"` に変更します。 プロパティを要素で直接、`"{x:Null}"` に設定することは、コードで `null` に設定することと同じであることに注意してください。 ただし、`"{x:Null}"` の値を setter で使うと、独自の効果があります。既定のスタイルで (同じプロパティの) setter がオーバーライドされ、ターゲット要素でプロパティの既定値が復元されます。
-   Background setter で、値を `"Transparent"` に変更して、その淡色の背景を削除します。
-   Template setter で、`Focused` という名前の表示状態を見つけ、そのストーリー ボードを削除して空のタグにします。
-   その他のすべての setter をマークアップから削除します。

最後に、`BookstoreListBoxStyle` を BookstoreStyles.xaml にコピーし、その 3 つの setter を削除して、空のタグにします。 このようにすると、モバイル以外のデバイスで、BookstoreStyles.xaml と `BookstoreListBoxStyle` への参照が解決されますが、その影響はありません。

![移植された Windows 10 アプリ](images/w8x-to-uwp-case-studies/c01-07-mob10-ported.png)

モバイルデバイスで実行されている移植された Windows 10 アプリ

## <a name="conclusion"></a>まとめ

このケース スタディでは、非常に単純なアプリ (実在しないと考えらえる単純なアプリ) を移植するプロセスを示しました。 たとえば、リスト ボックスは、選択を行ったり、ナビゲーションのコンテキストを確立したりするときに使うことができます。アプリは、タップされた項目に関する詳細を提示するページに移動します。 この特定のアプリは、ユーザーの選択に対して何も処理せず、またナビゲーション機能がありません。 それでも、このケース スタディは、まず移植プロセスを導入し、実際の UWP  アプリで使うことができる重要な手法をデモする役割を果たします。

また、新しいビュー モデルを移行することは、概してスムーズなプロセスであることを確認しました。 ただし、ユーザー インターフェイスや、フォーム ファクターのサポートは、移植する際に注意が必要と考えられる項目です。

次のケース スタディは「[Bookstore2](w8x-to-uwp-case-study-bookstore2.md)」です。ここでは、グループ化されたデータへのアクセスと表示について説明します。
