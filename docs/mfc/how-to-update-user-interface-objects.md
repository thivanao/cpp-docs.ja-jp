---
title: ユーザー インターフェイス オブジェクトの更新方法
ms.date: 11/04/2016
helpviewer_keywords:
- menus [MFC], updating as context changes
- user interface objects [MFC], updating
- user interface objects [MFC]
- update handlers [MFC]
- enabling UI elements [MFC]
- disabling menus [MFC]
- updating user-interface objects [MFC]
- disabling UI elements [MFC]
- commands [MFC], updating UI
- enabling menus [MFC]
ms.assetid: 82f09773-c978-427b-b321-05a6143b7369
ms.openlocfilehash: aec4067a7b5854ef872cfcef19a15db8438dd795
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84626385"
---
# <a name="how-to-update-user-interface-objects"></a>ユーザー インターフェイス オブジェクトの更新方法

通常、メニュー項目とツールバーボタンには複数の状態があります。 たとえば、メニュー項目が淡色表示されている場合 (淡色表示)、現在のコンテキストでは使用できません。 メニュー項目をオンまたはオフにすることもできます。 ツールバーのボタンは、使用できない場合は無効にすることも、確認することもできます。

プログラムの条件が論理的に変化したときにこれらの項目の状態を更新するのは、ドキュメントなどのメニュー項目によって処理されるコマンドが生成される場合、ドキュメントでメニュー項目を更新することに意味があります。 このドキュメントには、更新プログラムの基になっている情報が含まれている場合があります。

コマンドに複数のユーザーインターフェイスオブジェクト (メニュー項目やツールバーボタンなど) がある場合は、両方とも同じハンドラー関数にルーティングされます。 これにより、すべての同等のユーザーインターフェイスオブジェクトのユーザーインターフェイス更新コードが1つの場所にカプセル化されます。

フレームワークには、ユーザーインターフェイスオブジェクトを自動的に更新するための便利なインターフェイスが用意されています。 他の方法で更新を行うこともできますが、提供されるインターフェイスは効率的で使いやすくなります。

次のトピックでは、更新ハンドラーの使用方法について説明します。

- [更新ハンドラーが呼び出されたとき](when-update-handlers-are-called.md)

- [ON_UPDATE_COMMAND_UI マクロ](on-update-command-ui-macro.md)

- [CCmdUI クラス](the-ccmdui-class.md)

## <a name="see-also"></a>関連項目

[メニュー](menus-mfc.md)
