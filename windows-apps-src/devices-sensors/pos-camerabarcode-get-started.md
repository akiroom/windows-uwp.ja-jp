---
title: カメラ バーコード スキャナーの概要
description: カメラ バーコード スキャナーの使用方法について説明します。
ms.date: 05/02/2018
ms.topic: article
keywords: Windows 10, UWP, 店舗販売時点管理, POS
ms.localizationpriority: medium
ms.openlocfilehash: 66dc3d9e12f6ef73e5461b8fe0064f21a0848c7e
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57614077"
---
# <a name="getting-started-with-a-camera-barcode-scanner"></a>カメラ バーコード スキャナーの概要
## <a name="step-1-add-capability-declarations-to-your-app-manifest"></a>手順 1:アプリケーション マニフェストの機能の宣言を追加します。
1. Microsoft Visual Studio の**ソリューション エクスプローラー**で、**package.appxmanifest** 項目をダブルクリックしてアプリケーション マニフェストのデザイナーを開きます。
2. **[機能]** タブをクリックします。
3. **[Web カメラ]** と **[PointOfService]** のチェック ボックスをオンにします。 

>[!NOTE] 
> **Web カメラ**機能は、アプリケーションからプレビューを表示するだけでなく、ソフトウェア デコーダーでカメラからデコードするフレームを受信するためにも必要です。

## <a name="step-2-add-using-directives"></a>手順 2:Using ディレクティブを追加します。

```Csharp
using Windows.Devices.Enumeration;
using Windows.Devices.PointOfService;
```
## <a name="step-3-define-your-device-selector"></a>手順 3:デバイス セレクターを定義します。

### <a name="option-a-find-all-barcode-scanners"></a>**オプション a:すべてのバーコード スキャナーを見つける**

```Csharp
string selector = BarcodeScanner.GetDeviceSelector();       
```

### <a name="option-b-scoping-device-selector-to-connection-type"></a>**オプション b:デバイス セレクターの接続の種類のスコープ**

```Csharp
string selector = BarcodeScanner.GetDeviceSelector(PosConnectionTypes.Local);
DeviceInformationCollection deviceCollection = await DeviceInformation.FindAllAsync(selector);
```

## <a name="step-4-enumerate-barcode-scanners"></a>手順 4:バーコード スキャナを列挙します。
アプリケーションの有効期間においてデバイスのリストが変化することを想定しない場合は、*FindAllAsync* を使用して、1 回だけスナップショットを列挙することができますが、アプリケーションの有効期間においてバーコード スキャナーのリストが変化する可能性がある場合は、代わりに *DeviceWatcher* を使用します。  

> [!Important] 
> GetDefaultAsync を使用して PointOfService デバイスを列挙すると、結果の動作が一貫しない可能性があります。GetDefaultAsync は、クラスで見つかった最初のデバイスを返すだけであり、このデバイスはセッションによって変化する可能性があるためです。

### <a name="option-a-enumerate-a-snapshot-of-barcode-scanners"></a>**オプション a:バーコード スキャナのスナップショットを列挙します。**
```Csharp
DeviceInformationCollection deviceCollection = await DeviceInformation.FindAllAsync(selector);
```

> [!TIP]
> *FindAllAsync* の使用方法の詳細については、「[*デバイスのスナップショットの列挙*](https://docs.microsoft.com/windows/uwp/devices-sensors/enumerate-devices#enumerate-a-snapshot-of-devices)」を参照してください。

### <a name="option-b-enumerate-and-watch-for-changes-in-available-barcode-scanners"></a>**オプション b:列挙し、使用可能なバーコード スキャナーの変化を監視**
```Csharp
DeviceWatcher deviceWatcher = DeviceInformation.CreateWatcher(selector);

// TODO: Add Event Listeners and Handlers
```
> [!TIP]
> 詳細については、「[*デバイスの列挙と監視*](https://docs.microsoft.com/windows/uwp/devices-sensors/enumerate-devices#enumerate-and-watch-devices)」と「[*DeviceWatcher*](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher)」を参照してください。

## <a name="step-5-identify-camera-barcode-scanners"></a>手順 5:カメラのバーコード スキャナーを識別します。
カメラ バーコード スキャナーは、Windows によって、コンピューターに接続されているカメラとソフトウェア デコーダーがペアリングされたときに動的に作成されます。  カメラとデコーダーのペアはそれぞれ完全な機能を持つバーコード スキャナーです。

結果として得られるデバイス コレクションの各バーコード スキャナーについて、[*BarcodeScanner.VideoDeviceID*](https://docs.microsoft.com/uwp/api/windows.devices.pointofservice.barcodescanner.videodeviceid#Windows_Devices_PointOfService_BarcodeScanner_VideoDeviceId) プロパティを確認することによって、カメラ バーコード スキャナーと物理バーコード スキャナーを区別することができます。  VideoDeviceID が NULL 以外である場合は、デバイス コレクションのバーコード スキャナー オブジェクトがカメラ バーコード スキャナーであることを示します。  複数のカメラ バーコード スキャナーがある場合は、物理バーコード スキャナーを含まない別のコレクションを作成することもできます。 

Windows に付属しているデコーダーを使用するカメラ バーコード スキャナーは、次のように表示されます。 

> Microsoft BarcodeScanner (*使用しているカメラの名前*)

カメラがコンピューターのシャーシに組み込まれており、複数のカメラがある場合、名前は*前面*と*背面*で区別されます。  今後、新しいソフトウェア デコーダーが利用可能になり、別の命名規則が適用される可能性があります。

## <a name="step-6-claim-the-camera-barcode-scanner"></a>手順 6:要求のカメラのバーコード スキャナー 
[BarcodeScanner.ClaimScannerAsync](https://docs.microsoft.com/uwp/api/windows.devices.pointofservice.barcodescanner.claimscannerasync#Windows_Devices_PointOfService_BarcodeScanner_ClaimScannerAsync) を使用して、カメラ バーコード スキャナーの排他的使用を取得します。

## <a name="step-7-system-provided-preview"></a>手順 7:システム提供のプレビュー
ユーザーがカメラを正しくバーコードに向けるには、カメラ プレビューが必要です。  Windows には、カメラ バーコード スキャナーの基本的なコントロールを提供するためのダイアログを起動するシンプルなカメラ プレビューが用意されています。  ダイアログを開くときは [ClaimedBarcodeScanner.ShowVideoPreview](https://docs.microsoft.com/uwp/api/windows.devices.pointofservice.claimedbarcodescanner.showvideopreviewasync) を呼び出し、作業が終わってダイアログを閉じるときは [ClaimedBarcodeScanner.HideVideoPreview](https://docs.microsoft.com/uwp/api/windows.devices.pointofservice.claimedbarcodescanner.hidevideopreview) を呼び出すだけです。

> [!TIP]
> アプリケーションでカメラ バーコード スキャナーのプレビューをホストする方法については、「[プレビューのホスト](pos-camerabarcode-hosting-preview.md)」を参照してください。

## <a name="step-8-initiate-scan"></a>手順 8:スキャンを開始します。 
[  **StartSoftwareTriggerAsync**](https://docs.microsoft.com/uwp/api/windows.devices.pointofservice.claimedbarcodescanner.startsoftwaretriggerasync#Windows_Devices_PointOfService_ClaimedBarcodeScanner_StartSoftwareTriggerAsync) を呼び出すことでスキャン プロセスを開始できます。  
[  **IsDisabledOnDataReceived**](https://docs.microsoft.com/uwp/api/windows.devices.pointofservice.claimedbarcodescanner.isdisabledondatareceived#Windows_Devices_PointOfService_ClaimedBarcodeScanner_IsDisabledOnDataReceived) の値に応じて、スキャナーはバーコードを 1 つだけスキャンして停止することも、[**StopSoftwareTriggerAsync**](https://docs.microsoft.com/uwp/api/windows.devices.pointofservice.claimedbarcodescanner.stopsoftwaretriggerasync#Windows_Devices_PointOfService_ClaimedBarcodeScanner_StopSoftwareTriggerAsync) を呼び出すまで継続的にスキャンすることもできます。

[  **IsDisabledOnDataReceived**](https://docs.microsoft.com/uwp/api/windows.devices.pointofservice.claimedbarcodescanner.isdisabledondatareceived#Windows_Devices_PointOfService_ClaimedBarcodeScanner_IsDisabledOnDataReceived) を目的の値に設定することで、バーコードがデコードされたときのスキャナー動作を制御します。

| 値 | 説明 |
| ----- | ----------- |
| True   | バーコードを 1 つだけスキャンして停止する |
| False  | 停止せずに継続的にバーコードをスキャンする |