---
title: ユニバーサル Windows アプリ (C++)
ms.date: 03/30/2018
ms.assetid: 357121cc-d390-4bae-b34a-39614861a9f4
ms.topic: overview
ms.openlocfilehash: 500aa5337382cfb5aca4d4c8d1774d256498d0a0
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80214276"
---
# <a name="universal-windows-apps-c"></a>ユニバーサル Windows アプリ (C++)

ユニバーサル Windows プラットフォーム (UWP) は、Windows の最新のプログラミングインターフェイスです。 UWP では、アプリケーションまたはコンポーネントを1回記述し、任意の Windows 10 デバイスにデプロイします。 コンポーネントは、にC++記述できます。また、他の UWP 互換言語で記述されたアプリケーションでも使用できます。

UWP ドキュメントのほとんどは、[ユニバーサル Windows プラットフォームのドキュメント](/windows/uwp/)にある Windows コンテンツツリーに含まれています。 ここでは、最初のチュートリアルとリファレンスドキュメントを紹介します。

新しい UWP アプリとコンポーネントの場合は、Windows ランタイム api 向けの新しい標準 c++ 17 言語プロジェクションである[ C++/WinRT](/windows/uwp/cpp-and-winrt-apis/)を使用することをお勧めします。 C++/WinRT はバージョン 1803 以降から Windows 10 SDK で使用できます。 C++/WinRT はヘッダー ファイル、完全に実装されは最新の Windows API にファースト クラスのアクセス提供するために設計されています。 C++/Cx 実装とは異なります。 C++/WinRT には、非標準の構文または Microsoft 言語拡張機能を使用しないし、高度に最適化された出力を作成する C++ コンパイラを最大限に活用します。 詳細については、「 [ C++/WinRT の概要](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt)」を参照してください。

Desktop Bridge app converter を使用して、既存のデスクトップアプリケーションをパッケージ化して、Microsoft Store でデプロイできます。 詳細については、「Centennial プロジェクトと[デスクトップブリッジ](/windows/uwp/porting/desktop-to-uwp-root)[での Visual C++ Runtime の使用](https://blogs.msdn.microsoft.com/vcblog/2016/07/07/using-visual-c-runtime-in-centennial-project)」を参照してください。

## <a name="uwp-apps-that-use-ccx"></a>C++/CX を使用する UWP アプリ

|||
|-|-|
|[C++/CX 言語リファレンス](visual-c-language-reference-c-cx.md)|C++ を Windows ランタイム API の使用を簡略化し、例外に基づいているエラー処理を有効にする拡張機能のセットについて説明します。|
|[アプリケーションとライブラリのビルド (C++/CX)](building-apps-and-libraries-c-cx.md)|C ++/CX アプリケーションまたはコンポーネントからアクセスできるスタティック ライブラリと DLL を作成する方法について説明します。|
|[チュートリアル: UWP の "Hello, World" アプリを/Cx C++で作成する](/windows/uwp/get-started/create-a-basic-windows-10-app-in-cpp)|C++ /CX での UWP アプリ開発の基本概念を紹介するチュートリアル。 |
|[/Cx での Windows ランタイムC++コンポーネントの作成](/windows/uwp/winrt-components/creating-windows-runtime-components-in-cpp)|他の UWP アプリおよびコンポーネントが使用できる Dll を作成する方法について説明します。|
|[UWP ゲームのプログラミング](/windows/uwp/gaming/)|DirectX と C++/CX を使ってゲームを作成する方法を説明します。|

## <a name="uwp-apps-that-use-the-windows-runtime-c-template-library-wrl"></a>Windows ランタイムC++テンプレートライブラリ (wrl) を使用する UWP アプリ

Windows ランタイム C++ テンプレート ライブラリでは、例外のない環境で Windows ランタイムを ISO C のコードからアクセスできる低レベルの COM インターフェイスを提供します。 ほとんどの場合、UWPアプリ開発用indows ランタイム C++ テンプレート ライブラリの代わりに C++/WinRT または C++/CX を使用することを推奨します。 Windows ランタイムC++テンプレートライブラリの詳細については、「 [Windows ランタイムC++テンプレートライブラリ (wrl)](wrl/windows-runtime-cpp-template-library-wrl.md)」を参照してください。

## <a name="see-also"></a>参照

[Visual Studio での C++](../overview/visual-cpp-in-visual-studio.md)<br/>
[C++ でプログラミングする Windows の概要](../windows/overview-of-windows-programming-in-cpp.md)<br/>
