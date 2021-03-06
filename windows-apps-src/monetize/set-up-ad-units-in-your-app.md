---
ms.assetid: bb105fbe-bbbd-4d78-899b-345af2757720
description: ストアにアプリを送信する前に、アプリをパートナー センターからアプリケーション ID と ad 単位の ID 値を追加する方法について説明します。
title: アプリの広告ユニットをセットアップする
ms.date: 05/11/2018
ms.topic: article
keywords: Windows 10, UWP, 広告, Advertising, 広告ユニット, テスト
ms.localizationpriority: medium
ms.openlocfilehash: b2d01434e508d4a5067ffd66bdf86b3083b43016
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57651577"
---
# <a name="set-up-ad-units-in-your-app"></a>アプリの広告ユニットをセットアップする

ユニバーサル Windows プラットフォーム (UWP) アプリ内の各広告コントロールには、対応する*広告ユニット*があります。広告ユニットは、コントロールに広告を提供するためにサービスで使用されます。 各広告ユニットは、*広告ユニット ID* と*アプリケーション ID* があり、これらをアプリ内でコードに割り当てる必要があります。

テスト中にテスト広告がアプリに表示されていることを確認するために使用できる[テスト広告ユニット値](#test-ad-units)が用意されています。 これらのテスト値は、テスト バージョンのアプリでのみ使用できます。 いったん公開したアプリでテスト用の値を使うと、ライブ アプリで広告は表示されません。

テストが完了したら、UWP アプリとするパートナー センターに提出する準備が整ったら、する必要があります[ライブ広告ユニットを作成](#live-ad-units)から、[アプリ内広告](../publish/in-app-ads.md)パートナー センターでページし、アプリケーションを使用して、アプリのコードを更新ID と ad 単位 ID 値をこの ad 単位。

アプリケーション ID と広告ユニット ID の値をアプリのコードに割り当てる方法の詳細については、次の記事を参照してください。
* [XAML と .NET で AdControl](adcontrol-in-xaml-and--net.md)
* [HTML 5 で AdControl および Javascript](adcontrol-in-html-5-and-javascript.md)
* [スポット広告](../monetize/interstitial-ads.md)
* [ネイティブ広告](../monetize/native-ads.md)

<span id="test-ad-units" />

## <a name="test-ad-units"></a>広告ユニットをテストする

アプリを開発しているときには、このセクションに示されているテスト用のアプリケーション ID と広告ユニット ID の値を使って、テスト時にアプリでどのように広告がレンダリングされるかを確認します。

### <a name="banner-ads-using-the-adcontrol-class"></a>バナー広告 (AdControl クラスを使用)

* Ad のユニット ID: ```test```
* アプリケーション ID:  ```3f83fe91-d6be-434d-a0ae-7351c5a997f1```

    > [!IMPORTANT]
    > **AdControl** では、ライブ広告のサイズは **Width** プロパティと **Height** プロパティによって定義されます。 最善の結果を得るには、コード内の **Width** プロパティと **Height** プロパティが、[バナー広告でサポートされている広告サイズ](supported-ad-sizes-for-banner-ads.md)のいずれかであることを確認します。 **Width** プロパティと **Height** プロパティは、ライブ広告のサイズに基づいて変更されません。

### <a name="interstitial-ads-and-native-ads"></a>スポット広告やネイティブ広告

* Ad のユニット ID: ```test```
* アプリケーション ID:  ```d25517cb-12d4-4699-8bdc-52040c712cab```

<span id="live-ad-units" />

## <a name="live-ad-units"></a>ライブ広告ユニット

パートナー センターから、ライブ広告ユニットを取得し、アプリで使用します。

1.  [Ad 単位を作成](../publish/in-app-ads.md#create-ad-unit)上、**アプリ内広告**パートナー センターでのページ。 アプリで使用している広告コントロールに合わせて、適切な種類の広告ユニットを指定してください。
    > [!NOTE]
    > 必要に応じて、[[仲介設定]](../publish/in-app-ads.md#mediation) セクションで設定を構成することで、広告ユニットの広告仲介を有効にできます。 広告仲介を使うと、複数の広告ネットワークから広告を表示して、広告収益とアプリ プロモーションの機能を最大限に引き出すことができます。表示される広告には、他の有料広告ネットワークからの広告や、Microsoft のアプリ プロモーション キャンペーン用の広告などが含まれます。 既定では、アプリがサポートする市場全体で広告の収益を最大化できるように、機械学習アルゴリズムを使った仲介設定が自動的に構成されますが、必要に応じて仲介設定を手動で構成することができます。

2.  新しい ad 単位を作成した後は、取得、**アプリケーション ID**と**Ad ユニット ID**の ad ユニットの使用可能な ad 単位のテーブルの**Monetize** &gt; **アプリ内広告**ページ。
    > [!NOTE]
    > テスト広告ユニットとライブ UWP 広告ユニットでは、アプリケーション ID の値の形式が異なります。 テスト アプリケーション ID の値は GUID です。 パートナー センターでライブ UWP ad 単位を作成するときに ad 単体のアプリケーション ID の値は常に (Store ID 値の例を次のように 9NBLGGH4R315) アプリの Store ID を一致します。

3.  アプリのコードで、アプリケーション ID と広告ユニット ID の値を割り当てます。 詳しくは、次の記事をご覧ください。
    * [XAML と .NET で AdControl](adcontrol-in-xaml-and--net.md)
    * [HTML 5 で AdControl および Javascript](adcontrol-in-html-5-and-javascript.md)
    * [スポット広告](../monetize/interstitial-ads.md)
    * [ネイティブ広告](../monetize/native-ads.md)

<span id="manage" />

## <a name="manage-ad-units-for-multiple-ad-controls-in-your-app"></a>アプリで複数の広告コントロールの広告ユニットを管理する

1 つのアプリに複数のバナー広告コントロール、スポット広告コントロール、ネイティブ広告コントロールを使用できます。 このシナリオでは、各コントロールに異なる広告ユニットを割り当てることをお勧めします。 各コントロールに異なる広告ユニットを使用することで、別々に[仲介の設定を構成](../publish/in-app-ads.md#mediation)して、個別の[報告データ](../publish/advertising-performance-report.md)を取得することが可能です。 また、これにより、Microsoft のサービスはアプリに提供する広告を最適化できます。

> [!IMPORTANT]
> 各広告ユニットは 1 つのアプリのみで使用できます。 同じ広告ユニットを複数のアプリで使うと、その広告ユニットには広告が配信されません。

## <a name="related-topics"></a>関連トピック

* [XAML と .NET で AdControl](adcontrol-in-xaml-and--net.md)
* [HTML 5 で AdControl および Javascript](adcontrol-in-html-5-and-javascript.md)
* [スポット広告](interstitial-ads.md)
* [ネイティブ広告](native-ads.md)


 

 
