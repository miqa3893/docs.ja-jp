---
title: インターフェイスのインデクサー (C# プログラミング ガイド)
ms.date: 07/20/2015
helpviewer_keywords:
- indexers [C#], in interfaces
- accessors [C#], indexers
ms.assetid: e16b54bd-4a83-4f52-bd75-65819fca79e8
ms.openlocfilehash: 120b6e72a6ab906437c593d6eb33024d1df8f52b
ms.sourcegitcommit: 6bc4efca63e526ce6f2d257fa870f01f8c459ae4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2018
ms.locfileid: "36207966"
---
# <a name="indexers-in-interfaces-c-programming-guide"></a>インターフェイスのインデクサー (C# プログラミング ガイド)
[interface](../../../csharp/language-reference/keywords/interface.md) でインデクサーを宣言することができます。 インターフェイスのインデクサーのアクセサーは、[クラス](../../../csharp/language-reference/keywords/class.md)のインデクサーのアクセサーと次の点で異なります。  
  
-   インターフェイスのアクセサーは、修飾子は使用しません。  
  
-   インターフェイスのアクセサーには、本文はありません。  
  
 したがって、アクセサーの目的は、インデクサーが読み取り/書き込み、読み取り専用、または書き込み専用のどれかを示すことです。  
  
 インターフェイスのインデクサー アクセサーの例を次に示します。  
  
 [!code-csharp[csProgGuideIndexers#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/indexers-in-interfaces_1.cs)]  
  
 インデクサーのシグネチャは、同じインターフェイスで宣言されている他のすべてのインデクサーの署名とは異なる必要があります。  
  
## <a name="example"></a>例  
 次の例では、インターフェイスのインデクサーを実装する方法について説明します。  
  
 [!code-csharp[csProgGuideIndexers#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/indexers-in-interfaces_2.cs)]  
  
 前の例では、インターフェイス メンバーの完全修飾名を使用して明示的なインターフェイス メンバーの実装を使用することができます。 例:  
  
```  
string ISomeInterface.this[int index]   
{   
}   
```  
  
 ただし、完全修飾名は、クラスが同じインデクサーの署名を持つ 2 つ以上のインターフェイスを実装するときにあいまいさを避けるためにのみ必要です。 たとえば、`Employee` クラスが 2 つのインターフェイス `ICitizen` と `IEmployee` を実装し、両方のインターフェイスが同じインデクサーの署名を持っている場合、明示的なインターフェイス メンバーの実装が必要です。 つまり、次のインデクサーの宣言があります。  
  
```  
string IEmployee.this[int index]   
{   
}   
```  
  
 これは、`IEmployee` インターフェイス上でインデクサーを実装します。次の宣言があります。  
  
```  
string ICitizen.this[int index]
{   
}   
```  
  
 これは、`ICitizen` インターフェイスでインデクサーを実装します。  
  
## <a name="see-also"></a>参照  
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)  
 [インデクサー](../../../csharp/programming-guide/indexers/index.md)  
 [プロパティ](../../../csharp/programming-guide/classes-and-structs/properties.md)  
 [インターフェイス](../../../csharp/programming-guide/interfaces/index.md)
