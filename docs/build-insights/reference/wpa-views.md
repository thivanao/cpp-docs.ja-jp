---
title: 'リファレンス: Windows パフォーマンス アナライザービュー'
description: Windows パフォーマンス アナライザで使用できる C++ ビルド インサイト ビューのリファレンス。
ms.date: 11/03/2019
helpviewer_keywords:
- C++ Build Insights
- throughput analysis
- build time analysis
- vcperf.exe
ms.openlocfilehash: b54b1b76d83b77ec7b8d8d3309d81ed9eb2db2d0
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81323230"
---
# <a name="reference-windows-performance-analyzer-views"></a>リファレンス: Windows パフォーマンス アナライザービュー

::: moniker range="<=vs-2017"

C++ ビルドインサイト ツールは、Visual Studio 2019 で使用できます。 このバージョンのドキュメントを参照するには、この記事の Visual Studio**バージョン**セレクター コントロールを Visual Studio 2019 に設定します。 このページの目次の上部に表示されます。

::: moniker-end
::: moniker range="vs-2019"

この記事では、Windows パフォーマンス アナライザー (WPA) で使用できる C++ ビルド インサイトの各ビューの詳細について説明します。 このページを使用して、以下を検索します。

- データ列の説明。そして
- 各ビューで使用できるプリセット (使用目的や優先表示モードなど)

WPA を初めて使用する場合は、まず WPA for [C++ ビルド インサイトの基本](/cpp/build-insights/tutorials/wpa-basics)について理解しておくことをお勧めします。

## <a name="build-explorer"></a>ビルド エクスプローラー

ビルド エクスプローラ ビューは、次の用途に使用されます。

- 並列処理の問題を診断し、
- ビルド時間が解析、コード生成、リンクによって支配されているかどうかを判断し、
- ボトルネックと異常に長いビルドアクティビティを特定します。

### <a name="build-explorer-view-data-columns"></a>ビルド エクスプローラー ビューのデータ列

| 列名 | 説明 |
|-|-|
| タイムラインの説明 | 現在のアクティビティまたはプロパティが発生するタイムラインを説明するテキスト。 |
| ビルドタイムライン Id          | 現在のアクティビティまたはプロパティが発生するタイムラインの 0 から始まる識別子。 |
| コンポーネント                | 現在のイベントが生成されたときにコンパイルまたはリンクされているコンポーネント。 この列の値は、*\<\>* このイベントに関連付けられているコンポーネントがない場合の呼び出し X Info です。 X は、イベントが発生した時点で実行される呼び出しの一意の数値識別子です。 この識別子は、このイベントの InvocationId 列の識別子と同じです。 |
| Count                    | このデータ行によって表されるアクティビティまたはプロパティの数。 この値は常に 1 であり、複数の行がグループ化されている場合にのみ集計シナリオで役立ちます。 |
| 排他 CPU タイム         | このアクティビティで使用される CPU 時間 (ミリ秒単位)。 子アクティビティで費やされた時間は、この金額には含まれません。 |
| エクスクルーシブ期間        | アクティビティのミリ秒単位の期間。 子アクティビティの期間は、この金額には含まれません。 |
| インクルーシブ CPU タイム         | このアクティビティとすべての子アクティビティで使用される CPU 時間 (ミリ秒単位)。 |
| インクルーシブ期間        | すべての子アクティビティを含む、このアクティビティのミリ秒単位の期間。 |
| 呼び出し説明    | このイベントが発生した呼び出しのテキストの説明。 説明には *、cl.exe*または*link.exe*のどちらであったか、および一意の数値呼び出し識別子が含まれます。 該当する場合は、呼び出し中にコンパイルまたはリンクされたコンポーネントへの完全パスが含まれます。 コンポーネントをビルドしない呼び出し、または複数のコンポーネントをビルドする呼び出しの場合、パスは空白になります。 呼び出し ID は、InvocationId 列の呼び出し識別子と同じです。 |
| 呼び出し ID             | このイベントが発生した呼び出しの一意の数値識別子。 |
| 名前                     | このイベントによって表されるアクティビティまたはプロパティの名前。 |
| Time                     | イベントが発生した時刻を識別するタイムスタンプ。 |
| ツール                     | このイベントが発生したときに実行されるツール。 この列の値は、CL またはリンクです。 |
| Type                     | 現在のイベントの型。 この値は、アクティビティまたはプロパティのいずれかです。 |
| [値]                    | 現在のイベントがプロパティの場合、この列には値が格納されます。 現在のイベントがアクティビティの場合、この列は空白のままになります。 |

### <a name="build-explorer-view-presets"></a>ビルド エクスプローラー ビューのプリセット

| プリセット名           | 優先表示モード | 使用方法 |
|-----------------------|---------------------|------------|
| アクティビティ統計   | グラフ/表       | このプリセットを使用して、すべてのビルド・エクスプローラー・アクティビティーの集約統計を表示します。 テーブル モードでは、ビルドが解析、コード生成、リンカーによって優位に立っているかどうかを一目で確認します。 各アクティビティの集計期間は降順に並べ替えられます。 トップ ノードを展開してドリルインし、これらのトップ アクティビティに最も時間がかかる呼び出しを簡単に見つけることができます。 必要に応じて、平均や他の種類の集計を表示するように WPA 設定を調整できます。 グラフ モードでは、ビルド中に各アクティビティがいつアクティブになっているか確認します。 |
| 呼び出し           | グラフ               | グラフ ビュー内の呼び出しのリストを開始時刻で並べ替えて下にスクロールします。 CPU (サンプル) ビューと共に使用して、CPU 使用率の低いゾーンに合わせた呼び出しを見つけることができます。 並列処理の問題を検出します。 |
| 呼び出しプロパティ | テーブル               | 特定のコンパイラまたはリンカー呼び出しに関する重要な情報をすばやく見つけることができます。 そのバージョン、作業ディレクトリ、またはそれを呼び出すために使用される完全なコマンドラインを決定します。 |
| タイムライン             | グラフ               | ビルドがどのように並列化されたかを棒グラフで確認できます。 並列処理の問題とボトルネックを一目で特定します。 必要に応じて、さまざまな意味をバーに割り当てるように WPA を設定します。 最後のグループ化された列として呼び出しの説明を選択すると、すべての呼び出しのカラー・コード化された棒グラフが表示されます。 時間のかかる犯人を迅速に特定するのに役立ちます。 次に、拡大して、最も長い部分を表示する最後のグループ化された列としてアクティビティ名を選択します。 |

## <a name="files"></a>ファイル

ファイル ビューは、次の用途に使用されます。

- どのヘッダーが最も頻繁に含まれるかを決定し、
- を使用すると、コンパイル済みヘッダー (PCH) に含める内容を決定できます。

### <a name="files-view-data-columns"></a>ファイル ビュー データ列

| 列名              | 説明 |
|--------------------------|-------------|
| ActivityName             | このファイル イベントが生成されたときに進行中のアクティビティ。 現在、この値は常に*解析です*。 |
| タイムラインの説明 | * |
| ビルドタイムライン Id          | * |
| コンポーネント                | * |
| Count                    | * |
| 奥行き                    | インクルード ツリー内のこのファイルが見つかった位置を 0 から始まる位置。 カウントはインクルードツリーのルートから始まります。 値 0 は、通常、.c/.cpp ファイルに対応します。 |
| エクスクルーシブ期間        | * |
| 含まれるもの               | 現在のファイルを含むファイルの完全パス。 |
| インクルードパス             | 現在のファイルの完全パス。 |
| インクルーシブ期間        | * |
| 呼び出し ID             | * |
| StartTime                | 現在のファイル イベントが生成された時刻を表すタイムスタンプ。 |
| ツール                     | * |

\*この列の値は、[ビルド エクスプローラー](#build-explorer-view-data-columns)ビューと同じです。

### <a name="files-view-presets"></a>ファイルビュープリセット

| プリセット名 | 優先表示モード | 使用方法 |
|-------------|---------------------|------------|
| 統計  | テーブル               | リストを降順で確認して、集約解析時間が最も高かったファイルを確認します。 この情報は、ヘッダーの再構成や、PCH に含める内容の決定に役立ちます。 |

## <a name="functions"></a>関数

関数ビューは、コード生成時間が長すぎる関数を識別するために使用されます。

### <a name="functions-view-data-columns"></a>関数ビューデータ列

| 列名              | 説明 |
|--------------------------|-------------|
| ActivityName             | この関数イベントが生成されたときに進行中のアクティビティ。 現在、この値は常に*コードジェネレーション*です。 |
| タイムラインの説明 | * |
| ビルドタイムライン Id          | * |
| コンポーネント                | * |
| Count                    | * |
| Duration                 | この関数のコード生成アクティビティの期間。 |
| FunctionName             | コード生成中の関数の名前。 |
| 呼び出し ID             | * |
| StartTime                | 現在の関数イベントが生成された時刻を表すタイムスタンプ。 |
| ツール                     | * |

\*この列の値は、[ビルド エクスプローラー](#build-explorer-view-data-columns)ビューと同じです。

### <a name="functions-view-presets"></a>関数ビュープリセット

| プリセット名 | 優先表示モード | 使用方法 |
|-------------|---------------------|------------|
| 統計  | テーブル               | リストを降順で見て、集約されたコード生成時間が最も高かった関数を確認します。 コードが **__forceinline**キーワードを使い過ぎている場合や、一部の関数が大きすぎる可能性があることを示唆している場合があります。 |
| タイムライン   | グラフ               | この棒グラフを見て、生成に最も時間がかかる関数の位置と期間を確認します。 ビルド エクスプローラー ビューでボトルネックに対応しているかどうかを確認します。 その場合は、適切なアクションを実行してコード生成時間を短縮し、ビルド時間を有効に活用します。 |

## <a name="see-also"></a>関連項目

[C++ ビルドインサイトの概要](/cpp/build-insights/get-started-with-cpp-build-insights)\
[リファレンス: vcperf コマンド](vcperf-commands.md)\
[チュートリアル: Windows パフォーマンス アナライザの基本](/cpp/build-insights/tutorials/wpa-basics)\
[Windows Performance Analyzer](/windows-hardware/test/wpt/windows-performance-analyzer)

::: moniker-end
