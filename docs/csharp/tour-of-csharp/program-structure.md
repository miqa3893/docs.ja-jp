---
title: "C# プログラムの構造 | C# 言語のツアー"
description: "C# プログラムの基本的な構造について説明します"
keywords: .NET .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 984f0314-507f-47a0-af56-9011243f5e65
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9ef19d7fa2164990edd5e27651d28aa085ec90ad
ms.lasthandoff: 03/13/2017

---

# <a name="program-structure"></a>プログラムの構造

C# における主要な組織的概念は、***プログラム***、***名前空間***、***型***、***メンバー***、および***アセンブリ***です。 C# プログラムは、1 つまたは複数のソース ファイルで構成されています。 プログラムは型を宣言します。型にはメンバーが含まれていて、複数の名前空間に編成することができます。 型の例には、クラスおよびインターフェイスがあります。 メンバーの例には、フィールド、メソッド、プロパティ、およびイベントがあります。 C# プログラムはコンパイルされると、物理的にアセンブリにパッケージ化されます。 アセンブリには通常、***アプリケーション***または***ライブラリ***のどちらかを実行するかに応じて、それぞれ `.exe` または `.dll` のファイル拡張子があります。

次の例では、`Acme.Collections` と呼ばれる名前空間で `Stack` と呼ばれるクラスを宣言します。

[!code-csharp[Stack](../../../samples/snippets/csharp/tour/program-structure/program.cs#L1-L34)]

このクラスの完全修飾名は `Acme.Collections.Stack` です。 このクラスには複数のメンバーが含まれています: `top` という名前のフィールドが 1 つ、`Push` と `Pop` という名前のメソッドが合わせて 2 つ、そして `Entry` という名前の入れ子になったクラスです。 `Entry` クラスにはさらに、3 つのメンバーが含まれています: `next` という名前のフィールド、`data` という名前のフィールド、およびコンストラクターです。 例のソース コードが `acme.cs` のファイルに保存されていることを前提に、次のコマンド ラインをご覧ください。

```
csc /t:library acme.cs
```

このコマンド ラインは例をライブラリ (`Main` エントリ ポイントがないコード) としてコンパイルし、`acme.dll` という名前のアセンブリを生成します。

> [!IMPORTANT]
> 上記の例では `csc` をコマンド ライン C# コンパイラとして使用します。 このコンパイラは Windows で実行可能です。 C# を他のプラットフォームでも使用するには、.NET Core のツールを使用する必要があります。 .NET Core エコシステムでは、`dotnet` CLI を使用してコマンド ラインのビルドを管理します。 これには、依存関係の管理、および C# コンパイラの呼び出しが含まれます。 .NET Core でサポートされているプラットフォームでのこれらのツールに関する完全な説明については、[こちらのチュートリアル](../../core/tutorials/using-with-xplat-cli.md)を参照してください。

アセンブリには実行可能なコードが中間言語 (IL) の形式で含まれていて、シンボル情報がメタデータの形式で含まれています。 アセンブリの IL コードは実行前に、.NET 共通言語ランタイムの Just-In-Time (JIT) コンパイラによって、プロセッサ固有のコードに自動的に変換されます。

アセンブリはコードとメタデータの両方を含む自己記述的な機能的単位であるため、`#include` ディレクティブおよびヘッダー ファイルが C# に含まれている必要はありません。 特定のアセンブリに含まれているパブリックの型とメンバーは、単にプログラムのコンパイル中にそのアセンブリを参照することにより、C# プログラムで利用可能になります。 たとえば、このプログラムでは `acme.dll` アセンブリの `Acme.Collections.Stack` クラスを使用しています。

[!code-csharp[UsingStack](../../../samples/snippets/csharp/tour/program-structure/Program.cs#L38-L52)]

プログラムが `example.cs` のファイルに格納されている場合、`example.cs` がコンパイルされると、acme.dll アセンブリはコンパイラの /r オプションを使用して参照できるようになります。

```
csc /r:acme.dll example.cs
```

これにより `example.exe` という名前の実行可能なアセンブリが作成され、これが実行された場合に、次の出力が生成されます。

```
100
10
1
```

C# では、プログラムのソース テキストを複数のソース ファイルに保存することができます。 複数ファイルの C# プログラムがコンパイルされると、ソース ファイルはすべて同時に処理され、ソース ファイルは自由に相互を参照できるようになります。概念的には、ソース ファイルが処理される前に、すべて 1 つの大きいファイルに連結されるようなものです。 C# では事前宣言をする必要がありません。ごく一部の例外を除いて、宣言の順序は重要でないためです。 C# ではソース ファイルがパブリック型 1 つのみの宣言に制限されません。また、ソース ファイルの名前がソース ファイルで宣言された型に一致する必要もありません。

>[!div class="step-by-step"]
[前へ](index.md)
[次へ](types-and-variables.md)
