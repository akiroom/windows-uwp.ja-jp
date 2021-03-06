---
Description: パートナー センターで、実験を定義し、アプリでコードを実験、実験をアクティブに準備が完了し、パートナー センターを使用して、実験の結果を確認します。
title: パートナー センターで実験を管理する
ms.assetid: D48EE0B4-47F2-455C-8FB9-630769AC5ACE
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store Services SDK, A/B テスト, 実験
ms.localizationpriority: medium
ms.openlocfilehash: 6e5c0d0ca1b1d771df2b224cc41ec5a37e267bc9
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57594927"
---
# <a name="manage-your-experiment-in-partner-center"></a>パートナー センターで実験を管理する

したら[パートナー センターで、実験を定義](define-your-experiment-in-the-dev-center-dashboard.md)と[実験用のアプリをコード](code-your-experiment-in-your-app.md)実験をアクティブ化およびパートナー センターを使用して、実験の結果を確認する準備が整いました。 必要なすべてのデータを取得したら、実験を終了し、すべてのアプリでコントロールのバリエーションの変数値を使用し続けるか、他のバリエーションの変数値を使用することに切り替えるかを選択できます。

> [!NOTE]
> 実験をアクティブ化するとすぐにパートナー センターが、実験用のデータをログにインストルメント化されている任意のアプリからデータの収集を開始します。 ただし、実験のデータがパートナー センターで表示される数時間がかかることができます。

実験の作成と実行のプロセスについて詳しく示すチュートリアルについては、「[A/B テストを使用して最初の実験を作成および実行する](create-and-run-your-first-experiment-with-a-b-testing.md)」をご覧ください。

## <a name="activate-your-experiment"></a>実験をアクティブ化する

パートナー センターで、実験のパラメーターに満足したら、アプリ コードを更新すると、アプリから実験のデータの収集を開始できるように、実験をアクティブにする準備が整いました。 実験がアクティブの場合、アプリはバリエーションの 1 つの値を取得し、パートナー センターに表示し、変換のイベントを報告できます。

1. [パートナー センター](https://partner.microsoft.com/dashboard)にサインインします。
2. **[アプリ]** の下で、アクティブ化する実験を備えたアプリを選択します。
3. ナビゲーション ウィンドウで、**[サービス]** を選択し、**[実験]** を選択します。
4. **[プロジェクト]** セクションのプロジェクトの表で、目的の実験が含まれるプロジェクトを展開し、次のいずれかを実行します。
  * 実験の **[アクティブ化]** リンクをクリックします。 実験が、ページの上部にある **[アクティブな実験]** セクションに追加されます。
  * 実験の名前をクリックし、実験のページの下部までスクロールして、**[アクティブ化]** をクリックします。

> [!IMPORTANT]
> 実験の作成時に **[編集可能な実験]** チェック ボックスをオンにしていないと、実験をアクティブ化した後で実験のパラメーターを変更できなくなります。 アプリで実験のコードを記述してから実験をアクティブ化することをお勧めします。

## <a name="review-the-results-of-your-experiment"></a>実験の結果を確認する

1. パートナー センターでに戻り、**実験**アプリのページ。
2. **[アクティブな実験]** セクションで、目的のアクティブな実験の名前をクリックし、実験のページに移動します。
3. アクティブな実験または完了した実験の場合、このページの最初の 2 つのセクションに実験の結果が表示されます。
  * **[結果の概要]** セクションには、実験の目標と各バリエーションのコンバージョン率の一覧が表示されます。
  * **[結果の詳細]** セクションには、ビュー、コンバージョン、固有ユーザー数、コンバージョン率、デルタ %、信頼性、重要性など、実験のすべての目標に対する各検証結果の詳細が表示されます。 *信頼性*は、推定値の信頼性の統計的な計測であり、許容誤差を計算したものです。 *重要性*は、サンプル サイズに基づいた統計的な計測であり、結果が偶然に発生したのではなく、特定の原因によって発生した可能性があることを示すものです。

> [!NOTE]
> パートナー センターでは、24 時間の期間に各ユーザーの最初の変換イベントのみを報告します。 ユーザーが 24 時間以内にアプリで複数のコンバージョン イベントをトリガーした場合は、最初のコンバージョン イベントのみ報告されます。 これは、多数のコンバージョン イベントを使用する単一のユーザーによって、サンプルのユーザー グループの実験の実行結果が歪曲されないようにすることを目的としています。


## <a name="complete-your-experiment"></a>実験を完了する

1. パートナー センターでは、実験のページに戻ります。 手順については、前のセクションをご覧ください。
2. **[Results summary]** セクションで、次のいずれかの操作を行います。
  * 実験を終了し、アプリでコントロールのバリエーションの変数値を使用し続ける場合は、**[保存]** をクリックします。
  * 実験を終了するが、アプリでは別のバリエーションの変数値を使用する場合は、新たに使用するバリエーションの下にある **[切り替え]** をクリックします。
3. **[OK]** をクリックして、試験的機能を終了することを確認します。


## <a name="related-topics"></a>関連トピック

* [プロジェクトを作成し、パートナー センターでのリモート変数の定義](create-a-project-and-define-remote-variables-in-the-dev-center-dashboard.md)
* [実験用のアプリをコードします。](code-your-experiment-in-your-app.md)
* [パートナー センターでの実験を定義します。](define-your-experiment-in-the-dev-center-dashboard.md)
* [作成し、A で初めての実験を実行する B のテスト](create-and-run-your-first-experiment-with-a-b-testing.md)
* [A とアプリの実験を実行する B のテスト](run-app-experiments-with-a-b-testing.md)
