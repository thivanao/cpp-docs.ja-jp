---
title: イメージ リストのイメージの描画
ms.date: 11/04/2016
helpviewer_keywords:
- CImageList class [MFC], drawing images from
- drawing [MFC], images from image lists
- image lists [MFC], drawing images from
- images [MFC], drawing
ms.assetid: 2f6063fb-1c28-45f8-a333-008c064db11c
ms.openlocfilehash: 55c16ce5bff102d670e46867e121b0a0a2f304ac
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84622851"
---
# <a name="drawing-images-from-an-image-list"></a>イメージ リストのイメージの描画

イメージを描画するには、 [CImageList::D raw](reference/cimagelist-class.md#draw)メンバー関数を使用します。 デバイスコンテキストオブジェクトへのポインター、描画するイメージのインデックス、イメージを描画するデバイスコンテキスト内の位置、および描画スタイルを示す一連のフラグを指定します ()。

**ILD_TRANSPARENT**スタイルを指定すると、は `Draw` 2 段階のプロセスを使用して、マスクされたイメージを描画します。 まず、イメージのビットとマスクのビットに対して論理 AND 演算を実行します。 次に、最初の操作の結果と、宛先デバイスコンテキストのバックグラウンドビットに対して、論理 XOR 演算を実行します。 このプロセスでは、結果のイメージに透明な領域が作成されます。つまり、マスク内の各白ビットによって、結果のイメージ内の対応するビットが透明になります。

マスクされたイメージを単色の背景に描画する前に、 [SetBkColor](reference/cimagelist-class.md#setbkcolor)メンバー関数を使用して、イメージリストの背景色を変換先と同じ色に設定する必要があります。 色を設定すると、イメージ内に透明な領域を作成する必要がなくなり、が `Draw` イメージを目的のデバイスコンテキストに簡単にコピーできるようになり、パフォーマンスが大幅に向上します。 イメージを描画するには、を呼び出すときに**ILD_NORMAL**スタイルを指定し `Draw` ます。

マスクされたイメージリスト ([CImageList](reference/cimagelist-class.md)) の背景色は、任意の時点でいつでも設定できます。これにより、単色の背景で正しく描画されるようになります。 背景色を**CLR_NONE**に設定すると、既定で画像が透過的に描画されます。 イメージリストの背景色を取得するには、 [GetBkColor](reference/cimagelist-class.md#getbkcolor)メンバー関数を使用します。

**ILD_BLEND25**と**ILD_BLEND50**のスタイルによって、システムの強調表示色で画像がディザーされます。 これらのスタイルは、ユーザーが選択できるオブジェクトを表すためにマスクされたイメージを使用する場合に便利です。 たとえば、 **ILD_BLEND50**スタイルを使用して、ユーザーがイメージを選択したときにイメージを描画できます。

Nonmasked イメージは、ラスター操作を使用して、コピー先のデバイスコンテキストにコピーされ `SRCCOPY` ます。 イメージ内の色は、デバイスコンテキストの背景色に関係なく同じように表示されます。 で指定された描画スタイル `Draw` も、nonmasked イメージの外観には影響しません。

描画メンバー関数に加えて、別の関数[DrawIndirect](reference/cimagelist-class.md#drawindirect)は、イメージをレンダリングする機能を拡張します。 `DrawIndirect`は、パラメーターとして、 [Imagelistdrawparams](/windows/win32/api/commctrl/ns-commctrl-imagelistdrawparams)構造体を受け取ります。 この構造体は、ラスター操作 (ROP) コードの使用など、現在のイメージのレンダリングをカスタマイズするために使用できます。 ROP コードの詳細については、Windows SDK の「[ラスター操作コード](/windows/win32/gdi/raster-operation-codes)と[ブラシとしてのビットマップ](/windows/win32/gdi/bitmaps-as-brushes)」を参照してください。

## <a name="see-also"></a>関連項目

[CImageList の使い方](using-cimagelist.md)<br/>
[制限](controls-mfc.md)
