---
ms.assetid: 333f67f5-f012-4981-917f-c6fd271267c6
description: このケーススタディでは、書店に記載されている情報を基に、LongListSelector にグループ化されたデータを表示する Windows Phone Silverlight アプリを開始します。
title: Silverlight から UWP ケーススタディへの Windows Phone、Bookstore2
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 1d1440bf3cfded6b50eb58feffd322ea484e488a
ms.sourcegitcommit: b52ddecccb9e68dbb71695af3078005a2eb78af1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74260104"
---
# <a name="windowsphone-silverlight-to-uwp-case-study-bookstore2"></a>Silverlight から UWP ケーススタディへの Windows Phone: Bookstore2


このケーススタディは、 [Bookstore1](wpsl-to-uwp-case-study-bookstore1.md)で提供されている情報に基づいています。は、グループ化されたデータを**longlistselector**に表示する Windows Phone Silverlight アプリから始まります。 ビュー モデルでは、**Author** クラスの各インスタンスは、該当する著者によって書かれた書籍のグループを表します。**LongListSelector** では、著者ごとにグループ化された書籍の一覧を表示したり、縮小して著者のジャンプ リストを表示したりすることができます。 ジャンプ リストを使うと、書籍の一覧をスクロールするよりもすばやく移動することができます。 ここでは、アプリを Windows 10 ユニバーサル Windows プラットフォーム (UWP) アプリに移植する手順について説明します。

Visual Studio で Bookstore2Universal\_10 を開いたときに、"Visual Studio 更新プログラムが必要です" というメッセージが表示された場合は、 [Targetplatformversion](w8x-to-uwp-troubleshooting.md)でターゲットプラットフォームのバージョンを設定するための手順に従っ**て   し**ます。

## <a name="downloads"></a>ダウンロード

[Bookstore2WPSL8 Windows Phone Silverlight アプリをダウンロード](https://codeload.github.com/MicrosoftDocs/windows-topic-specific-samples/zip/Bookstore2WPSL8)します。

[Bookstore2Universal\_10 Windows 10 アプリをダウンロード](https://codeload.github.com/MicrosoftDocs/windows-topic-specific-samples/zip/Bookstore2Universal_10)します。

##  <a name="the-windowsphone-silverlight-app"></a>Windows Phone Silverlight アプリ

下の図は、ここで移植するアプリ Bookstore2WPSL8 の外観を示しています。 このアプリでは、著者ごとにグループ化された書籍の **LongListSelector** を縦方向にスクロールします。 このリストを縮小してジャンプ リストを表示し、そこから任意のグループに移動できます。 このアプリには 2 つの重要な機能があります。それらは、グループ化されたデータ ソースを提供するビュー モデルと、そのビュー モデルにバインドされるユーザー インターフェイスです。 ご覧のように、これらの両方の部分は、Silverlight テクノロジ Windows Phone からユニバーサル Windows プラットフォーム (UWP) に簡単に移植できます。

![Bookstore2WPSL8 の外観](images/wpsl-to-uwp-case-studies/c02-01-wpsl-how-the-app-looks.png)

##  <a name="porting-to-a-windows10-project"></a>Windows 10 プロジェクトへの移植

Visual Studio で新しいプロジェクトを作成し、そこへ Bookstore2WPSL8 からファイルをコピーし、コピーしたファイルを新しいプロジェクトに含めるというタスクは、短時間で実行できます。 最初に、"新しいアプリケーション (Windows ユニバーサル)" プロジェクトを新規作成します。 「Bookstore2Universal\_10」という名前を指定します。 これらは、Bookstore2WPSL8 から Bookstore2Universal\_10 にコピーするファイルです。

-   ブックのカバー画像 PNG ファイルが格納されているフォルダーをコピーします (このフォルダーは \\アセット\\カバーイメージ)。 フォルダーをコピーしたら、**ソリューション エクスプローラー**で **[すべてのファイルを表示]** がオンであることを確認します。 コピーしたフォルダーを右クリックし、 **[プロジェクトに含める]** をクリックします。 このコマンドは、ファイルまたはフォルダーをプロジェクトに "含める" ことを意味します。 ファイルやフォルダーをコピーするたびに、**ソリューション エクスプローラー**で **[更新]** をクリックしてから、ファイルまたはフォルダーをプロジェクトに含めます。 コピー先で置き換えるファイルについては、この手順を実行する必要はありません。
-   ビューモデルのソースファイルが格納されているフォルダーをコピーします (このフォルダーは \\ビューモデルです)。
-   MainPage.xaml をコピーして、コピー先のファイルを置き換えます。

App.xaml.cs は、Visual Studio によって Windows 10 プロジェクトに生成されたものを保持できます。

コピーしたソースコードとマークアップファイルを編集し、Bookstore2WPSL8 名前空間への参照を Bookstore2Universal\_10 に変更します。 これをすばやく行うには、 **[フォルダーを指定して置換]** 機能を使います。 ビュー モデルのソース ファイルに含まれている命令型コードでは、移植作業のために次の変更を行う必要があります。

-   `System.ComponentModel.DesignerProperties` を `DesignMode` に変更した後、これに対して **[解決]** コマンドを使います。 `IsInDesignTool` プロパティを削除し、IntelliSense を使って適切なプロパティ名 (`DesignModeEnabled`) を追加します。
-   **に対して**[解決]`ImageSource` コマンドを使います。
-   **に対して**[解決]`BitmapImage` コマンドを使います。
-   `using System.Windows.Media;` と `using System.Windows.Media.Imaging;` を削除します。
-   **Bookstore2Universal\_10. BookstoreViewModel. AppName**プロパティによって返される値を、"" から "Bookstore2Universal" に変更します。
-   「[Bookstore1](wpsl-to-uwp-case-study-bookstore1.md)」の場合と同じように、**BookSku.CoverImage** プロパティの実装を更新します (「[ビュー モデルへの画像のバインド](wpsl-to-uwp-case-study-bookstore1.md)」をご覧ください)。

MainPage.xaml では、初期の移植作業のために次の変更を行う必要があります。

-   `phone:PhoneApplicationPage` を `Page` に変更します (プロパティ要素構文での出現箇所を含みます)。
-   `phone` と `shell` の名前空間のプレフィックス宣言を削除します。
-   その他の名前空間のプレフィックス宣言で、"clr-namespace" を "using" に変更します。
-   `SupportedOrientations="Portrait"` と `Orientation="Portrait"` を削除し、新しいプロジェクトのアプリ パッケージ マニフェストで**縦方向**を構成します。
-   `shell:SystemTray.IsVisible="True"` を削除します。
-   ジャンプ リスト項目コンバーター (マークアップ内にリソースとして含まれています) の種類は、[**Windows.UI.Xaml.Controls.Primitives**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Primitives) 名前空間に移動しています。 そのため、名前空間プレフィックス宣言 Windows\_UI\_Xaml\_コントロール\_プリミティブに追加し、それを**windows**にマップします。 ジャンプ リスト項目コンバーターのリソースで、プレフィックスを `phone:` から `Windows_UI_Xaml_Controls_Primitives:` に変更します。
-   「[Bookstore1](wpsl-to-uwp-case-study-bookstore1.md)」の場合と同じように、`PhoneTextExtraLargeStyle` **TextBlock** スタイルに対するすべての参照を `SubtitleTextBlockStyle` に対する参照に置き換えます。また、`PhoneTextSubtleStyle` を `SubtitleTextBlockStyle` に、`PhoneTextNormalStyle` を `CaptionTextBlockStyle` に、`PhoneTextTitle1Style` を `HeaderTextBlockStyle` に置き換えます。
-   `BookTemplate` には例外が 1 つあります。 2 番目の **TextBlock** のスタイルは、`CaptionTextBlockStyle` を参照している必要があります。
-   **の内部の**TextBlock`AuthorGroupHeaderTemplate` から FontFamily 属性を削除し、**Border** の Background が `SystemControlBackgroundAccentBrush` の代わりに `PhoneAccentBrush` を参照するように設定します。
-   [表示ピクセルに関連する変更](wpsl-to-uwp-porting-xaml-and-ui.md)のため、マークアップ全体を調べて、すべての固定サイズの寸法 (余白、幅、高さなど) を 0.8 倍にする必要があります。

## <a name="replacing-the-longlistselector"></a>LongListSelector の置き換え


**LongListSelector** を [**SemanticZoom**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom) コントロールに置き換えるには、いくつかの手順があります。この手順を始めましょう。 **LongListSelector** はグループ化されたデータ ソースに直接バインドされますが、**SemanticZoom** には [**ListView**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ListView) コントロールや [**GridView**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.GridView) コントロールが含まれており、これらのコントロールは [**CollectionViewSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.CollectionViewSource) アダプターを経由してデータに間接的にバインドされます。 **CollectionViewSource** はマークアップ内にリソースとして含まれている必要があります。そのため、最初にこの項目を MainPage.xaml の `<Page.Resources>` 内にあるマークアップに追加します。

```xml
    <CollectionViewSource
        x:Name="AuthorHasACollectionOfBookSku"
        Source="{Binding Authors}"
        IsSourceGrouped="true"/>
```

**LongListSelector.ItemsSource** のバインディングは **CollectionViewSource.Source** の値になり、**LongListSelector.IsGroupingEnabled** は **CollectionViewSource.IsSourceGrouped** になることに注意してください。 **CollectionViewSource** には名前 (キーではないので注意してください) があるので、この名前に対してバインドすることができます。

次に、`phone:LongListSelector` をこのマークアップに置き換えます。これにより、暫定的な **SemanticZoom** が機能します。

```xml
    <SemanticZoom>
        <SemanticZoom.ZoomedInView>
            <ListView
                ItemsSource="{Binding Source={StaticResource AuthorHasACollectionOfBookSku}}"
                ItemTemplate="{StaticResource BookTemplate}">
                <ListView.GroupStyle>
                    <GroupStyle
                        HeaderTemplate="{StaticResource AuthorGroupHeaderTemplate}"
                        HidesIfEmpty="True"/>
                </ListView.GroupStyle>
            </ListView>
        </SemanticZoom.ZoomedInView>
        <SemanticZoom.ZoomedOutView>
            <ListView
                ItemsSource="{Binding CollectionGroups, Source={StaticResource AuthorHasACollectionOfBookSku}}"
                ItemTemplate="{StaticResource ZoomedOutAuthorTemplate}"/>
        </SemanticZoom.ZoomedOutView>
    </SemanticZoom>
```

**LongListSelector** でのフラット リスト モードとジャンプ リスト モードに関する概念は、**SemanticZoom** での拡大表示と縮小表示に関する概念にそれぞれ対応しています。 拡大表示はプロパティであり、そのプロパティを **ListView** のインスタンスに設定します。 この場合、縮小表示も **ListView** に設定され、両方の **ListView** コントロールが **CollectionViewSource** にバインドされます。 拡大表示では、**LongListSelector** のフラット リストで使われているものと同じ項目テンプレート、グループ ヘッダー テンプレート、および **HideEmptyGroups** 設定 (現在は **HidesIfEmpty** という名前) が使われます。 縮小表示では、**LongListSelector** のジャンプ リストのスタイル (`AuthorNameJumpListStyle`) に含まれているものと類似した項目テンプレートが使われます。 また、縮小表示は **CollectionViewSource** の特殊なプロパティ (**CollectionGroups**) にバインドされていることにも注意してください。このプロパティは、項目ではなくグループを含んでいるコレクションを表しています。

`AuthorNameJumpListStyle` は不要になりました (ただしすべてが不要になったわけではありません)。 縮小表示ビューで必要となるのは、グループ (このアプリでは著者) のデータ テンプレートだけです。 ここでは、`AuthorNameJumpListStyle` スタイルを削除し、このスタイルを次のデータ テンプレートに置き換えます。

```xml
   <DataTemplate x:Key="ZoomedOutAuthorTemplate">
        <Border Margin="9.6,0.8" Background="{Binding Converter={StaticResource JumpListItemBackgroundConverter}}">
            <TextBlock Margin="9.6,0,9.6,4.8" Text="{Binding Group.Name}" Style="{StaticResource SubtitleTextBlockStyle}"
            Foreground="{Binding Converter={StaticResource JumpListItemForegroundConverter}}" VerticalAlignment="Bottom"/>
        </Border>
    </DataTemplate>
```

このデータ テンプレートのデータ コンテキストは、項目ではなくグループであるため、**Group** という名前の特殊なプロパティにバインドすることに注意してください。

これで、アプリをビルドして実行できるようになりました。 モバイル エミュレーターでは次のように表示されます。

![最初のソース コードの変更を加えたモバイルの UWP アプリ](images/wpsl-to-uwp-case-studies/c02-02-mob10-initial-source-code-changes.png)

ビュー モデル、拡大表示、縮小表示は適切に連携しますが、スタイル設定やテンプレート化の作業を必要とする問題があります。 たとえば、正しいスタイルとブラシがまだ使用されていないので、クリックするとグループヘッダーのテキストが非表示になり、ズームアウトすることができます。デスクトップデバイスでアプリを実行すると、2つ目の問題が表示されます。これは、アプリがユーザーインターフェイスを調整して、最適なエクスペリエンスを提供し、windows がモバイルデバイスの画面よりもはるかに大きくなる可能性がある大規模なデバイスの領域を使用するようにしていないことを示します。 次のセクション (「[最初のスタイル設定とテンプレート化](#initial-styling-and-templating)」、「[アダプティブ UI](#adaptive-ui)」、「[最終的なスタイル設定](#final-styling)」) では、これらの問題に対処します。

## <a name="initial-styling-and-templating"></a>最初のスタイル設定とテンプレート化

適切な間隔でグループ ヘッダーを配置するには、`AuthorGroupHeaderTemplate` を編集し、**Border** で `"0,0,0,9.6"`Margin**を** に設定します。

適切な間隔で書籍項目を配置するには、`BookTemplate` を編集し、両方の **TextBlock** で `"9.6,0"`Margin**を** に設定します。

アプリ名とページ タイトルのレイアウトを向上させるには、`TitlePanel` 内で、2 番目の **TextBlock** の上余白を削除します。そのためには、**Margin** の値を `"7.2,0,0,0"` に設定します。 また、`TitlePanel` 自体で、余白を `0` (または適切な外観になる任意の値) に設定します。

`LayoutRoot` の Background を `"{ThemeResource ApplicationPageBackgroundThemeBrush}"` に変更します。

## <a name="adaptive-ui"></a>アダプティブ UI

Phone アプリを基にして作業を開始したため、この段階のプロセスでは、移植したアプリの UI レイアウトが小型のデバイスや狭いウィンドウにのみ適したレイアウトになっているのは当然です。 実現しようとしている UI レイアウトは、アプリを幅の広いウィンドウで実行しているとき (大型画面を備えたデバイスの場合) には自動的に調整して広い領域を活用し、アプリのウィンドウが狭い場合 (小型のデバイスが該当しますが、大型のデバイスの場合もあります) は現在の UI のみを使うレイアウトです。

これを実現するために、アダプティブな Visual State Manager 機能を使うことができます。 現在使っているテンプレートを利用して、既定で UI が幅の狭い状態でレイアウトされるように、視覚要素のプロパティを設定します。 その後で、アプリのウィンドウ幅が特定のサイズ以上になる状況を確認します (このサイズは[有効ピクセル](wpsl-to-uwp-porting-xaml-and-ui.md)の単位で測定します)。また、より大きなレイアウトやより幅の広いレイアウトを実現できるように、視覚要素のプロパティを変更します。 これらのプロパティの変更を表示状態として設定し、アダプティブなトリガーを使って、有効ピクセル単位のウィンドウ幅に応じて、その表示状態を適用するかどうかを継続的に監視し判断します。 この場合はウィンドウの幅でトリガーしていますが、ウィンドウの高さでトリガーすることもできます。

この使用事例では、ウィンドウの最小幅は 548 epx が適しています。これは、最も小型のデバイスで幅の広いレイアウトを表示する際に適したサイズであるためです。 通常、電話は 548 epx よりも小さいため、電話のような小型のデバイスでは既定の幅の狭いレイアウトをそのまま使います。 PC の既定では、ワイド状態への切り替えをトリガーできる十分な幅でウィンドウが開き、250 x 250 サイズの項目が表示されます。 この状態でウィンドウをドラッグして、250 x 250 サイズの項目を最低 2 列分は表示できる幅の狭いウィンドウにすることができます。 これよりも幅を狭くすると、トリガーが非アクティブ化されます。これにより、幅の広い表示状態が削除され、既定の幅の狭いレイアウトが有効になります。

アダプティブな Visual State Manager で作業する前に、まずワイド状態を設計する必要があります。つまり、マークアップに新しい視覚要素とテンプレートを追加することを意味します。 次の手順でその方法を説明します。 視覚要素およびテンプレートの命名規則として、ワイド状態用のすべての要素やテンプレートには、"wide" という単語を含めます。 要素またはテンプレートの名前に "wide" という単語が含まれていない場合、狭い状態の要素やテンプレートであると見なすことができます。これは、既定の状態であり、そのプロパティ値はページ内の視覚要素のローカル値として設定されます。 ワイド状態のプロパティ値のみが、マークアップ内の実際の表示状態によって設定されます。

-   マークアップ内の [**SemanticZoom**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom) コントロールのコピーを作成し、そのコピーで `x:Name="narrowSeZo"` を設定します。 元のコントロールでは、`x:Name="wideSeZo"` を設定し、既定ではワイド状態が表示されないように `Visibility="Collapsed"` も設定します。
-   `wideSeZo` で、拡大表示と縮小表示の両方の **ListView** を **GridView** に変更します。
-   3 つのリソース `AuthorGroupHeaderTemplate`、`ZoomedOutAuthorTemplate`、`BookTemplate` のコピーを作成し、コピーのキーに `Wide` という単語を追加します。 また、これらの新しいリソースのキーを参照するように、`wideSeZo` を更新します。
-   `AuthorGroupHeaderTemplateWide` の内容を `<TextBlock Style="{StaticResource SubheaderTextBlockStyle}" Text="{Binding Name}"/>` に置き換えます。
-   `ZoomedOutAuthorTemplateWide` の内容を次のように置き換えます。

```xml
    <Grid HorizontalAlignment="Left" Width="250" Height="250" >
        <Border Background="{StaticResource ListViewItemPlaceholderBackgroundThemeBrush}"/>
        <StackPanel VerticalAlignment="Bottom" Background="{StaticResource ListViewItemOverlayBackgroundThemeBrush}">
          <TextBlock Foreground="{StaticResource ListViewItemOverlayForegroundThemeBrush}"
              Style="{StaticResource SubtitleTextBlockStyle}"
            Height="80" Margin="15,0" Text="{Binding Group.Name}"/>
        </StackPanel>
    </Grid>
```

-   `BookTemplateWide` の内容を次のように置き換えます。

```xml
    <Grid HorizontalAlignment="Left" Width="250" Height="250">
        <Border Background="{StaticResource ListViewItemPlaceholderBackgroundThemeBrush}"/>
        <Image Source="{Binding CoverImage}" Stretch="UniformToFill"/>
        <StackPanel VerticalAlignment="Bottom" Background="{StaticResource ListViewItemOverlayBackgroundThemeBrush}">
            <TextBlock Style="{StaticResource SubtitleTextBlockStyle}"
                Foreground="{StaticResource ListViewItemOverlaySecondaryForegroundThemeBrush}"
                TextWrapping="NoWrap" TextTrimming="CharacterEllipsis"
                Margin="12,0,24,0" Text="{Binding Title}"/>
            <TextBlock Style="{StaticResource CaptionTextBlockStyle}" Text="{Binding Author.Name}"
                Foreground="{StaticResource ListViewItemOverlaySecondaryForegroundThemeBrush}" TextWrapping="NoWrap"
                TextTrimming="CharacterEllipsis" Margin="12,0,12,12"/>
        </StackPanel>
    </Grid>
```

-   ワイド状態では、拡大表示のグループ間の垂直方向の間隔を大きくする必要があります。 項目パネル テンプレートを作成し参照することで、必要な結果を得ることができます。 マークアップは次のようになります。

```xml
   <ItemsPanelTemplate x:Key="ZoomedInItemsPanelTemplate">
        <ItemsWrapGrid Orientation="Horizontal" GroupPadding="0,0,0,20"/>
    </ItemsPanelTemplate>
    ...

    <SemanticZoom x:Name="wideSeZo" ... >
        <SemanticZoom.ZoomedInView>
            <GridView
            ...
            ItemsPanel="{StaticResource ZoomedInItemsPanelTemplate}">
            ...
```

-   最後に、適切な Visual State Manager のマークアップを `LayoutRoot` の最初の子として追加します。

```xml
    <Grid x:Name="LayoutRoot" ... >
        <VisualStateManager.VisualStateGroups>
            <VisualStateGroup>
                <VisualState x:Name="WideState">
                    <VisualState.StateTriggers>
                        <AdaptiveTrigger MinWindowWidth="548"/>
                    </VisualState.StateTriggers>
                    <VisualState.Setters>
                        <Setter Target="wideSeZo.Visibility" Value="Visible"/>
                        <Setter Target="narrowSeZo.Visibility" Value="Collapsed"/>
                    </VisualState.Setters>
                </VisualState>
            </VisualStateGroup>
        </VisualStateManager.VisualStateGroups>

    ...
```

## <a name="final-styling"></a>最終的なスタイル設定

残りの作業は、スタイルの最終的な調整です。

-   `AuthorGroupHeaderTemplate` で、`Foreground="White"`TextBlock**に対して** を設定します。これにより、モバイル デバイス ファミリで実行したときに適切に表示されます。
-   `FontWeight="SemiBold"` と  **の両方で、** TextBlock`AuthorGroupHeaderTemplate` に `ZoomedOutAuthorTemplate` を追加します。
-   `narrowSeZo`で、縮小表示ビューでのグループ ヘッダーと著者は、伸縮表示ではなく左揃えで表示されます。ここではその設定を行います。 [  **HorizontalContentAlignment**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.groupstyle.headercontainerstyle) を [ に設定して、拡大表示ビュー用のHeaderContainerStyle](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.horizontalcontentalignment)`Stretch` を作成します。 次に、同じ [**Setter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemcontainerstyle) を含む、縮小表示ビュー用の [**ItemContainerStyle**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Setter) を作成します。 結果は次のようになります。

```xml
   <Style x:Key="AuthorGroupHeaderContainerStyle" TargetType="ListViewHeaderItem">
        <Setter Property="HorizontalContentAlignment" Value="Stretch"/>
    </Style>

    <Style x:Key="ZoomedOutAuthorItemContainerStyle" TargetType="ListViewItem">
        <Setter Property="HorizontalContentAlignment" Value="Stretch"/>
    </Style>

    ...

    <SemanticZoom x:Name="narrowSeZo" ... >
        <SemanticZoom.ZoomedInView>
            <ListView
            ...
                <ListView.GroupStyle>
                    <GroupStyle
                    ...
                    HeaderContainerStyle="{StaticResource AuthorGroupHeaderContainerStyle}"
                    ...
        <SemanticZoom.ZoomedOutView>
            <ListView
                ...
                ItemContainerStyle="{StaticResource ZoomedOutAuthorItemContainerStyle}"
                ...
```

スタイル設定操作の最後のシーケンスで、アプリの外観は次のようになります。

![デスクトップ デバイスで動作中の、移植された Windows 10 アプリ (2 つのサイズのウィンドウによる拡大表示)](images/w8x-to-uwp-case-studies/c02-07-desk10-zi-ported.png)

デスクトップデバイスで実行されている移植された Windows 10 アプリ、拡大ビュー、2つのサイズのウィンドウ  
![デスクトップデバイスで実行される移植された windows 10 アプリ、縮小表示ビュー、2つのサイズのウィンドウ](images/w8x-to-uwp-case-studies/c02-08-desk10-zo-ported.png)

デスクトップデバイスで実行される移植された Windows 10 アプリ、ズームアウトビュー、ウィンドウの2つのサイズ

![モバイル デバイスで動作中の、移植された Windows 10 アプリ (拡大表示)](images/w8x-to-uwp-case-studies/c02-09-mob10-zi-ported.png)

モバイルデバイスで実行されている移植された Windows 10 アプリ (拡大表示)

![モバイル デバイスで動作中の、移植された Windows 10 アプリ (縮小表示)](images/w8x-to-uwp-case-studies/c02-10-mob10-zo-ported.png)

モバイルデバイスで実行されている移植された Windows 10 アプリ (縮小表示)

## <a name="making-the-view-model-more-flexible"></a>ビュー モデルの柔軟性の向上

このセクションでは、UWP を使うようにアプリを移行することによって利用可能になる機能の例を紹介します。 ここでは、**CollectionViewSource** を使ってアクセスするときにビュー モデルの柔軟性を向上させるために実行できるオプションの手順について説明します。 ビューモデル (ソースファイルは、モデルビュー\\BookstoreViewModel.cs) で Windows Phone Silverlight アプリから移植されています。このクラスには、 **List&lt;t&gt;** ( **t**は booksku) から派生した Author というクラスが含まれています。 これは、Author クラスが BookSku の*グループである*ことを意味します。

**CollectionViewSource.Source** を Authors にバインドするとき、Authors 内の各 Author が*何か*のグループであるということを伝える必要があります。 このケース スタディでは、**CollectionViewSource** に依存して、Author が BookSku のグループであることを特定しています。 この設定でも機能しますが、柔軟性はありません。 Author が BookSku のグループ*および*著者の住所のグループの*両方*を表す必要がある場合は、どうしたらよいでしょうか。 Author を、これらの両方のグループにすることは*できません*。 ただし、Author に任意の数のグループを*保持させる*ことはできます。 これが解決策となります。つまり、現在使っている "*グループである*" というパターンの代わりに、またはこのパターンに加えて、"*グループを保持する*" というパターンを使います。 以下にその方法を示します。

-   Author が **List&lt;T&gt;** から派生しないように変更します。
-   このフィールドをに追加します。 
-   このプロパティをに追加します。 
-   当然ですが、上の 2 つの手順を繰り返して、必要な数のグループを Author に追加できます。
-   AddBookSku メソッドの実装を `this.BookSkus.Add(bookSku);` に変更します。
-   これで、Author は少なくとも 1 つのグループを*保持する*ようになりました。また、**CollectionViewSource** に対して、どのグループを使うかを伝える必要があります。 そのためには、**CollectionViewSource** に `ItemsPath="BookSkus"` プロパティを追加します。

これらの変更を行っても、このアプリの機能は変更されません。ここでは、必要に応じて Author と **CollectionViewSource** を拡張する方法を理解してください。 Author に対して最後の変更を加えましょう。この変更により、*CollectionViewSource.ItemsPath* を指定**しないで** Author を使う場合に、選んだ既定のグループが使われるようになります。

```csharp
    public class Author : IEnumerable<BookSku>
    {
        ...

        public IEnumerator<BookSku> GetEnumerator()
        {
            return this.BookSkus.GetEnumerator();
        }
        System.Collections.IEnumerator System.Collections.IEnumerable.GetEnumerator()
        {
            return this.BookSkus.GetEnumerator();
        }
    }
```

これで、アプリが同じように動作を続ける場合は、必要に応じて `ItemsPath="BookSkus"` を削除できます。

## <a name="conclusion"></a>まとめ

このケース スタディには、前のケース スタディよりも複雑なユーザー インターフェイスが関連しています。 Windows Phone Silverlight **Longlistselector**のすべての機能と概念は、 **SemanticZoom**、 **ListView**、 **GridView**、および**collectionviewsource**という形式の UWP アプリで使用できることがわかりました。 UWP アプリで命令型コードやマークアップの両方を再利用 (コピーと編集) して、最小および最大の Windows デバイスのフォーム ファクターや、その中間のあらゆるサイズに合わせて調整された機能、UI、および操作を実現する方法について説明しました。
