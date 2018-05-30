---
title: リアルタイム アクティビティ サービスのプログラミング
author: KevinAsgari
description: C++ API を使った Xbox Live リアルタイム アクティビティ サービスのプログラミングについて説明します。
ms.assetid: 98cdcb1f-41d8-43db-98fc-6647755d3b17
ms.author: kevinasg
ms.date: 04/04/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, ゲーム, uwp, windows 10, xbox one, リアルタイム アクティビティ
ms.localizationpriority: low
ms.openlocfilehash: 77b2be18fdda6dbf173814787bde151f088086c2
ms.sourcegitcommit: 6618517dc0a4e4100af06e6d27fac133d317e545
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="programming-the-real-time-activity-service-using-c-apis"></a>C++ API を使用したリアルタイム アクティビティ サービスのプログラミング

この記事は、次のセクションで構成されています。

* Xbox Live からのリアルタイム アクティビティ サービスへの接続
* リアルタイム アクティビティ サービスからの切断
* 統計の作成
* リアルタイム アクティビティからの統計へのサブスクライブ
* リアルタイム アクティビティ サービスからの統計へのサブスクライブの解除
* サンプル

## <a name="connecting-to-the-real-time-activity-service-from-xbox-live"></a>Xbox Live からのリアルタイム アクティビティ サービスへの接続

アプリケーションは、リアルタイム アクティビティ (RTA) サービスに接続して、Xbox Live からイベント情報を取得する必要があります。 ここでは、そうした接続の作成方法を示します。

> [!NOTE]
> このトピックの例では、1 人のユーザーのメソッド呼び出しを示します。 ただし、タイトルは、リアルタイム アクティビティ (RTA) サービスに対する接続と接続解除を行うすべてのユーザーに対してこれらの呼び出しを行う必要があります。

### <a name="connecting-to-the-real-time-activity-service"></a>リアルタイム アクティビティ サービスへの接続

```cpp
void Example_RealTimeActivity_ConnectAsync()
{
    // Get the list of users from the system, and create an Xbox Live context from the first.
    // This user's authentication token will be used for the service requests.

    // Note, only retrieve an XboxLiveContext for a given user *once*.  Otherwise you may encounter unpredictable behavior.
    std::shared_ptr<xbox_live_context> xboxLiveContext = std::make_shared<xbox_live_context>(User::Users->GetAt(0));

    xboxLiveContext->real_time_activity_service()->activate();
}
```

### <a name="creating-a-statistic"></a>統計の作成

XDK デベロッパーである場合やクロスプレイ タイトルの開発を行う場合は、XDP で統計を作成します。  Windows 10 で実行される純粋な UWP を作成する場合は、デベロッパー センターで統計を作成します。

#### <a name="xdk-developers"></a>XDK の開発者

XDP で統計を作成する方法については、[XDP のドキュメント](https://developer.xboxlive.com/en-us/xdphelp/development/xdpdocs/Pages/setting_up_service_configuration_10_27_15_a.aspx#events)を参照してください。  統計を作成してイベントを定義したら、[XCETool](https://developer.xboxlive.com/en-us/platform/development/documentation/software/Pages/atoc_xce_jun15.aspx) を実行して、アプリケーションが使用するヘッダーを生成する必要があります。  このヘッダーには、統計を変更するイベントを送信するために呼び出すことができる関数が含まれています。

#### <a name="uwp-developers"></a>UWP の開発者

クロスプレイ タイトルではない Windows 10 上の UWP を開発している場合は、デベロッパー センターで統計を定義します。  これを行う方法についてのドキュメントは間もなく公開されます。  それまで、質問については担当の DAM にお問い合わせください。

### <a name="disconnecting-from-the-real-time-activity-service"></a>リアルタイム アクティビティ サービスからの切断

```cpp
void Example_RealTimeActivity_Disconnect()
{
    // Get the list of users from the system, and create an Xbox Live context from the first.
    // This user's authentication token will be used for the service requests.
    std::shared_ptr<xbox_live_context> xboxLiveContext = std::make_shared<xbox_live_context>(User::Users->GetAt(0));

    xboxLiveContext->real_time_activity_service()->deactivate();
}
```

## <a name="subscribing-to-a-statistic-from-the-real-time-activity"></a>リアルタイム アクティビティからの統計へのサブスクライブ

アプリケーションはリアルタイム アクティビティ (RTA) にサブスクライブして、Xbox デベロッパー ポータル (XDP) で構成した統計が変化したときに最新情報を取得します。

### <a name="subscribing-to-a-statistic-from-the-real-time-activity-service"></a>リアルタイム アクティビティ サービスからの統計へのサブスクライブ

```cpp
void Example_RealTimeActivity_SubscribeToStatisticChangeAsync()
{
    // Obtain xboxLiveContext as shown in the connect function.  Then add a handler to be called on statistic changes.
    function_context statisticsChangeContext = xboxLiveContext->user_statistics_service().add_statistic_changed_handler(
        [](statistic_change_event_args args )
        {
            // Called on statistic change.  Inspect args to see which one.
            DebugPrint("%S %S", args.latest_statistic().statistic_name().c_str(), args.latest_statistic().value().c_str());
        }
    );

    // Call to subscribe to an individual statistic.  Once the subscription is complete, the handler will be called with the initial value of the statistic.
    auto statisticResults = xboxLiveContext->user_statistics_service().subscribe_to_statistic_change(
        User::Users->GetAt(0)->XboxUserId->Data(),
        L"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx",    // Get SCID from "Product Details" page in XDP
         L"YourStat"
        );

    std::shared_ptr<statistic_change_subscription> statisticsChangeSubscription;

    if(!statisticResults.err())
    {
        statisticsChangeSubscription = statisticResults.payload();
    }
    else
    {
        DebugPrint("Error calling SubscribeToStatistic: %S", statisticResults.err_message().c_str());
    }
}
```

## <a name="unsubscribing-from-a-statistic-from-the-real-time-activity-service"></a>リアルタイム アクティビティ サービスからの統計へのサブスクライブの解除

アプリケーションはリアルタイム アクティビティ (RTA) サービスからの統計にサブスクライブして、統計が変化したときに最新情報を取得します。 更新が不要になったら、サブスクリプションを終了できます。このトピックのコードではその方法を示します。

### <a name="unsubscribing-from-a-real-time-services-statistic"></a>リアルタイム サービス統計のサブスクライブ解除

```cpp
void Example_RealTimeActivity_UnsubscribeFromStatisticChangeAsync()
{
    // statisticsChangeSubscription from the Example_RealTimeActivity_SubscribeToStatisticChangeAsync function.
    xboxLiveContext->user_statistics_service().unsubscribe_from_statistic_change(
        statisticsChangeSubscription
        );
}
```