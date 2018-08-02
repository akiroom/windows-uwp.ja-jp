---
author: mijacobs
Description: Use pointer animations to provide users with visual feedback when the user taps on an item.
title: UWP アプリでのポインター クリックのアニメーション
ms.assetid: EEB10A2C-629A-4705-8468-4D019D74DDFF
ms.author: jimwalk
ms.date: 08/9/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, UWP
ms.localizationpriority: medium
ms.openlocfilehash: 479da70c48fd28d6f877917f6a8cc6e411cf659b
ms.sourcegitcommit: 0ab8f6fac53a6811f977ddc24de039c46c9db0ad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
ms.locfileid: "1652581"
---
# <a name="pointer-click-animations"></a>ポインター クリックのアニメーション



ポインター アニメーションを使って、ユーザーが項目をタップまたはクリックしたときに視覚的なフィードバックをユーザーに提供します。 ポインター ダウン アニメーション (押された項目を若干縮小して傾ける) は、項目が最初にタップされたときに再生されます。 ポインター アップ アニメーション (項目を元の位置に復元する) は、ユーザーがポインターから指を離したときに再生されます。


> **重要な API**: [**PointerUpThemeAnimation クラス**](https://msdn.microsoft.com/library/windows/apps/hh969168)、[**PointerDownThemeAnimation クラス**](https://msdn.microsoft.com/library/windows/apps/hh969164)


## <a name="dos-and-donts"></a>推奨と非推奨

-   ポインター アップ アニメーションを使うときには、ユーザーが指を離した直後にアニメーションを開始するようにします。 これにより、タップによってトリガーされたアクション (新しいページへの移動など) の応答が遅れたとしても、ユーザーの操作が認識されたというフィードバックを即座に返すことができます。

## <a name="related-articles"></a>関連記事

* [アニメーションの概要](https://msdn.microsoft.com/library/windows/apps/mt187350)
* [ポインター クリックのアニメーション化](https://msdn.microsoft.com/library/windows/apps/xaml/jj649432)
* [クイック スタート: ライブラリのアニメーションを使った UI のアニメーション化](https://msdn.microsoft.com/library/windows/apps/xaml/hh452703)
* [**PointerUpThemeAnimation クラス**](https://msdn.microsoft.com/library/windows/apps/hh969168)
* [**PointerDownThemeAnimation クラス**](https://msdn.microsoft.com/library/windows/apps/hh969164)

 

 



