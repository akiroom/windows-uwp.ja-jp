---
title: ビュー
description: "\"ビュー\" という用語は、\"要求された形式のデータ\" という意味で使われます。 たとえば、定数バッファー ビュー (CBV) は、適切な形式の定数バッファー データを表します。 このセクションでは、最もよく使われる便利なビューについて説明します。"
ms.assetid: 0C7FB99F-7391-472F-BA53-576888DFC171
keywords:
- ビュー
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: df106a400a7ba8c8f94aa6dd35325aabacd36eca
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57663297"
---
# <a name="views"></a>ビュー


"ビュー" という用語は、"要求された形式のデータ" という意味で使われます。 たとえば、定数バッファー ビュー (CBV) は、適切な形式の定数バッファー データを表します。 このセクションでは、最もよく使われる便利なビューについて説明します。

## <a name="span-idin-this-sectionspanin-this-section"></a><span id="in-this-section"></span>このセクションの内容


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
<td align="left"><p><a href="constant-buffer-view--cbv-.md">定数バッファー ビュー (CBV)</a></p></td>
<td align="left"><p>定数バッファーには、シェーダーの定数データが含まれます。 それらの価値は、データを変更する必要があるまでデータが存続し、任意の GPU シェーダーからアクセスできることです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="vertex-buffer-view--vbv-.md">頂点バッファー ビュー (VBV) とインデックス バッファー ビュー (IBV)</a></p></td>
<td align="left"><p>頂点バッファーには、頂点のリストのデータが保持されます。 各頂点のデータには、位置、色、法線ベクトル、テクスチャ座標などを含めることができます。 インデックス バッファーには、頂点バッファーへの整数インデックス (オフセット) が保持されます。インデックス バッファーは、頂点の完全なリストのサブセットから成るオブジェクトを定義してレンダリングするために使われます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="shader-resource-view--srv-.md">シェーダー リソース ビュー (SRV) と順序付けられていないアクセス ビュー (UAV)</a></p></td>
<td align="left"><p>シェーダー リソース ビューは、通常、シェーダーがアクセスできる形式でテクスチャをラップします。 順序指定されていないアクセス ビューも同様の機能を提供しますが、任意の順序でテクスチャ (またはその他のリソース) の読み取りや書き込みを行うことができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="sampler.md">サンプラー</a></p></td>
<td align="left"><p>テクスチャまたはその他のリソースから入力値を読み取るプロセスをサンプリングと呼びます。 &quot;サンプラー&quot; は、リソースからの読み取りを行う任意のオブジェクトです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="render-target-view--rtv-.md">レンダー ターゲット ビュー (RTV)</a></p></td>
<td align="left"><p>レンダー ターゲットは、画面にレンダリングされるバック バッファーではなく、一時的な中間バッファーにシーンがレンダリングできるようにします。 この機能を使うと複雑なシーンを実現できます。たとえば、グラフィックス パイプライン内で反射テクスチャなどの用途に使われるシーンをレンダリングしたり、レンダリング前にシーンにピクセル シェーダー効果を追加したりできます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="depth-stencil-view--dsv-.md">深度ステンシル ビュー (DSV)</a></p></td>
<td align="left"><p>深度ステンシル ビューは、深度とステンシルの情報を保持するための形式とバッファーを提供します。 深度バッファーは、近くにあるオブジェクトによって視界から遮られる、ビューアーには見えないピクセルの描画を省くために使われます。 ステンシル バッファーを使って、定義した図形以外のすべての描画をカリングすることができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="stream-output-view--sov-.md">Stream 出力ビュー (SOV)</a></p></td>
<td align="left"><p>ストリーム出力ビューを使うと、頂点、テセレーション、ジオメトリ シェーダーによって生成された頂点情報を、後で利用できるようにアプリケーションに戻すことができます。 たとえば、これらのシェーダーによってゆがめられたオブジェクトをアプリケーションに書き戻して、より正確な入力を物理エンジンや他のエンジンに提供できます。 ただし実際には、ストリーム出力ビューは、グラフィックス パイプラインの機能の中でも使われることが少ない機能です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="rasterizer-ordered-view--rov-.md">ラスタライザー ビュー (ROV) 順序付け</a></p></td>
<td align="left"><p>ラスタライザー順序指定ビューを使うと、深度バッファーの一部の制約に対処できます。特に、透明度が含まれた複数のテクスチャがあって、それらがすべて同じピクセルに適用される場合に有効です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[Direct3D グラフィックス学習ガイド](index.md)

 

 




