---
title: __identifier (C++/CLI)
ms.date: 10/12/2018
ms.topic: reference
f1_keywords:
- __identifier
- __identifier_cpp
helpviewer_keywords:
- __identifier keyword [C++]
ms.assetid: 348428af-afa7-4ff3-b571-acf874301cf2
ms.openlocfilehash: 0da32aae9a8c2c7f21ee9576e1e1147822314a36
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80172179"
---
# <a name="__identifier-ccli"></a>__identifier (C++/CLI)

C++ キーワードを識別子として使用できるようにします。

## <a name="all-platforms"></a>すべてのプラットフォーム

### <a name="syntax"></a>構文

```cpp
__identifier(C++_keyword)
```

### <a name="remarks"></a>解説

キーワードではない識別子での **__identifier** キーワードの使用は許可されていますが、スタイルの問題として、極力回避することをお勧めします。

## <a name="windows-runtime"></a>Windows ランタイム

### <a name="requirements"></a>必要条件

コンパイラ オプション: `/ZW`

### <a name="examples"></a>例

**例**

次の例では、C# で **template** という名前のクラスが作成され、DLL として配布されます。 **template** クラスを使用する C++/CLI プログラムでは、 **__identifier** キーワードは **template** が標準 C++ のキーワードであるという事実が隠されます。

```csharp
// identifier_template.cs
// compile with: /target:library
public class template {
   public void Run() { }
}
```

```cpp
// keyword__identifier.cpp
// compile with: /ZW
#using <identifier_template.dll>
int main() {
   __identifier(template)^ pTemplate = ref new __identifier(template)();
   pTemplate->Run();
}
```

## <a name="common-language-runtime"></a>共通言語ランタイム

### <a name="remarks"></a>解説

**__identifier** キーワードは、`/clr` コンパイラ オプションで有効です。

### <a name="requirements"></a>必要条件

コンパイラ オプション: `/clr`

### <a name="examples"></a>例

次の例では、C# で **template** という名前のクラスが作成され、DLL として配布されます。 **template** クラスを使用する C++/CLI プログラムでは、 **__identifier** キーワードは **template** が標準 C++ のキーワードであるという事実が隠されます。

```csharp
// identifier_template.cs
// compile with: /target:library
public class template {
   public void Run() { }
}
```

```cpp
// keyword__identifier.cpp
// compile with: /clr
#using <identifier_template.dll>

int main() {
   __identifier(template) ^pTemplate = gcnew __identifier(template)();
   pTemplate->Run();
}
```

## <a name="see-also"></a>参照

[.NET および UWP でのコンポーネント拡張](component-extensions-for-runtime-platforms.md)<br/>
[.NET および UWP でのコンポーネント拡張](component-extensions-for-runtime-platforms.md)
