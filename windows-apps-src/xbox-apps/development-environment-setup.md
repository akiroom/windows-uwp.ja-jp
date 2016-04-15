---
title: Xbox の開発環境に UWP を設定する
description: Xbox の開発環境に UWP を設定してテストする手順
area: Xbox
---

# Xbox の開発環境に UWP を設定する

Xbox の開発環境のユニバーサル Windows プラットフォーム (UWP) は、ローカル ネットワークを介して Xbox One コンソールに接続されている開発用 PC で構成されます。
開発用 PC には、Windows 10、Visual Studio 2015 Update 2、Windows 10 SDK プレビュー ビルド 14295 などの幅広いサポート ツールが必要です。


この記事では、開発環境を設定およびテストする手順について説明します。

## Visual Studio のセットアップ

1. Visual Studio 2015 Update 2 以降をインストールします。 詳しい情報とインストール方法については、「[Windows 10 のダウンロードとツール](https://dev.windows.com/downloads)」をご覧ください。

1. Visual Studio 2015 Update 2 をインストールするときは、**[ユニバーサル Windows アプリ開発ツール]** チェック ボックスがオンになっていることを確認します。

  ![Visual Studio 2015 Update 2 をインストールする](images/vs_install_tools.png)

## Windows 10 SDK のセットアップ

Windows 10 SDK プレビュー ビルド 14295 をインストールします。 詳しくは、「[開発者向け Insider Preview 更新プログラムをダウンロード](http://go.microsoft.com/fwlink/p/?LinkId=780552)」をご覧ください。

  > **重要**&nbsp;&nbsp;最新の SDK をインストールする必要があります。ただし、オペレーティング システムの Windows Insider Preview の最新リリースをインストールする必要は_ありません_。

## 初めてのアプリケーションを作成する

1. 開発用 PC がターゲットの Xbox One コンソールと同じローカル ネットワーク上にあることを確認します。 通常、これらは同じルーターを使用し、同じサブネット上にある必要があります。 ワイヤード (有線) ネットワーク接続をお勧めします。

1. Xbox One コンソールが開発者モードになっていることを確認します。  詳しくは、「[Xbox One で開発者モードを有効にする](devkit-activation.md)」をご覧ください。

1. UWP アプリに使用するプログラミング言語を決定します。

1. 開発用 PC で、**[新しいプロジェクト]** をクリックし、**[Windows]、[ユニバーサル]、[空のアプリケーション]** の順にクリックします。

### C# プロジェクトの開始

  ![[新しいプロジェクト] ダイアログ ボックス](images/vs_universal_blank.jpg)

1. **[New Universal Windows Project]** ダイアログ ボックスで既定のオプションを選択します。 **[開発者モード]** ダイアログ ボックスが表示されたら、**[OK]** をクリックします。 新しい空のアプリが作成されます。

1. リモート デバッグの開発環境を構成します。

  1. プロジェクトを右クリックし、**[プロパティ]** をクリックします。
  1. **[デバッグ]** タブで、**[ターゲット デバイス]** を **[リモート コンピューター]** に変更します。
  1. **[リモート コンピューター]** で、システムの IP アドレスまたは Xbox One コンソールのホスト名を入力します。 IP アドレスまたはホスト名の取得について詳しくは、「[Xbox One ツールの概要](introduction-to-xbox-tools.md)」をご覧ください。
  1. **[認証モード]** ドロップダウン リストで、**[ユニバーサル (暗号化されていないプロトコル)]** をクリックします。

    ![C# BlankApp Property Pages](images/vs_remote.jpg)

### C++ プロジェクトの開始

  ![C++ プロジェクト](images/vs_universal_cpp_blank.jpg)

1. **[New Universal Windows Project]** ダイアログ ボックスで既定のオプションを選択します。 **[開発者モード]** ダイアログ ボックスが表示されたら、**[OK]** をクリックします。 新しい空のアプリが作成されます。

1. リモート デバッグの開発環境を構成します。

   1. プロジェクトを右クリックし、**[プロパティ]** をクリックします。
   1. **[デバッグ]** タブで、**[起動するデバッガー]** を **[リモート コンピューター]** に変更します。
   1. **[コンピューター名]** で、システムの IP アドレスまたは Xbox One コンソールのホスト名を入力します。 IP アドレスまたはホスト名の取得について詳しくは、「[Xbox One ツールの概要](introduction-to-xbox-tools.md)」をご覧ください。
   1. **[認証の種類]** ドロップダウン リストで、**[ユニバーサル (暗号化されていないプロトコル)]** をクリックします。

    ![C++ BlankApp プロパティ ページ](images/vs_remote_cpp.jpg)

### PIN を使用してデバイスと Visual Studio をペアリングする

1. 設定を保存し、Xbox One コンソールが開発者モードになっていることを確認します。

1. F5 キーを押します。

1. 初めて展開する場合、Visual Studio に PIN を使用してデバイスとペアリングすることを求めるダイアログ ボックスが表示されます。

  1. PIN を取得するには、Xbox One コンソールのホーム画面から **[Dev Home]** を開きます。
  1. **[Pair with Visual Studio]** をクリックします。

    ![Pair with Visual Studio dialog](images/devhome_visualstudio.png)

  1. **[Pair with Visual Studio]** ダイアログ ボックスに PIN を入力します。 次の PIN は単なる例であり、実際のものとは異なります。

    ![Pair with Visual Studio PIN dialog](images/devhome_pin.png)

  1. 展開エラーが発生した場合、**[出力]** ウィンドウに表示されます。

これで、Xbox に初めての UWP アプリが正しく作成および展開されました。



## 参照
- [Xbox One で開発者モードを有効にする](devkit-activation.md)  
- [Windows 10 用のダウンロードとツール](https://dev.windows.com/downloads)  
- [開発者向け Insider Preview 更新プログラムをダウンロード](http://go.microsoft.com/fwlink/?LinkId=780552)  
- [Xbox One ツールの概要](introduction-to-xbox-tools.md) 
- [Xbox One の UWP](index.md)

----


<!--HONumber=Mar16_HO5-->

