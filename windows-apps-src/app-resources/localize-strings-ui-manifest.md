---
author: stevewhims
Description: "アプリで複数の表示言語をサポートする必要があり、コード、XAML マークアップ、アプリ パッケージ マニフェスト内に文字列リテラルが含まれている場合は、その文字列をリソース ファイル (.resw) に移動します。 アプリでサポートする各言語用に、このリソース ファイルを翻訳したコピーを作成することができます。"
title: "UI とアプリ パッケージ マニフェスト内の文字列をローカライズする"
ms.assetid: E420B9BB-C0F6-4EC0-BA3A-BA2875B69722
label: Localize strings in your UI and app package manifest
template: detail.hbs
ms.author: stwhi
ms.date: 11/01/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: "Windows 10, UWP, リソース, 画像, アセット, MRT, 修飾子"
localizationpriority: medium
ms.openlocfilehash: cca9c9b731831ce1c87ee74b7f8b502130ef97fd
ms.sourcegitcommit: d0c93d734639bd31f264424ae5b6fead903a951d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2017
---
<link rel="stylesheet" href="https://az835927.vo.msecnd.net/sites/uwp/Resources/css/custom.css">

# <a name="localize-strings-in-your-ui-and-app-package-manifest"></a>UI とアプリ パッケージ マニフェスト内の文字列をローカライズする

アプリのローカライズの価値提案の詳細については、「[グローバリゼーションとローカライズ](../globalizing/globalizing-portal.md)」をご覧ください。

アプリで複数の表示言語をサポートする必要があり、コード、XAML マークアップ、アプリ パッケージ マニフェスト内に文字列リテラルが含まれている場合は、その文字列をリソース ファイル (.resw) に移動します。 アプリでサポートする各言語用に、このリソース ファイルを翻訳したコピーを作成することができます。

ハードコードされた文字列リテラルは、命令型コードや XAML マークアップに (たとえば、**TextBlock** の **Text** プロパティとして)表示できます。 また、アプリ パッケージ マニフェスト (`Package.appxmanifest` ファイル) に (たとえば、Visual Studio マニフェスト デザイナーの [アプリケーション] タブで表示名の値として) 表示することもできます。 これらの文字列をリソース ファイル (.resw) に移動し、アプリやリソース内のハードコードされた文字列リテラルをリソース識別子への参照に置き換えます。

画像リソース ファイルに画像リソースが 1 つだけ含まれている画像リソースとは異なり、文字列リソース ファイルには*複数の*文字列リソースが含まれています。 文字列リソース ファイルはリソース ファイル (.resw) であり、通常、この種類のリソース ファイルはプロジェクトの \Strings フォルダー内に作成します。 リソース ファイル (.resw) の名前に修飾子を使用する方法の詳細については、「[言語、スケール、その他の修飾子用にリソースを調整する](tailor-resources-lang-scale-contrast.md)」をご覧ください。

## <a name="create-a-resources-file-resw-and-put-your-strings-in-it"></a>リソース ファイル (.resw) を作成し、文字列を配置する

1. アプリの既定の言語を設定します。
    1. Visual Studio でソリューションを開いた状態で、`Package.appxmanifest` を開きます。
    2. [アプリケーション] タブで、既定の言語が適切に設定されている ("en"や "en-us" など) ことを確認します。 残りの手順では、既定の言語を "en-US" に設定していることを前提としています。
    <br>**注:** 最低でも、この既定の言語のローカライズされた文字列リソースを提供する必要があります。 これらは、ユーザーの優先する言語や表示言語の設定に一致するものが見つからない場合に読み込まれるリソースです。
2. 既定の言語のリソース ファイル (.resw) を作成します。
    1. プロジェクト ノードで、新しいフォルダーを作成し、"Strings" という名前を付けます。
    2. `Strings` で、新しいサブフォルダーを作成し、"en-US" という名前を付けます。
    3. `en-US` で、新しいリソース ファイル (.resw) を作成し、その名前が "Resources.resw" になっていることを確認します。
    <br>**注:** .NET リソース ファイル (.resx) を移植する場合は、「[XAML と UI の移植](../porting/wpsl-to-uwp-porting-xaml-and-ui.md#localization-and-globalization)」をご覧ください。
3.  `Resources.resw` を開き、次の文字列リソースを追加します。

    `Strings/en-US/Resources.resw`

    ![リソースの追加 (英語)](images/addresource-en-us.png)

    この例では、"Greeting" が、マークアップから参照できる文字列リソース識別子です。 識別子 "Greeting" について、Text プロパティの文字列が提供され、Width プロパティの文字列が提供されています。 "Greeting.Text" は、UI 要素のプロパティに対応しているため、プロパティ識別子の例です。 また、たとえば、[名前] 列で "Greeting.Foreground" を追加し、その値を "Red" に設定することもできます。 "Farewell" 識別子は、単純な文字列リソース識別子です。サブプロパティを持たず、後で説明するように、命令型コードから読み込むことができます。 [コメント] 列は、翻訳者に特別な指示を提供するのに適しています。

    この例では、"Farewell" という名前の単純な文字列リソース識別子エントリがあるため、同じ識別子に基づくプロパティ識別子*も*指定することはできません。 そのため、"Farewell.Text" を追加すると、`Resources.resw` をビルドするときに、重複したエントリのエラーが出力されます。

## <a name="refer-to-a-string-resource-identifier-from-xaml-markup"></a>XAML マークアップから文字列リソース識別子を参照する

[x:Uid ディレクティブ](../xaml-platform/x-uid-directive.md)を使用して、マークアップ内のコントロールやその他の要素を文字列リソース識別子に関連付けます。

**XAML**
```xml
<TextBlock x:Uid="Greeting"/>
```

実行時に、`\Strings\en-US\Resources.resw` が読み込まれます (現時点では、プロジェクト内の唯一のリソース ファイルであるためです)。 **TextBlock** の **x:Uid** ディレクティブによって、参照が実行され、`Resources.resw` 内の "Greeting" 文字列リソース識別子を含むプロパティ識別子が見つかります。 "Greeting.Text" および "Greeting.Width" プロパティ識別子が見つかり、その値が **TextBlock** に適用され、マークアップでローカルに設定されている値がオーバーライドされます。 "Greeting.Foreground" 値を追加していた場合は、この値も適用されます。 ただし、XAML マークアップ要素でプロパティを設定するための使用されるのはプロパティ識別子のみであるため、この TextBlock で **x:Uid** を "Farewell" に設定しても効果はありません。 `Resources.resw` 文字列リソース識別子 "Farewell" が含まれて*います*が、そのプロパティ識別子はありません。

XAML 要素に文字列リソース識別子を割り当てるときには、その識別子の*すべて*のプロパティ識別子が XAML 要素で適切であることを確認します。 たとえば、**TextBlock** で `x:Uid="Greeting"` を設定する場合、**TextBlock**型は Text プロパティを持つため、"Greeting.Text" は解決されます。 **Button** で `x:Uid="Greeting"` を設定する場合、**Button** 型には Text プロパティがないため、"Greeting.Text" によって実行時エラーが発生します。 その場合の解決策の 1 つは、"ButtonGreeting.Content" という名前のプロパティ識別子を作成し、**Button** で `x:Uid="ButtonGreeting"` を設定することです。

リソース ファイルから **Width** を設定する代わりに、コンテンツに合わせてコントロールのサイズを動的に変更できるようにすることが必要になる場合があります。

**注** [添付プロパティ](../xaml-platform/attached-properties-overview.md)の場合、.resw ファイルの [名前] 列で特別な構文が必要です。 たとえば、"Greeting" 識別子用に [AutomationProperties.Name](/uwp/api/windows.ui.xaml.automation.automationproperties?branch=live#Windows_UI_Xaml_Automation_AutomationProperties_NameProperty) 添付プロパティの値を設定するには、これが [名前] 列に入力する内容です。

```
Greeting.[using:Windows.UI.Xaml.Automation]AutomationProperties.Name
```

## <a name="refer-to-a-string-resource-identifier-from-code"></a>コードから文字列リソース識別子を参照する

単純な文字列リソース識別子に基づいて、文字列リソースを明示的に読み込むことができます。

**C#**
```csharp
var resourceLoader = Windows.ApplicationModel.Resources.ResourceLoader.GetForCurrentView();
this.myXAMLTextBlockElement.Text = resourceLoader.GetString("Farewell");
```

**C++**
```cpp
auto resourceLoader = Windows::ApplicationModel::Resources::ResourceLoader::GetForCurrentView();
this->myXAMLTextBlockElement->Text = resourceLoader->GetString("Farewell");
```

クラス ライブラリ (ユニバーサル Windows) または[Windows ランタイム ライブラリ (ユニバーサル Windows)](../winrt-components/index.md) プロジェクト内からこの同じコードを使用することができます。 実行時に、ライブラリをホストしているアプリのリソースが読み込まれます。 アプリはローカライズの度合いが大きくなる可能性があるため、ライブラリでは、ライブラリをホストしているアプリからリソースを読み込むことをお勧めします。 ライブラリがリソースを提供する必要がある場合、ライブラリをホストしているアプリがそれらのリソースを入力に置き換えられるようにするオプションを提供する必要があります。

**注** この方法で値を読み込むことができるのは単純な文字列リソース識別子のみであり、プロパティ識別子の値を読み込むことはできません。 したがって、このようなコードを使用して "Farewell" の値を読み込むことはできますが、"Greeting.Text" の値を読み込むことはできません。 これを試行すると、空の文字列が返されます。

## <a name="refer-to-a-string-resource-identifier-from-your-app-package-manifest"></a>アプリ パッケージ マニフェストから文字列リソース識別子を参照する

1. アプリ パッケージ マニフェスト (`Package.appxmanifest` ファイル) を開きます。既定では、アプリの表示名は文字列リテラルで表されます。

   ![リソースの追加 (英語)](images/display-name-before.png)

2. この文字列のローカライズ可能なバージョンを作成するには、`Resources.resw` を開き、"AppDisplayName"という名前で、"Adventure Works Cycles" という値の新しい文字列リソースを追加します。

3. 表示名の文字列リテラルを、作成した文字列リソース識別子 ("AppDisplayName") への参照に置き換えます。 これを行うには、`ms-resource` URI (Uniform Resource Identifier) スキームを使用します。

   ![リソースの追加 (英語)](images/display-name-after.png)

4. マニフェスト内のローカライズする各文字列について、この手順を繰り返します。 たとえば、アプリの短い名前 (スタート画面でアプリのタイルに表示されるように構成できる) です。 アプリ パッケージ マニフェスト内で、ローカライズできるすべての項目の一覧については、「[マニフェストのローカライズ可能な項目](/uwp/schemas/appxpackage/uapmanifestschema/localizable-manifest-items-win10?branch=live)」をご覧ください。

## <a name="localize-the-string-resources"></a>文字列リソースをローカライズする

1. 別の言語用にリソース ファイル (.resw) のコピーを作成します。
    1. "Strings" の下に新しいサブフォルダーを作成し、Deutsch (Deutschland) を表す "de-DE" という名前を付けます。
   <br>**注** フォルダー名には、任意の [BCP 47 言語タグ](http://go.microsoft.com/fwlink/p/?linkid=227302)を使用できます。 言語修飾子の詳しい情報と共通の言語タグの一覧は、「[言語、スケール、その他の修飾子用にリソースを調整する](tailor-resources-lang-scale-contrast.md)」をご覧ください。
   2. `Strings/de-DE` フォルダー内に `Strings/en-US/Resources.resw` のコピーを作成します。
2. 文字列に変換します。
    1. `Strings/de-DE/Resources.resw` を開き、[値] 列の値を翻訳します。 コメントを翻訳する必要はありません。

    `Strings/de-DE/Resources.resw`

    ![リソースを追加する (ドイツ語)](images/addresource-de-de.png)

必要に応じて、他の言語について手順 1. と 2. を繰り返すことができます。

`Strings/fr-FR/Resources.resw`

![リソースを追加する (フランス語)](images/addresource-fr-fr.png)

## <a name="test-your-app"></a>アプリのテスト

既定の表示言語に対してアプリをテストします。 **[設定]** > **[時刻と言語]** > **[地域と言語]** (または**[言語]**) で表示言語を変更し、アプリを再テストできます。 UI やシェルの文字列 (タイトル バー (表示名) やタイルの短い名前など) を確認します。

**注** 表示言語の設定に一致するフォルダー名が見つかった場合、そのフォルダー内のリソース ファイルが読み込まれます。 それ以外の場合、フォールバックが行われ、最終的にはアプリの既定の言語用のリソースになります。

## <a name="factoring-strings-into-multiple-resources-files"></a>文字列を複数のリソース ファイルにファクタリングする

1 つのリソース ファイル (resw) にすべての文字列を保持することも、複数のリソース ファイルに文字列をファクタリングすることもできます。 たとえば、エラー メッセージを 1 つのリソース ファイルに、アプリ パッケージ マニフェストの文字列を別のリソース ファイルに、UI の文字列を第 3 のリソース ファイルに保持することができます。 この場合、フォルダー構造は次のようになります。

![リソースの追加 (英語)](images/manifest-resources.png)

文字列リソース識別子の参照を特定のファイルに限定する場合は、識別子の前に `/<resources-file-name>/` を追加するだけです。 次のマークアップの例では、`ErrorMessages.resw` にリソースが含まれており、その名前が "PasswordTooWeak.Text" であり、その値がエラーの説明であることを想定しています。

**XAML**
```xml
<TextBlock x:Uid="/ErrorMessages/PasswordTooWeak"/>
```

次のコードの例では、`ErrorMessages.resw` にリソースが含まれており、その名前が "MismatchedPasswords" であり、その値がエラーの説明であることを想定しています。

**C#**
```csharp
var resourceLoader = Windows.ApplicationModel.Resources.ResourceLoader.GetForCurrentView("ManifestResources");
this.myXAMLTextBlockElement.Text = resourceLoader.GetString("/ErrorMessages/MismatchedPasswords");
```

**C++**
```cpp
auto resourceLoader = Windows::ApplicationModel::Resources::ResourceLoader::GetForCurrentView("ManifestResources");
this->myXAMLTextBlockElement->Text = resourceLoader->GetString("/ErrorMessages/MismatchedPasswords");
```

"AppDisplayName" リソースを `Resources.resw` から `ManifestResources.resw` に移動する場合は、アプリ パッケージ マニフェストで `ms-resource:AppDisplayName` を `ms-resource:/ManifestResources/AppDisplayName` に変更します。

`Resources.resw` *以外の*リソース ファイルの場合にのみ、文字列リソース識別子の前に `/<resources-file-name>/` を追加する必要があります。 これは、"Resources.resw" が既定のファイル名であり、(このトピックの前の例で行ったように) ファイル名を省略した場合に既定のファイル名が想定されるためです。

## <a name="load-a-string-for-a-specific-language-or-other-context"></a>特定の言語または他のコンテキスト用の文字列を読み込む

既定の [**ResourceContext**](/uwp/api/windows.applicationmodel.resources.core.resourcecontext?branch=live) ([**ResourceContext.GetForCurrentView**](/uwp/api/windows.applicationmodel.resources.core.resourcecontext?branch=live#Windows_ApplicationModel_Resources_Core_ResourceContext_GetForCurrentView) から取得された) には、既定の実行時コンテキスト (つまり、現在のユーザーとコンピューターの設定) を表す、各修飾子名の修飾子の値が含まれています。 リソース ファイル (.resw) は、(その名前に含まれる修飾子に基づいて) 実行時コンテキストでの修飾子の値と比較されます。

ただし、アプリでシステム設定を上書きし、読み込むリソース ファイルを検索するときに使用する言語、スケール、その他の修飾子の値を明示的に指定することが必要になる場合があります。 たとえば、ユーザーがヒントやエラー メッセージに別の言語を選ぶことができるように設定できます。

そのためには、(既定のものを使用する代わりに) 新しい **ResourceContext** を作成し、その値をオーバーライドして、文字列検索でそのコンテキスト オブジェクトを使用します。

**C#**
```csharp
var resourceContext = new Windows.ApplicationModel.Resources.Core.ResourceContext(); // not using ResourceContext.GetForCurrentView
resourceContext.QualifierValues["Language"] = "de-DE";
var resourceMap = Windows.ApplicationModel.Resources.Core.ResourceManager.Current.MainResourceMap.GetSubtree("Resources");
this.myXAMLTextBlockElement.Text = resourceMap.GetValue("Farewell", resourceContext).ValueAsString;
```

上記のコード例で示した **QualifierValues** の使用方法は、任意の修飾子についても適用できます。 言語の特殊な場合には、代わりに次のようにすることができます。

**C#**
```csharp
resourceContext.Languages = new string[] { "de-DE" };
```

グローバル レベルで同じ効果を実現するために、既定の **ResourceContext** で修飾子の値を上書きすることが*できます*。 ただし、その代わりに、[**ResourceContext.SetGlobalQualifierValue**](/uwp/api/windows.applicationmodel.resources.core.resourcecontext?branch=live#Windows_ApplicationModel_Resources_Core_ResourceContext_SetGlobalQualifierValue_System_String_System_String_Windows_ApplicationModel_Resources_Core_ResourceQualifierPersistence_) を呼び出すことをお勧めします。 **SetGlobalQualifierValue** の呼び出しで一度値を設定すると、ResourceContext を検索に使用するたびに、これらの値が既定の **ResourceContext** で有効になります。

**C#**
```csharp
Windows.ApplicationModel.Resources.Core.ResourceContext.SetGlobalQualifierValue("Language", "de-DE");
var resourceLoader = Windows.ApplicationModel.Resources.ResourceLoader.GetForCurrentView();
this.myXAMLTextBlockElement.Text = resourceLoader.GetString("Farewell");
```

一部の修飾子には、システム データ プロバイダーがあります。 したがって、**SetGlobalQualifierValue** を呼び出す代わりに、プロバイダー独自の API によってプロバイダーを調整できます。 たとえば、次のコードは、[**PrimaryLanguageOverride**](/uwp/api/Windows.Globalization.ApplicationLanguages?branch=live#Windows_Globalization_ApplicationLanguages_PrimaryLanguageOverride) を設定する方法を示しています。

**C#**
```csharp
Windows.Globalization.ApplicationLanguages.PrimaryLanguageOverride = "de-DE";
```

## <a name="updating-strings-in-response-to-qualifier-value-change-events"></a>修飾子の値の変更イベントへの応答で文字列を更新する

実行中のアプリは、既定の **ResourceContext** で修飾子の値に影響を与えるシステム設定の変更に応答できます。 これらのシステム設定のいずれかが、[**ResourceContext.QualifierValues**](/uwp/api/windows.applicationmodel.resources.core.resourcecontext?branch=live#Windows_ApplicationModel_Resources_Core_ResourceContext_QualifierValues) の [**MapChanged**](/uwp/api/windows.foundation.collections.iobservablemap_k_v_?branch=live#Windows_Foundation_Collections_IObservableMap_2_MapChanged) イベントを呼び出します。

このイベントへの応答で、既定の **ResourceContext** から文字列を再読み込みすることができます。

**C#**
```csharp
public MainPage()
{
    this.InitializeComponent();

    ...

    // Subscribe to the event that's raised when a qualifier value changes.
    var qualifierValues = Windows.ApplicationModel.Resources.Core.ResourceContext.GetForCurrentView().QualifierValues;
    qualifierValues.MapChanged += new Windows.Foundation.Collections.MapChangedEventHandler<string, string>(QualifierValues_MapChanged);
}

private async void QualifierValues_MapChanged(IObservableMap<string, string> sender, IMapChangedEventArgs<string> @event)
{
    var dispatcher = this.myXAMLTextBlockElement.Dispatcher;
    if (dispatcher.HasThreadAccess)
    {
        this.RefreshUIText();
    }
    else
    {
        await dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () => this.RefreshUIText());
    }
}

private void RefreshUIText()
{
    var resourceLoader = Windows.ApplicationModel.Resources.ResourceLoader.GetForCurrentView();
    this.myXAMLTextBlockElement.Text = resourceLoader.GetString("Farewell");
}
```

## <a name="loading-strings-from-a-class-library-or-a-windows-runtime-library"></a>クラス ライブラリまたは Windows ランタイム ライブラリから文字列を読み込む

参照されているクラス ライブラリ (ユニバーサル Windows) または [Windows ランタイム ライブラリ (ユニバーサル Windows)](../winrt-components/index.md) の文字列リソースは、通常、構築プロセス中にそれらが含まれているパッケージのサブフォルダーに追加されます。 このような文字列のリソース識別子は、通常、*LibraryName/ResourcesFileName/ResourceIdentifier* という形式になります。

ライブラリは、独自のリソースについて、ResourceLoader を取得できます。 たとえば、次のコードは、ライブラリ、またはそれを参照するアプリで、ライブラリの文字列リソースの ResourceLoader を取得できます。

**C#**
```csharp
var resourceLoader = new Windows.ApplicationModel.Resources.ResourceLoader("ContosoControl/Resources");
resourceLoader.GetString("string1");
```

## <a name="loading-strings-from-other-packages"></a>他のパッケージから文字列を読み込む

アプリ パッケージのリソースは、現在の [ResourceManager](/uwp/api/windows.applicationmodel.resources.core.resourcemanager?branch=live) からアクセスできる、パッケージ独自のトップ レベルの [ResourceMap](/uwp/api/windows.applicationmodel.resources.core.resourcemap?branch=live) を介して管理され、アクセスされます。 各パッケージ内では、さまざまなコンポーネントが独自の ResourceMap サブツリーを持つことができます。これらは、[ResourceMap.GetSubtree](https://docs.microsoft.com/en-us/uwp/api/Windows.ApplicationModel.Resources.Core.ResourceMap#Windows_ApplicationModel_Resources_Core_ResourceMap_GetSubtree_System_String_) によってアクセスできます。

フレームワーク パッケージは、絶対リソース識別子 URI を使って独自のリソースにアクセスできます。 「[URI スキーム](uri-schemes.md)」もご覧ください。

## <a name="important-apis"></a>重要な API

* [ApplicationModel.Resources.ResourceLoader](https://msdn.microsoft.com/library/windows/apps/br206014)

## <a name="related-topics"></a>関連トピック

* [XAML と UI の移植](../porting/wpsl-to-uwp-porting-xaml-and-ui.md#localization-and-globalization)
* [x:Uid ディレクティブ](../xaml-platform/x-uid-directive.md)
* [アタッチされるプロパティ](../xaml-platform/attached-properties-overview.md)
* [マニフェストのローカライズ可能な項目](/uwp/schemas/appxpackage/uapmanifestschema/localizable-manifest-items-win10?branch=live)
* [BCP-47 言語タグ](http://go.microsoft.com/fwlink/p/?linkid=227302)
* [言語、スケール、その他の修飾子用にリソースを調整する](tailor-resources-lang-scale-contrast.md)
* [文字列リソースを読み込む方法](https://msdn.microsoft.com/library/windows/apps/xaml/hh965323)