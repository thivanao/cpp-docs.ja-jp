---
title: リソース ファイルの操作 (C++)
ms.date: 02/14/2019
helpviewer_keywords:
- resources [C++], about resources
- resources [C++], about resource files
- resource files [C++], about resource files
ms.assetid: 2699a539-b369-4b78-80f0-df03eb7b6780
ms.openlocfilehash: 142a9120e0b6b95e659fcb47c275653fbefd8cbe
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80165887"
---
# <a name="working-with-resource-files"></a>リソース ファイルの操作

> [!WARNING]
> このセクションは、C++ で記述された Windows デスクトップ アプリケーションに適用されます。
>
> でC++記述され .NET Framework たユニバーサル Windows プラットフォームアプリのリソースの詳細についてはC++、「開発者ガイド[」の「](/windows/uwp/app-resources/)[デスクトップアプリのリソース](/dotnet/framework/resources/index)」を参照してください。

リソースは、次のようなさまざまな要素で構成できます。

- ビットマップ、アイコン、カーソルなどの情報をユーザーに提供するインターフェイス要素。
- データとアプリケーションのニーズを含むカスタムリソース。
- セットアップ Api によって使用されるバージョンリソース。
- メニューおよびダイアログボックスのリソース。

新しいリソースをプロジェクトに追加し、適切なリソース エディターを使用してそれらのリソースを変更できます。 ほとんどの Visual C++ ウィザードでは、プロジェクトの .rc ファイルが自動的に生成されます。

> [!NOTE]
> **リソースエディター**と**リソースビュー**は、Express edition では使用できません。

マネージプロジェクトにリソースファイルを手動で追加する方法については、「[デスクトップアプリ用のリソースファイルの作成](/dotnet/framework/resources/creating-resource-files-for-desktop-apps)」を参照してください。 この記事では、リソースへのアクセス方法、静的リソースの表示方法、およびプロパティへのリソース文字列の割り当て方法について説明します。

管理対象アプリのリソースをグローバライズおよびローカライズするには、「 [.NET Framework アプリケーションのグローバライズとローカライズ](/dotnet/standard/globalization-localization/index)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容

[リソース ファイル](../windows/resource-files-visual-studio.md)<br/>
リソースファイルと、それらが Windows デスクトップアプリケーションでどのように使用されるかについて説明します。 また、リソースファイルの使用方法を説明する記事へのリンクも示します。

[リソース識別子 (シンボル)](../windows/symbols-resource-identifiers.md)<br/>
シンボルについて説明し、プロジェクトのシンボルを管理するための **[リソース シンボル]** ダイアログ ボックスの使用方法に関する情報を提供します。

[リソース エディター](../windows/resource-editors.md)<br/>
Visual Studio で提供されるリソースエディターと、各エディターで変更できるリソースの種類について説明します。 各エディターの使用方法に関する詳細情報へのリンクも示します。

## <a name="related-sections"></a>関連項目

[Visual Studio での C++](../overview/visual-cpp-in-visual-studio.md)<br/>
Visual C++ のドキュメントへのリンクを示します。

[ご意見](/visualstudio/ide/talk-to-us)<br/>
ドキュメント セットの使用方法、製品サポートへの連絡、アクセシビリティ機能の使用に関する情報へのリンクを示します。

## <a name="see-also"></a>参照

[Windows デスクトップアプリケーション](../windows/windows-desktop-applications-cpp.md)<br/>
[メニューとその他のリソース](/windows/win32/menurc/resources)
