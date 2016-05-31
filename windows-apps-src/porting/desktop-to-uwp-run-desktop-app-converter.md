---
author: awkoren
Description: Desktop Converter App を実行して、Windows デスクトップ アプリケーション (Win32、WPF、Windows フォームなど) をユニバーサル Windows プラットフォーム (UWP) アプリに変換します。
Search.Product: eADQiWindows 10XVcnh
title: Desktop App Converter プレビュー (Project Centennial)
---

# Desktop App Converter プレビュー (Project Centennial)

\[一部の情報はリリース前の製品に関することであり、正式版がリリースされるまでに大幅に変更される可能性があります。 ここに記載された情報について、マイクロソフトは明示または黙示を問わずいかなる保証をするものでもありません。\]

[Desktop App Converter を入手しましょう。](http://go.microsoft.com/fwlink/?LinkId=785437)

Desktop App Converter は、.NET 4.6.1 または Win32 向けに記述された既存のデスクトップ アプリをユニバーサル Windows プラットフォーム (UWP) に変換するためのプレリリース版ツールです。 このコンバーターを使って、無人 (サイレント) モードでデスクトップのインストーラーを実行し、開発コンピューターで PowerShell の Add-appxpackage コマンドレットを使ってインストールすることができる AppX パッケージを作成できます。

このコンバーターは、コンバーターのダウンロードに含まれるクリーンな状態の基本イメージを使って、分離された Windows 環境でデスクトップのインストーラーを実行します。 デスクトップ インストーラーが作成するすべてのレジストリとファイル システムの I/O をキャプチャし、出力の一部としてパッケージ化します。 パッケージ ID を持ち、多くの WinRT API を呼び出すことができる AppX を出力します。

## システム要件

### サポートされるオペレーティング システム
+ Windows 10 Anniversary Update Enterprise edition preview (Build 10.0.14316.0 以上)

### 必要なハードウェア構成

コンピューターの能力の最低条件を示します。
+ 64 ビット (x64) プロセッサ
+ ハードウェア支援による仮想化
+ Second Level Address Translation (SLAT)

### 推奨されるリソース
+ [Windows 10 用 Windows ソフトウェア開発キット (SDK)](https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk)

## Desktop App Converter をセットアップする   
Desktop App Converter は、Windows Insider Preview ビルドに含まれている Windows 10 の機能に依存しています。 このコンバーターを利用するには、最新ビルドであることを確認します。

1. 最新の Windows 10 Insider Preview OS - Enterprise edition (Build 10.0.14316.0 以上) であることを確認します。
2. DesktopAppConverter.zip と BaseImage 14316.wim をダウンロードします。
3. ローカル フォルダーに DesktopAppConverter.zip を抽出します。
4. 管理者 PowerShell ウィンドウの場合。  
```CMD
PS C:\> Set-ExecutionPolicy bypass
```
5. 管理者 PowerShell ウィンドウから、次のコマンドを実行してコンバーターをセットアップします。
```CMD
PS C:\> .\DesktopAppConverter.ps1 -Setup -BaseImage .\BaseImage-14316.wim
```
6. 上のコマンドを実行したときに再起動を求めるメッセージが表示されたら、コンピューターを再起動してコマンドをもう一度実行します。

## Desktop App Converter を実行する
Desktop App Converter のエントリ ポイントは、PowerShell とコマンド シェルの 2 つです。 変換プロセスを開始するには、これらのエントリ ポイントのいずれかを使います。

### 用途
```CMD
DesktopAppConverter.ps1
-ExpandedBaseImage <String>
-Installer <String> [-InstallerArguments <String>] [-InstallerValidExitCodes <Int32>]
-Destination <String>
-PackageName <String>
-Publisher <String>
-Version <Version>
[-AppExecutable <String>]
[-AppFileTypes <String>]
[-AppId <String>]
[-AppDisplayName <String>]
[-AppDescription <String>]
[-PackageDisplayName <String>]
[-PackagePublisherDisplayName <String>]
[-MakeAppx]
[-NatSubnetPrefix <String>]
[-LogFile <String>]
[<CommonParameters>]  
```

### 例
次の例では、*MyApp* という名前のデスクトップ アプリを *&lt;publisher_name&gt;* で UWP パッケージ (AppX) に変換する方法を説明します。

+ 管理者 PowerShell ウィンドウから次のコマンドを実行します。
```CMD
PS C:\>.\DesktopAppConverter.ps1 -ExpandedBaseImage C:\ProgramData\Microsoft\Windows\Images\BaseImage-14316
-Installer C:\Installer\MyApp.exe -InstallerArguments "/S" -Destination C:\Output\MyApp
-PackageName "MyApp" -Publisher "CN=<publisher_name>" -Version 0.0.0.1 -MakeAppx -Verbose
```

## 変換済み AppX を展開する
Powershell で [Add-appxpackage](https://technet.microsoft.com/en-us/library/hh856048.aspx) コマンドレットを使って、ユーザー アカウントに対して署名済みのアプリ パッケージ (.appx) を展開します。 .appx パッケージに署名するには、セクション「.Appx パッケージの署名」をご覧ください。 また、このコマンドレットに *Register* パラメーターを指定して、開発プロセス中にパッケージ化を解除したファイルのフォルダーからインストールすることもできます。 詳細については、「[変換済みの UWP アプリを展開してデバッグする](desktop-to-uwp-deploy-and-debug.md)」をご覧ください。

## .Appx パッケージに署名する

Add-appxpackage コマンドレットを使うには、展開するアプリケーション パッケージ (.appx) が署名されている必要があります。 .appx パッケージに署名するには、Microsoft Windows 10 SDK に付属している SignTool.exe を使います。

### 例
```CMD
C:\> MakeCert.exe -r -h 0 -n "CN=<publisher_name>" -eku 1.3.6.1.5.5.7.3.3 -pe -sv <my.pvk> <my.cer>
C:\> pvk2pfx.exe -pvk <my.pvk> -spc <my.cer> -pfx <my.pfx>
C:\> signtool.exe sign -f <my.pfx> -fd SHA256 -v .\<outputAppX>.appx
```
**注:** MakeCert.exe を実行したときにパスワードの入力を求められたら、**[なし]** を選択します。

証明書と署名について詳しくは、以下をご覧ください。

+ [方法: 開発中に使う一時的な証明書を作成する](https://msdn.microsoft.com/library/ms733813.aspx)
+ [SignTool](https://msdn.microsoft.com/library/windows/desktop/aa387764.aspx)
+ [SignTool.exe (署名ツール)](https://msdn.microsoft.com/library/8s9b9yaz.aspx)

### 注意事項
1. ホスト コンピューターの Windows 10 ビルドは、Desktop App Converter ダウンロードに含まれていた基本イメージと一致する必要があります。  
2. コンバーターはディレクトのすべての内容を分離されている Windows 環境にコピーするため、デスクトップ インストーラーが独立したディレクトリにあることを確認します。  
3. 現時点では、Desktop App Converter は 64 ビット オペレーティング システムのみで、変換処理の実行をサポートします。 変換済みの .appx パッケージは、64 ビット (x64) OS のみに展開できます。  
4. Desktop App Converter では、デスクトップ インストーラーを無人モードで実行する必要があります。 *- InstallerArguments* パラメーターを使って、インストーラーのサイレント フラグをコンバーターに渡してください。
5. パブリック SxS Fusion アセンブリの公開は機能しません。 アプリケーションは、インストール中にパブリック side-by-side Fusion アセンブリを公開して、他のプロセスからアクセスできるようにします。 これらのアセンブリは、プロセスのアクティブ化コンテキストの作成中に、CSRSS.exe という名前のシステム プロセスによって取得されます。 Centennial プロセスでこれが行われると、アクティブ化コンテキスト作成とこれらのアセンブリのモジュール読み込みは失敗します。 ComCtl などの受信トレイ アセンブリは OS に同梱されているので、Centennial プロセスがこれらのアセンブリに依存していても安全です。 SxS Fusion アセンブリは、次の場所に登録されています。
  + レジストリ: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\SideBySide\Winners`
  + ファイル システム: %windir%\\SideBySide

## Desktop App Converter の利用統計情報  
Desktop App Converter は、ソフトウェアの使用者と使用方法に関する情報を収集して、この情報を Microsoft に送信することがあります。 Microsoft のデータ収集と製品ドキュメントでの使用の詳細については、「[マイクロソフトのプライバシーに関する声明](http://go.microsoft.com/fwlink/?LinkId=521839)」をご覧ください。 マイクロソフトのプライバシーに関する声明の該当するすべての条項に準拠することに同意します。

既定では、Desktop App Converter の利用統計情報は有効にされています。 利用統計情報を目的の設定に構成するには、次のレジストリ キーを追加します。  
```CMD
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DesktopAppConverter
```
+ DWORD を 1 に設定して、*DisableTelemetry* 値を追加または編集します。
+ 利用統計情報を有効にするには、このキーを削除するかキーの値を 0 に設定します。

## Desktop App Converter の使用法
Desktop App Converter のパラメーターの一覧を示します。 この一覧は、次のコマンドを実行して、Windows Powershell ウィンドウでも表示できます。  
```CMD
get-help .\DesktopAppConverter.ps1 -detailed
```

### セットアップ パラメーター  
|パラメーター|説明|
|---------|-----------|
|```-Setup [<SwitchParameter>]``` | このフラグは、DesktopAppConverter をセットアップ モードで実行する場合に使います。 セットアップ モードでは、用意されている基本イメージの展開をサポートします。|
|```-BaseImage <String>``` | 展開されていない基本イメージの完全パス。 このパラメーターは、-Setup を指定する場合に必要です。|
|```-LogFile <String>``` (省略可能) | ログ ファイルを指定します。 省略すると、ログ ファイルの一時的な場所が作成されます。|

### 変換パラメーター  
|パラメーター|説明|
|---------|-----------|
|```-ExpandedBaseImage <String>``` | 既に展開済みの基本イメージの完全パス。|
|```-Installer <String>``` | アプリケーションのインストーラーのパス。無人/サイレント モードで実行できる必要があります。|
|```-InstallerArguments <String>``` (省略可能) | インストーラーに無人/サイレント モードでの実行を強制する引数の文字列、またはコンマ区切り一覧。 インストーラーが msi の場合は、このパラメーターは省略可能です。 インストーラーからログを取得するには、ここで、インストーラーのログ記録の引数を指定し、パス ```<log_folder>``` (コンバーターが適切なパスに置換するトークン) を使います。 <br><br>**注: 無人/サイレント フラグとログの引数は、インストーラー テクノロジごとに異なります。** <br><br>このパラメーターの使用例:```-InstallerArguments "/silent /log <log_folder>\install.log"```。ログ ファイルを生成しない別の例: ```-InstallerArguments "/quiet", "/norestart"```。繰り返しになりますが、コンバーターでログをキャプチャし、最終的なログ フォルダーに格納する場合は、文字どおりすべてのログにトークン パス ```<log_folder>``` を指定する必要があります。|
|```-InstallerValidExitCodes <Int32>``` (省略可能) | インストーラーの正常な実行を示す、コンマで区切った終了コードの一覧 (例: 0, 1234, 5678)。  既定では、非 msi は 0、msi は 0, 1641, 3010 です。|
|```-Destination <String>``` | コンバーターが appx を出力する場所。この場所がまだ存在しない場合は、DesktopAppConverter が作成できます。|

### Appx ID パラメーター  
|パラメーター|説明|
|---------|-----------|
|```-PackageName <String>``` | ユニバーサル Windows アプリ パッケージの名前
|```-Publisher <String>``` | ユニバーサル Windows アプリ パッケージの発行元
|```-Version <Version>``` | ユニバーサル Windows アプリ パッケージのバージョン番号

### Appx マニフェストのオプションのパラメーター  
|パラメーター|説明|
|---------|-----------|
|```-AppExecutable <String>``` (省略可能) | アプリケーションの主な実行可能ファイルをインストールした場合、その完全パス (インストールは必須ではありません)。例: "C:\Program Files (x86)\MyApp\MyApp.exe"。|
|```-AppFileTypes <String>``` (省略可能) | アプリケーションに関連付ける、ファイルの種類のコンマ区切りの一覧 (例: ".txt, .doc"。引用符は不要)。|
|```-AppId <String>``` (省略可能) | appx マニフェストでアプリケーション ID を設定する値を指定します。 指定しないと、*PackageName* で渡した値が設定されます。|
|```-AppDisplayName <String>``` (省略可能) | appx マニフェストでアプリケーション表示名を設定する値を指定します。 指定しないと、*PackageName* で渡した値が設定されます。 |
|```-AppDescription <String>``` (省略可能) | appx マニフェストでアプリケーションの説明を設定する値を指定します。 指定しないと、*PackageName* で渡した値が設定されます。|
|```-PackageDisplayName <String>``` (省略可能) | appx マニフェストでパッケージ表示名を設定する値を指定します。 指定しないと、*PackageName* で渡した値が設定されます。 |
|```-PackagePublisherDisplayName <String>``` (省略可能) | appx マニフェストでパッケージの発行元表示名を設定する値を指定します。 指定しないと、*Publisher* で渡した値が設定されます。 |

### その他の変換パラメーター  
|パラメーター|説明|
|---------|-----------|
|```-MakeAppx [<SwitchParameter>]``` (省略可能) | このスクリプトに出力で MakeAppx を呼び出すように指示するスイッチ (存在する場合)。 |
|```-NatSubnetPrefix <String>``` (省略可能) | Nat インスタンスで使うプレフィックス値。 通常この値は、ホスト コンピューターがコンバーターの NetNat と同じサブネット範囲に割り当てられている場合にのみ変更します。 現在のコンバーターの NetNat 構成は **Get NetNat** コマンドレットを使って照会できます。 |
|```-LogFile <String>``` (省略可能) | ログ ファイルを指定します。 省略すると、ログ ファイルの一時的な場所が作成されます。 |
|```<Common parameters>``` | このコマンドレットは、次の共通パラメーターをサポートします: *Verbose*、*Debug*、*ErrorAction*、*ErrorVariable*、*WarningAction*、*WarningVariable*、*OutBuffer*、*PipelineVariable*、および *OutVariable*。 詳細については、「[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216)」をご覧ください。 |

## 参照
+ [Desktop App Converter を入手する](http://go.microsoft.com/fwlink/?LinkId=785437)
+ [ユニバーサル Windows プラットフォームへのデスクトップ アプリの移行](https://developer.microsoft.com/en-us/windows/bridges/desktop)
+ [Desktop App Converter を使う UWP へのデスクトップ アプリの移行](https://channel9.msdn.com/events/Build/2016/P504)
+ [Project Centennial: ユニバーサル Windows プラットフォームへの既存のデスクトップ アプリケーションの移行](https://channel9.msdn.com/events/Build/2016/B829)  
+ [デスクトップ ブリッジの UserVoice (Project Centennial)](http://aka.ms/UserVoiceDesktopToUwp)


<!--HONumber=May16_HO2-->

