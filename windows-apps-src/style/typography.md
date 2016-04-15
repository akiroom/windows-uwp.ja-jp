---
Description: 言語の視覚的な表現として、文字体裁の主な役割は明確であることです。 スタイルによってその目的が邪魔されてはなりません。 ただし、文字体裁にはレイアウト コンポーネントとしての重要な役割もあり、そのデザインの密度と複雑さに強い影響を与え、そのデザインのユーザー エクスペリエンスにも影響します。 
title: 文字体裁
ms.assetid: ca35f78a-e4da-423d-9f5b-75896e0b8f82
label: Typography
template: detail.hbs
extraBodyClass: style-typography
brief: As the visual representation of language, typography’s main task is to be clear. Its style should never get in the way of that goal. But typography also has an important role as a layout component—with a powerful effect on the density and complexity of the design—and on the user’s experience of that design.
---

# UWP アプリの文字体裁

言語の視覚的な表現として、文字体裁の主な役割は明確であることです。 スタイルによってその目的が邪魔されてはなりません。 ただし、文字体裁にはレイアウト コンポーネントとしての重要な役割もあり、そのデザインの密度と複雑さに強い影響を与え、そのデザインのユーザー エクスペリエンスにも影響します。

## 書体

すべての Microsoft デジタル デザインで使う書体として Segoe UI が選択されました。 Segoe UI には多くの文字が用意されており、さまざまなサイズとピクセル密度で最適な読みやすさが維持されるように設計されています。 システムのコンテンツを補完する、きれいで明るくオープンな美しさを備えています。

![Segoe UI フォントのサンプル テキスト](images/segoe-sample.png)

## 太さ

Microsoft では、シンプルさと効率性を考慮に入れて文字体裁に取り組んでいます。 1 つの書体、最小限の太さとサイズ、明確な階層構造を使うことを選択しました。 配置と位置合わせは、各言語の既定のスタイルに従います。 英語では、文字が左から右、上から下へと進みます。 テキストと画像の関係は、明確で直接的です。

![サポートされるフォントの太さを示します。 ライト、セミ ライト、レギュラー、セミ ボールド、ボールド](images/weights.png)

## 行間

![行間 125% の例](images/line-spacing.png)

行間はフォント サイズの 125% で計算し、必要に応じて 4 の倍数の近似値に丸めてください。 たとえば 15 ピクセルの Segoe UI の場合、15 ピクセルの 125% は 18.75 ピクセルです。 4 ピクセル グリッドが維持されるように、行の高さを 20 ピクセルに切り上げて設定することをお勧めします。 これにより、読みやすくなり、発音区分符のスペースが十分確保されます。 具体的な例については、以下の「書体見本」をご覧ください。

小さい書体の上に大きい書体を重ねる場合、大きい書体の最後のベースラインから小さい書体の最初のベースラインまでの距離が、大きい書体の行の高さと等しくなるようにしてください。

![大きい書体を小さい書体に重ねる方法を示します。](images/line-height-stacking.png)

XAML では、これは 2 つの [TextBlocks](https://msdn.microsoft.com/en-us/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) を重ね、適切な余白を設定することで実現できます。

```xaml
<StackPanel Width="200">
    <!-- Setting a bottom margin of 3px on the header
         puts the baseline of the body text exactly 24px
         below the baseline of the header. 24px is the
         recommended line height for a 20px font size,
         which is what's set in SubtitleTextBlockStyle.
         The bottom margin will be different for
         different font size pairings. -->
    <TextBlock
        Style="{StaticResource SubtitleTextBlockStyle}"
        Margin="0,0,0,3"
        Text="Header text" />
    <TextBlock
        Style="{StaticResource BodyTextBlockStyle}"
        TextWrapping="Wrap"
        Text="This line of text should be positioned where the above header would have wrapped." />
</StackPanel>
```


<!-- OP version -->

## カーニングとトラッキング

Segoe は、ソフトでわかりやすい外観をした人間的な書体であり、手書き文字に基づく自然でオープンな形をしています。 できるだけ読みやすくし、人間的な一貫性を保つため、カーニングとトラッキングの設定を特定の値にする必要があります。

カーニングを "メトリック" に設定し、トラッキングを "0" に設定してください。

<img src="images/kerning-tracking.png" alt="Shows the difference between kerning and tracking" />

## 単語や文字の間隔

カーニングやトラッキングと同様、できるだけ読みやすくし、人間的な一貫性を保つため、単語の間隔と文字間隔でも特定の設定を使います。

既定では、単語の間隔は常に 100% であり、文字間隔は "0" に設定する必要があります。

<img src="images/word-letter.png" alt="Shows the difference between word and letter spacing" />


<aside class="aside-dev">
    <div class="aside-dev-title">
    </div>
    <div class="aside-dev-content">
            In a XAML text control use [Typogrphy.Kerning](https://msdn.microsoft.com/en-us/library/windows/apps/windows.ui.xaml.documents.typography.kerning.aspx) to control kerning and [FontStretch](https://msdn.microsoft.com/en-us/library/windows/apps/windows.ui.xaml.controls.control.fontstretch.aspx) to control tracking. By default Typography.Kerning is set to “true” and FontStretch is set to “Normal”, which are the recommended values.
    </div>
</aside>



<!-- OP version -->
## 配置

通常は、ビジュアル要素と書体の列を左揃えにすることをお勧めします。 ほとんどの場合、このような左揃えおよび右不揃いのアプローチによって、コンテンツが一貫したアンカー設定となり、均一なレイアウトになります。

<img src="images/alignment.png" alt="Shows flush-left text" />

## 行の末尾

文字体裁が左揃えおよび右不揃いで配置されていない場合、行の末尾が均等になるようにし、ハイフンを使わないでください。

<img src="images/line-endings.png" alt="Shows even line endings" />

## 段落

列の端を揃えるため、インデントなしの行をスキップすることで段落を示してください。

![段落間のスペースの行全体を示します。](images/paragraphs.png)

## 文字カウント

行が短すぎると、目を左から右へと頻繁に動かさなければならなくなり、読者のリズムが崩れます。 可能であれば、1 行あたり 50 ~ 60 文字にすると最も読みやすくなります。

Segoe UI には多くの文字が用意されており、サイズが小さくても大きくても、またはピクセル密度が低くても高くても最適な読みやすさが維持されるように設計されています。 テキスト列の行の文字数を最適にすると、アプリケーションでの読みやすさが確保されます。

行が長すぎると目に負担がかかり、ユーザーが混乱する可能性があります。 行が短すぎると読者が目を頻繁に動かさなければならず、疲れる可能性があります。

![行の長さが異なる 3 つの段落を示します。](images/character-count.png)

## ぶら下げテキストの配置

横方向に配置されたテキスト付きアイコンは、アイコンのサイズとテキストの量に応じてさまざまな方法で処理することができます。 1 行であっても複数行であってもテキストがアイコンの高さに収まる場合、テキストを上下に中央揃えにしてください。

テキストの高さがアイコンの高さより高い場合、テキストの先頭行を縦方向に揃え、残りのテキストが自然に下に流れるようにしてください。 より大きい大文字、高さが上昇または下降する文字を使うときは、同じ配置ガイダンスが守られるように注意してください。

![いくつかのアイコンとテキストの組み合わせを示します。](images/hanging-text-alignment.png)

<aside class="aside-dev">
    <div class="aside-dev-title">
    </div>
    <div class="aside-dev-content">
            XAML's [TextBlock.TextLineBounds](https://msdn.microsoft.com/en-us/library/windows/apps/windows.ui.xaml.controls.textblock.textlinebounds.aspx) property provides access to the cap height and baseline font metrics. It can be used to visually vertically center or top-align type.
    </div>
</aside>

## クリッピングと省略記号

既定でクリップ - 赤線により指定されている場合除き、テキストが折り返されることを前提とします。 折り返しのないテキストを使う場合、省略記号ではなくクリッピングをお勧めします。 クリッピングは、コンテナーの端、デバイスの端、スクロール バーの端などで行われます。

例外: 明確に定義されていないコンテナーの場合 (はっきりした背景色がないなど)、折り返しのないテキストに赤線を付けて省略記号 "..." を使うことができます。

![いくつかのテキスト クリッピングがあるデバイス フレームを示します。](images/clipping.png)

# 書体見本

書体見本の階層を作成するため、さまざまなサイズの Segoe UI を使ってください。 この階層により、ユーザーが書面によるコミュニケーションを通じて簡単にナビゲートできる構造が作成されます。

<figure class="figure-img" >
    <img src="images/type-ramp.png" alt="Shows the type ramp"  />
        <figcaption>すべてのサイズは有効ピクセル単位です。 詳しくは、「TODO: link」をご覧ください。</figcaption>
</figure>

<aside class="aside-dev">
    <div class="aside-dev-title">
    </div>
    <div class="aside-dev-content">
            Most levels of the ramp are available as XAML [static resources](https://msdn.microsoft.com/en-us/library/windows/apps/Mt187274.aspx#the_xaml_type_ramp) that follow the `*TextBlockStyle` naming convention (ex: `HeaderTextBlockStyle`). 
    </div>
</aside>


## プライマリ テキストとセカンダリ テキスト

書体見本を超えて追加の階層を作成するには、セカンダリ テキストの不透明度を 60% に設定します。 [テーマ カラー パレット](color.md#color-themes) で、BaseMedium を使います。 プライマリ テキストは、常に不透明度を 100% にするか、BaseHigh にしてください。

## すべて大文字のタイトル

特定のページ タイトルでは、階層に新たな次元を加えるため、すべて大文字にしてください。 これらのタイトルでは、BaseAlt を使い、文字間隔を em の 1,000 分の 75 にしてください。 この処理は、アプリのナビゲーションに使っても役立つことがあります。

ただし、言語によっては大文字にすると固有名詞の意味が変わるため、名前やユーザー入力に基づくページ タイトルはすべて大文字に変換*しない*でください。


## 推奨と非推奨
* ほとんどのテキストには Body を使う
* スペースに制約がある場合はタイトルに Base を使う
* 最上位レベルのコンテンツを強調することで、SubtitleAlt を組み込んでコントラストと階層を作る
* 長い文字列やプライマリ操作には Caption を使わない
* テキストを折り返す必要がある場合は Header や Subheader を使わない
* 同じページで Subtitle と SubtitleAlt を組み合わせない

## 関連記事

* [テキスト コントロール](../controls-and-patterns/text-controls.md)


<!--HONumber=Mar16_HO5-->

