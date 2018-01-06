---
author: drewbatgit
ms.assetid: 
description: "UWP アプリのゲームのブロードキャストを管理する方法を示します。"
title: "ゲームのブロードキャストを管理する"
ms.author: drewbat
ms.date: 09/27/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: "Windows 10, ゲーム, ブロードキャスト"
ms.localizationpriority: medium
ms.openlocfilehash: 613dd69c00257ac5d750bc67b174d7ff010e0b59
ms.sourcegitcommit: f9a4854b6aecfda472fb3f8b4a2d3b271b327800
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="manage-game-broadcasting"></a>ゲームのブロードキャストを管理する
この記事では、UWP アプリのゲームのブロードキャストを管理する方法を示します。 ユーザーは、Windows に組み込まれているシステム UI を使用してゲームのブロードキャストを開始する必要がありますが、Windows 10 バージョン 1709 以降、アプリでシステムのブロードキャスト UI を起動でき、ブロードキャストが開始および停止されたときには通知を受信できます。

## <a name="add-the-windows-desktop-extensions-for-the-uwp-to-your-app"></a>UWP 用の Windows デスクトップ拡張機能をアプリに追加する
アプリのブロードキャストを管理するための API は、**[Windows.Media.AppBroadcasting](https://docs.microsoft.com/uwp/api/windows.media.appbroadcasting)** 名前空間にあり、ユニバーサル API コントラクトに含まれていません。 この API にアクセスするには、次の手順に従って、UWP 用の Windows デスクトップ拡張機能への参照をアプリに追加する必要があります。

1. Visual Studio の**ソリューション エクスプローラー**で、UWP プロジェクトを展開し、**[参照]** を右クリックして、**[参照の追加]** を選択します。 
2. **[ユニバーサル Windows]** ノードを展開し、**[拡張機能]** を選択します。
3. 拡張機能の一覧で、プロジェクトのターゲット ビルドに一致する **[Windows Desktop Extensions for the UWP]** エントリの横にあるチェック ボックスをオンにします。 アプリのブロードキャスト機能を使用するには、バージョンが 1709 以上である必要があります。
4. **[OK]** をクリックします。

## <a name="launch-the-system-ui-to-allow-the-user-to-initiate-broadcasting"></a>システム UI を起動して、ユーザーがブロードキャストを開始できるようにします。
現在、アプリでブロードキャストできない場合は、いくつかの原因があります。たとえば、現在のデバイスがブロードキャストのハードウェア要件を満たしていない場合や、別のアプリが現在ブロードキャストしている場合です。 システム UI を起動する前に、アプリが現在ブロードキャストできるかどうかを確認できます。 最初に、ブロードキャスト API が現在のデバイスで利用可能かどうかを確認します。 この API は、Windows 10 バージョン 1709 より前のバージョンの OS を実行しているデバイスでは利用できません。 特定の OS バージョンを確認するのではなく、**[ApiInformation.IsApiContractPresent](https://docs.microsoft.com/uwp/api/windows.foundation.metadata.apiinformation#Windows_Foundation_Metadata_ApiInformation_IsApiContractPresent_System_String_System_UInt16_System_UInt16_)** メソッドで、*Windows.Media.AppBroadcasting.AppBroadcastingContract* バージョン 1.0 を照会します。 このコントラクトが存在する場合は、デバイスでブロードキャスト API を利用できます。

次に、一度に 1 人のユーザーがサインインしている PC で、ファクトリ メソッド **[GetDefault](https://docs.microsoft.com/uwp/api/windows.media.appbroadcasting.appbroadcastingui#Windows_Media_AppBroadcasting_AppBroadcastingUI_GetDefault)** を呼び出すことによって、**[AppBroadcastingUI](https://docs.microsoft.com/uwp/api/windows.media.appbroadcasting.appbroadcastingui)** クラスのインスタンスを取得します。 複数のユーザーがログインできる XBox では、代わりに **[GetForUser](https://docs.microsoft.com/uwp/api/windows.media.appbroadcasting.appbroadcastingui#Windows_Media_AppBroadcasting_AppBroadcastingUI_GetForUser_Windows_System_User_)** を呼び出します。 次に、**[GetStatus](https://docs.microsoft.com/uwp/api/windows.media.appbroadcasting.appbroadcastingui#Windows_Media_AppBroadcasting_AppBroadcastingUI_GetStatus)** を呼び出して、アプリのブロードキャストの状態を取得します。

**AppBroadcastingStatus** クラスの **[CanStartBroadcast](https://docs.microsoft.com/uwp/api/windows.media.appbroadcasting.appbroadcastingstatus#Windows_Media_AppBroadcasting_AppBroadcastingStatus_CanStartBroadcast)** プロパティは、アプリが現在ブロードキャストを開始できるかどうかを通知します。 開始できない場合は、**[Details](https://docs.microsoft.com/uwp/api/windows.media.appbroadcasting.appbroadcastingstatus#Windows_Media_AppBroadcasting_AppBroadcastingStatus_Details)** プロパティを調べて、ブロードキャストを利用できない理由を確認できます。 理由に応じて、ユーザーに対してステータスを表示したり、ブロードキャストを有効にするための手順を示したりすることができます。

[!code-cpp[CanStartBroadcast](./code/AppBroadcast/cpp/AppBroadcastExampleApp/App.cpp#SnippetCanStartBroadcast)]

**[ShowBroadcastUI](https://docs.microsoft.com/uwp/api/windows.media.appbroadcasting.appbroadcastingui#Windows_Media_AppBroadcasting_AppBroadcastingUI_ShowBroadcastUI)** を呼び出すことによって、アプリのブロードキャスト UI をシステムで表示することを要求します。

> [!NOTE] 
> **ShowBroadcastUI** メソッドは、システムの現在の状態に応じて、成功しない可能性がある要求を示します。 アプリでは、このメソッドを呼び出した後、ブロードキャストが開始済みであることを想定しないでください。 ブロードキャストが開始または停止するときに通知される **[IsCurrentAppBroadcastingChanged](https://docs.microsoft.com/uwp/api/windows.media.appbroadcasting.appbroadcastingmonitor#Windows_Media_AppBroadcasting_AppBroadcastingMonitor_IsCurrentAppBroadcastingChanged)** イベントを使用します。

[!code-cpp[LaunchBroadcastUI](./code/AppBroadcast/cpp/AppBroadcastExampleApp/App.cpp#SnippetLaunchBroadcastUI)]

## <a name="receive-notifications-when-broadcasting-starts-and-stops"></a>ブロードキャストが開始および停止するときに通知を受信する
ユーザーがシステム UI を使用して、**[AppBroadcastingMonitor](https://docs.microsoft.com/uwp/api/windows.media.appbroadcasting.appbroadcastingmonitor)** クラスのインスタンスを初期化し、**[IsCurrentAppBroadcastingChanged](https://docs.microsoft.com/uwp/api/windows.media.appbroadcasting.appbroadcastingmonitor#Windows_Media_AppBroadcasting_AppBroadcastingMonitor_IsCurrentAppBroadcastingChanged)** イベントのハンドラーを登録することによって、アプリのブロードキャストを開始または停止するときに通知を受信することを登録します。 前のセクションで説明したように、必ずある時点で **[ApiInformation.IsApiContractPresent](https://docs.microsoft.com/uwp/api/windows.foundation.metadata.apiinformation#Windows_Foundation_Metadata_ApiInformation_IsApiContractPresent_System_String_System_UInt16_System_UInt16_)** を使用して、ブロードキャスト API を使用する前に、デバイスにブロードキャスト API が存在することを確認します。 

[!code-cpp[AppBroadcastingRegisterChangedHandler](./code/AppBroadcast/cpp/AppBroadcastExampleApp/App.cpp#SnippetAppBroadcastingRegisterChangedHandler)]

**IsCurrentAppBroadcastingChanged** イベントのハンドラーで、現在のブロードキャストの状態を反映するように、アプリの UI を更新することもできます。

[!code-cpp[AppBroadcastingChangedHandler](./code/AppBroadcast/cpp/AppBroadcastExampleApp/App.cpp#SnippetAppBroadcastingChangedHandler)]

## <a name="related-topics"></a>関連トピック

* [ゲーム](index.md)

 

 



