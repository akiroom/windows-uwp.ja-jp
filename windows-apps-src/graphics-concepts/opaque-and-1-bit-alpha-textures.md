---
title: 不透明なテクスチャと 1 ビットのアルファ テクスチャ
description: テクスチャ形式 BC1 は、不透明または単一透明色のテクスチャに使用します。
ms.assetid: 8C53ACDD-72ED-4307-B4F3-2FCF9A9F53EC
keywords:
- 不透明なテクスチャと 1 ビットのアルファ テクスチャ
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 74768202554a3eb49c0df8ee5f17a4fe5f979be8
ms.sourcegitcommit: 82edc63a5b3623abce1d5e70d8e200a58dec673c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2019
ms.locfileid: "58291810"
---
# <a name="span-iddirect3dconceptsopaqueand1-bitalphatexturesspanopaque-and-1-bit-alpha-textures"></a><span id="direct3dconcepts.opaque_and_1-bit_alpha_textures"></span>不透明な直線および 1 ビットのアルファ テクスチャ

テクスチャ形式 BC1 は、不透明または単一透明色のテクスチャに使用します。

不透明ブロックまたは 1 ビットのアルファ ブロックごとに、16 ビット値 (RGB 5:6:5 形式) が 2 つと 2 ビット/ピクセルの 4x4 ビットマップが 1 つ格納されます。 これは、16 テクセルで合計 64 ビット、つまりテクセルあたり 4 ビットとなります。 ブロック ビットマップには 2 ビット/ピクセルがあり、4 つの色から選択できます。4 つの色のうち 2 つは、エンコードされたデータに格納されます。 他の 2 つの色は、線形補間によって、格納されたこれらの色から派生します。 レイアウトは次の図をご覧ください。

![ビットマップ レイアウトの図](images/colors1.png)

1 ビットのアルファ形式は、ブロックに格納された 2 つの 16 ビット色値を比較することにより、不透明な形式から区別されます。 これらは、符号なし整数として扱われます。 最初の色が 2 番目の色より大きい場合、不透明な色だけが定義されていることを示しています。 これは、テクセルを表すために 4 つの色が使われることを意味します。 4 色のエンコードでは、派生した色が 2 つあり、RGB 色空間で 4 つの色すべてが均等に分散されます。 この形式は、RGB 5:6:5 形式に似ています。 それ以外の場合、1 ビットのアルファ透明度では、3 つの色が使われ、4 つ目の色は透明なテクセルを表現するために予約されます。

3 色のエンコードでは、派生した色が 1 つあり、4 つ目の 2 ビット コードは透明なテクセルを示すために予約されます (アルファ情報)。 この形式は、最終ビットがアルファ マスクのエンコードに使われる RGBA 5:5:5:1 に似ています。

次のコード例は、3 色のエンコードと 4 色のエンコードのどちらが選択されているかを判断するためのアルゴリズムを示しています。

```cpp
if (color_0 > color_1) 
{
    // Four-color block: derive the other two colors. 
    
    // 00 = color_0, 01 = color_1, 10 = color_2, 11 = color_3
    // These 2-bit codes correspond to the 2-bit fields 
    // stored in the 64-bit block.
    color_2 = (2 * color_0 + color_1 + 1) / 3;
    color_3 = (color_0 + 2 * color_1 + 1) / 3;
}    
else
{ 
    // Three-color block: derive the other color.
    // 00 = color_0,  01 = color_1,  10 = color_2,  
    // 11 = transparent.
    // These 2-bit codes correspond to the 2-bit fields 
    // stored in the 64-bit block. 
    color_2 = (color_0 + color_1) / 2;    
    color_3 = transparent;    

}
```

ブレンド前に、透明度ピクセルの RGBA コンポーネントを 0 に設定することをお勧めします。

次の表は、8 バイト ブロックのメモリ レイアウトを示しています。 最初のインデックスが y 座標に対応しており、2 つ目が x 座標に対応していることを想定しています。 たとえば、テクセル\[1\]\[2\] (x, y) では、テクスチャ マップのピクセルを指す = (2, 1)。

8 バイト (64 ビット) ブロックのメモリ レイアウトを次に示します。

| ワード アドレス | 16 ビットのワード    |
|--------------|----------------|
| 0            | 色\_0       |
| 1            | 色\_1       |
| 2            | Word のビットマップ\_0 |
| 3            | Word のビットマップ\_1 |

 

色\_0 と色\_1、2 つの両極端に色が次のようにレイアウトします。

| ビット        | 色                 |
|-------------|-----------------------|
| 4:0 (LSB\*) | 青のカラー コンポーネント  |
| 10:5        | 緑のカラー コンポーネント |
| 15:11       | 赤のカラー コンポーネント   |

 

\*最下位ビット

Word のビットマップ\_0 が次のようにレイアウトします。

| ビット          | テクセル           |
|---------------|-----------------|
| 1:0 (LSB)     | テクセル\[0\]\[0\] |
| 3:2           | テクセル\[0\]\[1\] |
| 5:4           | テクセル\[0\]\[2\] |
| 7:6           | テクセル\[0\]\[3\] |
| 9:8           | テクセル\[1\]\[0\] |
| 11:10         | テクセル\[1\]\[1\] |
| 13:12         | テクセル\[1\]\[2\] |
| 15時 14分 (MSB\*) | テクセル\[1\]\[3\] |

 

\*最上位ビット (MSB)

Word のビットマップ\_1 が次のようにレイアウトします。

| ビット        | テクセル           |
|-------------|-----------------|
| 1:0 (LSB)   | テクセル\[2\]\[0\] |
| 3:2         | テクセル\[2\]\[1\] |
| 5:4         | テクセル\[2\]\[2\] |
| 7:6         | テクセル\[2\]\[3\] |
| 9:8         | テクセル\[3\]\[0\] |
| 11:10       | テクセル\[3\]\[1\] |
| 13:12       | テクセル\[3\]\[2\] |
| 15:14 (MSB) | テクセル\[3\]\[3\] |

 

## <a name="span-idexampleofopaquecolorencodingspanspan-idexampleofopaquecolorencodingspanspan-idexampleofopaquecolorencodingspanexample-of-opaque-color-encoding"></a><span id="Example_of_Opaque_Color_Encoding"></span><span id="example_of_opaque_color_encoding"></span><span id="EXAMPLE_OF_OPAQUE_COLOR_ENCODING"></span>不透明な色のエンコーディングの例


不透明なエンコードの例として、赤と黒の色が極端であるとします。 赤が色\_0、および黒の色は、\_1。 それらの色の間で均一に分散したグラデーションを形成する 4 つの補間色があります。 4x4 ビットマップの値を調べるには、次の計算を使います。

```cpp
00 ? color_0
01 ? color_1
10 ? 2/3 color_0 + 1/3 color_1
11 ? 1/3 color_0 + 2/3 color_1
```

この場合、ビットマップは次の図のようになります。

![拡大したビットマップ レイアウトの図](images/colors2.png)

これは、図に示された次の一連の色のようになります。

**注**  ピクセル (0, 0) は、イメージの左上が表示されます。

 

![エンコードされた不透明なグラデーションの図](images/redsquares.png)

## <a name="span-idexampleof1bitalphaencodingspanspan-idexampleof1bitalphaencodingspanspan-idexampleof1bitalphaencodingspanexample-of-1-bit-alpha-encoding"></a><span id="Example_of_1_Bit_Alpha_Encoding"></span><span id="example_of_1_bit_alpha_encoding"></span><span id="EXAMPLE_OF_1_BIT_ALPHA_ENCODING"></span>1 ビットのアルファ エンコーディングの例


この形式を選択したときに、16 ビット符号なし整数、色\_0 の場合は、符号なし 16 ビット整数、色より小さい\_1。 この形式を使うことができる例は、青い空に映る木の葉などです。 一部のテクセルは透明とマークできますが、その場合も葉には緑の 3 つの色調を使うことができます。 2 つの色により極端な色が修正され、3 つ目は補間色になります。

そのような絵の例を、次の図に示します。

![1 ビットのアルファ エンコードの図](images/greenthing.png)

イメージが白で表示される場合、テクセルは透明でエンコードされます。 透明テクセルの RGBA コンポーネントは、ブレンド前に 0 に設定する必要があります。

色と透明度のビットマップ エンコードは、次の計算を使って決定されます。

```cpp
00 ? color_0
01 ? color_1
10 ? 1/2 color_0 + 1/2 color_1
11   ?   Transparent
```

この場合、ビットマップは次の図のようになります。

![拡大したビットマップ レイアウトの図](images/colors3.png)

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[圧縮されたテクスチャのリソース](compressed-texture-resources.md)

 

 




