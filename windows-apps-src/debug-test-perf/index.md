---
ms.assetid: 16976d00-1564-49fe-81ad-2568e25e9e41
title: デバッグ、テスト、パフォーマンス
description: Microsoft Visual Studio およびその他のツールを使用して、アプリのデバッグとテストを行い、Microsoft Store 認定プロセス用に準備します。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 757de9201d1cb7f753419024271f2be5c1aa67f4
ms.sourcegitcommit: f727b68e86a86c94eff00f67ed79a1c12666e7bc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "63787105"
---
# <a name="debugging-testing-and-performance"></a>デバッグ、テスト、パフォーマンス


このセクションでは、Microsoft Visual Studio を使用して、アプリをデバッグ、テスト、および最適化する方法を示します。 (デバイスの監視と構成用の) Windows デバイス ポータルや (Microsoft Store 用のアプリを準備するための) Windows アプリ認定キットのようなツールも含まれます。

| トピック | 説明 |
|-------|-------------|
| [UWP アプリの展開とデバッグ](deploying-and-debugging-uwp-apps.md) | この記事では、さまざまな展開およびデバッグのターゲットを指定する手順について説明します。 |
| [プロセス ライフタイム管理 (PLM) のテスト ツールとデバッグ ツール](testing-debugging-plm.md) | アプリがプロセス ライフタイム管理と連携する方法をデバッグしてテストするためのツールと手法。 |
| [Microsoft Emulator for Windows 10 Mobile を使ったテスト](test-with-the-emulator.md) | Microsoft Emulator for Windows 10 Mobile に用意されているツールを使って、デバイスでの実際の操作をシミュレートし、アプリの機能をテストします。 エミュレーターは、Windows 10 を実行するモバイル デバイスをエミュレートするデスクトップ アプリケーションです。 このアプリケーションを使用すると、仮想化された環境が提供されるため、物理デバイスを使用せずに Windows アプリのデバッグとテストを実行できます。 また、アプリケーションのプロトタイプのための隔離環境としても使用できます。 |
| [Visual Studio を使った Surface Hub アプリのテスト](test-surface-hub-apps-using-visual-studio.md) | Visual Studio シミュレーターは、ユニバーサル Windows プラットフォーム (UWP) アプリの設計、開発、デバッグ、テストを行える環境を提供します。これには Microsoft Surface Hub 用に作成されたアプリを含みます。 シミュレーターでは、Surface Hub と同じユーザー インターフェイスは使用できませんが、Surface Hub の画面サイズと解像度でのアプリの外観と動作をテストするために有用です。 |
| [ルーズ ファイルの登録によるアプリの展開](loose-file-registration.md) | このガイドでは、ルーズ ファイル レイアウトを使用して、Windows 10 アプリをパッケージ化することなく、検証および共有する方法を示します。 |
| [ベータ テスト](beta-testing.md) | **ベータ テスト**を行うと、まだリリースされていないアプリをアプリ開発チームの外部の人に自分のデバイスで試してもらい、その人たちからのフィードバックに基づいてアプリを改善することができます。 |
| [Windows Device Portal](device-portal.md) | Windows Device Portal では、ネットワーク経由でリモートから、または USB 接続によって、デバイスの構成と管理を行えます。 |
| [Windows アプリ認定キット](windows-app-certification-kit.md) | 作成したアプリを Microsoft Store に公開する、または Windows 認定を受ける最善の方法は、認定のためにアプリを提出する前に、ローカルでアプリの検証とテストを行うことです。 このトピックでは、Windows アプリ認定キットのインストール方法と実行方法について説明します。 |
| [パフォーマンス](performance-and-xaml-ui.md) | ユーザーは、高い応答性と自然な使用感、そしてバッテリーが消耗しないことをアプリに期待しています。 技術的には、パフォーマンスは機能要件ではありませんが、パフォーマンスを機能として扱うことで、ユーザーの期待に沿うことができます。 鍵となる要因は、目標の明確化と測定の実施です。 パフォーマンスが重要なシナリオを決定し、優れたパフォーマンスとは何を意味するかを定義します。 次に、プロジェクトの初期とライフサイクル全体で十分な回数の測定を行って、目標を達成できることを確認します。 |
| [バージョン アダプティブ アプリ](version-adaptive-apps.md) | 最新の API と機能を活用する一方で、可能な限り幅広いユーザーに対応します。 ランタイム API チェックを使うと、アプリが実行されている Windows 10 のバージョンに基づき、そのバージョンで利用可能な機能に合わせてコードと XAML を実行時に調整できます。 |
