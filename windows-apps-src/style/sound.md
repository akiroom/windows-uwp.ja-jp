---
Description: サウンドは、アプリケーションのユーザー エクスペリエンスの完成をサポートし、オーディオを際立たせます。オーディオは、すべてのプラットフォームで Windows の使い勝手を一致させるために必要なものです。
label: Sound
title: サウンド
template: detail.hbs
ms.assetid: 9fa77494-2525-4491-8f26-dc733b6a18f6
extraBodyClass: style-sound
brief: Sound helps complete an application's user experience, and gives them that extra audio edge they need to match the feel of Windows across all platforms.
---
[一部の情報はリリース前の製品に関することであり、正式版がリリースされるまでに大幅に変更される可能性があります。 ここに記載された情報について、マイクロソフトは明示または黙示を問わずいかなる保証をするものでもありません。]*この記事では、まだリリースされていない機能のプレビューを提供します。*

# UWP アプリのサウンド

サウンドは、アプリケーションのユーザー エクスペリエンスの完成をサポートし、オーディオを際立たせます。オーディオは、すべてのプラットフォームで Windows の使い勝手を一致させるために必要なものです。

## サウンドのグローバル API
UWP には使いやすいサウンド システムが用意されていて、「スイッチを切り替える」だけで、アプリ全体にイマーシブなオーディオ エクスペリエンスを実装することができます。

**ElementSoundPlayer** は、XAML 内の統合的なサウンド システムで、オンにすると、すべての既定のコントロールで自動的にサウンドが再生されます。
```C#
ElementSoundPlayer.State = ElementSoundPlayerState.On;
```
**ElementSoundPlayer** には、3 つの異なる状態、**On**、**Off**、**Auto** があります。

**Off** に設定すると、アプリの実行環境に関わらず、サウンドが再生されることはありません。 **On** に設定すると、すべてのプラットフォームで、アプリのサウンドが再生されます。
### テレビや Xbox のサウンド
サウンドは 10 フィート エクスペリエンスの重要なパーツなので、既定では、**ElementSoundPlayer** の状態は **Auto**、つまり、アプリが Xbox で実行されているときにのみサウンドが再生されます。
テレビや Xbox のサウンドのしくみの詳細については、「[テレビや Xbox の設計](http://go.microsoft.com/fwlink/?LinkId=760736)」の記事をご覧ください。

## 音量設定のオーバーライド
アプリ内のすべてのサウンドは、**Volume** コントロールで小さくすることができます。 しかし、アプリ内のサウンドを*システムの音量より大きく*することができません。

アプリの音量レベルを設定するには、次のように呼び出します。
```C#
ElementSoundPlayer.Volume = 0.5f;
```
ここで、最大の音量はシステムの音量に相対的に1.0、最小は 0.0 (本質的にサイレント)です。

## コントロール レベルの状態
コントロールの既定のサウンドが望ましくない場合は、これを無効にできます。 サウンドを無効にするには、コントロールで **ElementSoundMode** を使います。

**ElementSoundMode** には、**Off** と **Default** の 2 つの状態があります。 設定しないと、**Default** になります。 **Off** に設定すると、コントロールが再生するすべてのサウンドはミュートされます (*フォーカスを除く*)。

```XAML
<Button Name="ButtonName" Content="More Info" ElementSoundMode="Off"/>
```

```C#
ButtonName.ElementSoundState = ElementSoundMode.Off;
```

## 適切なサウンドの選択
カスタム コントロールを作成したり、既にあるコントロールのサウンドを変更したりするときには、システムが提供するすべてのサウンドの使用法を理解することが重要です。

各サウンドは特定の基本的なユーザー操作に関連付けられています。すべての対話式操作で再生するサウンドをカスタマイズできますが、このセクションでは、すべての UWP アプリで一貫したエクスペリエンスを維持するためにサウンドを使う必要がある、というシナリオを説明します。

### 要素の呼び出し
現在のシステムで最も一般的な、コントロールにトリガーされるサウンドは、**Invoke** サウンドです。 このサウンドは、ユーザーがタップ、クリック、入力、スペース、または、ゲームパッドの [A] ボタンを押すことでコントロールを呼び出したときに、再生されます。

通常このサウンドは、ユーザーが[入力デバイス](/input-and-devices/guidelines-for-interactions/)を介して明示的に単純なコントロールまたはコントロールの一部を対象としたときにのみ再生されます。

<SelectButtonClick.mp3 サウンド クリップ>

任意のコントロール イベントからこのサウンドを再生するには、シンプルに **ElementSoundPlayer** から Play メソッドを呼び出し、**ElementSound.Invoke** に渡します。
```C#
ElementSoundPlayer.Play(ElementSoundKind.Invoke);
```

### コンテンツの表示と非表示
XAML には多くのポップアップやダイアログ、閉じることができる UI があり、これらのオーバーレイのいずれかをトリガーするすべての操作で **Show** または **Hide** サウンドを呼び出す必要があります、

オーバーレイのコンテンツ ウィンドウをビューに読み込むときに、**Show** サウンドを呼び出す必要があります。

<OverlayIn.mp3 サウンド クリップ>

```C#
ElementSoundPlayer.Play(ElementSoundKind.Show);
```
逆に、オーバーレイのコンテンツ ウィンドウを閉じる (または簡易非表示にする) ときに、**Hide** サウンドを呼び出す必要があります。

<OverlayOut.mp3 サウンド クリップ>

```C#
ElementSoundPlayer.Play(ElementSoundKind.Hide);
```
### ページ内でのナビゲーション
アプリのページ内でパネルまたはビューの間をナビゲーションする場合 (「[ハブ](/controls-and-patterns/hub/)」または「[タブとピボット](/controls-and-patterns/tabs-pivot/)」をご覧ください)、通常は、移動の方向は双方向です。 つまり、現在表示しているアプリのページを離れずに、次のビュー/パネルまたは前のビュー/パネルに移動できます。

このナビゲーションの概念に関するオーディオ エクスペリエンスは、**MovePrevious** サウンドと **MoveNext** サウンドに包含されています。

リストの*次の項目*と考えられるビュー/パネルに移動するときは、次のように呼び出します。

<PageTransitionRight.mp3 サウンド クリップ>

```C#
ElementSoundPlayer.Play(ElementSoundKind.MoveNext);
```
リストの*前の項目*と考えられるビュー/パネルに移動するときは、次のように呼び出します。

<PageTransitionLeft.mp3 サウンド クリップ>

```C#
ElementSoundPlayer.Play(ElementSoundKind.MovePrevious);
```
### 戻るナビゲーション
アプリ内で現在のページから前のページにナビゲーションするときは、**GoBack** サウンドを呼び出す必要があります。

<BackButtonClick.mp3 サウンド クリップ>

```C#
ElementSoundPlayer.Play(ElementSoundKind.GoBack);
```
### 要素へのフォーカス
マイクロソフトのシステムの **Focus** サウンドは、唯一の暗黙的なサウンドです。 つまり、ユーザーは、何かを直接操作していなくてもサウンドが聞こえます。

フォーカスは、ユーザーがアプリをナビゲーションしたときに、ゲームパッド、キーボード、リモート、キネクトのいずれかで起こります。 通常、**Focus** サウンドは、*PointerEntered またはマウス ホバー イベント時には再生されません*。

コントロールがフォーカスされたときに **Focus** サウンドを再生するように設定するには、次のように呼び出します。

<ElementFocus1.mp3 サウンド クリップ>

```C#
ElementSoundPlayer.Play(ElementSoundKind.Focus);
```
### フォーカス サウンドの循環
**ElementSound.Focus** 呼び出しの追加機能として、サウンド システムは、既定で、ナビゲーション トリガーごとに 4 つの異なるサウンドを循環させます。 つまり、2 つの同じフォーカス サウンドが前後して再生されることはありません。

この循環機能の目的は、フォーカス サウンドが単調になることを防ぎ、ユーザーの注意をひかない状態を保つことです。フォーカス サウンドは、最もよく再生されるため、最も繊細なサウンドにする必要があります。

## 関連記事
* [Xbox およびテレビ向け設計](http://go.microsoft.com/fwlink/?LinkId=760736)


<!--HONumber=Mar16_HO5-->

