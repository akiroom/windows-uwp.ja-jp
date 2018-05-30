---
title: Unity プロジェクトにプレイヤーの統計とランキングを追加する
author: KevinAsgari
description: Xbox Live Unity プラグインを使用してプレイヤーの統計とランキングを Unity プロジェクトに追加する方法について説明します。
ms.assetid: 756b3c31-a459-4ad2-97af-119adcd522b5
ms.author: kevinasg
ms.date: 10/19/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One, Unity, クリエーター
ms.localizationpriority: low
ms.openlocfilehash: c39d1680e60d3575d449b5472de462b2057eea36
ms.sourcegitcommit: 01760b73fa8cdb423a9aa1f63e72e70647d8f6ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/24/2018
---
# <a name="add-player-stats-and-leaderboards-to-your-unity-project"></a>Unity プロジェクトにプレイヤーの統計とランキングを追加する

> [!IMPORTANT]
> Xbox Live Unity プラグインでは、実績とオンライン マルチプレイヤーがサポートされていないため、[Xbox Live クリエーターズ プログラム](../developer-program-overview.md)のメンバーに対してのみお勧めしています。

[Xbox Live サインイン](sign-in-to-xbox-live-in-unity.md)を Unity プロジェクトに追加したら、次の手順として、プレイヤーの統計とその統計に基づくランキングを追加します。

[Xbox Live Unity プラグイン](https://github.com/Microsoft/xbox-live-unity-plugin)を使用すると、プレイヤーの統計とランキングを Unity プロジェクトに簡単に追加できます。 サインイン手順と同様、付属のプレハブを使用したり、付属のスクリプトを独自のカスタム ゲーム オブジェクトにアタッチしたりすることができます。

## <a name="prerequisites"></a>前提条件
1. [Unity で Xbox Live を構成する](configure-xbox-live-in-unity.md)
2. [Unity で Xbox Live にサインインする](sign-in-to-xbox-live-in-unity.md)

## <a name="player-stats"></a>プレイヤーの統計

プレイヤーの統計とは、プレイヤーに関して追跡される統計情報であり、プレイヤーの関心を引くために使用されます。 Xbox Live で追跡する統計は、プレイヤーに関連する統計であることが必要です。またこの統計は、所定の方法で表示されます。 こうしたプレイヤーの統計は、一般的にランキングの作成に使用されます。プレイヤーはこのランキングを確認することで、ゲームをプレイしたときのランクが他のプレイヤーと比べてどの順位にあるかを判断することができます。 すべてのプレイヤーの統計は、「注目の統計」と見なされます。つまり、その統計はゲームのゲーム ハブに表示されます。

プレイヤーの統計は、1 つの値を表す必要があります。 Xbox Live Unity プラグインには、整数型、倍精度浮動小数点数型、および文字列型の各統計に対応したプレハブが用意されています。また、他のデータ型に拡張可能な基本統計オブジェクト用のスクリプトも用意されています。

プレイヤーの統計について詳しくは、「[プレイヤーの統計](../leaderboards-and-stats-2017/player-stats.md)」をご覧ください。

> [!NOTE]
> Xbox Live サービスでプレイヤーの統計やランキングを使用する場合、データにアクセスするためには、ユーザーが正常にサインインしている必要があります。

## <a name="using-the-player-stat-prefabs"></a>プレイヤーの統計プレハブを使用する

Xbox Live Unity プラグインには、プレイヤーの統計に関連して使用できるプレハブがいくつか用意されています。

* IntegerStat: ラウンドでの撃墜の合計数など、整数値として表すことができる統計です。
* DoubleStat: 撃墜/死亡の割合など、浮動小数点値として表すことができる統計です。
* StringStat: "ゴールド"、"シルバー"、"ブロンズ" といったラウンドで付与されるランクなど、文字列値 (通常は列挙型) として表すことができる統計です。
* StatPanel: 現在の統計の値を表示する際に使用できるサンプル UI です。

プレイヤーの統計を追加するには、統計のデータ型に一致するプレハブをシーンにドラッグするだけです。 統計の Unity インスペクターでは、3 つの値を指定できます。

* 統計の ID です。これは、Windows デベロッパー センターで構成されている ID に一致する必要があり、大文字と小文字が区別されます。
* 統計の表示名 (この名前は StatPanel プレハブ UI に表示されます)。
* シーンが開始したときの統計の初期値。

**StatPanel** プレハブを使用すると、統計の値を表示できます。これを行うには、**StatPanel** プレハブをシーンにドラッグします。 Unity Inspector で **StatPanel** オブジェクトの **Stat** フィールドに統計ゲーム オブジェクトをドラッグすることにより、統計が表示されるように指定できます。

### <a name="manipulating-the-player-stat-values"></a>プレイヤーの統計値を操作する

プレイヤー統計オブジェクトには、統計の値を調整するために呼び出すことができる多くの関数があります。これらの関数は、他のルーチンから呼び出したり、UI 要素にバインドしたりすることができます。 **DoubleStat**、**IntegerStat**、**StringStat** の各スクリプトを調べると、統計の値を変更する関数の例を確認できます。新しいスクリプトを変更または作成し、より複雑な関数とロジックをして統計を表示できます。 新しい統計クラスは、`StatBase` スクリプトで定義された `StatBase` クラスを拡張します。

たとえば、簡単なテストとして、UI ボタンをシーンに追加します。次に、Unity インスペクターにあるボタンの `OnClick` イベントで **IntegerStat** オブジェクトを追加し、`Increment()` 関数を呼び出して、ボタンをクリックするたびに統計の値が大きくなるようにします。

統計が **StatPanel** オブジェクトにもバインドされている場合、ボタンをクリックするたびに統計の値が更新されるのを確認できます。

統計を更新するたびに (増加、減少など)、値がローカルで更新されます。 データは、`StatManagerComponent` スクリプトにより 5 分ごとに自動的にフラッシュされます。  5 分経過する前にゲームが終了する場合は、その進行状況が失われないように、まずデータを手動でフラッシュする必要があります。 そのためには、`statManagerComponent.RequestFlushToService()` メソッドを呼び出す必要があります。必ず、統計が書き込まれる **XboxLiveUser** に対して呼び出してください。

> [!TIP]
> ベスト プラクティスとして、進行状況が失われないように、必ずゲームが終了する前にデータをフラッシュしてください。

## <a name="leaderboards"></a>ランキング

ランキングは、統計の "ベスト" な値を獲得したプレイヤーを順番に並べた番号付き一覧です。たとえば、ランキングにはレースのラップ タイムで最も速いタイムを獲得したプレイヤーが一覧表示されるため、プレイヤーは自分のベスト レース タイムと他のプレイヤーのベスト レース タイムを比較できます。

ランキングは、ゲームによって Xbox Live サービスに送信されたプレイヤーの統計に基づいて作成されます。 したがって、ランキング データは読み取り専用であり、直接変更できません。

Xbox Live Unity プラグインには、ランキングをゲームに実装する方法を理解する際に役立つサンプルのランキング プレハブが用意されています。

ランキングについて詳しくは、「[ランキング](../leaderboards-and-stats-2017/leaderboards.md)」をご覧ください。

## <a name="using-the-leaderboard-prefabs"></a>ランキング プレハブを使用する

Xbox Live Unity プラグインには、ランキング用の 2 つのプレハブが用意されています。

* Leaderboard: ランキングを表示するオブジェクトであり、ランキングの値を表示するためのシンプルな UI が含まれています。
* LeaderboardEntry: ランキングの単一の行を表示するオブジェクトです。

**ランキング** プレハブはシーンにドラッグできます。 Unity インスペクターでは、次の属性を設定できます。

* 統計: このランキングが関連付けられている統計ゲーム オブジェクト。 
* ランキングの種類: ランキング エントリに返される結果のスコープ。 
* エントリ数: 1 ページあたりに表示するデータの行数。

Unity エディターでは、インスペクターの設定に関係なく、常に同じモック データが**ランキング** プレハブに表示されます。 実際のデータ値を表示するには、プロジェクトをビルドして Visual Studio にエクスポートし、承認されたユーザーとしてログインする必要があります。 詳しくは、「[Unity で Xbox Live を構成する](configure-xbox-live-in-unity.md)」をご覧ください。

## <a name="see-also"></a>関連項目

* [Unity で Xbox Live にサインインする](sign-in-to-xbox-live-in-unity.md)
* [Unity で Xbox Live を構成する](configure-xbox-live-in-unity.md)