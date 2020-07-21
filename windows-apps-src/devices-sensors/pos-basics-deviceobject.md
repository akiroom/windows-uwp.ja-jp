---
title: PointOfService デバイス オブジェクト
description: PointOfService デバイス オブジェクトの作成の詳細
ms.date: 06/19/2018
ms.topic: article
keywords: Windows 10, UWP, 店舗販売時点管理, POS
ms.localizationpriority: medium
ms.openlocfilehash: a2fa7e107d890a5be7c8d27af03289b839ec3c09
ms.sourcegitcommit: ca1b5c3ab905ebc6a5b597145a762e2c170a0d1c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79209988"
---
# <a name="pointofservice-device-objects"></a>PointOfService デバイス オブジェクト

## <a name="creating-a-device-object"></a>デバイス オブジェクトの作成
新しい列挙または保存された DeviceID のいずれかから、使用する PointOfService デバイスを特定したら、プログラムにより選択した、またはユーザーが新しい POS デバイス オブジェクトを作成するために選択した [**DeviceID**](https://docs.microsoft.com/uwp/api/windows.devices.pointofservice.barcodescanner.fromidasync) を使用して [**FromIdAsync**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.id) を呼び出します。

このサンプルでは、DeviceID を使用して FromIdAsync で新しい BarcodeScanner オブジェクトを作成することを試みています。 オブジェクトの作成に失敗した場合は、デバッグ メッセージが書き込まれます。

```Csharp

    BarcodeScanner barcodeScanner = await BarcodeScanner.FromIdAsync(DeviceId);

    if(barcodeScanner != null)
    {
        // after successful creation, claim the scanner for exclusive use and enable it to exchange data
    }
    else
    {
        Debug.WriteLine("Failure to create barcodeScanner object");
    }
    
```

デバイス オブジェクトを作成したら、デバイスのメソッド、プロパティ、およびイベントにアクセスできます。  

## <a name="device-object-lifecycle"></a>デバイス オブジェクトのライフサイクル
Windows 8 より前は、アプリのライフサイクルは単純でした。 Win32 アプリや .NET アプリは、実行されているか、実行されていないかのどちらかであり、PointOfService 周辺機器は通常、アプリの完全なライフ サイクルに対して要求されています。 ユーザーがアプリを最小化し、他のアプリに切り替えても、アプリは引き続き実行されています。 ポータブル デバイスが台頭し、電源管理がますます重要になるまでは、これで問題はありませんでした。

Windows 8 では、UWP アプリにより新しいアプリケーション モデルが導入されました。 大まかに言うと、新しい中断状態が追加されました。 UWP アプリは、ユーザーがアプリを最小化するか、別のアプリに切り替えた後、すぐに中断されます。 つまり、アプリのスレッドは停止し、オペレーティング システムがリソースを再利用する必要がある場合を除き、アプリはメモリ内に残ります。PointOfService 周辺機器を表すデバイス オブジェクトは自動的に終了し、他のアプリケーションが周辺機器にアクセスできるようになります。 ユーザーが元のアプリに切り替えると、アプリはすばやく実行中の状態に復元されます。また、PointOfService 周辺機器が再開時にまだ利用可能であれば、PointOfService 周辺機器の接続が復元されます。

\<DeviceObject\>を使用して、何らかの理由でオブジェクトが閉じられたことを検出できます。イベントハンドラーは、後で接続を再確立するためのデバイス ID をメモしておきます。   または、アプリの一時停止通知でこれを処理し、アプリの再開通知でデバイスの接続を再確立するためにデバイス ID を保存することができます。  \<DeviceObject\>の両方で、イベントハンドラーとデバイスオブジェクトの重複したアクションが実行されていないことを確認します。終了とアプリの中断。

> [!TIP]
> Windows 10 ユニバーサル Windows プラットフォーム (UWP) アプリケーションのライフサイクルの詳細については、次のトピックを参照してください。
> - [Windows 10 ユニバーサル Windows プラットフォーム (UWP) アプリのライフサイクル](../launch-resume/app-lifecycle.md)
> - [アプリの中断を処理する](../launch-resume/suspend-an-app.md)
> - [アプリの再開の処理](../launch-resume/resume-an-app.md)
