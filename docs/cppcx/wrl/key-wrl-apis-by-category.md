---
title: カテゴリ別の主要な WRL API
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 7367bacf-6b7c-4ecd-a0ce-a662db46fc66
ms.openlocfilehash: 8ac89f3286866ac61bac5ae256bdb448fe88f07d
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80213825"
---
# <a name="key-wrl-apis-by-category"></a>カテゴリ別の主要な WRL API

次の表は、プライマリC++ Windows ランタイムテンプレートライブラリのクラス、構造体、関数、およびマクロを示しています。 ヘルパー名前空間とクラスのコンストラクトは省略されています。 これらのリストは、名前空間によって配置される API ドキュメントを拡張したものです。

## <a name="classes"></a>クラス

|タイトル|説明|
|-----------|-----------------|
|[ActivationFactory クラス](activationfactory-class.md)|1 つ以上のクラスを Windows ランタイムによってアクティブ化できるようにします。|
|[AsyncBase クラス](asyncbase-class.md)|Windows ランタイムの非同期ステート マシンを実装します。|
|[ClassFactory クラス](classfactory-class.md)|`IClassFactory` インターフェイスの基本機能を実装します。|
|[ComPtr クラス](comptr-class.md)|テンプレート パラメーターで指定されたインターフェイスを表す *スマート ポインター* 型を作成します。 ComPtr は、基になるインターフェイス ポインターの参照カウントを自動的に維持し、参照カウントがゼロになるとそのインターフェイスを解放します。|
|[Event クラス (Windows ランタイム C++ テンプレート ライブラリ)](event-class-wrl.md)|イベントを表します。|
|[EventSource クラス](eventsource-class.md)|イベントを表します。 `EventSource` メンバー関数は、イベント ハンドラーの追加、削除、および呼び出しを実行します。|
|[FtmBase クラス](ftmbase-class.md)|フリー スレッド マーシャラー オブジェクトを表します。|
|[HandleT クラス](handlet-class.md)|オブジェクトへのハンドルを表します。|
|[HString クラス](hstring-class.md)|HSTRING ハンドルの操作をサポートします。|
|[HStringReference クラス](hstringreference-class.md)|既存の文字列から作成された HSTRING を表します。|
|[Module クラス](module-class.md)|関連するオブジェクトから成るコレクションを表します。|
|[Module::GenericReleaseNotifier クラス](module-genericreleasenotifier-class.md)|現在のモジュールの最後のオブジェクトが解放されたときに、イベントハンドラーを呼び出します。 イベントハンドラーは、ラムダ、ファンクタ、またはポインターから関数によって指定されます。|
|[Module::MethodReleaseNotifier クラス](module-methodreleasenotifier-class.md)|現在のモジュールの最後のオブジェクトが解放されたときに、イベントハンドラーを呼び出します。 イベントハンドラーは、オブジェクトおよびそのポインターからメソッドへのメンバーによって指定されます。|
|[Module::ReleaseNotifier クラス](module-releasenotifier-class.md)|モジュール内の最後のオブジェクトが解放されたときに、イベントハンドラーを呼び出します。|
|[RoInitializeWrapper クラス](roinitializewrapper-class.md)|Windows ランタイムを初期化します。|
|[RuntimeClass クラス](runtimeclass-class.md)|指定した数のインターフェイスを継承し、指定した Windows ランタイム、クラシック COM、および弱い参照をサポートする、インスタンス化されたクラスを表します。|
|[SimpleActivationFactory クラス](simpleactivationfactory-class.md)|Windows ランタイムまたはクラシック COM の基底クラスを作成するための基本的なメカニズムを提供します。|
|[SimpleClassFactory クラス](simpleclassfactory-class.md)|基底クラスを作成するための基本的なメカニズムを提供します。|
|[WeakRef クラス](weakref-class.md)|クラシック COM ではなく、Windows ランタイムでのみ使用できる *弱い参照* を表します。 弱い参照は、アクセスできる場合とできない場合があるオブジェクトを表します。|

## <a name="structures"></a>構造体

|タイトル|説明|
|-----------|-----------------|
|[ChainInterfaces 構造体](chaininterfaces-structure.md)|一連のインターフェイス ID に適用できる検証および初期化関数を指定します。|
|[CloakedIid 構造体](cloakediid-structure.md)|指定したインターフェイスに IID の一覧でアクセスできない `RuntimeClass`、`Implements`、および `ChainInterfaces` テンプレートを示します。|
|[Implements 構造体](implements-structure.md)|指定されたインターフェイスの `QueryInterface` と `GetIid` を実装します。|
|[MixIn 構造体](mixin-structure.md)|ランタイム クラスが Windows ランタイム インターフェイス (存在する場合) から派生し、次にクラシック COM インターフェイスから派生していることを確認します。|

## <a name="functions"></a>関数

|タイトル|説明|
|-----------|-----------------|
|[ActivateInstance 関数](activateinstance-function.md)|指定したクラス ID で定義されている、指定した型のインスタンスを登録して取得します。|
|[AsWeak 関数](asweak-function.md)|指定されたインスタンスへの弱い参照を取得します。|
|[コールバック関数](callback-function-wrl.md)|メンバー関数がコールバック メソッドであるオブジェクトを作成します。|
|[CreateActivationFactory 関数](createactivationfactory-function.md)|Windows ランタイムによるアクティブ化が可能な、指定されたクラスのインスタンスを生成するファクトリを作成します。|
|[CreateClassFactory 関数](createclassfactory-function.md)|指定されたクラスのインスタンスを生成するファクトリを作成します。|
|[GetActivationFactory 関数](getactivationfactory-function.md)|テンプレートパラメーターによって指定された型のアクティベーションファクトリを取得します。|
|[Make 関数](make-function.md)|指定した Windows ランタイムクラスを初期化します。|

## <a name="macros"></a>マクロ

|タイトル|説明|
|-----------|-----------------|
|[ActivatableClass マクロ](activatableclass-macros.md)|指定したクラスのインスタンスを作成できるファクトリを含む内部キャッシュを作成します。|
|[InspectableClass マクロ](inspectableclass-macro.md)|ランタイム クラス名と信頼レベルを設定します。|

## <a name="see-also"></a>参照

[Windows ランタイム C++ テンプレート ライブラリ (WRL)](windows-runtime-cpp-template-library-wrl.md)
