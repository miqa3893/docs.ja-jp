---
title: ".NET Compiler Platform SDK の概念とオブジェクト モデル"
description: "この概要では、.NET Compiler SDK を効果的に使用するために必要な背景を示します。 API レイヤー、関連する主な型、全体のオブジェクト モデルについて学習します。"
author: billwagner
ms.author: wiwagn
ms.date: 10/10/2017
ms.topic: conceptual
ms.prod: .net
ms.devlang: devlang-csharp
ms.custom: mvc
ms.openlocfilehash: 65a4695c6f4e5268582d83452246ed8262d6fe2f
ms.sourcegitcommit: d095094e942eedf09530ea5636fbaf9029853027
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2017
---
# <a name="understand-the-net-compiler-platform-sdk-model"></a><span data-ttu-id="1ea81-104">.NET Compiler Platform SDK モデルについて</span><span class="sxs-lookup"><span data-stu-id="1ea81-104">Understand the .NET Compiler Platform SDK model</span></span>

<span data-ttu-id="1ea81-105">コンパイラは、多くの場合、人間がコードを読み取り、理解する方法とは異なる構造化された規則に従って書き込まれたコードを処理します。</span><span class="sxs-lookup"><span data-stu-id="1ea81-105">Compilers process the code you write following structured rules that often differ from the way humans read and understand code.</span></span> <span data-ttu-id="1ea81-106">コンパイラで使用されるモデルの基礎知識は、Roslyn ベースのツールを構築するときに使用する API を理解するのに必須です。</span><span class="sxs-lookup"><span data-stu-id="1ea81-106">A basic understanding of the model used by compilers is essential to understanding the APIs you use when building Roslyn-based tools.</span></span> 

## <a name="compiler-pipeline-functional-areas"></a><span data-ttu-id="1ea81-107">コンパイラ パイプラインの機能領域</span><span class="sxs-lookup"><span data-stu-id="1ea81-107">Compiler pipeline functional areas</span></span>

<span data-ttu-id="1ea81-108">.NET Compiler Platform SDK は、従来のコンパイラ パイプラインを反映する API レイヤーを提供することで、コンシューマーに C# と Visual Basic コンパイラーのコード分析を公開します。</span><span class="sxs-lookup"><span data-stu-id="1ea81-108">The .NET Compiler Platform SDK exposes the C# and Visual Basic compilers' code analysis to you as a consumer by providing an API layer that mirrors a traditional compiler pipeline.</span></span>

![ソース コードからオブジェクト コードへのコンパイラ パイプラインの処理ステップ](media/compiler-pipeline.png)

<span data-ttu-id="1ea81-110">このパイプラインの各フェーズは別のコンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="1ea81-110">Each phase of this pipeline is a separate component.</span></span> <span data-ttu-id="1ea81-111">最初に、解析フェーズで、言語文法に従う構文にソース テキストをトークン化して解析します。</span><span class="sxs-lookup"><span data-stu-id="1ea81-111">First, the parse phase tokenizes and parses source text into syntax that follows the language grammar.</span></span> <span data-ttu-id="1ea81-112">2 番目に、宣言フェーズで、ソースとインポートされたメタデータを分析して、名前付け規則を形成します。</span><span class="sxs-lookup"><span data-stu-id="1ea81-112">Second the declaration phase analyzes source and imported metadata to form named symbols.</span></span> <span data-ttu-id="1ea81-113">次に、バインド フェーズで、コード内の識別子をシンボルと一致させます。</span><span class="sxs-lookup"><span data-stu-id="1ea81-113">Next the bind phase matches identifiers in the code to symbols.</span></span> <span data-ttu-id="1ea81-114">最後に、生成フェーズで、コンパイラによって構築されたすべての情報でアセンブリを生成します。</span><span class="sxs-lookup"><span data-stu-id="1ea81-114">Finally, the emit phase, emits an assembly with all the information built up by the compiler.</span></span>

![コンパイラ パイプライン API は、コンパイラ パイプラインの一部である各ステップへのアクセスを提供します](media/compiler-pipeline-api.png)

<span data-ttu-id="1ea81-116">これらの各フェーズに応じて、.NET Compiler Platform SDK はオブジェクト モデルを公開します。これにより、各フェーズの情報にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="1ea81-116">Corresponding to each of those phases, the .NET Compiler Platform SDK exposes an object model that allows access to the information at that phase.</span></span> <span data-ttu-id="1ea81-117">解析フェーズでは構文ツリーを公開し、宣言フェーズでは階層シンボル テーブルを公開し、バインド フェーズではコンパイラのセマンティック分析結果を公開します。生成フェーズは IL バイト コードを生成する API です。</span><span class="sxs-lookup"><span data-stu-id="1ea81-117">The parsing phase exposes a syntax tree, the declaration phase exposes a hierarchical symbol table, the binding phase exposes the result of the compiler’s semantic analysis, and the emit phase is an API that produces IL byte codes.</span></span>

![コンパイラ パイプラインの各ステップでコンパイラ API から使用可能な言語サービス](media/compiler-pipeline-lang-svc.png)

<span data-ttu-id="1ea81-119">各コンパイラは、これらのコンポーネントを一緒に単一のエンド ツー エンド全体として結合します。</span><span class="sxs-lookup"><span data-stu-id="1ea81-119">Each compiler combines these components together as a single end-to-end whole.</span></span>

<span data-ttu-id="1ea81-120">これらの API は、Visual Studio で使用されるものと同じです。</span><span class="sxs-lookup"><span data-stu-id="1ea81-120">These APIs are the same used by Visual Studio.</span></span> <span data-ttu-id="1ea81-121">たとえば、コードのアウトライン表示と書式設定機能では構文ツリーを使用し、オブジェクト ブラウザーとナビゲーション機能ではシンボル テーブルを使用します。リファクタリングと定義へ移動ではセマンティック モデルを使用し、エディット コンティニュでは、生成 API を含む、これらすべてを使用します。</span><span class="sxs-lookup"><span data-stu-id="1ea81-121">For instance, the code outlining and formatting features use the syntax trees, the Object Browser and navigation features use the symbol table, refactorings and Go to Definition use the semantic model, and Edit and Continue uses all of these, including the Emit API.</span></span> 

## <a name="api-layers"></a><span data-ttu-id="1ea81-122">API レイヤー</span><span class="sxs-lookup"><span data-stu-id="1ea81-122">API layers</span></span>

<span data-ttu-id="1ea81-123">.NET Compiler SDK は、2 つの主要な API レイヤー (コンパイラ API とワークスペース API) で構成されています。</span><span class="sxs-lookup"><span data-stu-id="1ea81-123">The .NET compiler SDK consists of two main layers of APIs: compiler APIs and workspaces APIs.</span></span>

![コンパイラ パイプライン API で表される API レイヤー](media/api-layers.png)

### <a name="compiler-apis"></a><span data-ttu-id="1ea81-125">コンパイラ API</span><span class="sxs-lookup"><span data-stu-id="1ea81-125">Compiler APIs</span></span>

<span data-ttu-id="1ea81-126">コンパイラ レイヤーには、構文とセマンティックの両方のコンパイラ パイプラインの各フェーズで公開される情報に対応するオブジェクト モデルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1ea81-126">The compiler layer contains the object models that correspond to information exposed at each phase of the compiler pipeline, both syntactic and semantic.</span></span> <span data-ttu-id="1ea81-127">また、コンパイラ レイヤーには、アセンブリ参照、コンパイラ オプション、ソース コード ファイルを含む、コンパイラの単一呼び出しの不変のスナップショットも含まれています。</span><span class="sxs-lookup"><span data-stu-id="1ea81-127">The compiler layer also contains an immutable snapshot of a single invocation of a compiler, including assembly references, compiler options, and source code files.</span></span> <span data-ttu-id="1ea81-128">C# 言語と Visual Basic 言語を表す 2 つの異なる API があります。</span><span class="sxs-lookup"><span data-stu-id="1ea81-128">There are two distinct APIs that represent the C# language and the Visual Basic language.</span></span> <span data-ttu-id="1ea81-129">これら 2 つの API の形は似ていますが、各言語を忠実に再現するために調整されます。</span><span class="sxs-lookup"><span data-stu-id="1ea81-129">These two APIs are similar in shape but tailored for high-fidelity to each individual language.</span></span> <span data-ttu-id="1ea81-130">このレイヤーは Visual Studio のコンポーネントには依存しません。</span><span class="sxs-lookup"><span data-stu-id="1ea81-130">This layer has no dependencies on Visual Studio components.</span></span>

### <a name="diagnostic-apis"></a><span data-ttu-id="1ea81-131">診断 API</span><span class="sxs-lookup"><span data-stu-id="1ea81-131">Diagnostic APIs</span></span>

<span data-ttu-id="1ea81-132">コンパイラは、分析の一環として、構文、セマンティック、および限定代入エラーからさまざまな警告と情報診断に至るすべてをカバーする一連の診断情報を生成する場合があります。</span><span class="sxs-lookup"><span data-stu-id="1ea81-132">As part of its analysis the compiler may produce a set of diagnostics covering everything from syntax, semantic, and definite assignment errors to various warnings and informational diagnostics.</span></span> <span data-ttu-id="1ea81-133">コンパイラ API レイヤーは拡張可能な API を介して診断情報を公開し、ユーザー定義のアナライザーをコンパイル プロセスに接続できるようにします。</span><span class="sxs-lookup"><span data-stu-id="1ea81-133">TThe Compiler API layer exposes diagnostics through an extensible API that allows user-defined analyzers to be plugged into the compilation process.</span></span> <span data-ttu-id="1ea81-134">これにより、StyleCop や FxCop などのツールで生成されるものなど、ユーザー定義の診断情報を、コンパイラ定義の診断情報と一緒に生成することができます。</span><span class="sxs-lookup"><span data-stu-id="1ea81-134">It allows user-defined diagnostics, such as those produced by tools like StyleCop or FxCop, to be produced alongside compiler-defined diagnostics.</span></span> <span data-ttu-id="1ea81-135">この方法で診断情報を生成すると、ポリシーに基づくビルドの停止、エディターでの破線の即時表示、コード修正の提案などの操作の診断に依存する、MSBuild や Visual Studio などのツールに自然に統合できるという利点があります。</span><span class="sxs-lookup"><span data-stu-id="1ea81-135">Producing diagnostics in this way has the benefit of integrating naturally with tools such as MSBuild and Visual Studio which depend on diagnostics for experiences such as halting a build based on policy and showing live squiggles in the editor and suggesting code fixes.</span></span>

### <a name="scripting-apis"></a><span data-ttu-id="1ea81-136">スクリプト API</span><span class="sxs-lookup"><span data-stu-id="1ea81-136">Scripting APIs</span></span>

<span data-ttu-id="1ea81-137">ホスト API とスクリプト API は、コンパイラ レイヤーの一部です。</span><span class="sxs-lookup"><span data-stu-id="1ea81-137">Hosting and scripting APIs are part of the compiler layer.</span></span> <span data-ttu-id="1ea81-138">コード スニペットを実行して、ランタイム実行コンテキストを蓄積する場合にこれらを使用できます。</span><span class="sxs-lookup"><span data-stu-id="1ea81-138">You can use them for executing code snippets and accumulating a runtime execution context.</span></span>
<span data-ttu-id="1ea81-139">C# 対話型 REPL (Read-Evaluate-Print Loop) ではこれらの API を使用します。</span><span class="sxs-lookup"><span data-stu-id="1ea81-139">The C# interactive REPL (Read-Evaluate-Print Loop) uses these APIs.</span></span> <span data-ttu-id="1ea81-140">REPL では、コードの書き込み時に対話的にコードを実行して、スクリプト言語として C# を使用できます。</span><span class="sxs-lookup"><span data-stu-id="1ea81-140">The REPL enables you to use C# as a scripting language, executing the code interactively as you write it.</span></span>

### <a name="workspaces-apis"></a><span data-ttu-id="1ea81-141">ワークスペース API</span><span class="sxs-lookup"><span data-stu-id="1ea81-141">Workspaces APIs</span></span>

<span data-ttu-id="1ea81-142">ワークスペース レイヤーにはワークスペース API が含まれます。この API は、ソリューション全体でのコード分析とリファクタリングの開始点となります。</span><span class="sxs-lookup"><span data-stu-id="1ea81-142">The Workspaces layer contains the Workspace API, which is the starting point for doing code analysis and refactoring over entire solutions.</span></span> <span data-ttu-id="1ea81-143">単一オブジェクト モデルにソリューションのプロジェクトに関するすべての情報を簡単にまとめることができ、コンパイラ レイヤー オブジェクト モデルに直接アクセスできます。ファイルの解析、オプションの構成、プロジェクト間の依存関係の管理は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="1ea81-143">It assists you in organizing all the information about the projects in a solution into single object model, offering you direct access to the compiler layer object models without needing to parse files, configure options, or manage project-to-project dependencies.</span></span>

<span data-ttu-id="1ea81-144">さらに、ワークスペース レイヤーには、Visual Studio IDE のような、ホスト環境内で機能するコード分析およびリファクタリング ツールを実装するときに使用される一連の API も示されます。</span><span class="sxs-lookup"><span data-stu-id="1ea81-144">In addition, the Workspaces layer surfaces a set of APIs used when implementing code analysis and refactoring tools that function within a host environment like the Visual Studio IDE.</span></span> <span data-ttu-id="1ea81-145">たとえば、すべての参照の検索、書式設定、コード生成 API などです。</span><span class="sxs-lookup"><span data-stu-id="1ea81-145">Examples include the Find All References, Formatting, and Code Generation APIs.</span></span>

<span data-ttu-id="1ea81-146">このレイヤーは Visual Studio のコンポーネントには依存しません。</span><span class="sxs-lookup"><span data-stu-id="1ea81-146">This layer has no dependencies on Visual Studio components.</span></span>