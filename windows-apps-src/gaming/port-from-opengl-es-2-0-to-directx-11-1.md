---
title: OpenGL ES 2.0 から Direct3D 11 への移植
description: OpenGL ES 2.0 グラフィックス パイプラインを Direct3D 11 と Windows ランタイムに移植するための記事、概要、チュートリアルを紹介します。
ms.assetid: 1e1cf668-a15f-0c7b-8daf-3260d27c6d9c
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10、UWP、ゲーム、OpenGL、Direct3D 11, 移植, グラフィックス
ms.localizationpriority: medium
ms.openlocfilehash: 9215c06c97fb8e45a445ccd3691f484a6b2ad513
ms.sourcegitcommit: b52ddecccb9e68dbb71695af3078005a2eb78af1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74258453"
---
# <a name="port-from-opengl-es-20-to-direct3d-11"></a>OpenGL ES 2.0 から Direct3D 11 への移植



OpenGL ES 2.0 グラフィックス パイプラインを Direct3D 11 と Windows ランタイムに移植するための記事、概要、チュートリアルを紹介します。

> **注**   OpenGL ES 2.0 プロジェクトを移植するための中間手順は、MICROSOFT STORE の角度を使用することです。 ANGLE では、OpenGL ES API 呼び出しを DirectX 11 API 呼び出しに変換することにより、Windows で OpenGL ES コンテンツを実行することができます。 ANGLE について詳しくは、[Microsoft Store 用の ANGLE に関する Wiki ページ](https://github.com/microsoft/angle/wiki)をご覧ください。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="map-concepts-and-infrastructure.md">OpenGL ES 2.0 を Direct3D 11.1 にマップする</a></p></td>
<td align="left"><p>OpenGL ES 2.0 から Direct3D へのグラフィックス アーキテクチャの移植プロセスを初めて開始する場合は、API 間の主要な違いについて把握しておいてください。 このセクションのトピックは、グラフィックスの処理を Direct3D に移行する際に必ず必要な API の変更と移植戦略を計画するのに役立ちます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="port-a-simple-opengl-es-2-0-renderer-to-directx-11-1.md">方法: 単純な OpenGL ES 2.0 レンダラーを Direct3D 11.1 に移植する</a></p></td>
<td align="left"><p>この移植作業では、基本から始めます。Visual Studio 2015 の DirectX 11 アプリ (ユニバーサル Windows) テンプレートに対応するように、頂点シェーディングされた回転する立方体の簡単なレンダラーを OpenGL ES 2.0 から Direct3D に移植します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="opengl-es-2-0-to-directx-11-1-reference.md">OpenGL ES 2.0 から Direct3D 11.1 へのリファレンス</a></p></td>
<td align="left"><p>OpenGL ES 2.0 から Direct3D 11 への移植の際に API マッピングや簡単なコード サンプルを探す場合は、これらのリファレンス トピックをご覧ください。</p></td>
</tr>
</tbody>
</table>

 

 

 




