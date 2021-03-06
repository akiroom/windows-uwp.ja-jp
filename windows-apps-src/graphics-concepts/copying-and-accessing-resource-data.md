---
title: リソース データのコピーとアクセス
description: 使用法フラグは、アプリケーションがリソース データをどのように使用するかを示し、リソースを可能な限りメモリのパフォーマンスの高い領域に配置します。 リソース データはリソース間でコピーされ、CPU または GPU がパフォーマンスに影響を与えることなくリソースにアクセスできるようにします。
ms.assetid: 6A09702D-0FF2-4EA6-A353-0F95A3EE34E2
keywords:
- リソース データのコピーとアクセス
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 3d4364bf9973b69587ae042a809d026b553ee2ea
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57662317"
---
# <a name="copying-and-accessing-resource-data"></a>リソース データのコピーとアクセス


使用法フラグは、アプリケーションがリソース データをどのように使用するかを示し、リソースを可能な限りメモリのパフォーマンスの高い領域に配置します。 リソース データはリソース間でコピーされ、CPU または GPU がパフォーマンスに影響を与えることなくリソースにアクセスできるようにします。

リソースをビデオ メモリまたはシステム メモリのどちらに作成するかを考える必要はなく、ランタイムがメモリを管理するかどうかを決定する必要はありません。 WDDM (Windows Display Driver Model) のアーキテクチャでは、アプリケーションは、アプリケーションがリソース データをどのように使用するかを示すさまざまな使用法フラグを付けて、Direct3D リソースを作成します。 このドライバー モデルは、リソースが使用するメモリを仮想化します。予想される使用法を考慮して、リソースを可能な限りメモリのパフォーマンスの高い領域に配置するのは、オペレーティング システム/ドライバー/メモリ マネージャの役割です。

既定のケースは、GPU で使用できるリソースを対象としています。 そのリソース データを CPU が使用する必要がある場合もあります。 パフォーマンスに影響を与えることなく、適切なプロセッサがリソース データにアクセスできるようにリソース データをコピーするには、API メソッドの仕組みに関する知識が必要になります。

## <a name="span-idcopyingspanspan-idcopyingspanspan-idcopyingspancopying-resource-data"></a><span id="Copying"></span><span id="copying"></span><span id="COPYING"></span>リソースのデータのコピー


Direct3D が Create の呼び出しを実行すると、メモリ内にリソースが作成されます。 それらは、ビデオ メモリ、システム メモリ、または他の任意の種類のメモリに作成することができます。 WDDM ドライバー モデルはこのメモリを仮想化するため、アプリケーションはリソースが作成されるメモリの種類を把握する必要がありません。

理想的には、GPU が直ちにアクセスできるように、すべてのリソースをビデオ メモリに配置します。 ただし、CPU がリソース データを読み取ったり、CPU が書き込んだリソース データに GPU がアクセスしたりする必要がある場合があります。 Direct3D では、アプリケーションが使用法を指定するように要求することにより、これらのさまざまなシナリオを処理し、さらに必要に応じてリソース データをコピーするためのメソッドをいくつか提供します。

リソースの作成方法によっては、そのデータに直接アクセスできないことがあります。 つまり、ソース リソースから適切なプロセッサーがアクセスできる別のリソースに、リソース データをコピーする必要があることを意味します。 Direct3D では、既定のリソースには GPU から直接アクセスでき、動的リソースおよびステージング リソースには CPU から直接アクセスできます。

リソースが作成されると、その使用法を変更することはできません。 その代わりに、あるリソースの内容を別の使用法で作成された別のリソースにコピーします。 あるリソースから別のリソースにリソース データをコピーするか、またはメモリからリソースにデータをコピーします。

リソースには主に 2 種類があります。マッピング可能なものと、マッピング不可能なものです。 動的またはステージングの使用法で作成されたリソースはマッピング可能ですが、既定または固定の使用法で作成されたリソースはマッピング不可能です。

マッピング不可能なリソース間でのデータのコピーは、最も一般的なケースであり、適切に実行されるよう最適化されているため、非常に高速です。 これらのリソースは CPU から直接アクセスできないため、GPU から高速に操作できるように最適化されています。

マッピング可能なリソース間でのデータのコピーは、リソースの作成時の使用法によりパフォーマンスが異なるので、より問題が生じやすくなります。 たとえば、GPU は動的リソースをかなり高速で読み取ることができますが、書き込むことができません。また、GPU はステージング リソースの直接読み取り、または書き込みができません。

使用法が既定のリソースから、使用法がステージングのリソースへデータをコピーしようとする (CPU でデータを読み取ることができるようにするため、つまり GPU のリードバックの問題) アプリケーションは、注意して実行する必要があります。 詳しくは、「[リソース データへのアクセス](#accessing)」をご覧ください。

## <a name="span-idaccessingspanspan-idaccessingspanspan-idaccessingspanaccessing-resource-data"></a><span id="Accessing"></span><span id="accessing"></span><span id="ACCESSING"></span>リソース データにアクセスします。


リソースにアクセスするには、リソースをマッピングする必要があります。マッピングとは、基本的には、アプリケーションが CPU からメモリへのアクセスを行おうとすることです。 CPU から基になるメモリへアクセスできるようリソースをマッピングするプロセスでは、何らかのパフォーマンス ボトルネックが発生する場合があります。このため、このタスクをいつどのように実行するかについて、注意を払う必要があります。

アプリケーションが不適切なときにリソースをマッピングしようとすると、パフォーマンスが大幅に低下することがあります。 ある操作が終了する前に、アプリケーションがその操作の結果にアクセスしようとすると、パイプライン ストールが発生します。

不適切なときにマッピング操作を実行すると、GPU および CPU が互いに強制的に同期させられ、パフォーマンスの深刻な低下を引き起こす潜在的な可能性があります。 この同期化は、CPU がマッピング可能なリソースに GPU がリソースをコピーし終わる前に、アプリケーションがそのリソースにアクセスしようとすると発生します。

### <a name="span-idperformanceconsiderationsspanspan-idperformanceconsiderationsspanspan-idperformanceconsiderationsspanperformance-considerations"></a><span id="Performance_Considerations"></span><span id="performance_considerations"></span><span id="PERFORMANCE_CONSIDERATIONS"></span>パフォーマンスに関する考慮事項

PC は、主に 2 種類のプロセッサを含む並列アーキテクチャとして動作しているマシンと考えてください。2 種類のプロセッサとは、1 つ以上の CPU のものと、1 つ以上の GPU のものです。 どの並列アーキテクチャでも、最高のパフォーマンスが得られるのは、各プロセッサがアイドル状態にならないように十分なタスクがスケジュールされているときと、1 つのプロセッサの仕事が別のプロセッサの仕事を待機していないときです。

GPU および CPU の並列処理の最悪のケースのシナリオは、あるプロセッサが別のプロセッサが行った仕事の結果を待機する必要があるという場合です。 Direct3D では、コピー メソッドを非同期にすることにより、このコストを取り除こうとしています。コピーは、メソッドが返されるときまでに必ずしも実行しておく必要はありません。

この方法の利点は、Map が呼び出されて CPU がデータにアクセスするまで、データを実際にコピーするというパフォーマンスのコストをアプリケーションが負担しないことです。 データが実際にコピーされた後に Map メソッドが呼び出されると、パフォーマンスの損失が発生しません。 一方、データがコピーされる前に Map メソッドが呼び出される場合は、パイプライン ストールが発生します。

Direct3D の非同期呼び出し (メソッドの大多数の呼び出し、および特にレンダリング呼び出し) は、*コマンド バッファー*と呼ばれる場所に格納されます。 このバッファーは、グラフィックス ドライバー内部にあり、Microsoft Windows のユーザー モードからカーネル モードへの負荷の大きい切り替えができるだけ発生しないように、基になるハードウェアへの呼び出しをバッチ処理するために使用されます。

以下の 4 つの状況のいずれかで、コマンド バッファーがフラッシュされ、ユーザー モードとカーネル モードの切り替えが発生します。

1.  Present が呼び出されます。
2.  Flush が呼び出されます。
3.  コマンド バッファーがいっぱいです。コマンド バッファーのサイズは動的で、オペレーティング システムとグラフィックス ドライバーで制御されます。
4.  CPU は、コマンド バッファーで実行を待っているコマンドの結果にアクセスする必要があります。

この 4 つの状況で、4 番目がパフォーマンスにおいて最も重要です。 アプリケーションがリソース コピーの呼び出しまたはサブリソース コピーの呼び出しを発行する場合、この呼び出しはコマンド バッファーにキューイングされます。

そこでアプリケーションが、コピー呼び出しの対象だったステージング リソースを、コマンド バッファーがフラッシュされる前にマッピングしようとすると、Copy メソッドの呼び出しを実行する必要があるだけでなく、コマンド バッファー内にバッファーされたその他すべてのコマンドも実行しなければならないため、パイプライン ストールが発生します。 れにより、GPU がコマンド バッファーを空にし、CPU が必要とするリソースに最終的にデータを格納する間、CPU はステージング リソースへのアクセスを待機するので、GPU と CPU の同期が発生します。 GPU がコピーを終了すると、CPU はステージング リソースへのアクセスを開始します。しかしこの間、GPU はアイドル状態となります。

ランタイムにこれを頻繁に行うと、パフォーマンスが著しく低下します。 そのため、既定の使用法で作成されたリソースのマッピングは、注意して行う必要があります。 アプリケーションは、コマンド バッファーが空になるのに十分な時間待機し、対応するステージング リソースにマッピングしようとする前に、こうしたコマンドをすべて実行し終える必要があります。

アプリケーションはどれだけ待機すればよいのでしょうか。 少なくとも 2 フレームです。これにより CPU と GPU 間の並列処理が最大限利用できるからです。 GPU がどのように動作するかというと、アプリケーションがコマンド バッファーに呼び出しを送信することにより N 番目のフレームを処理する間、GPU は前のフレームである N-1 番目からの呼び出しの実行でビジー状態です。

そこで、アプリケーションがビデオ メモリにあるリソースをマッピングしようとし、N 番目のフレームでリソースをコピーする場合、この呼び出しは実際には、アプリケーションが次のフレームの呼び出しを送信しているとき、N + 1 番目のフレームで実行を開始します。 コピーは、アプリケーションが N + 2 番目のフレームを処理しているときに完了します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Frame</th>
<th align="left">GPU/CPU の状態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">N</td>
<td align="left"><ul>
<li>CPU が現在のフレームのレンダリング呼び出しを行います。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">N+1</td>
<td align="left"><ul>
<li>N 番目のフレームの間、GPU は CPU から送信された呼び出しを実行しています。</li>
<li>CPU が現在のフレームのレンダリング呼び出しを行います。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">N+2</td>
<td align="left"><ul>
<li>N 番目のフレームの間に、GPU は CPU から送信された呼び出しの実行を完了しました。結果の準備ができています。</li>
<li>N + 1 番目のフレームの間、GPU は CPU から送信された呼び出しを実行しています。</li>
<li>CPU が現在のフレームのレンダリング呼び出しを行います。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">N+3</td>
<td align="left"><ul>
<li>N + 1 番目のフレームの間に、GPU は CPU から送信された呼び出しの実行を完了しました。 結果の準備ができています。</li>
<li>N + 2 番目のフレームの間、GPU は CPU から送信された呼び出しを実行しています。</li>
<li>CPU が現在のフレームのレンダリング呼び出しを行います。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">N+4</td>
<td align="left">...</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[リソース](resources.md)

 

 




