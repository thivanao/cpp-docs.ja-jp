---
title: '方法: プロジェクト ファイルを変更せずに C++ プロジェクトのプロパティとターゲットを変更する'
ms.date: 11/28/2018
helpviewer_keywords:
- project properties [C++], modifying outside project file
ms.openlocfilehash: 72107b572e35f222c0b03959e0edd2d23bd0130a
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81328456"
---
# <a name="how-to-modify-c-project-properties-and-targets-without-changing-the-project-file"></a>方法: プロジェクト ファイルを変更せずに C++ プロジェクトのプロパティとターゲットを変更する

プロジェクト ファイルを変更することなく、MSBuild のコマンド プロンプトからプロジェクトのプロパティとターゲットをオーバーライドできます。 これは、一時的に、またはときどき一部のプロパティを適用する場合に便利です。 MSBuild のある程度の知識が必要です。 詳しくは、「[MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild)」をご覧ください。

> [!IMPORTANT]
> Visual Studio の XML エディターまたは任意のテキスト エディターを使って、.props ファイルまたは .targets ファイルを作成します。 **プロパティ マネージャー**はプロジェクト ファイルにプロパティを追加するため、このシナリオでは使わないでください。

*プロジェクトのプロパティをオーバーライドするには:*

1. オーバーライドするプロパティを指定する .props ファイルを作成します。

1. コマンド プロンプトから、ForceImportBeforeCppTargets="C:\sources\my_props.props" を設定します

*プロジェクトのターゲットをオーバーライドするには:*

1. 実装または特定のターゲットの .targets ファイルを作成します

2. コマンド プロンプトから、ForceImportAfterCppTargets ="C:\sources\my_target.targets" を設定します

msbuild のコマンド ラインで /p: オプションを使って、いずれかのオプションを設定することもできます。

```cmd
> msbuild myproject.sln /p:ForceImportBeforeCppTargets="C:\sources\my_props.props"
> msbuild myproject.sln /p:ForceImportAfterCppTargets="C:\sources\my_target.targets"
```

この方法でプロパティとターゲットをオーバーライドするのは、ソリューション内のすべての .vcxproj ファイルに次のインポートを追加することと同じです。

```cmd
<Import Project=="C:\sources\my_props.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
<Import Project==" C:\sources\my_target.targets"" />
```
