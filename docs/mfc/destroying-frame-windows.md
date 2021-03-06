---
title: フレーム ウィンドウの破棄
ms.date: 11/04/2016
f1_keywords:
- PostNcDestroy
helpviewer_keywords:
- Default method [MFC]
- DestroyWindow method [MFC]
- frame windows [MFC], destroying
- OnNcDestroy method, and frame windows
- document frame windows [MFC], destroying
- destroying frame windows
- MFC, frame windows
- windows [MFC], destroying
- OnClose method [MFC]
- PostNcDestroy method [MFC]
ms.assetid: 5affca77-1999-4507-a2b2-9aa226611b4b
ms.openlocfilehash: 4bc7945ecd9aee9021ce97fa3ea05f512c58fe20
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84621930"
---
# <a name="destroying-frame-windows"></a>フレーム ウィンドウの破棄

MFC フレームワークは、ウィンドウの破棄と、フレームワークのドキュメントやビューに関連付けられたウィンドウの作成を管理します。 追加のウィンドウを作成する場合は、そのウィンドウを破棄する必要があります。

フレームワークでは、ユーザーがフレームウィンドウを閉じると、ウィンドウの既定の[OnClose](reference/cwnd-class.md#onclose)ハンドラーは[DestroyWindow](reference/cwnd-class.md#destroywindow)を呼び出します。 Windows ウィンドウが破棄されるときに呼び出される最後のメンバー関数は[OnNcDestroy](reference/cwnd-class.md#onncdestroy)であり、一部のクリーンアップでは、windows クリーンアップを実行する[既定](reference/cwnd-class.md#default)のメンバー関数を呼び出し、最後に仮想メンバー関数[PostNcDestroy](reference/cwnd-class.md#postncdestroy)を呼び出します。 の[CFrameWnd](reference/cframewnd-class.md)実装は、 `PostNcDestroy` C++ ウィンドウオブジェクトを削除します。 フレームウィンドウでは、C++ **delete**演算子を使用しないでください。 代わりに、`DestroyWindow` を使用してください。

メインウィンドウが閉じると、アプリケーションが閉じます。 未保存のドキュメントが変更されている場合、フレームワークは、ドキュメントを保存するかどうかを確認するメッセージボックスを表示し、必要に応じて適切なドキュメントが保存されるようにします。

## <a name="what-do-you-want-to-know-more-about"></a>詳細については、次を参照してください。

- [ドキュメント フレーム ウィンドウの作成](creating-document-frame-windows.md)

## <a name="see-also"></a>関連項目

[フレームウィンドウの使用](using-frame-windows.md)
