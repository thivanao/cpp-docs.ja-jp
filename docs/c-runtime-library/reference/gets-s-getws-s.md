---
title: gets_s、_getws_s
ms.date: 4/2/2020
api_name:
- _getws_s
- gets_s
- _o__getws_s
- _o_gets_s
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
- api-ms-win-crt-stdio-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _getws_s
- gets_s
helpviewer_keywords:
- getws_s function
- _getws_s function
- lines, getting
- streams, getting lines
- buffers, avoiding overruns
- buffer overruns
- buffers, buffer overruns
- gets_s function
- standard input, reading from
ms.assetid: 5880c36f-122c-4061-a1a5-aeeced6fe58c
ms.openlocfilehash: b01456d3ed37c34dbc10980ebdfbe008e27f624a
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82913612"
---
# <a name="gets_s-_getws_s"></a>gets_s、_getws_s

**Stdin**ストリームから行を取得します。 これらの [gets および _getws](../../c-runtime-library/gets-getws.md) のバージョンは、「[Security Features in the CRT](../../c-runtime-library/security-features-in-the-crt.md)」(CRT のセキュリティ機能) で説明されているように、セキュリティが強化されています。

## <a name="syntax"></a>構文

```C
char *gets_s(
   char *buffer,
   size_t sizeInCharacters
);
wchar_t *_getws_s(
   wchar_t *buffer,
   size_t sizeInCharacters
);
```

```cpp
template <size_t size>
char *gets_s( char (&buffer)[size] ); // C++ only

template <size_t size>
wchar_t *_getws_s( wchar_t (&buffer)[size] ); // C++ only
```

### <a name="parameters"></a>パラメーター

*格納*<br/>
入力文字列の格納場所。

*sizeInCharacters*<br/>
バッファーのサイズ。

## <a name="return-value"></a>戻り値

成功した場合は、*バッファー*を返します。 エラーが発生した場合またはファイルの終端に達した場合は、**NULL** ポインターを返します。 どちらが発生したかを確認するには、 [ferror](ferror.md) または [feof](feof.md) を使用します。

## <a name="remarks"></a>解説

**Gets_s**関数は、標準入力ストリーム**stdin**から行を読み取り、*バッファー*に格納します。 行は、最初の改行文字 ('\n') までのすべての文字 (改行文字を含む) で構成されます。 次に、行を返す前に、改行文字を null 文字 (' \ 0 ') で置換**gets_s**ます。 これに対し、 **fgets_s**関数は改行文字を保持します。

最初に読み取られた文字がファイルの終端文字である場合は、null 文字が*バッファー*の先頭に格納され、 **null**が返されます。

**_getws_s**は**gets_s**のワイド文字バージョンです。引数と戻り値はワイド文字列です。

*Buffer*が**NULL**の場合、または*sizeincharacters*が0以下の場合、またはバッファーが小さすぎて入力行と NULL ターミネータを格納できない場合、「[パラメーターの検証](../../c-runtime-library/parameter-validation.md)」で説明されているように、これらの関数は無効なパラメーターハンドラーを呼び出します。 実行の継続が許可された場合、これらの関数は**NULL**を返し、Errno を**ERANGE**に設定します。

C++ では、これらの関数の使用はテンプレートのオーバーロードによって簡素化されます。オーバーロードでは、バッファー長を自動的に推論できる (サイズの引数を指定する必要がなくなる) だけでなく、古くてセキュリティが万全ではない関数を新しく安全な関数に自動的に置き換えることができます。 詳細については、「[セキュリティ保護されたテンプレート オーバーロード](../../c-runtime-library/secure-template-overloads.md)」を参照してください。

既定では、この関数のグローバル状態はアプリケーションにスコープが設定されています。 これを変更するには、「 [CRT でのグローバル状態](../global-state.md)」を参照してください。

### <a name="generic-text-routine-mappings"></a>汎用テキスト ルーチンのマップ

|TCHAR.H のルーチン|_UNICODE および _MBCS が未定義の場合|_MBCS が定義されている場合|_UNICODE が定義されている場合|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_getts_s**|**gets_s**|**gets_s**|**_getws_s**|

## <a name="requirements"></a>必要条件

|ルーチン|必須ヘッダー|
|-------------|---------------------|
|**gets_s**|\<stdio.h>|
|**_getws_s**|\<stdio.h> または \<wchar.h>|

コンソールは、ユニバーサル Windows プラットフォーム (UWP) アプリではサポートされていません。 コンソール、 **stdin**、 **stdout**、および**stderr**に関連付けられている標準ストリームハンドルは、C ランタイム関数が UWP アプリで使用できるようになる前にリダイレクトする必要があります。 互換性の詳細については、「[互換性](../../c-runtime-library/compatibility.md)」を参照してください。

## <a name="example"></a>例

```C
// crt_gets_s.c
// This program retrieves a string from the stdin and
// prints the same string to the console.

#include <stdio.h>

int main( void )
{
   char line[21]; // room for 20 chars + '\0'
   gets_s( line, 20 );
   printf( "The line entered was: %s\n", line );
}
```

```Input
Hello there!
```

```Output
The line entered was: Hello there!
```

## <a name="see-also"></a>関連項目

[ストリーム入出力](../../c-runtime-library/stream-i-o.md)<br/>
[を取得し、_getws します。](../../c-runtime-library/gets-getws.md)<br/>
[fgets、fgetws](fgets-fgetws.md)<br/>
[fputs、fputws](fputs-fputws.md)<br/>
[puts、_putws](puts-putws.md)<br/>
