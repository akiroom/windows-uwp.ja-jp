---
description: さまざまなデバイスや画面サイズで、ナビゲーションがわかりやすく見た目にも優れた UWP アプリを設計およびコーディングする方法について説明します。
title: 設計の基本
keywords: UWP アプリのレイアウト, ユニバーサル Windows プラットフォーム, アプリの設計, インターフェイス
ms.date: 03/07/2018
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 78462d5d29ebcc31792aa46da7657c57fb960e13
ms.sourcegitcommit: f0f933d5cf0be734373a7b03e338e65000cc3d80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65984111"
---
# <a name="design-basics-for-uwp-apps"></a>UWP アプリの設計の基本

![設計の基本のアイコン](../images/basics-2x.png)

ユニバーサル Windows プラットフォーム (UWP) の設計ガイダンスは、美しく洗練されたアプリを設計および構築するのに役立つリソースです。 これは規範的な規則の一覧ではなく、進化する Fluent Design System、およびアプリ構築コミュニティのニーズに適応するように設計された生きたドキュメントです。 

## <a name="overview"></a>概要

[**UWP アプリ設計の概要**](design-and-ui-intro.md)

すべての種類の Windows デバイスで適切に対応するアプリを作成するためのベスト プラクティスと組み合わされた、UWP 機能の概要です。

[**Fluent Design System**](/windows/apps/fluent-design-system)

Fluent Design System では、順応性が高く、親近感があり、優れた美しさを持つユーザー インターフェイスを作成するための目標や原則を示します。

## <a name="basics"></a>基本

[**ナビゲーションの基本**](navigation-basics.md)

UWP アプリのナビゲーションは、ナビゲーション構造、ナビゲーション要素、システム レベルの機能から成る柔軟なモデルに基づいています。 この記事では、これらの構成要素を紹介します。また、これらの構成要素を組み合わせて使い、優れたナビゲーション エクスペリエンスを作成する方法について説明します。

[**コマンドの基本**](commanding-basics.md)

コマンド要素は、ユーザーがメール送信、項目の削除、フォームの送信などの操作を実行できる対話型の UI 要素です。 この記事では、ボタンやチェック ボックスなどのコマンド要素、それらの要素でサポートされる操作、それらの要素をホストするコマンド サーフェス (コマンド バーやショートカット メニューなど) について説明します。

[**コンテンツの基本**](content-basics.md)

どのようなアプリでも、主な目的はコンテンツへのアクセスを提供することです。たとえば、写真編集アプリでは写真がコンテンツであり、旅行アプリでは地図と旅行の目的地に関する情報がコンテンツです。 この記事では、3 つのコンテンツ シナリオ (使用、作成、対話式操作) でのコンテンツの設計に関する推奨事項について説明します。

## <a name="tutorials"></a>チュートリアル

XAML と C# で基本的な写真編集アプリケーションを作成する方法について説明します。
<!-- <img src="images/landing-page/photolab-50.png" style="{height: 339px}" alt=" " /> -->

[**1.基本的な UI を作成する**](xaml-basics-ui.md)

XAML を使用して基本的なユーザー インターフェイスを作成します。

[**2.アダプティブ レイアウトを作成する**](xaml-basics-adaptive-layout.md)

写真編集アプリケーションにアダプティブ レイアウトを提供します。

[**3.カスタム スタイルを作成する**](xaml-basics-style.md)

カスタム スタイルを作成することで、UWP コントロールに独自の外観を提供します。