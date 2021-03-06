---
ms.assetid: ee51eae3-ed55-419e-ad74-6adf1e1fb8b9
title: 手動でのアプリのパッケージ化
description: このセクションには、ユニバーサル Windows プラットフォーム (UWP) アプリの手動でのパッケージ化に関する記事または記事へのリンクが記載されています。
ms.date: 04/30/2018
ms.topic: article
keywords: Windows 10, UWP, パッケージ化
ms.localizationpriority: medium
ms.openlocfilehash: d90307560c315741751a5ab58ccdf0eaf35d97fc
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372793"
---
# <a name="manual-app-packaging"></a>手動でのアプリのパッケージ化

アプリ パッケージを作成して署名するときに、Visual Studio を使ってアプリを開発していない場合は、手動でのアプリのパッケージ化ツールを使用する必要があります。

> [!IMPORTANT] 
> Visual Studio を使用してアプリを開発する場合は、Visual Studio のウィザードを使ってアプリ パッケージを作成し、署名することをお勧めします。 詳しくは、「[Visual Studio での UWP アプリのパッケージ化](https://docs.microsoft.com/windows/uwp/packaging/packaging-uwp-apps)」をご覧ください。

## <a name="purpose"></a>目的

このセクションには、ユニバーサル Windows プラットフォーム (UWP) アプリの手動でのパッケージ化に関する記事または記事へのリンクが記載されています。

| トピック | 説明 |
|-------|-------------|
| [MakeAppx.exe ツールを使用してアプリ パッケージを作成します。](create-app-package-with-makeappx-tool.md) | MakeAppx.exe は、アプリ パッケージとバンドルからのファイルの作成、暗号化、暗号化解除、抽出を行います。 |
| [パッケージに署名するための証明書を作成します。](create-certificate-package-signing.md) | PowerShell ツールを使ってアプリ パッケージ署名用を作成し、エクスポートします。 |
| [SignTool を使用して、アプリ パッケージを署名します。](sign-app-package-using-signtool.md) | SignTool を使って手動でアプリ パッケージに証明書による署名を行います。 |

### <a name="advanced-topics"></a>高度なトピック

このセクションには、より効率的なパッケージ化とインストールのために大規模なアプリや複雑なアプリをコンポーネント化する高度なトピックが含まれています。 

> [!IMPORTANT]
> Microsoft Store にアプリを提出する予定がある場合、[Windows 開発者向けサポート](https://developer.microsoft.com/windows/support)に連絡してこのセクションの高度な機能を使う承認を得る必要があります。


| トピック | 説明 |
|-------|-------------|
| [アセット パッケージの概要](asset-packages.md) | アセット パッケージは、アプリケーションの共通ファイルの一元的な場所として機能するパッケージの種類です。これにより、そのアーキテクチャ パッケージ全体で重複するファイルが事実上不要になります。 |
| [アセット パッケージとパッケージの圧縮を使用した開発](package-folding.md) | アセット パッケージとパッケージ圧縮を使ってアプリケーションを効率的に整理する方法について説明します。 |
| [フラットなバンドルのアプリ パッケージ](flat-bundles.md) | アプリのパッケージ ファイルのフラット バンドルを作成する方法について説明します。 |
| [パッケージ レイアウトでパッケージの作成](packaging-layout.md) | パッケージ レイアウトは、アプリのパッケージ構造を記述する 1 つのドキュメントです。 アプリのバンドル (プライマリおよびオプション)、バンドル内のパッケージ、パッケージ内のファイルを指定します。 |
