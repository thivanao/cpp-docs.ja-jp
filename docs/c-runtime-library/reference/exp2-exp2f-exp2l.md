---
title: exp2、exp2f、exp2l
ms.date: 4/2/2020
api_name:
- exp2
- exp2f
- exp2l
- _o_exp2
- _o_exp2f
- _o_exp2l
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-math-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- exp2
- math/exp2
- exp2f
- math/exp2f
- exp2l
- math/exp2l
helpviewer_keywords:
- exp2 function
- exp2f function
- exp2l function
ms.assetid: 526e3e10-201a-4610-a886-533f44ece344
ms.openlocfilehash: 3a80efab34b45348ca00f09b2fd6e2ea5077fd86
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82909631"
---
# <a name="exp2-exp2f-exp2l"></a>exp2、exp2f、exp2l

指定された値に2を計算します。

## <a name="syntax"></a>構文

```C
double exp2(
   double x
);

float exp2(
   float x
);  // C++ only

long double exp2(
   long double x
); // C++ only

float exp2f(
   float x
);

long double exp2l(
   long double x
);
```

### <a name="parameters"></a>パラメーター

*x*<br/>
指数部の値です。

## <a name="return-value"></a>戻り値

成功した場合は、 *x*の底2の指数、つまり 2<sup>x</sup>を返します。 それ以外の場合は、次のいずれかの値が返されます。

|問題|戻り値|
|-----------|------------|
|*x* = ±0|1|
|*x* =-無限大|+0|
|*x* = + 無限大|+INFINITY|
|*x* = NaN|(NaN)|
|オーバーフロー範囲エラー|+HUGE_VAL、+HUGE_VALF、または +HUGE_VALL|
|アンダーフロー範囲エラー|丸めた後の正しい結果|

エラーは、[_matherr](matherr.md) で指定されたとおりに報告されます。

## <a name="remarks"></a>解説

C++ ではオーバーロードが可能であるため、 **float**型および**long double**型を受け取って返す**exp2**のオーバーロードを呼び出すことができます。 C プログラムでは、 **exp2**は常に**double**を受け取り、返します。

既定では、この関数のグローバル状態はアプリケーションにスコープが設定されています。 これを変更するには、「 [CRT でのグローバル状態](../global-state.md)」を参照してください。

## <a name="requirements"></a>必要条件

|ルーチン|C ヘッダー|C++ ヘッダー|
|-------------|--------------|------------------|
|**exp**, **、** **expl**|\<math.h>|\<cmath>|

互換性の詳細については、「[互換性](../../c-runtime-library/compatibility.md)」を参照してください。

## <a name="see-also"></a>関連項目

[関数リファレンス (アルファベット順)](crt-alphabetical-function-reference.md)<br/>
[exp、expf、expl](exp-expf.md)<br/>
[log2、log2f、log2l](log2-log2f-log2l.md)<br/>
