---
title: numpunct クラス
ms.date: 11/04/2016
f1_keywords:
- xlocnum/std::numpunct
- xlocnum/std::numpunct::char_type
- xlocnum/std::numpunct::string_type
- xlocnum/std::numpunct::decimal_point
- xlocnum/std::numpunct::do_decimal_point
- xlocnum/std::numpunct::do_falsename
- xlocnum/std::numpunct::do_grouping
- xlocnum/std::numpunct::do_thousands_sep
- xlocnum/std::numpunct::do_truename
- xlocnum/std::numpunct::falsename
- xlocnum/std::numpunct::grouping
- xlocnum/std::numpunct::thousands_sep
- xlocnum/std::numpunct::truename
helpviewer_keywords:
- std::numpunct [C++]
- std::numpunct [C++], char_type
- std::numpunct [C++], string_type
- std::numpunct [C++], decimal_point
- std::numpunct [C++], do_decimal_point
- std::numpunct [C++], do_falsename
- std::numpunct [C++], do_grouping
- std::numpunct [C++], do_thousands_sep
- std::numpunct [C++], do_truename
- std::numpunct [C++], falsename
- std::numpunct [C++], grouping
- std::numpunct [C++], thousands_sep
- std::numpunct [C++], truename
ms.assetid: 73fb93cc-ac11-4c98-987c-bfa6267df596
ms.openlocfilehash: 0bdd6556df892e5e231919dbc4ae95d14a6f95fe
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81373616"
---
# <a name="numpunct-class"></a>numpunct クラス

数値式とブール式の書式設定と句読点に関する情報を表すために使用される型`CharType`のシーケンスを記述する、ローカル ファセットとして機能するオブジェクトを記述するクラス テンプレート。

## <a name="syntax"></a>構文

```cpp
template <class CharType>
class numpunct : public locale::facet;
```

### <a name="parameters"></a>パラメーター

*Chartype*\
ロケールの文字をエンコードするためにプログラム内で使用される型。

## <a name="remarks"></a>解説

すべてのロケールのファセットと同様、静的オブジェクト ID に最初に格納されている値は 0 です。 格納されている値に初めてアクセスしようとすると、**id** に一意の正の値が格納されます。

### <a name="constructors"></a>コンストラクター

|Constructor|説明|
|-|-|
|[numpunct](#numpunct)|`numpunct` 型のオブジェクトのコンストラクター。|

### <a name="typedefs"></a>Typedefs

|種類の名前。|説明|
|-|-|
|[char_type](#char_type)|ロケールによって使用される文字を表すために使用される型。|
|[string_type](#string_type)|`CharType` 型の文字を格納する文字列を表す型。|

### <a name="member-functions"></a>メンバー関数

|メンバー関数|説明|
|-|-|
|[decimal_point](#decimal_point)|小数点として使用するロケール固有の要素を返します。|
|[do_decimal_point](#do_decimal_point)|小数点として使用するロケール固有の要素を返すために呼び出されるプロテクト仮想メンバー関数。|
|[do_falsename](#do_falsename)|値**false**のテキスト表現として使用する文字列を返すために呼び出されるプロテクト仮想メンバー関数。|
|[do_grouping](#do_grouping)|小数点の左側の数字をグループ化する方法を決定するロケール固有の規則を返すために呼び出されるプロテクト仮想メンバー関数。|
|[do_thousands_sep](#do_thousands_sep)|桁区切り記号として使用するロケール固有の要素を返すために呼び出されるプロテクト仮想メンバー関数。|
|[do_truename](#do_truename)|**true** 値のテキスト表現として使用する文字列を返すために呼び出されるプロテクト仮想メンバー関数。|
|[falsename](#falsename)|**false** 値のテキスト表現として使用する文字列を返します。|
|[グループ](#grouping)|小数点の左側の数字をグループ化する方法を決定するロケール固有の規則を返します。|
|[thousands_sep](#thousands_sep)|桁区切り記号として使用するロケール固有の要素を返します。|
|[truename](#truename)|**true** 値のテキスト表現として使用する文字列を返します。|

## <a name="requirements"></a>必要条件

**ヘッダー:** \<locale>

**名前空間:** std

## <a name="numpunctchar_type"></a><a name="char_type"></a>numpunct::char_type

ロケールによって使用される文字を表すために使用される型。

```cpp
typedef CharType char_type;
```

### <a name="remarks"></a>解説

この型は、テンプレート パラメーター CharType のシノニム**です。**

## <a name="numpunctdecimal_point"></a><a name="decimal_point"></a>numpunct::decimal_point

小数点として使用するロケール固有の要素を返します。

```cpp
CharType decimal_point() const;
```

### <a name="return-value"></a>戻り値

小数点として使用するロケール固有の要素。

### <a name="remarks"></a>解説

このメンバー関数は、[do_decimal_point](#do_decimal_point) を返します。

### <a name="example"></a>例

```cpp
// numpunct_decimal_point.cpp
// compile with: /EHsc
#include <locale>
#include <iostream>
#include <sstream>
using namespace std;
int main( )
{
   locale loc( "german_germany" );

   const numpunct <char> &npunct =
   use_facet <numpunct <char> >( loc);
   cout << loc.name( ) << " decimal point "<<
   npunct.decimal_point( ) << endl;
   cout << loc.name( ) << " thousands separator "
   << npunct.thousands_sep( ) << endl;
};
```

```Output
German_Germany.1252 decimal point ,
German_Germany.1252 thousands separator .
```

## <a name="numpunctdo_decimal_point"></a><a name="do_decimal_point"></a>numpunct::do_小数点

小数点として使用するロケール固有の要素を返すために呼び出されるプロテクト仮想メンバー関数。

```cpp
virtual CharType do_decimal_point() const;
```

### <a name="return-value"></a>戻り値

小数点として使用するロケール固有の要素。

### <a name="example"></a>例

[decimal_point](#decimal_point) の例 (仮想メンバー関数が `decimal_point` で呼び出される) を参照してください。

## <a name="numpunctdo_falsename"></a><a name="do_falsename"></a>numpunct::do_falsename

このプロテクト仮想メンバー関数は、**false** 値のテキスト表現として使用するシーケンスを返します。

```cpp
virtual string_type do_falsename() const;
```

### <a name="return-value"></a>戻り値

**false** 値のテキスト表現として使用するシーケンスを含む文字列。

### <a name="remarks"></a>解説

このメンバー関数は、すべてのロケールで **false** 値を表す文字列 "false" を返します。

### <a name="example"></a>例

[falsename](#falsename) の例 (仮想メンバー関数が `falsename` で呼び出される) をご覧ください。

## <a name="numpunctdo_grouping"></a><a name="do_grouping"></a>numpunct::do_grouping

小数点の左側の数字をグループ化する方法を決定するロケール固有の規則を返すために呼び出されるプロテクト仮想メンバー関数。

```cpp
virtual string do_grouping() const;
```

### <a name="return-value"></a>戻り値

小数点の左側の数字をグループ化する方法を決定するロケール固有の規則。

### <a name="remarks"></a>解説

このプロテクト仮想メンバー関数は、小数点の左側の数字をグループ化する方法を決定するロケール固有の規則を返します。 エンコーディングは **lconv::grouping** の場合と同じです。

### <a name="example"></a>例

仮想メンバー関数が[grouping](#grouping)によって`grouping`呼び出される grouping の例を参照してください。

## <a name="numpunctdo_thousands_sep"></a><a name="do_thousands_sep"></a>numpunct::do_千_9月

桁区切り記号として使用するロケール固有の要素を返すために呼び出されるプロテクト仮想メンバー関数。

```cpp
virtual CharType do_thousands_sep() const;
```

### <a name="return-value"></a>戻り値

桁区切り記号として使用するロケール固有の要素を返します。

### <a name="remarks"></a>解説

プロテクト仮想メンバー関数は、小数点の左側にグループ区切`CharType`り記号として使用する、ロケール固有の型の要素を返します。

### <a name="example"></a>例

[thousands_sep](#thousands_sep) の例 (仮想メンバー関数が `thousands_sep` で呼び出される) を参照してください。

## <a name="numpunctdo_truename"></a><a name="do_truename"></a>numpunct::do_truename

**true** 値のテキスト表現として使用する文字列を返すために呼び出されるプロテクト仮想メンバー関数。

```cpp
virtual string_type do_truename() const;
```

### <a name="remarks"></a>解説

**true** 値のテキスト表現として使用する文字列。

すべてのロケールは、**true** 値を表す文字列 "true" を返します。

### <a name="example"></a>例

[truename](#truename) の例 (仮想メンバー関数が `truename` で呼び出される) をご覧ください。

## <a name="numpunctfalsename"></a><a name="falsename"></a>numpunct::偽名

**false** 値のテキスト表現として使用する文字列を返します。

```cpp
string_type falsename() const;
```

### <a name="return-value"></a>戻り値

値 false のテキスト`CharType`表現として使用する s のシーケンスを**false**含む文字列。

### <a name="remarks"></a>解説

このメンバー関数は、すべてのロケールで **false** 値を表す文字列 "false" を返します。

このメンバー関数は、[do_falsename](#do_falsename) を返します。

### <a name="example"></a>例

```cpp
// numpunct_falsename.cpp
// compile with: /EHsc
#include <locale>
#include <iostream>
#include <sstream>
using namespace std;
int main( )
{
   locale loc( "English" );

   const numpunct <char> &npunct = use_facet <numpunct <char> >( loc );
   cout << loc.name( ) << " truename "<< npunct.truename( ) << endl;
   cout << loc.name( ) << " falsename "<< npunct.falsename( ) << endl;

   locale loc2( "French" );
   const numpunct <char> &npunct2 = use_facet <numpunct <char> >(loc2);
   cout << loc2.name( ) << " truename "<< npunct2.truename( ) << endl;
   cout << loc2.name( ) << " falsename "<< npunct2.falsename( ) << endl;
}
```

```Output
English_United States.1252 truename true
English_United States.1252 falsename false
French_France.1252 truename true
French_France.1252 falsename false
```

## <a name="numpunctgrouping"></a><a name="grouping"></a>numpunct::グループ化

小数点の左側の数字をグループ化する方法を決定するロケール固有の規則を返します。

```cpp
string grouping() const;
```

### <a name="return-value"></a>戻り値

小数点の左側の数字をグループ化する方法を決定するロケール固有の規則。

### <a name="remarks"></a>解説

このメンバー関数は、[do_grouping](#do_grouping) を返します。

### <a name="example"></a>例

```cpp
// numpunct_grouping.cpp
// compile with: /EHsc
#include <locale>
#include <iostream>
#include <sstream>
using namespace std;
int main( )
{
   locale loc( "german_germany");

   const numpunct <char> &npunct =
       use_facet < numpunct <char> >( loc );
   for (unsigned int i = 0; i < npunct.grouping( ).length( ); i++)
   {
      cout << loc.name( ) << " international grouping:\n the "
           << i <<"th group to the left of the radix character "
           << "is of size " << (int)(npunct.grouping ( )[i])
           << endl;
   }
}
```

```Output
German_Germany.1252 international grouping:
the 0th group to the left of the radix character is of size 3
```

## <a name="numpunctnumpunct"></a><a name="numpunct"></a>数字::数字

`numpunct` 型のオブジェクトのコンストラクター。

```cpp
explicit numpunct(size_t _Refs = 0);
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

コンストラクターは、基本オブジェクトを**locale: ファ**[セット](../standard-library/locale-class.md#facet_class)(`_Refs`) で初期化します。

## <a name="numpunctstring_type"></a><a name="string_type"></a>数字::string_type

**CharType** 型の文字を格納する文字列を表す型。

```cpp
typedef basic_string<CharType, Traits, Allocator> string_type;
```

### <a name="remarks"></a>解説

この型は、句読点シーケンスのコピーを格納できるオブジェクトを持つクラス テンプレート[basic_string](../standard-library/basic-string-class.md)の特殊化を表します。

## <a name="numpunctthousands_sep"></a><a name="thousands_sep"></a>numpunct::thousands_sep

桁区切り記号として使用するロケール固有の要素を返します。

```cpp
CharType thousands_sep() const;
```

### <a name="return-value"></a>戻り値

桁区切り記号として使用するロケール固有の要素。

### <a name="remarks"></a>解説

このメンバー関数は、[do_thousands_sep](#do_thousands_sep) を返します。

### <a name="example"></a>例

```cpp
// numpunct_thou_sep.cpp
// compile with: /EHsc
#include <locale>
#include <iostream>
#include <sstream>
using namespace std;
int main( )
{
   locale loc( "german_germany" );

   const numpunct <char> &npunct =
   use_facet < numpunct < char > >( loc );
   cout << loc.name( ) << " decimal point "<<
   npunct.decimal_point( ) << endl;
   cout << loc.name( ) << " thousands separator "
   << npunct.thousands_sep( ) << endl;
};
```

```Output
German_Germany.1252 decimal point ,
German_Germany.1252 thousands separator .
```

## <a name="numpuncttruename"></a><a name="truename"></a>numpunct::真の名前

**true** 値のテキスト表現として使用する文字列を返します。

```cpp
string_type falsename() const;
```

### <a name="return-value"></a>戻り値

**true** 値のテキスト表現として使用する文字列。

### <a name="remarks"></a>解説

このメンバー関数は、[do_truename](#do_truename) を返します。

すべてのロケールは、**true** 値を表す文字列 "true" を返します。

### <a name="example"></a>例

```cpp
// numpunct_truename.cpp
// compile with: /EHsc
#include <locale>
#include <iostream>
#include <sstream>
using namespace std;
int main( )
{
   locale loc( "English" );

   const numpunct < char> &npunct = use_facet <numpunct <char> >( loc );
   cout << loc.name( ) << " truename "<< npunct.truename( ) << endl;
   cout << loc.name( ) << " falsename "<< npunct.falsename( ) << endl;

   locale loc2("French");
   const numpunct <char> &npunct2 = use_facet <numpunct <char> >( loc2 );
   cout << loc2.name( ) << " truename "<< npunct2.truename( ) << endl;
   cout << loc2.name( ) << " falsename "<< npunct2.falsename( ) << endl;
}
```

```Output
English_United States.1252 truename true
English_United States.1252 falsename false
French_France.1252 truename true
French_France.1252 falsename false
```

## <a name="see-also"></a>関連項目

[\<ロケール>](../standard-library/locale.md)\
[ファセットクラス](../standard-library/locale-class.md#facet_class)\
[C++ 標準ライブラリ内のスレッド セーフ](../standard-library/thread-safety-in-the-cpp-standard-library.md)
