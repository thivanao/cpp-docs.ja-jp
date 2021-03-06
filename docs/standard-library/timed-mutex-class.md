---
title: timed_mutex クラス
ms.date: 11/04/2016
f1_keywords:
- mutex/std::timed_mutex
- mutex/std::timed_mutex::timed_mutex
- mutex/std::timed_mutex::lock
- mutex/std::timed_mutex::try_lock
- mutex/std::timed_mutex::try_lock_for
- mutex/std::timed_mutex::try_lock_until
- mutex/std::timed_mutex::unlock
ms.assetid: cd198081-6f38-447a-9dba-e06dfbfafe59
helpviewer_keywords:
- std::timed_mutex [C++]
- std::timed_mutex [C++], timed_mutex
- std::timed_mutex [C++], lock
- std::timed_mutex [C++], try_lock
- std::timed_mutex [C++], try_lock_for
- std::timed_mutex [C++], try_lock_until
- std::timed_mutex [C++], unlock
ms.openlocfilehash: 6c9840d9b8c00d4b03e6ea329c7707a0edff9512
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81368014"
---
# <a name="timed_mutex-class"></a>timed_mutex クラス

*時間指定ミューテックス型*を表します。 この型のオブジェクトは、プログラム内での時間制限ブロックを使った相互排他を強制するのに使用されます。

## <a name="syntax"></a>構文

```cpp
class timed_mutex;
```

## <a name="members"></a>メンバー

### <a name="public-constructors"></a>パブリック コンストラクター

|名前|説明|
|----------|-----------------|
|[timed_mutex](#timed_mutex)|ロックされていない `timed_mutex` オブジェクトを構築します。|
|[timed_mutex:~timed_mutexデストラクタ](#dtortimed_mutex_destructor)|`timed_mutex` オブジェクトによって使用されるすべてのリソースを解放します。|

### <a name="public-methods"></a>パブリック メソッド

|名前|説明|
|----------|-----------------|
|[ロック](#lock)|呼び出しスレッドが `mutex` の所有権を取得するまでそのスレッドをブロックします。|
|[try_lock](#try_lock)|ブロックせずに `mutex` の所有権を取得しようとします。|
|[try_lock_for](#try_lock_for)|指定した時間のあいだ `mutex` の所有権の取得を試みます。|
|[try_lock_until](#try_lock_until)|指定した時刻まで `mutex` の所有権の取得を試みます。|
|[ロック 解除](#unlock)|`mutex` の所有権を解放します。|

## <a name="requirements"></a>必要条件

**ヘッダー:**\<ミューテックス>

**名前空間:** std

## <a name="timed_mutexlock"></a><a name="lock"></a>timed_mutex::ロック

呼び出しスレッドが `mutex` の所有権を取得するまでそのスレッドをブロックします。

```cpp
void lock();
```

### <a name="remarks"></a>解説

呼び出しスレッドが既に `mutex` を所有している場合の動作は未定義です。

## <a name="timed_mutextimed_mutex-constructor"></a><a name="timed_mutex"></a>timed_mutex::timed_mutexコンストラクタ

ロックされていない `timed_mutex` オブジェクトを構築します。

```cpp
timed_mutex();
```

## <a name="timed_mutextimed_mutex-destructor"></a><a name="dtortimed_mutex_destructor"></a>timed_mutex:~timed_mutexデストラクタ

`mutex` オブジェクトによって使用されるすべてのリソースを解放します。

```cpp
~timed_mutex();
```

### <a name="remarks"></a>解説

デストラクターの実行時にオブジェクトがロックされる場合の動作は未定義です。

## <a name="timed_mutextry_lock"></a><a name="try_lock"></a>timed_mutex::try_lock

ブロックせずに `mutex` の所有権を取得しようとします。

```cpp
bool try_lock();
```

### <a name="return-value"></a>戻り値

メソッドがの所有権を正常に取得する場合は`mutex` **true。** それ以外の場合**は false。**

### <a name="remarks"></a>解説

呼び出しスレッドが既に `mutex` を所有している場合の動作は未定義です。

## <a name="timed_mutextry_lock_for"></a><a name="try_lock_for"></a>timed_mutex::try_lock_for

ブロックせずに `mutex` の所有権を取得しようとします。

```cpp
template <class Rep, class Period>
bool try_lock_for(const chrono::duration<Rep, Period>& Rel_time);
```

### <a name="parameters"></a>パラメーター

*Rel_time*\
メソッドが `mutex` の所有権の取得を試行する時間について、その最大値を指定する [chrono::duration](../standard-library/duration-class.md) オブジェクト。

### <a name="return-value"></a>戻り値

メソッドがの所有権を正常に取得する場合は`mutex` **true。** それ以外の場合**は false。**

### <a name="remarks"></a>解説

呼び出しスレッドが既に `mutex` を所有している場合の動作は未定義です。

## <a name="timed_mutextry_lock_until"></a><a name="try_lock_until"></a>timed_mutex::try_lock_until

ブロックせずに `mutex` の所有権を取得しようとします。

```cpp
template <class Clock, class Duration>
bool try_lock_for(const chrono::time_point<Clock, Duration>& Abs_time);

bool try_lock_until(const xtime* Abs_time);
```

### <a name="parameters"></a>パラメーター

*Abs_time*\
メソッドが `mutex` の所有権の取得を止めるしきい値を指定する時点。

### <a name="return-value"></a>戻り値

メソッドがの所有権を正常に取得する場合は`mutex` **true。** それ以外の場合**は false。**

### <a name="remarks"></a>解説

呼び出しスレッドが既に `mutex` を所有している場合の動作は未定義です。

## <a name="timed_mutexunlock"></a><a name="unlock"></a>timed_mutex::ロック解除

`mutex` の所有権を解放します。

```cpp
void unlock();
```

### <a name="remarks"></a>解説

呼び出しスレッドが `mutex` を所有していない場合の動作は未定義です。

## <a name="see-also"></a>関連項目

[ヘッダー ファイル リファレンス](../standard-library/cpp-standard-library-header-files.md)\
[\<ミューテックス>](../standard-library/mutex.md)
