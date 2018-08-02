---
description: さまざまなデバイスや画面サイズで、ナビゲーションがわかりやすく見た目にも優れた UWP アプリを設計およびコーディングする方法について説明します。
title: 設計の基本
author: mijacobs
keywords: UWP アプリのレイアウト, ユニバーサル Windows プラットフォーム, アプリの設計, インターフェイス
ms.author: mijacobs
ms.date: 3/7/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
ms.openlocfilehash: d092a3fe1120dc5763b5c30ed834c1902a1f8752
ms.sourcegitcommit: 517c83baffd344d4c705bc644d7c6d2b1a4c7e1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2018
ms.locfileid: "1842379"
---
# <a name="design-basics-for-uwp-apps"></a>UWP アプリの設計の基本

![ヒーロー イメージ](images/header-design-basics.svg)

ユニバーサル Windows プラットフォーム (UWP) の設計ガイダンスは、美しく洗練されたアプリを設計および構築するのに役立つリソースです。 これは規範的な規則の一覧ではなく、進化する Fluent Design System、およびアプリ構築コミュニティのニーズに適応するように設計された生きたドキュメントです。 

<!-- This introduction provides an overview of the Fluent Design System, UWP app design basics, and the XAML platform, helping you build user interfaces (UI) that scale beautifully across a range of devices. -->

## <a name="overview"></a>概要

[**UWP アプリ設計の概要**](design-and-ui-intro.md)

すべての種類の Windows デバイスで適切に対応するアプリを作成するためのベスト プラクティスと組み合わされた、UWP 機能の概要です。

[**Fluent Design System**](../fluent-design-system/index.md)

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

[**1. 基本的な UI を作成する**](xaml-basics-ui.md)

XAML を使用して基本的なユーザー インターフェイスを作成します。

[**2. アダプティブ レイアウトを作成する**](xaml-basics-adaptive-layout.md)

写真編集アプリケーションにアダプティブ レイアウトを提供します。

[**3. カスタム スタイルを作成する**](xaml-basics-style.md)

カスタム スタイルを作成することで、UWP コントロールに独自の外観を提供します。