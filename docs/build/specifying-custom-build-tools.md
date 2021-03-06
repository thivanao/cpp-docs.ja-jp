---
title: カスタム ビルド ツールの指定
ms.date: 06/05/2018
f1_keywords:
- VC.Project.VCCustomBuildTool.CustomBuildToolBeforeTargets
- VC.Project.VCCustomBuildTool.Outputs
- VC.Project.VCCustomBuildTool.Command
- VC.Project.VCCustomBuildTool.CommandLine
- VC.Project.VCCustomBuildTool.AdditionalDependencies
- VC.Project.VCCustomBuildTool.Message
- VC.Project.VCCustomBuildTool.CustomBuildToolAfterTargets
- VC.Project.VCCustomBuildTool.Description
- VC.Project.VCCustomBuildTool.AdditionalInputs
helpviewer_keywords:
- build tools (C++), specifying
- custom build tools (C++), specifying
- builds (C++), custom build tools
ms.openlocfilehash: dbce226b34503a9e8e70b6f19d9aa0c68ef487f3
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62314755"
---
# <a name="specify-custom-build-tools"></a>カスタム ビルド ツールを指定する

*カスタム ビルド ツール*は、特定の入力ファイルのビルドに必要な情報をビルド システムに提供します。 カスタム ビルド ツールは、実行するコマンド、入力ファイルの一覧、コマンドによって生成される出力ファイルの一覧、ツールの任意の説明を指定します。

カスタム ビルド ツールとカスタム ビルド ステップの全般情報については、「[カスタム ビルド ステップとビルド イベントについて](understanding-custom-build-steps-and-build-events.md)」を参照してください。

### <a name="to-specify-a-custom-build-tool"></a>カスタム ビルド ツールを指定するには

1. プロジェクトの **[プロパティ ページ]** ダイアログ ボックスを開きます。 詳しくは、「[Visual Studio で C++ コンパイラとビルド プロパティを設定する](working-with-project-properties.md)」をご覧ください。

1. **[構成プロパティ]** を選択し、 **[構成]** ボックスを有効にします。 **[構成]** ボックスで、カスタム ビルド ツールを指定する構成を選択します。

1. **[ソリューション エクスプローラー]** で、カスタム ビルド ツールの入力ファイルを選択します。

   **[カスタム ビルド ツール]** フォルダーが表示されない場合、選択したファイルのファイル拡張子が既定のツールに関連付けられています。 たとえば、.c ファイルと .cpp ファイルの既定のツールはコンパイラです。 既定のツール設定をオーバーライドするには、 **[構成プロパティ]** ノードの **[全般]** フォルダーの **[項目の種類]** プロパティで **[カスタム ビルド ツール]** を選択します。 **[適用]** を選択します。 **[カスタム ビルド ツール]** ノードが表示されます。

1. **[カスタム ビルド ツール]** ノードの **[全般]** フォルダーで、カスタム ビルド ツールに関連付けられているプロパティを指定します。

   - **[追加の依存ファイル]** で、カスタム ビルド ツールが定義されているファイル以外の追加ファイルを指定します (カスタム ビルド ツールが関連付けられているファイルはツールへの入力として暗黙的に見なされます)。 追加の入力ファイルを指定することは、カスタム ビルド ツールの要件ではありません。 追加入力が複数になる場合、セミコロンで区切ります。

      **[追加の依存ファイル]** の日付が入力ファイルより後になっている場合、カスタム ビルド ツールは実行されます。 **[追加の依存ファイル]** がすべて入力ファイルより古く、入力ファイルが **[出力]** プロパティ ファイルより古い場合、カスタム ビルド ツールは実行されません。

      たとえば、MyInput.x を入力として受け取り、MyInput.cpp を生成するカスタム ビルド ツールがある場合、その MyInput.x にはヘッダー ファイル MyHeader.h が含まれます。 MyInput.x に対する入力依存関係として MyHeader.h を指定できます。MyInput.cpp が MyInput.x または MyHeader.h に対して古くなっている場合は、ビルドされます。

      また、入力依存関係があることで、それに求められる順番でカスタム ビルド ツールが実行されます。 上記の例で、MyHeader.h が実際、カスタム ビルド ツールの出力であると仮定します。 MyHeader.h が MyInput.x の依存関係であるため、先に Myheader.h がビルドされ、それから MyInput.x でカスタム ビルド ツールが実行されます。

   - **[コマンド ライン]** で、コマンド プロンプトの場合と同様にコマンドを指定します。 有効なコマンドまたはバッチ ファイルと必要な入力ファイルまたは出力ファイルがあればそれを指定します。 後続のコマンドがすべて確実に実行されるように、バッチ ファイル名の前に **call** バッチ コマンドを指定します。

      MSBuild マクロを利用すれば、複数の入力ファイルと出力ファイルを数式で指定できます。 ファイルの場所またはファイル セットの名前を指定する方法については、「[Common macros for build commands and properties](reference/common-macros-for-build-commands-and-properties.md)」 (ビルドのコマンドとプロパティの共通マクロ) を参照してください。

      '%' は MSBuild に予約されている文字です。環境変数を指定する場合、エスケープ文字 **%** をそれぞれ、16 進数エスケープ シーケンス **%25** に変更してください。 たとえば、 **%WINDIR%** を **%25WINDIR%25** に変更します。 MSBuild は **%25** シーケンスをそれぞれ **%** 文字に変更し、それから環境変数にアクセスします。

   - **[説明]** に、このカスタム ビルド ツールに関する説明メッセージを入力します。 ビルド システムでこのツールが処理されるとき、このメッセージが **[出力]** ウィンドウに表示されます。

   - **[出力]** に出力ファイルの名前を指定します。 これは入力必須項目です。このプロパティに値がないと、カスタム ビルド ツールは実行されません。 1 つのカスタム ビルド ツールに複数の出力がある場合、ファイル名をセミコロンで区切ります。

      出力ファイルの名前は、 **[コマンド ライン]** プロパティに指定されている名前と同じにする必要があります。 プロジェクト ビルド システムはファイルを探し、その日付を確認します。 出力ファイルが入力ファイルより古いか、出力ファイルが見つからない場合は、カスタム ビルド ツールが実行されます。 **[追加の依存ファイル]** がすべて入力ファイルより古いか、入力ファイルが **[出力]** プロパティに指定されているファイルより古い場合、カスタム ビルド ツールは実行されません。

カスタム ビルド ツールによって生成される出力ファイルをビルド システムに処理させる場合、その出力ファイルを手動でプロジェクトに追加する必要があります。 ビルド中、カスタム ビルド ツールはファイルを更新します。

## <a name="example"></a>例

parser.l という名前のファイルをプロジェクトに含めるとします。 実行可能パスには、**lexer.exe** という字句解析ツールを置いています。 それを使用して parser.l を処理し、同じ基本名 (parser.c) を持つ .c ファイルを生成します。

まず、parser.l と parser.c をプロジェクトに追加します。 ファイルがまだ存在しない場合、参照をファイルに追加します。 parser.l のカスタム ビルド ツールを作成し、 **[コマンド]** プロパティに次を入力します。

> **lexer %(FullPath) .\%(Filename).c**

このコマンドは parser.l で字句解析ツールを実行し、parser.c をプロジェクト ディレクトリに出力します。

**[出力]** プロパティに、次を入力します。

> **.\%(Filename).c**

プロジェクトをビルドすると、parser.l と parser.c のタイムスタンプが比較されます。 parser.l のほうが新しいか、parser.c が存在しない場合、 **[コマンド ライン]** プロパティの値が実行され、parser.c を最新の状態にします。 parser.c もプロジェクトに追加されていたため、parser.c がコンパイルされます。

## <a name="see-also"></a>関連項目

[ビルドのコマンドとプロパティの共通マクロ](reference/common-macros-for-build-commands-and-properties.md)<br>
[ビルドのカスタマイズのトラブルシューティング](troubleshooting-build-customizations.md)
