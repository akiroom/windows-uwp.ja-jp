---
Description: アプリの基本価格を選択し、価格変更をスケジュールします。 これらのオプションを特定の市場向けにカスタマイズすることもできます。
title: アプリの価格の設定とスケジュール
ms.date: 10/31/2018
ms.topic: article
keywords: windows 10, uwp, 価格設定, アプリの価格設定, アプリの価格, アプリの販売, 価格変更, カスタム価格, 価格, 料金, コスト, 基本価格の上書き, 自由設定価格, 自由設定
ms.localizationpriority: medium
ms.openlocfilehash: 451a22ffef2d8062de7bf7d29d921db7197987b5
ms.sourcegitcommit: fca0132794ec187e90b2ebdad862f22d9f6c0db8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "63788279"
---
# <a name="set-and-schedule-app-pricing"></a>アプリの価格の設定とスケジュール

[[価格と使用可能状況]](set-app-pricing-and-availability.md) ページの **[価格設定]** セクションでは、アプリの基本価格を選択できます。 [価格変更をスケジュール](#schedule-price-changes)して、アプリの価格を変更する日時を指定することもできます。 また、[特定の市場の基本価格を上書きする](#override-base-price-for-specific-markets)こともできます。その場合は、新しい価格帯を選択するか、市場の現地通貨で自由設定価格を入力します。

> [!NOTE]
> このトピックはアプリについて説明していますが、アドオンの申請の価格設定にも同じプロセスを使います。 [サブスクリプションのアドオン](../monetize/enable-subscription-add-ons-for-your-app.md)、基本価格を選択することはできませんこれまで増やすことが (基本価格を変更することであるかどうか、または価格の変更をスケジュールすることによって) が、減らすことができます。

## <a name="base-price"></a>基本価格

アプリの **[基本価格]** を選ぶと、いずれかの市場で基本価格を上書きしない限り、アプリを販売するすべての市場で基本価格が使用されます。

**[基本価格]** は、**[無料]** に設定することも、利用可能な価格帯から選択することもできます。価格帯は、アプリの配布先となるすべての国での販売価格を設定するものです。 価格帯は、0.99 米国ドルから始まり、増分を加算して段階的に上がっていきます (1.09 米国ドル、1.19 米国ドルなど)。 価格が高くなるにつれ、増分も徐々に大きくなります。 

> [!NOTE]
> これらの価格帯はアドオンにも適用されます。 

各価格帯には、ストアで提供されている 60 を超える通貨それぞれに対応する値があります。 これらの値は、世界中で同等の小売価格でアプリを販売するために使われます。 基本価格は任意の通貨で選択でき、別の市場では対応する値が自動的に使われます。 特定市場の対応する値は、通貨換算レートの変動を考慮し、必要に応じて調整されることがあります。

すべての通貨での対応する価格を確認するには、**[価格設定]** セクションで **[変換テーブルを表示]** をクリックします。 これにより、各価格帯に関連付けられている ID 番号も表示されます。この ID は、[Microsoft Store 申請 API](../monetize/manage-app-submissions.md#price-tiers) を使って価格を入力する場合に必要になります。 **[ダウンロード]** をクリックすると、価格帯の表のコピーを .csv ファイルとしてダウンロードできます。

選んだ価格帯には、ユーザーが支払う必要のある売上税や付加価値税が含まれている場合があることに注意してください。 選択した市場でのアプリの税について詳しくは、「[有料アプリの税金の詳細](tax-details-for-paid-apps.md)」をご覧ください。 また、[特定の市場の価格に関する考慮事項](define-market-selection.md#price-considerations-for-specific-markets)も確認する必要があります。

> [!NOTE]
> 選択した場合、**の取得を停止**オプションで **ストアに、この製品を使用できますが、探索されないように**で、[可視性](choose-visibility-options.md#discoverability)セクション)、設定することはできません(だれも、アプリを無料で入手するプロモーション コードを使用しない限り、アプリを取得できない) ために、お客様の提出の価格設定です。

## <a name="schedule-price-changes"></a>価格変更のスケジュール

アプリの基本価格を特定の日時に変更する必要がある場合は、価格変更を 1 回以上スケジュールできます。 

> [!IMPORTANT]
> 価格変更は、Windows 10 デバイス (Xbox を含む) のユーザーにのみ表示されます。 以前に発行アプリでは、以前の OS バージョンをサポートする場合に顧客価格変更は適用されません。 Windows 8 のユーザーに対しては、追加の価格変更をスケジュールしても、アプリは常に**基本価格**で提供されます (市場固有の価格も適用されません)。 Windows 8.1、および Windows Phone 8.1、および以前の顧客、アプリは常に顧客の市場向けの最初の価格レベルで提供されます。

価格変更のオプションを表示するには、**[価格変更のスケジュール]** をクリックします。 使用する価格帯を選び (または、単一市場ベースで基本価格を上書きするには、自由設定価格を入力し)、日付、時刻、タイム ゾーンを選択します。

クリックすることができます**価格変更のスケジュール**それ以降の多くの変更、希望のスケジュールを設定するには、もう一度です。

> [!NOTE]
> スケジュールされた価格変更は、[セール価格](put-apps-and-add-ons-on-sale.md)とは動作が異なります。 アプリのセールを開始すると、Microsoft Store では元の価格に取り消し線が引かれます。指定した期間中、ユーザーはセール価格でアプリを購入できます。 セール期間が終わると、セール価格の適用が終了し、アプリは基本価格 (市場に対して別の価格を指定した場合は、その価格) に戻ります。
>
> 価格変更をスケジュールする場合は、価格を調整して高くすることも低くすることもできます。 変更は指定日に実施されますが、Microsoft Store でセールとして表示されることも、特別な書式が適用されることもなく、アプリに新しい基本価格が設定されるだけです。 


## <a name="override-base-price-for-specific-markets"></a>特定市場の基本価格の上書き

既定では、上で選択したオプションは、アプリが提供されるすべての市場に適用されます。 オプションで、1 つまたは複数の市場に対して価格を変更することもできます。その場合は、別の価格帯を選択するか、市場の現地通貨で自由設定価格を入力します。

> [!IMPORTANT]
> 以前発行されたアプリは、Windows 8 をサポートする場合、顧客が常にでアプリを表示、**基本価格**市場のさまざまな価格を選択した場合でも、します。

特定の市場に対して価格を変更するには、**[基本価格を上書きする市場の選択]** をクリックします。 **[市場の選択]** ポップアップ ウィンドウが開き、アプリの提供先として選択されているすべての市場の一覧が表示されます。 (**[市場]** セクションで除外した市場がある場合、それらの市場は表示されません。) 

基本価格は、1 市場ずつ上書きすることも、市場のグループに対してまとめて上書きすることもできます。 この操作を実行した後、別の市場 (または別の市場グループ) に対して基本価格を上書きすることもできます。その場合は、**[基本価格を上書きする市場の選択]** をもう一度選択し、上のプロセスを繰り返します。 市場 (または市場グループ) に対して指定した上書き価格を削除するには、**[削除]** をクリックします。


### <a name="override-the-base-price-for-a-single-market"></a>単一市場に対して基本価格を上書きする

1 つの市場のみに対して価格を変更するには、市場を選択して **[作成]** をクリックします。 上の説明と同じ **[基本価格]** と **[価格変更のスケジュール]** のオプションが表示されます。ただし、ここでの選択はその市場に固有になります。 1 つの市場のみの基本価格を上書きするため、価格帯はその市場の現地通貨で表示されます。 すべての通貨での対応する価格を確認するには、**[変換テーブルを表示]** をクリックします。 

単一市場に対して基本価格を上書きした場合は、選択した自由設定価格を市場の現地通貨で入力することもできます。 価格は、(最低価格から最高価格までの範囲で) 自由に選択して入力でき、いずれかの標準価格帯に対応する必要はありません。 この価格は、選択した市場で Windows 10 (Xbox を含む) のユーザーに対してのみ使用されます。 

> [!IMPORTANT]
> 新しい価格で更新プログラムを提出する場合を除き、自由設定で価格を入力すると (コンバージョン率が変化しても) 価格が調整されません。 

### <a name="override-the-base-price-for-a-market-group"></a>市場グループに対して基本価格を上書きする

複数の市場に対して基本価格を上書きするには、*市場グループ*を作成します。 これを行うには、グループに含める市場を選択し、オプションでグループの名前を入力します  (この名前は参照用のみには、すべての顧客に表示されません)。完了したら、クリックして**作成**です。 上の説明と同じ **[基本価格]** と **[価格変更のスケジュール]** のオプションが表示されます。ただし、ここでの選択はその市場グループに固有になります。 市場グループには自由設定価格を使用できません。利用可能な価格帯を選択する必要があります。

市場グループに含まれている市場を変更するには、市場グループの名前をクリックし、市場を追加または削除します。**[OK]** をクリックすると変更が保存されます。 

> [!NOTE]
> **[価格設定]** セクションでは、1 つの市場を複数の市場グループに含めることはできません。





