---
title: デベロッパー センターでのデータ共有の構成
author: KevinAsgari
description: デベロッパー センターでデータ共有を構成して他のアプリ、ゲーム、サービスが Xbox Live の設定にアクセスすることを許可する方法について説明します。
ms.assetid: ''
ms.author: kevinasg
ms.date: 02/21/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: low
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One, UDC, ユニバーサル デベロッパー センター
ms.openlocfilehash: 46ad77cd5e966e4e48ec13d64684580df82a52e9
ms.sourcegitcommit: 0ee9c6848cb9d624f15cdab1d0c5991ca7245e70
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2018
---
# <a name="configure-data-sharing-on-dev-center"></a>デベロッパー センターでのデータ共有の構成

[Windows デベロッパー センター](https://developer.microsoft.com/dashboard/windows/overview)を使うと、他のサービス、ゲーム、アプリがタイトルの Xbox Live 設定とデータにアクセスすることを許可できます。 たとえば、Web サイトでのランキングを Web サービスに表示したり、ゲームのタイトル ストレージにアクセスしてセーブされたゲーム データを表示または変更できる比較アプリを作成したりすることができます。

既定では、タイトル自体のみが Xbox Live サービスに保存された設定とデータにアクセスできます。 これは、デベロッパー センターでデータ共有を構成することによって変更できます。

> [!NOTE]
> このトピックは、Xbox Live クリエーターズ プログラムのタイトルには適用されません。

次の手順に従って、構成を追加します。

1. [デベロッパー センター](https://developer.microsoft.com/dashboard/windows/overview)でタイトルを選択したら、**[サービス]** > **[Xbox Live]** に移動します。

2. **データ共有**へのリンクをクリックします。

3. アクセスを許可する設定をクリックし、アプリ/サービスの追加ボタンをクリックします。 その設定にアクセスできるように構成されたアプリ/サービスの一覧の下に新しい行が追加されます。

4. ドロップダウン ボックスでアプリまたはサービスの種類を選択し、詳細ボックスに入力して、データにアクセスするアプリやサービスのアプリ、タイトル ID、サービス ID を指定します。

5. アプリまたはサービスがデータを読み取るだけなのか、データにフル アクセスするのかを選択します。

6. 設定ごと、およびそれらの設定へのアクセスが必要なアプリやサービスごとに繰り返します。 **[削除]** をクリックすると配列を削除できます。

7. 作業が完了したら、**[保存]** ボタンをクリックして変更を保存します。

![データ共有、アプリやサービスの追加画面](../../images/dev-center/data-sharing-2.png)