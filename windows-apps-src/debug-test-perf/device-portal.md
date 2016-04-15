---
ms.assetid: 60fc48dd-91a9-4dd6-a116-9292a7c1f3be
title: Windows Device Portal の概要
description: Windows Device Portal で、ネットワーク経由でリモートから、または USB 接続によって、デバイスの構成と管理を行うための方法を説明します。
---
# Windows Device Portal の概要

Windows Device Portal では、ネットワーク経由でリモートから、または USB 接続によって、デバイスの構成と管理を行えます。 また、Windows デバイスのトラブルシューティングを行ったり、リアルタイムのパフォーマンスを表示するための高度な診断ツールも用意されています。 

デバイス ポータルは、お使いの PC に Web ブラウザーから接続することができるデバイス上の Web サーバーです。 デバイスに Web ブラウザーがある場合、デバイスのブラウザーにローカル接続することもできます。

各デバイス ファミリで Windows Device Portal を利用できますが、機能と設定はデバイスの要件によって異なります。 ここでは、デバイス ポータルの一般的な説明と、各デバイス ファミリに関するさらに詳細な情報が掲載されている記事へのリンクを示します。

Windows Device Portal のすべての機能は [REST API](device-portal-api-core.md) の上に構築されます。REST API を使用してデータにアクセスしたり、プログラムを使ってデバイスを制御することができます。

## 設定

デバイス ポータルへの接続の具体的な手順はデバイスによって異なりますが、どのデバイスでも次の一般的な手順が必要です。
1. デバイスで開発者モードとデバイス ポータルを有効にします。
2. デバイスと PC をローカル ネットワークまたは USB 経由で接続します。
3. ブラウザーでデバイス ポータルのページに移動します。 次の表は、各デバイス ファミリで使用されるポートとプロトコルを示しています。

デバイス ファミリ | 既定でオンになっているか | HTTP | HTTPS | USB
--------------|----------------|------|-------|----
HoloLens | 開発者モードでオン | 80 (既定) | 443 (既定) | localhost:10080
IoT | 開発者モードでオン | 8080 | レジストリ キーで有効化する | 該当なし
Xbox | 開発者モードで有効化 | 無効 | 11443 | 該当なし
Desktop| 開発者モードで有効化 | ランダム > 50,000 (xx080) | ランダム > 50,000 (xx443) | 該当なし
Phone | 開発者モードで有効化 | 80| 443 | localhost:10080

デバイス固有のセットアップ手順については、以下をご覧ください。
- [HoloLens 向けのデバイス ポータル](https://dev.windows.com/holographic/using_the_windows_device_portal)
- [IoT 向けのデバイス ポータル](http://ms-iot.github.io/content/en-US/win10/tools/DevicePortal.htm)
- [モバイル向けのデバイス ポータル](device-portal-mobile.md#setup)
- [Xbox 向けのデバイス ポータル](device-portal-xbox.md)

## 機能

### ツールバーとナビゲーション

ページの上部にあるツールバーは、一般的に使用されるステータスと機能へのアクセスを可能にします。
- **シャット ダウン**: デバイスをオフにします。
- **再起動**: デバイスの電源を入れ直します。
- **ヘルプ**: ヘルプ ページを開きます。

ページの左側にあるナビゲーション ウィンドウのリンクを使用して、デバイスの管理と監視に利用可能なツールに移動します。

ここでは、すべてのデバイスに共通のツールについて説明します。 デバイスによってはその他のオプションを利用できる場合があります。 詳しくは、お使いのデバイス用のページをご覧ください。

### ホーム

デバイス ポータル セッションはホーム ページで開始します。 通常、ホーム ページには、名前や OS のバージョンなどのデバイスに関する情報、およびデバイスについて設定できる項目が表示されます。

### アプリ

デバイスへの AppX パッケージとバンドルのインストール/アンインストールおよび管理を行う機能を提供します。

![モバイル向けのデバイス ポータル](images/device-portal/mob-device-portal-apps.png)

- **インストール済みのアプリ**: アプリを削除および起動します。
- **Running apps**: 現在実行されているアプリを一覧表示します。
- **アプリケーションのインストール**: コンピューターまたはネットワーク上のフォルダーからインストールするアプリ パッケージを選択します。
- **依存関係**: インストールするアプリの依存関係を追加します。
- **展開**: 選択したアプリと依存関係をデバイスに展開します。

**アプリをインストールするには**

1.  [アプリ パッケージを作成](https://msdn.microsoft.com/library/windows/apps/xaml/hh454036(v=vs.140).aspx)したら、デバイス上にリモートでインストールできます。 Visual Studio でビルドすると、出力フォルダーが生成されます。 

    ![アプリのインストール](images/device-portal/iot-installapp0.png)    
2.  [参照] をクリックして、アプリ パッケージ (.appx) を検索します。
3.  [参照] をクリックして、証明書ファイル (.cer) を検索します。 (デバイスによっては不要です。)
4.  依存関係を追加します。 1 つ以上ある場合は、それぞれを個別に追加します。     
5.  [展開] で、[実行] をクリックします。 
6.  別のアプリをインストールするには、リセット ボタンをクリックしてフィールドをクリアします。


**アプリをアンインストールするには**

1.  アプリが実行中でないことを確認します。 
2.  実行中の場合、[Running apps] に移動してそのアプリを閉じます。 アプリの実行中にアンインストールすると、そのアプリを再インストールしようとするときに問題が発生することがあります。 
3.  準備ができたら、[アンインストール] をクリックします。

### プロセス

現在実行中のプロセスに関する詳細を表示します。 これには、アプリとシステムの両方のプロセスが含まれます。

このページでは、PC のタスク マネージャーと同様に、現在実行されているプロセスと、そのプロセスのメモリ使用量を確認できます。  一部のプラットフォーム (Desktop、IoT、および HoloLens) では、プロセスを終了することができます。 

![モバイル向けのデバイス ポータル](images/device-portal/mob-device-portal-processes.png)

### パフォーマンス

電力消費、フレーム レート、CPU 負荷など、システムの診断情報のグラフをリアルタイムで表示します。

利用可能なメトリックを次に示します。
- **CPU**: 使用可能量の合計に対するパーセント
- **メモリ**: 合計メモリ、使用中のメモリ、使用可能なコミット メモリ、ページ メモリ、および非ページ メモリ
- **GPU**: GPU エンジンの使用率、使用可能量の合計に対するパーセント
- **I/O**: 読み取りと書き込み
- **ネットワーク**: 受信と送信

![モバイル向けのデバイス ポータル](images/device-portal/mob-device-portal-perf.png)

### Windows イベント トレーシング (ETW)

デバイス上の Windows イベント トレーシング (ETW) をリアルタイムで管理します。

![モバイル向けのデバイス ポータル](images/device-portal/mob-device-portal-etw.png)

[Hide Providers] チェックボックスをオンにすると、イベントの一覧のみが表示されます。
- **登録済みプロバイダー**: ETW プロバイダーとトレース レベルを選択します。 トレース レベルは次のいずれかの値になります。
    1. 異常終了または終了
    2. 重大なエラー
    3. 警告
    4. エラーではない警告
    5. 詳細なトレース (*)

トレースを開始するには、[有効にする] をクリックまたはタップします。 [有効なプロバイダー] ドロップダウン リストにプロバイダーが追加されます。
- **カスタム プロバイダー**: カスタム ETW プロバイダーとトレース レベルを選択します。 GUID を使用してプロバイダーを識別します。 GUID にはかっこを含めないでください。
- **有効なプロバイダー**: 有効なプロバイダーを一覧表示します。 ドロップダウンからプロバイダーを選択し、[無効にする] をクリックまたはタップしてトレースを停止します。 すべてのトレースを中断するには、[Stop All] をクリックまたはタップします。
- **Providers history**: 現在のセッション中に有効になった ETW プロバイダーを表示します。 無効になっているプロバイダーをアクティブ化するには、[有効にする] をクリックまたはタップします。 履歴をクリアするには、[クリア] をクリックまたはタップします。
- **イベント**: 選択したプロバイダーの ETW イベントを表形式で一覧表示します。 この表は、リアルタイムで更新されます。 すべての ETW イベントを表から削除するには、表の下にある [クリア] ボタンをクリックします。 これによってプロバイダーが無効になることはありません。 [ファイルに保存] をクリックすると、現在収集されている ETW イベントをローカルの CSV ファイルにエクスポートできます。

### パフォーマンス トレース

[Windows Performance Recorder](https://msdn.microsoft.com/library/windows/hardware/hh448205.aspx) (WPR) のトレースをデバイスからキャプチャします。

![モバイル向けのデバイス ポータル](images/device-portal/mob-device-portal-perf-tracing.png)

- **Available profiles**: ドロップダウン リストから WPR プロファイルを選択し、[開始] をクリックまたはタップすると、トレースを開始できます。
- **Custom profiles**: [参照] をクリックまたはタップして、PC から WPR プロファイルを選択します。 [アップロード] をクリックまたはタップすると、トレースが開始します。

トレースを停止するには、停止リンクをクリックします。 トレース ファイル (.ETL) のダウンロードが完了するまで、このページを閉じないでください。

キャプチャした ETL ファイルは、[Windows Performance Analyzer](https://msdn.microsoft.com/library/windows/hardware/hh448170.aspx) で開いて分析に使用できます。

### デバイス

デバイスに接続されているすべての周辺機器を列挙します。

![モバイル向けのデバイス ポータル](images/device-portal/mob-device-portal-devices.png)

### ネットワーク

デバイス上のネットワーク接続を管理します。  デバイス ポータルに USB 経由で接続している場合を除き、これらの設定を変更するとデバイス ポータルとの接続が切断される可能性があります。 
- **プロファイル**: 使用する Wi-Fi プロファイルを選択します。  
- **利用可能なネットワーク**: デバイスで利用可能な Wi-Fi ネットワーク。  ネットワークをクリックまたはタップすると、そのネットワークに接続し、必要に応じてパスキーを提供できます。  注: デバイス ポータルでは Enterprise Authentication はまだサポートされていません。 

![モバイル向けのデバイス ポータル](images/device-portal/mob-device-portal-network.png)



<!--HONumber=Mar16_HO5-->

