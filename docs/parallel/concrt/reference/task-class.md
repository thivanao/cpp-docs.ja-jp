---
title: task クラス (コンカレンシー ランタイム)
ms.date: 07/30/2019
f1_keywords:
- task
- PPLTASKS/concurrency::task
- PPLTASKS/concurrency::task::task
- PPLTASKS/concurrency::task::get
- PPLTASKS/concurrency::task::is_apartment_aware
- PPLTASKS/concurrency::task::is_done
- PPLTASKS/concurrency::task::scheduler
- PPLTASKS/concurrency::task::then
- PPLTASKS/concurrency::task::wait
helpviewer_keywords:
- task class
ms.assetid: cdc3a8c0-5cbe-45a0-b5d5-e9f81d94df1a
ms.openlocfilehash: d42c7fbd3e065fc295027b7c56e207b2a49221bb
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81358733"
---
# <a name="task-class-concurrency-runtime"></a>task クラス (コンカレンシー ランタイム)

並列パターン ライブラリ (PPL) `task` クラス。 オブジェクト`task`は、同時実行ランタイムで並列アルゴリズムによって生成される他のタスクや並列処理と非同期に同時に実行できる作業を表します。 正常に終了した場合は、型 `_ResultType` の結果が生成されます。 型 `task<void>` のタスクでは結果が作成されません。 タスクは、他のタスクと関係なく待機および取り消しできます。 また、継続( )、結合`then``when_all`()、選択()`when_any`パターンを使用して、他のタスクと組み合わせることも可能です。 タスク オブジェクトが新しい変数に割り当てられると、動作は`std::shared_ptr`、 の動作になります。つまり、両方のオブジェクトが同じ基本タスクを表します。

## <a name="syntax"></a>構文

```cpp
template <>
class task<void>;

template<typename _ResultType>
class task;
```

### <a name="parameters"></a>パラメーター

*_ResultType*<br/>
タスクによって生成される結果の型。

## <a name="members"></a>メンバー

### <a name="public-typedefs"></a>パブリック typedef

|名前|説明|
|----------|-----------------|
|`result_type`|このクラスのオブジェクトによって生成される結果の型。|

### <a name="public-constructors"></a>パブリック コンストラクター

|名前|説明|
|----------|-----------------|
|[タスク](#ctor)|オーバーロードされます。 `task` オブジェクトを構築します。|

### <a name="public-methods"></a>パブリック メソッド

|名前|説明|
|----------|-----------------|
|[get](#get)|オーバーロードされます。 このタスクによって生成された結果を返します。 タスクが終了状態にない場合、`get` への呼び出しは、そのタスクが完了するまで待機します。 このメソッドは、`result_type` が `void` に指定されたタスクで呼び出された場合は値を返しません。|
|[is_apartment_aware](#is_apartment_aware)|タスクが Windows ランタイム `IAsyncInfo` インターフェイスをラップ解除するか、こうしたタスクの子であるかを決定します。|
|[is_done](#is_done)|タスクが完了したかどうかを決定します。|
|[スケジューラ](#scheduler)|このタスクのスケジューラを返します|
|[そうしたら](#then)|オーバーロードされます。 継続タスクをこのタスクに追加します。|
|[待つ](#wait)|このタスクが終了状態になるまで待機します。 タスクの依存関係すべてが満たされ、バックグラウンド ワーカーによって実行用にまだ検出されていない場合、`wait` はタスクをインラインで実行できます。|

### <a name="public-operators"></a>パブリック演算子

|名前|説明|
|----------|-----------------|
|[演算子!=](#operator_neq)|オーバーロードされます。 2 つの `task` オブジェクトが異なる内部タスクを表すかどうかを決定します。|
|[演算子=](#operator_eq)|オーバーロードされます。 ある `task` オブジェクトの内容を別のオブジェクトの内容で置き換えます。|
|[演算子==](#operator_eq_eq)|オーバーロードされます。 2 つの `task` オブジェクトが同じ内部タスクを表すかどうかを決定します。|

## <a name="remarks"></a>解説

詳細については、「[タスクの並列処理](../../../parallel/concrt/task-parallelism-concurrency-runtime.md)」を参照してください。

## <a name="inheritance-hierarchy"></a>継承階層

`task`

## <a name="requirements"></a>必要条件

**ヘッダー:** ppltasks.h

**名前空間:** 同時実行

## <a name="get"></a><a name="get"></a>取得

このタスクによって生成された結果を返します。 タスクが終了状態にない場合、`get` への呼び出しは、そのタスクが完了するまで待機します。 このメソッドは、`result_type` が `void` に指定されたタスクで呼び出された場合は値を返しません。

```cpp
_ResultType get() const;

void get() const;
```

### <a name="return-value"></a>戻り値

タスクの結果。

### <a name="remarks"></a>解説

タスクが取り消されると、 を`get`呼び出すと[、task_canceled](task-canceled-class.md)例外がスローされます。 タスクで別の例外が発生したり、継続元タスクからこのタスクに例外が反映された場合、`get` の呼び出しは、その例外をスローします。

> [!IMPORTANT]
> ユニバーサル Windows プラットフォーム (UWP) アプリでは、ユーザー インターフェイス スレッドで実行されるコードで`wait`同時`get`実行を呼び出す必要はありません:[タスク::待機](#wait)または`get`( 呼び出し ) 。 それ以外の場合、ランタイムは、現在のスレッドをブロックし、アプリが応答しなくなる可能性があるため、[同時実行をスローします::invalid_operation。](invalid-operation-class.md) ただし、結果は直ちに使用できるため、タスク ベースの継続で継続元タスクの結果を受け取るために `get` メソッドを呼び出すことができます。

## <a name="is_apartment_aware"></a><a name="is_apartment_aware"></a>is_apartment_aware

タスクが Windows ランタイム `IAsyncInfo` インターフェイスをラップ解除するか、こうしたタスクの子であるかを決定します。

```cpp
bool is_apartment_aware() const;
```

### <a name="return-value"></a>戻り値

タスクが`IAsyncInfo`インターフェイスをラップ解除する場合、またはそのようなタスクの子孫である場合は**true、** それ以外の場合は**false。**

## <a name="taskis_done-method-concurrency-runtime"></a><a name="is_done"></a>タスク::is_done メソッド (同時実行ランタイム)

タスクが完了したかどうかを決定します。

```cpp
bool is_done() const;
```

### <a name="return-value"></a>戻り値

タスクが完了した場合は true を返します。それ以外の場合は false を返します。

### <a name="remarks"></a>解説

関数は、タスクが完了した場合または取り消された場合に true を返します (ユーザー例外の有無は問いません)。

## <a name="operator"></a><a name="operator_neq"></a>演算子!=

2 つの `task` オブジェクトが異なる内部タスクを表すかどうかを決定します。

```cpp
bool operator!= (const task<_ResultType>& _Rhs) const;

bool operator!= (const task<void>& _Rhs) const;
```

### <a name="parameters"></a>パラメーター

*_Rhs*<br/>
比較するタスク。

### <a name="return-value"></a>戻り値

オブジェクトが別の基本タスクを参照する場合**は true、** それ以外の場合**は false。**

## <a name="operator"></a><a name="operator_eq"></a>演算子=

ある `task` オブジェクトの内容を別のオブジェクトの内容で置き換えます。

```cpp
task& operator= (const task& _Other);

task& operator= (task&& _Other);
```

### <a name="parameters"></a>パラメーター

*_Other*<br/>
ソース `task` オブジェクト。

### <a name="return-value"></a>戻り値

### <a name="remarks"></a>解説

`task` がスマート ポインターのように動作すると、コピーの代入の後では、この `task` オブジェクトは `_Other` が実行する実際のタスクと同じタスクを表します。

## <a name="operator"></a><a name="operator_eq_eq"></a>演算子==

2 つの `task` オブジェクトが同じ内部タスクを表すかどうかを決定します。

```cpp
bool operator== (const task<_ResultType>& _Rhs) const;

bool operator== (const task<void>& _Rhs) const;
```

### <a name="parameters"></a>パラメーター

*_Rhs*<br/>
比較するタスク。

### <a name="return-value"></a>戻り値

オブジェクトが同じ基本タスクを参照する場合は**true、** それ以外の場合**は false。**

## <a name="taskscheduler-method-concurrency-runtime"></a><a name="scheduler"></a>タスク::スケジューラメソッド(同時実行ランタイム)

このタスクのスケジューラを返します

```cpp
scheduler_ptr scheduler() const;
```

### <a name="return-value"></a>戻り値

スケジューラへのポインター

## <a name="task"></a><a name="ctor"></a> タスク

`task` オブジェクトを構築します。

```cpp
task();

template<typename T>
__declspec(
    noinline) explicit task(T _Param);

template<typename T>
__declspec(
    noinline) explicit task(T _Param, const task_options& _TaskOptions);

task(
    const task& _Other);

task(
    task&& _Other);
```

### <a name="parameters"></a>パラメーター

*T*<br/>
パラメーターの型。これに基づいてタスクが構築されます。

*_Param*<br/>
パラメーター。これに基づいてタスクが構築されます。 これは、Windows ランタイム アプリでタスクを使用`task_completion_event<result_type>`している場合は、ラムダ、関数オブジェクト、オブジェクト、または Windows::Foundation::IAsyncInfo です。 ラムダまたは関数のオブジェクトは`std::function<X(void)>`、X が型 、、`result_type``task<result_type>`または Windows ランタイム アプリの Windows::Foundation::IAsyncInfo の変数である場合に等しい型である必要があります。

*_TaskOptions*<br/>
タスク オプションには、キャンセル トークン、スケジューラなどがあります。

*_Other*<br/>
ソース `task` オブジェクト。

### <a name="remarks"></a>解説

`task` の既定のコンストラクターは、タスクをコンテナー内で使用できるようにすることのみを目的としています。 構築された既定のタスクは、有効なタスクを割り当てるまで使用できません。 などの`get`メソッド、`wait`または`then`、既定の構築タスクで呼び出されたときに[invalid_argument](../../../standard-library/invalid-argument-class.md)例外をスローします。

`task_completion_event` から作成されたタスクは、タスクの完了イベントが設定されたときに完了します (その後で継続がスケジュールされます)。

キャンセル トークンを使用するバージョンのコンストラクターは、トークンの取得元となる `cancellation_token_source` を使用して取り消すことができるタスクを作成します。 キャンセル トークンを使用せずに作成されたタスクは、取り消すことはできません。

`Windows::Foundation::IAsyncInfo` インターフェイスまたは `IAsyncInfo` インターフェイスを返すラムダから作成されたタスクは、取り込まれている Windows ランタイムの非同期操作または非同期アクションが完了すると、終了状態になります。 同様に、ラムダから作成されたタスクは`task<result_type>`、内部タスクが終了状態に達したときに、その終了状態に達するが、ラムダが戻ったときではない、その終了状態に達する。

`task` は、スマート ポインターのように動作し、安全に値渡しされます。 この task には、複数のスレッドからアクセスできます。ロックする必要はありません。

Windows::Foundation::IAsyncInfo インターフェイスを受け取るコンストラクターオーバーロード、またはそのようなインターフェイスを返すラムダは、Windows ランタイム アプリでのみ使用できます。

詳細については、「[タスクの並列処理](../../../parallel/concrt/task-parallelism-concurrency-runtime.md)」を参照してください。

## <a name="then"></a><a name="then"></a>そうしたら

継続タスクをこのタスクに追加します。

```cpp
template<typename _Function>
__declspec(
    noinline) auto then(const _Function& _Func) const -> typename details::_ContinuationTypeTraits<_Function,
    _ResultType>::_TaskOfType;

template<typename _Function>
__declspec(
    noinline) auto then(const _Function& _Func,
    const task_options& _TaskOptions) const -> typename details::_ContinuationTypeTraits<_Function,
    _ResultType>::_TaskOfType;

template<typename _Function>
__declspec(
    noinline) auto then(const _Function& _Func,
    cancellation_token _CancellationToken,
    task_continuation_context _ContinuationContext) const -> typename details::_ContinuationTypeTraits<_Function,
    _ResultType>::_TaskOfType;

template<typename _Function>
__declspec(
    noinline) auto then(const _Function& _Func,
    const task_options& _TaskOptions = task_options()) const -> typename details::_ContinuationTypeTraits<_Function,
    void>::_TaskOfType;

template<typename _Function>
__declspec(
    noinline) auto then(const _Function& _Func,
    cancellation_token _CancellationToken,
    task_continuation_context _ContinuationContext) const -> typename details::_ContinuationTypeTraits<_Function,
    void>::_TaskOfType;
```

### <a name="parameters"></a>パラメーター

*_Function*<br/>
このタスクによって呼び出される関数オブジェクトの型。

*_Func*<br/>
このタスクが完了したときに実行される継続関数。 この継続関数では、`result_type` または `task<result_type>` の変数を入力として使用する必要があります。`result_type` は、このタスクによって生成される結果の型です。

*_TaskOptions*<br/>
タスク オプションには、キャンセル トークン、スケジューラ、および継続コンテキストなどがあります。 既定では、これら 3 つのオプションは継続元タスクから継承されます。

*_CancellationToken*<br/>
継続タスクに関連付けるキャンセル トークン。 キャンセル トークンなしで作成された継続タスクは、その継続元タスクのトークンを継承します。

*_ContinuationContext*<br/>
継続を実行する状況を指定する変数。 この変数は、UWP アプリで使用する場合にのみ役立ちます。 詳細については[、「task_continuation_context](task-continuation-context-class.md)を参照してください。

### <a name="return-value"></a>戻り値

新しく作成された継続タスク。 返されるタスクの結果の型は、`_Func` が返す値によって決まります。

### <a name="remarks"></a>解説

`then`そのオーバーロードは、Windows::Foundation::IAsyncInfo インターフェイスを返すラムダまたはファンクタを受け取り、Windows ランタイム アプリでのみ使用できます。

タスク継続を使用して非同期作業を作成する方法の詳細については、「[タスクの並列処理](../../../parallel/concrt/task-parallelism-concurrency-runtime.md)」を参照してください。

## <a name="wait"></a><a name="wait"></a>待つ

このタスクが終了状態になるまで待機します。 タスクの依存関係すべてが満たされ、バックグラウンド ワーカーによって実行用にまだ検出されていない場合、`wait` はタスクをインラインで実行できます。

```cpp
task_status wait() const;
```

### <a name="return-value"></a>戻り値

`task_status` の値。`completed` または `canceled` に設定される可能性があります。 タスクの実行時に例外が発生したり、継続元タスクからこのタスクに例外が反映された場合、`wait` はその例外をスローします。

### <a name="remarks"></a>解説

> [!IMPORTANT]
> ユニバーサル Windows プラットフォーム (UWP) アプリでは、`wait`ユーザー インターフェイス スレッドで実行されるコードを呼び出しません。 そうしないと、このメソッドが現在のスレッドをブロックして、アプリケーションが応答しなくなる場合があるため、ランタイムは [concurrency::invalid_operation](invalid-operation-class.md) をスローします。 ただし、タスク ベースの継続で継続元タスクの結果を受け取るために [concurrency::task::get](#get) のメソッドを呼び出すことができます。

## <a name="see-also"></a>関連項目

[同時実行名前空間](concurrency-namespace.md)
