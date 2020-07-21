---
ms.assetid: 88132B6F-FB50-4B03-BC21-233988746230
title: 印刷プレビュー UI のカスタマイズ
description: このセクションでは、印刷プレビュー UI の印刷オプションや設定をカスタマイズする方法について説明します。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10、uwp、印刷
ms.localizationpriority: medium
ms.openlocfilehash: 000985d5f9dac5363a1ea2fb002c2be40e2777dd
ms.sourcegitcommit: b52ddecccb9e68dbb71695af3078005a2eb78af1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74258653"
---
# <a name="customize-the-print-preview-ui"></a>印刷プレビュー UI のカスタマイズ



**重要な API**

-   [**Windows. Graphics. 印刷**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Printing)
-   [**Windows. UI. .Xaml. 印刷**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Printing)
-   [**PrintManager**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Printing.PrintManager)

このセクションでは、印刷プレビュー UI の印刷オプションや設定をカスタマイズする方法について説明します。 印刷機能の詳細については、「[アプリからの印刷](print-from-your-app.md)」を参照してください。

**ヒント**  このトピックのほとんどの例は、印刷のサンプルに基づいています。 完全なコードを確認するには、GitHub の [Windows-universal-samples リポジトリ](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Printing)から[ユニバーサル Windows プラットフォーム (UWP) 印刷サンプル](https://github.com/Microsoft/Windows-universal-samples)をダウンロードしてください。

 

## <a name="customize-print-options"></a>印刷オプションのカスタマイズ

既定では、印刷プレビュー UI には [**ColorMode**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.colormode)、[**Copies**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.copies)、および [**Orientation**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.orientation) の印刷オプションが表示されます。 これらに加え、印刷プレビュー UI に追加できるその他の一般的なプリンター オプションがいくつか用意されています。

-   [**関連付け**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.binding)
-   [**規則**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.collation)
-   [**通信**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.duplex)
-   [**HolePunch**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.holepunch)
-   [**InputBin**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.inputbin)
-   [**MediaSize**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.mediasize)
-   [**MediaType**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.mediatype)
-   [**NUp**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.nup)
-   [**PrintQuality**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.printquality)
-   [**ステープル**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.staple)

これらのオプションは、[**StandardPrintTaskOptions**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Printing.StandardPrintTaskOptions) クラスで定義されます。 印刷プレビュー UI に表示されるオプションの一覧へのオプションの追加や、この一覧からのオプションの削除ができます。 また、オプションが表示される順序の変更や、ユーザーに表示される既定の設定の構成もできます。

ただし、この方法を使って加えた変更は、印刷プレビュー UI にのみ影響します。 ユーザーは印刷プレビュー UI で **[その他の設定]** をタップすることで、プリンターでサポートされているすべてのオプションにいつでもアクセスできます。

**メモ**  表示する印刷オプションはアプリで指定できますが、[印刷プレビュー] UI には、選択したプリンターでサポートされているものだけが表示されます。 印刷 UI には、選んだプリンターでサポートされないオプションは表示されません。

 

### <a name="define-the-options-to-display"></a>表示するオプションの定義

アプリの画面が読み込まれると、印刷コントラクトに登録されます。 その登録には、[**PrintTaskRequested**](https://docs.microsoft.com/uwp/api/Windows.Foundation.IAsyncOperationWithProgress_TResult_TProgress_#Windows_Foundation_IAsyncOperationWithProgress_2_Progress) イベント ハンドラーの定義が含まれています。 印刷プレビュー UI に表示されるオプションをカスタマイズするコードは、**PrintTaskRequested** イベント ハンドラーに追加します。

[  **PrintTaskRequested**](https://docs.microsoft.com/uwp/api/Windows.Foundation.IAsyncOperationWithProgress_TResult_TProgress_#Windows_Foundation_IAsyncOperationWithProgress_2_Progress) イベント ハンドラーを変更して、印刷プレビュー UI に表示する印刷設定を構成する [**printTask.options**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.printtask.options) 命令を含めます。印刷オプションのカスタマイズ リストを表示するアプリの画面の場合は、ヘルパー クラスの **PrintTaskRequested** イベント ハンドラーを上書きし、この画面が印刷されるときに表示するオプションを指定するコードを含めます。

``` csharp
protected override void PrintTaskRequested(PrintManager sender, PrintTaskRequestedEventArgs e)
{
   PrintTask printTask = null;
   printTask = e.Request.CreatePrintTask("C# Printing SDK Sample", sourceRequestedArgs =>
   {
         IList<string> displayedOptions = printTask.Options.DisplayedOptions;

         // Choose the printer options to be shown.
         // The order in which the options are appended determines the order in which they appear in the UI
         displayedOptions.Clear();
         displayedOptions.Add(Windows.Graphics.Printing.StandardPrintTaskOptions.Copies);
         displayedOptions.Add(Windows.Graphics.Printing.StandardPrintTaskOptions.Orientation);
         displayedOptions.Add(Windows.Graphics.Printing.StandardPrintTaskOptions.MediaSize);
         displayedOptions.Add(Windows.Graphics.Printing.StandardPrintTaskOptions.Collation);
         displayedOptions.Add(Windows.Graphics.Printing.StandardPrintTaskOptions.Duplex);

         // Preset the default value of the printer option
         printTask.Options.MediaSize = PrintMediaSize.NorthAmericaLegal;

         // Print Task event handler is invoked when the print job is completed.
         printTask.Completed += async (s, args) =>
         {
            // Notify the user when the print operation fails.
            if (args.Completion == PrintTaskCompletion.Failed)
            {
               await scenarioPage.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
               {
                     MainPage.Current.NotifyUser("Failed to print.", NotifyType.ErrorMessage);
               });
            }
         };

         sourceRequestedArgs.SetSource(printDocumentSource);
   });
}
```

**重要**  displayedOptions () を呼び出すと、 **[詳細設定]** リンクを含む、印刷プレビュー UI からすべての印刷オプションが削除され[**ます。** ](https://docs.microsoft.com/uwp/api/windows.graphics.printing.printtaskoptions.displayedoptions) 印刷プレビュー UI に表示するオプションを必ず追加してください。

### <a name="specify-default-options"></a>既定のオプションの指定

印刷プレビュー UI には、オプションの既定値を設定することもできます。 次のコード行は前の例から抜粋したものであり、[**MediaSize**](https://docs.microsoft.com/uwp/api/windows.graphics.printing.standardprinttaskoptions.mediasize) オプションの既定値を設定しています。

``` csharp
         // Preset the default value of the printer option
         printTask.Options.MediaSize = PrintMediaSize.NorthAmericaLegal;
```         

## <a name="add-new-print-options"></a>新しい印刷オプションの追加

このセクションでは、新しい印刷オプションを作成し、オプションがサポートする値の一覧を定義して、印刷プレビューにオプションを追加する方法について説明します。 前のセクションと同様に、[**PrintTaskRequested**](https://docs.microsoft.com/uwp/api/Windows.Foundation.IAsyncOperationWithProgress_TResult_TProgress_#Windows_Foundation_IAsyncOperationWithProgress_2_Progress) イベント ハンドラーに新しい印刷オプションを追加します。

まず、[**PrintTaskOptionDetails**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Printing.OptionDetails.PrintTaskOptionDetails) オブジェクトを取得します。 これは、印刷プレビュー UI に新しい印刷オプションを追加するために使用します。 次に、印刷プレビュー UI に表示されるオプションの一覧をクリアし、ユーザーがアプリから印刷する場合に表示するオプションを追加します。 その後、新しい印刷オプションを作成し、オプションの値の一覧を初期化します。 最後に、新しいオプションを追加して **OptionChanged** イベントのハンドラーを割り当てます。

``` csharp
protected override void PrintTaskRequested(PrintManager sender, PrintTaskRequestedEventArgs e)
{
   PrintTask printTask = null;
   printTask = e.Request.CreatePrintTask("C# Printing SDK Sample", sourceRequestedArgs =>
   {
         PrintTaskOptionDetails printDetailedOptions = PrintTaskOptionDetails.GetFromPrintTaskOptions(printTask.Options);
         IList<string> displayedOptions = printDetailedOptions.DisplayedOptions;

         // Choose the printer options to be shown.
         // The order in which the options are appended determines the order in which they appear in the UI
         displayedOptions.Clear();

         displayedOptions.Add(Windows.Graphics.Printing.StandardPrintTaskOptions.Copies);
         displayedOptions.Add(Windows.Graphics.Printing.StandardPrintTaskOptions.Orientation);
         displayedOptions.Add(Windows.Graphics.Printing.StandardPrintTaskOptions.ColorMode);

         // Create a new list option
         PrintCustomItemListOptionDetails pageFormat = printDetailedOptions.CreateItemListOption("PageContent", "Pictures");
         pageFormat.AddItem("PicturesText", "Pictures and text");
         pageFormat.AddItem("PicturesOnly", "Pictures only");
         pageFormat.AddItem("TextOnly", "Text only");

         // Add the custom option to the option list
         displayedOptions.Add("PageContent");

         printDetailedOptions.OptionChanged += printDetailedOptions_OptionChanged;

         // Print Task event handler is invoked when the print job is completed.
         printTask.Completed += async (s, args) =>
         {
            // Notify the user when the print operation fails.
            if (args.Completion == PrintTaskCompletion.Failed)
            {
               await scenarioPage.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
               {
                     MainPage.Current.NotifyUser("Failed to print.", NotifyType.ErrorMessage);
               });
            }
         };

         sourceRequestedArgs.SetSource(printDocumentSource);
   });
}
```

オプションは、追加された順番で印刷プレビュー UI に表示されます。したがって、最初のオプションがウィンドウの最上部に表示されます。 この例では、カスタム オプションは最後に追加されるため、オプションの一覧の最下部に表示されます。 ただし、カスタム オプションは一覧のどこにでも配置可能です。必ずしもカスタム印刷オプションを最後に追加する必要はありません。

ユーザーがカスタム オプションの選択オプションを変更した場合は、印刷プレビューの画像を更新する必要があります。 印刷プレビュー UI の画像を再描画するには、次の例のように、[**InvalidatePreview**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.printing.printdocument.invalidatepreview) メソッドを呼び出します。

``` csharp
async void printDetailedOptions_OptionChanged(PrintTaskOptionDetails sender, PrintTaskOptionChangedEventArgs args)
{
   // Listen for PageContent changes
   string optionId = args.OptionId as string;
   if (string.IsNullOrEmpty(optionId))
   {
         return;
   }

   if (optionId == "PageContent")
   {
         await scenarioPage.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
         {
            printDocument.InvalidatePreview();
         });
   }
}
```

## <a name="related-topics"></a>関連トピック

* [印刷のデザインガイドライン](https://docs.microsoft.com/windows/uwp/devices-sensors/printing-and-scanning)
* [ビルド2015ビデオ: Windows 10 で印刷するアプリの開発](https://channel9.msdn.com/Events/Build/2015/2-94)
* [UWP 印刷のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Printing)
