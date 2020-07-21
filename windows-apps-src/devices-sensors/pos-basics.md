---
title: サービスポイントの基礎
description: この記事では、PointOfService Windows ランタイム Api の概要について説明します。
ms.date: 12/3/2019
ms.topic: article
keywords: Windows 10, UWP, 店舗販売時点管理, POS
ms.localizationpriority: medium
ms.openlocfilehash: cb8acf5f7dce8e81d72850a4dbd097083b240864
ms.sourcegitcommit: ef723e3d6b1b67213c78da696838a920c66d5d30
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/02/2020
ms.locfileid: "82730044"
---
# <a name="point-of-service-basics"></a>サービスポイントの基礎

このセクションには、すべての POS デバイス カテゴリに共通するトピックが含まれています。

|トピック |説明 |
|------|------------|
| [機能の宣言](pos-basics-capability.md)      | **pointOfService** 機能をアプリケーション マニフェストに追加する方法について説明します。  Windows.Devices.PointOfService 名前空間の使用にはこの機能が必要になります。  |
| [デバイスの列挙](pos-basics-enumerating.md)        | システムが利用できるデバイスを照会するために使用するデバイス セレクターを定義し、このセレクターを使用して POS デバイスを列挙する方法について説明します。  |
| [デバイスオブジェクトの作成](pos-basics-deviceobject.md)  | 周辺機器の読み取り専用のプロパティにアクセスできるようにする PointOfService デバイス オブジェクトを作成し、排他的使用のために周辺機器を要求する方法について説明します。 |
| [要求と有効化](pos-basics-claim.md)  | PointOfService ペリフェラルを予約して排他的に使用し、i/o 操作を有効にする方法について説明します。  |
| [周辺機器の共有](pos-basics-sharing.md) | 複数の Pc が各コンピューターに接続された専用の周辺機器ではなく、共有周辺機器に依存している環境で、ネットワークまたは Bluetooth で接続された周辺機器を他のコンピューターと共有する方法について説明します。
| [PointOfService エンドツーエンド](pos-get-started.md)  | これは、上の例を利用して、PointOfService ペリフェラルと対話する方法のエンドツーエンドの例です。 |
|

## <a name="see-also"></a>関連項目

| トピック   | 説明 |
|:--------|:------------|
| [アプリケーションの配布](../publish/distribute-lob-apps-to-enterprises.md) | 企業のお客様にアプリを配布するためのオプションについて説明します。 |
| [アプリケーションのライフサイクル](../launch-resume/app-lifecycle.md) | UWP アプリケーションのライフサイクルと、Windows がアプリを起動、中断、再開するときの動作について説明します。 |
| [アプリケーションリソース](../app-resources/index.md) | アプリの文字列、イメージ、およびファイルリソースを作成、パッケージ化、使用する方法について説明します。 |
| [データ バインディング](../data-binding/index.md) | データバインディングを使用して、アプリの UI にデータを表示する方法について説明します。 |
| [デバイス列挙型](enumerate-devices.md) | 詳細な列挙方法を使用して周辺機器を見つける方法について説明します。|
| [バージョンアダプティブアプリケーション](../debug-test-perf/version-adaptive-apps.md) | 複数のバージョンの Windows 10 で動作するようにアプリを設計する方法を説明します。|
|


## <a name="sample-code"></a>サンプル コード
+ [バーコード スキャナーのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BarcodeScanner)
+ [キャッシュ ドロワーのサンプル]( https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CashDrawer)
+ [ライン ディスプレイのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/LineDisplay)
+ [磁気ストライプ リーダーのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MagneticStripeReader)
+ [POS プリンターのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/PosPrinter)
