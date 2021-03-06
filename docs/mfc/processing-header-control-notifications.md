---
title: ヘッダー コントロール通知の処理
ms.date: 11/04/2016
helpviewer_keywords:
- CHeaderCtrl class [MFC], processing notifications
- controls [MFC], header
- notifications [MFC], processing for CHeaderCtrl
- header controls [MFC], processing notifications
- header control notifications
ms.assetid: e6c6af7c-d458-4d33-85aa-48014ccde5f6
ms.openlocfilehash: c313382b8be7538ba5bb465c6ba383955e414662
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84619792"
---
# <a name="processing-header-control-notifications"></a>ヘッダー コントロール通知の処理

ビューまたはダイアログクラスで、[クラスウィザード](reference/mfc-class-wizard.md)を使用して、処理するすべてのヘッダーコントロール ([CHeaderCtrl](reference/cheaderctrl-class.md)) 通知メッセージの Switch ステートメントを含む[OnChildNotify](reference/cwnd-class.md#onchildnotify) handler 関数を作成します (「[関数へのメッセージのマッピング](reference/mapping-messages-to-functions.md)」を参照してください)。 ユーザーがヘッダー項目をクリックまたはダブルクリックしたり、項目の間に区分線をドラッグしたりすると、通知が親ウィンドウに送信されます。

ヘッダーコントロールに関連付けられている通知メッセージは、Windows SDK の[ヘッダーコントロールリファレンス](/windows/win32/controls/header-control-reference)に一覧表示されます。

## <a name="see-also"></a>関連項目

[CHeaderCtrl の使い方](using-cheaderctrl.md)<br/>
[制限](controls-mfc.md)
