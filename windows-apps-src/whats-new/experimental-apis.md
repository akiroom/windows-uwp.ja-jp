---
title: 試験的な API
description: 試験的な API について
ms.date: 11/13/2017
ms.topic: article
keywords: windows 10, uwp, 試験的, api
ms.localizationpriority: medium
ms.openlocfilehash: 542e007d07d490c2f18077e646f7598bfd2587c3
ms.sourcegitcommit: 76e8b4fb3f76cc162aab80982a441bfc18507fb4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "75684910"
---
# <a name="experimental-apis"></a>試験的な API

試験的な API は、設計の初期段階で使用され、所有者がフィードバックを反映したり、他のシナリオに対するサポートを追加したりする場合に変更される可能性があります。

これらの API は、[Windows Insider SDK](https://www.microsoft.com/software-download/windowsinsiderpreviewSDK) を利用して、外部でフライトされます。そのため、API が正式なプラットフォームに組み込まれる前に、開発者は API を試したり、フィードバックを提供したりすることができます。 これらの API がフライトされている場合は、安定性や問題への対応は保証されません。

## <a name="consuming-experimental-apis"></a>試験的な API の使用
Intellisense を利用すると、API が試験的なものであるかどうかを確認できます。 また、試験的な API を使用したときに、"評価のみを目的としており、今後の更新プログラムで変更または削除されることがあります" などのコンパイラの警告が表示されます。

これらの警告は、実稼働プロジェクトで試験的な API に対する依存関係を作成するのを防ぐ場合に役立ちます。 試験的なプロジェクトでは、これらの警告を無視したり、無効にしたりすることができます。

既定では、これらの API は実行時に無効になっており、これらの API を呼び出すとランタイム例外が発生します。 このもう一つのセーフガードにより、不注意による依存関係の作成や、試験的な API を使用するアプリの広範な配布を防ぐことができます。

これらの API を試験用に有効にするには、[Windows デバイス ポータル (WDP)](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal) 機能のプラグインをターゲット デバイスで使用し、呼び出す API に対応する機能を有効にします。

特定の試験的な API に関するドキュメントは、API を所有するチームの裁量に任されています。

## <a name="providing-feedback"></a>フィードバックの提供

試験的な API を試し、フィードバックを提供する場合は、[Windows フィードバック Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub) の **"開発者向けプラットフォーム"** カテゴリをご利用ください。