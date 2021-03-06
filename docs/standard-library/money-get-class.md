---
title: money_get クラス
ms.date: 11/04/2016
f1_keywords:
- xlocmon/std::money_get
- xlocmon/std::money_get::char_type
- xlocmon/std::money_get::iter_type
- xlocmon/std::money_get::string_type
- xlocmon/std::money_get::do_get
- xlocmon/std::money_get::get
helpviewer_keywords:
- std::money_get [C++]
- std::money_get [C++], char_type
- std::money_get [C++], iter_type
- std::money_get [C++], string_type
- std::money_get [C++], do_get
- std::money_get [C++], get
ms.assetid: 692d3374-3fe7-4b46-8aeb-f8d91ed66b2e
ms.openlocfilehash: ac85e99bfb834fd970a804269f25ec9f20960a23
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81375911"
---
# <a name="money_get-class"></a>money_get クラス

クラス テンプレートは、型`CharType`のシーケンスから通貨値への変換を制御するロケール ファセットとして機能するオブジェクトを表します。

## <a name="syntax"></a>構文

```cpp
template <class CharType, class InputIterator = istreambuf_iterator<CharType>>
class money_get : public locale::facet;
```

### <a name="parameters"></a>パラメーター

*Chartype*\
ロケールの文字をエンコードするためにプログラム内で使用される型。

*入力反復器*\
get 関数が入力を読み取る反復子の型。

## <a name="remarks"></a>解説

すべてのロケールのファセットと同様、静的オブジェクト ID に最初に格納されている値は 0 です。 格納されている値に初めてアクセスしようとすると、**id** に一意の正の値が格納されます。

### <a name="constructors"></a>コンストラクター

|Constructor|説明|
|-|-|
|[money_get](#money_get)|通貨値を表すシーケンスから数値を抽出するために使用される `money_get` 型のオブジェクトのコンストラクター。|

### <a name="typedefs"></a>Typedefs

|種類の名前。|説明|
|-|-|
|[char_type](#char_type)|ロケールによって使用される文字を表すために使用される型。|
|[iter_type](#iter_type)|入力反復子を表す型。|
|[string_type](#string_type)|`CharType` 型の文字を格納する文字列を表す型。|

### <a name="member-functions"></a>メンバー関数

|メンバー関数|説明|
|-|-|
|[do_get](#do_get)|通貨値を表す文字シーケンスから数値を抽出するために呼び出される仮想関数。|
|[get](#get)|通貨値を表す文字シーケンスから数値を抽出します。|

## <a name="requirements"></a>必要条件

**ヘッダー:** \<locale>

**名前空間:** std

## <a name="money_getchar_type"></a><a name="char_type"></a>money_get::char_type

ロケールによって使用される文字を表すために使用される型。

```cpp
typedef CharType char_type;
```

### <a name="remarks"></a>解説

この型は、テンプレート パラメーター *CharType* のシノニムです。

## <a name="money_getdo_get"></a><a name="do_get"></a>money_get::do_get

通貨値を表す文字シーケンスから数値を抽出するために呼び出される仮想関数。

```cpp
virtual iter_type do_get(iter_type first,
    iter_type last,
    bool Intl,
    ios_base& Iosbase,
    ios_base::iostate& State,
    long double& val) const virtual iter_type do_get(iter_type first,
    iter_type last,
    bool Intl,
    ios_base& Iosbase,
    ios_base::iostate& State,
    string_type& val) const
```

### <a name="parameters"></a>パラメーター

*まずは*\
変換されるシーケンスの開始位置を示す入力反復子。

*前の*\
変換されるシーケンスの終了位置を示す入力反復子。

*国際 空港*\
シーケンスで期待される通貨記号の種類を示すブール値。国際通貨の場合は **true**、国内通貨の場合は **false**。

*イオスベース*\
書式設定フラグ。これが設定されている場合、通貨記号は省略可能です。それ以外の場合は必須です。

*状態*\
操作が成功したか失敗したかに基づいて、ストリームの状態に適したビットマスク要素を設定します。

*ヴァル*\
変換後のシーケンスを格納する文字列。

### <a name="return-value"></a>戻り値

通貨入力フィールドを超える先頭の要素を示す入力反復子。

### <a name="remarks"></a>解説

1 番目のプロテクト仮想メンバー関数は、シーケンス [ `first`, `last`) の先頭から始め、空でない完全な通貨入力フィールドを認識するまで、連続した要素との一致を試みます。 成功した場合、このフィールドは、1 つまたは複数の 10 進数のシーケンスに変換され、オプションで負`-`符号 ( ) が付き、その量を表す値が[string_type](#string_type)オブジェクト*val*に格納されます。 そして、通貨入力フィールドを超える先頭の要素を指す反復子を返します。 それ以外の場合、関数は空の*val*シーケンスを`ios_base::failbit`val に格納し、設定を*State*に格納します。 そして、有効な通貨入力フィールドのプレフィックスを超える先頭の要素を指す反復子を返します。 いずれの場合も、戻り値が `last` と等しい場合、関数は `State` に `ios_base::eofbit` を設定します。

2 番目の仮想プロテクト メンバー関数は、最初の関数と同じ動作をしますが、成功した場合はオプションで符号付きの数字シーケンスを**long double**型の値に変換し、その値を*val*に格納します。

通貨入力フィールドの形式は[、moneypunct](../standard-library/moneypunct-class.md) \< **CharType** **、intl**>>( **iosbase**) [use_facet](../standard-library/locale-functions.md#use_facet) < 有効な呼び出しによって返される[ロケールファセット](../standard-library/locale-class.md#facet_class)**fac**によって決定されます。 [ゲロック](../standard-library/ios-base-class.md#getloc)ス)。

具体的な内容は次のとおりです。

- **ファク**. [neg_format](../standard-library/moneypunct-class.md#neg_format)フィールドのコンポーネントが出現する順序を決定します。

- **ファク**. [curr_symbol](../standard-library/moneypunct-class.md#curr_symbol)通貨記号を構成する要素の順序を決定します。

- **ファク**. [positive_sign](../standard-library/moneypunct-class.md#positive_sign)は、正の符号を構成する要素のシーケンスを決定します。

- **ファク**. [negative_sign](../standard-library/moneypunct-class.md#negative_sign)は、負の符号を構成する要素のシーケンスを決定します。

- **ファク**. [グループ化](../standard-library/moneypunct-class.md#grouping)によって、小数点の左側に桁をグループ化する方法が決まります。

- **ファク**. [thousands_sep](../standard-library/moneypunct-class.md#thousands_sep)小数点の左側にある数字のグループを区切る要素を決定します。

- **ファク**. [decimal_point](../standard-library/moneypunct-class.md#decimal_point)は、整数の桁数と小数の数字を区切る要素を決定します。

- **ファク**. [frac_digits](../standard-library/moneypunct-class.md#frac_digits)小数点の右側の有効小数部桁数を決定します。 `frac_digits` によって要求される小数桁数を上回る桁数の値を解析する場合、`do_get` は最大で `frac_digits` 文字を処理した後、解析を停止します。

符号文字列 ( **fac**. `negative_sign`または**fac**. `positive_sign`) には複数の要素があり、最初の要素だけが一致し **、money_base::sign**に等しい要素がフォーマット パターン ( **fac**. `neg_format`). 残りの要素は、通貨入力フィールドの末尾で一致します。 いずれの文字列も通貨入力フィールド内の先頭の要素が次の要素と一致していない場合、符号文字列は空と見なされ、符号は正になります。

**iosbase の**場合 . [フラグ](../standard-library/ios-base-class.md#flags) & [showbase](../standard-library/ios-functions.md#showbase)は 0 以外の文字列**です**。 `curr_symbol`**money_base::symbol**に等しい要素が書式パターンで現れる場所と一致する必要があります。 このようにしないと、書式パターンの末尾に **money_base::symbol** が出現する場合、および一致せずに残っている符号文字列の要素がない場合に、通貨記号は一致しません。 それ以外の場合は、必要に応じて通貨記号が一致します。

**fac**のインスタンスがない場合。 `thousands_sep`通貨入力フィールドの値部分 **(money_base::value**に等しい要素が書式パターンに表示される) で発生し、グループ化制約は課されません。 それ以外の場合は **、fac**によって課されるグループ化制約。 **グループ化**が強制されます。 結果の数字のシーケンスは、下位**の fac**を持つ整数を表します。 `frac_digits`小数点の右側に 10 進数が考慮されます。

任意の余白は、書式パターンの末尾以外に出現する場合、**money_base::space** と等しい要素が書式パターンに出現しているときに一致します。 それ以外の場合、内部の余白は一致しません。 要素*ch*は[、ctype](../standard-library/ctype-class.md) \< **CharType**> >( **iosbase**) [use_facet](../standard-library/locale-functions.md#use_facet) < 場合は空白と見なされます。 [ゲロック](../standard-library/ios-base-class.md#getloc)ス)。 [は](../standard-library/ctype-class.md#is)、 **( ctype_base::スペース**、 *ch*) が**true です**。

### <a name="example"></a>例

[get](#get) の例 (`do_get` を呼び出す) を参照してください。

## <a name="money_getget"></a><a name="get"></a>money_get::取得

通貨値を表す文字シーケンスから数値を抽出します。

```cpp
iter_type get(iter_type first,
    iter_type last,
    bool Intl,
    ios_base& Iosbase,
    ios_base::iostate& State,
    long double& val) const;

iter_type get(iter_type first,
    iter_type last,
    bool Intl,
    ios_base& Iosbase,
    ios_base::iostate& State,
    string_type& val) const;
```

### <a name="parameters"></a>パラメーター

*まずは*\
変換されるシーケンスの開始位置を示す入力反復子。

*前の*\
変換されるシーケンスの終了位置を示す入力反復子。

*国際 空港*\
シーケンスで期待される通貨記号の種類を示すブール値。国際通貨の場合は **true**、国内通貨の場合は **false**。

*イオスベース*\
書式設定フラグ。これが設定されている場合、通貨記号は省略可能です。それ以外の場合は必須です

*状態*\
操作が成功したかどうかに基づき、ストリームの状態に適したビットマスク要素を設定します。

*ヴァル*\
変換後のシーケンスを格納する文字列。

### <a name="return-value"></a>戻り値

通貨入力フィールドを超える先頭の要素を示す入力反復子。

### <a name="remarks"></a>解説

両方のメンバー関数[は do_get](#do_get)`(first, last, Intl, Iosbase, State, val)`を返します。

### <a name="example"></a>例

```cpp
// money_get_get.cpp
// compile with: /EHsc
#include <locale>
#include <iostream>
#include <sstream>
using namespace std;

int main( )
{
   locale loc( "german_germany" );

   basic_stringstream< char > psz;
   psz << use_facet<moneypunct<char, 1> >(loc).curr_symbol() << "-1.000,56";
   basic_stringstream< char > psz2;
   psz2 << "-100056" << use_facet<moneypunct<char, 1> >(loc).curr_symbol();

   ios_base::iostate st = 0;
   long double fVal;

   psz.flags( psz.flags( )|ios_base::showbase );
   // Which forced the READING the currency symbol
   psz.imbue(loc);
   use_facet < money_get < char > >( loc ).
      get( basic_istream<char>::_Iter( psz.rdbuf( ) ),
           basic_istream<char>::_Iter( 0 ), true, psz, st, fVal );

   if ( st & ios_base::failbit )
      cout << "money_get(" << psz.str( ) << ", intl = 1) FAILED"
           << endl;
   else
      cout << "money_get(" << psz.str( ) << ", intl = 1) = "
           << fVal/100.0 << endl;

   use_facet < money_get < char > >( loc ).
      get(basic_istream<char>::_Iter(psz2.rdbuf( )),
          basic_istream<char>::_Iter(0), false, psz2, st, fVal);

   if ( st & ios_base::failbit )
      cout << "money_get(" << psz2.str( ) << ", intl = 0) FAILED"
           << endl;
   else
      cout << "money_get(" << psz2.str( ) << ", intl = 0) = "
           << fVal/100.0 << endl;
};
```

## <a name="money_getiter_type"></a><a name="iter_type"></a>money_get::iter_type

入力反復子を表す型。

```cpp
typedef InputIterator iter_type;
```

### <a name="remarks"></a>解説

この型は、テンプレート パラメーター **InputIterator** のシノニムです。

## <a name="money_getmoney_get"></a><a name="money_get"></a>money_get::money_get

通貨値を表すシーケンスから数値を抽出するために使用される `money_get` 型のオブジェクトのコンストラクター。

```cpp
explicit money_get(size_t _Refs = 0);
```

### <a name="parameters"></a>パラメーター

*_Refs*\
オブジェクトのメモリ管理の種類を指定するために使用する整数値。

### <a name="remarks"></a>解説

*_Refs*パラメータとその有意性の値は次のとおりです。

- 0: オブジェクトの有効期間はそれが含まれるロケールによって管理されます。

- 1: オブジェクトの有効期間を手動で管理する必要があります。

- \>1: これらの値は定義されていません。

デストラクターが保護されているため、利用できる直接的な例はありません。

コンストラクターは、基本オブジェクトを**locale: ファ**[セット](../standard-library/locale-class.md#facet_class)(*_Refs*) で初期化します。

## <a name="money_getstring_type"></a><a name="string_type"></a>money_get::string_type

**CharType** 型の文字を格納する文字列を表す型。

```cpp
typedef basic_string<CharType, Traits, Allocator> string_type;
```

### <a name="remarks"></a>解説

この型は、クラス テンプレート basic_string の特殊化[を](../standard-library/basic-string-class.md)表します。

## <a name="see-also"></a>関連項目

[\<ロケール>](../standard-library/locale.md)\
[ファセットクラス](../standard-library/locale-class.md#facet_class)\
[C++ 標準ライブラリ内のスレッド セーフ](../standard-library/thread-safety-in-the-cpp-standard-library.md)
