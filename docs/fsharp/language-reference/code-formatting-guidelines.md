---
title: "コードのフォーマットに関するガイドライン (F#)"
description: "F# のプログラミングの読みやすさ、美しさ、標準化、およびコンパイル言語のコードのインデントのフォーマットに関するガイドラインを説明します。"
keywords: "visual f#, f#, 関数型プログラミング"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 3f79717c-f84e-448d-9ce4-90e40a644ba1
ms.openlocfilehash: cc56c67f356b99defd8dc28770f87be1f58443c5
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="code-formatting-guidelines"></a><span data-ttu-id="a042e-104">コードのフォーマットに関するガイドライン</span><span class="sxs-lookup"><span data-stu-id="a042e-104">Code Formatting Guidelines</span></span>

<span data-ttu-id="a042e-105">このトピックでは、f# のコードのインデントのガイドラインをまとめたものです。</span><span class="sxs-lookup"><span data-stu-id="a042e-105">This topic summarizes code indentation guidelines for F#.</span></span> <span data-ttu-id="a042e-106">F# 言語は改行文字とインデントに機密性の高いためは、読みやすさの問題、見た目の問題、または、コードを正しく書式設定するコーディングの標準化問題だけです。</span><span class="sxs-lookup"><span data-stu-id="a042e-106">Because the F# language is sensitive to line breaks and indentation, it is not just a readability issue, aesthetic issue, or coding standardization issue to format your code correctly.</span></span> <span data-ttu-id="a042e-107">正常に正しくコンパイルするコードの書式を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a042e-107">You must format your code correctly for it to compile correctly.</span></span>


## <a name="general-rules-for-indentation"></a><span data-ttu-id="a042e-108">インデントの一般的な規則</span><span class="sxs-lookup"><span data-stu-id="a042e-108">General Rules for Indentation</span></span>
<span data-ttu-id="a042e-109">インデントが必要な場合は、スペース、タブではなくを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a042e-109">When indentation is required, you must use spaces, not tabs.</span></span> <span data-ttu-id="a042e-110">少なくとも 1 つの領域が必要です。</span><span class="sxs-lookup"><span data-stu-id="a042e-110">At least one space is required.</span></span> <span data-ttu-id="a042e-111">組織がインデントに使用する空白文字の数を指定するコーディング規則を作成できます。インデントを設定する各レベルのインデントの 3 つまたは 4 つのスペースが一般的です。</span><span class="sxs-lookup"><span data-stu-id="a042e-111">Your organization can create coding standards to specify the number of spaces to use for indentation; three or four spaces of indentation at each level where indentation occurs is typical.</span></span> <span data-ttu-id="a042e-112">Visual Studio でのオプションを変更することによって、組織のインデントの標準に合わせてを構成することができます、 `Options`  ダイアログ ボックスから利用できる、`Tools`メニュー。</span><span class="sxs-lookup"><span data-stu-id="a042e-112">You can configure Visual Studio to match your organization's indentation standards by changing the options in the `Options` dialog box, which is available from the `Tools` menu.</span></span> <span data-ttu-id="a042e-113">`Text Editor`  ノードを展開`F#` をクリックし、`Tabs`です。</span><span class="sxs-lookup"><span data-stu-id="a042e-113">In the `Text Editor` node, expand `F#` and then click `Tabs`.</span></span> <span data-ttu-id="a042e-114">使用可能なオプションの説明は、次を参照してください。[オプション、テキスト エディター、すべての言語、タブ](https://msdn.microsoft.com/library/7sffa753.aspx)です。</span><span class="sxs-lookup"><span data-stu-id="a042e-114">For a description of the available options, see [Options, Text Editor, All Languages, Tabs](https://msdn.microsoft.com/library/7sffa753.aspx).</span></span>

<span data-ttu-id="a042e-115">一般に、コンパイラがコードを解析するときは、内部スタックを現在の入れ子レベルを示すを維持します。</span><span class="sxs-lookup"><span data-stu-id="a042e-115">In general, when the compiler parses your code, it maintains an internal stack that indicates the current level of nesting.</span></span> <span data-ttu-id="a042e-116">コードにインデントは、新しい入れ子のレベルが作成されると、か、この内部スタックにプッシュされます。</span><span class="sxs-lookup"><span data-stu-id="a042e-116">When code is indented, a new level of nesting is created, or pushed onto this internal stack.</span></span> <span data-ttu-id="a042e-117">構成要素の終了時に、レベルがポップされます。</span><span class="sxs-lookup"><span data-stu-id="a042e-117">When a construct ends, the level is popped.</span></span> <span data-ttu-id="a042e-118">インデント レベルの終了を通知し、内部のスタックをポップする方法の 1 つが発生する、レベルなど、ポップできますをも特定のトークン、`end`キーワード、または右中かっこまたはかっこを入力します。</span><span class="sxs-lookup"><span data-stu-id="a042e-118">Indentation is one way to signal the end of a level and pop the internal stack, but certain tokens also cause the level to be popped, such as the `end` keyword, or a closing brace or parenthesis.</span></span>

<span data-ttu-id="a042e-119">関数定義の種類の定義など、複数行の構成体コード`try...with`構造やループ構造にコンストラクトの開始行にインデントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a042e-119">Code in a multiline construct, such as a type definition, function definition, `try...with` construct, and looping constructs, must be indented relative to the opening line of the construct.</span></span> <span data-ttu-id="a042e-120">インデントを設定した 1 行目では、同じ構成要素で後続のコードの列の位置を設定します。</span><span class="sxs-lookup"><span data-stu-id="a042e-120">The first indented line establishes a column position for subsequent code in the same construct.</span></span> <span data-ttu-id="a042e-121">インデント レベルを呼び出す、*コンテキスト*です。</span><span class="sxs-lookup"><span data-stu-id="a042e-121">The indentation level is called a *context*.</span></span> <span data-ttu-id="a042e-122">列の位置と呼ばれる最小の列の設定、*オフサイド ライン*、同じコンテキストでは、後続の行のコードにします。</span><span class="sxs-lookup"><span data-stu-id="a042e-122">The column position sets a minimum column, referred to as an *offside line*, for subsequent lines of code that are in the same context.</span></span> <span data-ttu-id="a042e-123">コードの行が発生した場合に、この設定された列の位置よりも少ないインデント、コンパイラには、コンテキストが終了したこととするようになりましたをコーディングする次のレベルに、以前のコンテキストが前提としています。</span><span class="sxs-lookup"><span data-stu-id="a042e-123">When a line of code is encountered that is indented less than this established column position, the compiler assumes that the context has ended and that you are now coding at the next level up, in the previous context.</span></span> <span data-ttu-id="a042e-124">用語*オフサイド*を十分に離れたインデントされませんので、コードの行構造の末尾をトリガーする条件を記述するために使用します。</span><span class="sxs-lookup"><span data-stu-id="a042e-124">The term *offside* is used to describe the condition in which a line of code triggers the end of a construct because it is not indented far enough.</span></span> <span data-ttu-id="a042e-125">つまり、オフサイド ラインの左側にあるコードはオフサイドです。</span><span class="sxs-lookup"><span data-stu-id="a042e-125">In other words, code to the left of an offside line is offside.</span></span> <span data-ttu-id="a042e-126">正しくインデントされたコードで利用するオフサイド ルールの構成要素の終了を示すためにします。</span><span class="sxs-lookup"><span data-stu-id="a042e-126">In correctly indented code, you take advantage of the offside rule in order to delineate the end of constructs.</span></span> <span data-ttu-id="a042e-127">インデントを不適切に使用する場合オフサイド状態コンパイラ警告を発行する可能性があります。 またはコードの誤った解釈につながることができます。</span><span class="sxs-lookup"><span data-stu-id="a042e-127">If you use indentation improperly, an offside condition can cause the compiler to issue a warning or can lead to the incorrect interpretation of your code.</span></span>

<span data-ttu-id="a042e-128">オフサイド ラインは、次のように決定されます。</span><span class="sxs-lookup"><span data-stu-id="a042e-128">Offside lines are determined as follows.</span></span>


- <span data-ttu-id="a042e-129">`=`トークンに関連付けられている、`let`後の最初のトークンの 1 列にオフサイド ラインが、`=`記号。</span><span class="sxs-lookup"><span data-stu-id="a042e-129">An `=` token associated with a `let` introduces an offside line at the column of the first token after the `=` sign.</span></span>


- <span data-ttu-id="a042e-130">`if...then...else`式、後の最初のトークンの列の位置、`then`キーワードまたは`else`キーワード オフサイド ラインが導入されています。</span><span class="sxs-lookup"><span data-stu-id="a042e-130">In an `if...then...else` expression, the column position of the first token after the `then` keyword or the `else` keyword introduces an offside line.</span></span>


- <span data-ttu-id="a042e-131">`try...with`式、後の最初のトークン`try`オフサイド ラインします。</span><span class="sxs-lookup"><span data-stu-id="a042e-131">In a `try...with` expression, the first token after `try` introduces an offside line.</span></span>


- <span data-ttu-id="a042e-132">`match`式、後の最初のトークン`with`とそれぞれの後に最初のトークン`->`オフサイド ラインします。</span><span class="sxs-lookup"><span data-stu-id="a042e-132">In a `match` expression, the first token after `with` and the first token after each `->` introduce offside lines.</span></span>


- <span data-ttu-id="a042e-133">後の最初のトークン`with`拡張機能の種類ではオフサイド ラインが導入されています。</span><span class="sxs-lookup"><span data-stu-id="a042e-133">The first token after `with` in a type extension introduces an offside line.</span></span>


- <span data-ttu-id="a042e-134">最初のトークンの後に左中かっこまたはかっこ、または後に、`begin`キーワード、オフサイド ラインが導入されています。</span><span class="sxs-lookup"><span data-stu-id="a042e-134">The first token after an opening brace or parenthesis, or after the `begin` keyword, introduces an offside line.</span></span>


- <span data-ttu-id="a042e-135">キーワードの最初の文字`let`、 `if`、および`module`オフサイド ラインします。</span><span class="sxs-lookup"><span data-stu-id="a042e-135">The first character in the keywords `let`, `if`, and `module` introduce offside lines.</span></span>


<span data-ttu-id="a042e-136">次のコード例では、インデント規則を示します。</span><span class="sxs-lookup"><span data-stu-id="a042e-136">The following code examples illustrate the indentation rules.</span></span> <span data-ttu-id="a042e-137">ここでは、print ステートメントは、適切なコンテキストと関連付けるインデントに依存します。</span><span class="sxs-lookup"><span data-stu-id="a042e-137">Here, the print statements rely on indentation to associate them with the appropriate context.</span></span> <span data-ttu-id="a042e-138">インデントが変わるたびにコンテキストがポップされ、以前のコンテキストを返します。</span><span class="sxs-lookup"><span data-stu-id="a042e-138">Every time the indentation shifts, the context is popped and returns to the previous context.</span></span> <span data-ttu-id="a042e-139">各反復の末尾にスペースを印刷するそのため、「完了」です。</span><span class="sxs-lookup"><span data-stu-id="a042e-139">Therefore, a space is printed at the end of each iteration; "Done!"</span></span> <span data-ttu-id="a042e-140">オフサイド インデント、ループの一部ではないことを確立するため、1 回を出力のみがします。</span><span class="sxs-lookup"><span data-stu-id="a042e-140">is only printed one time because the offside indentation establishes that it is not part of the loop.</span></span> <span data-ttu-id="a042e-141">文字列"最上位レベルのコンテキスト の印刷は、関数の一部ではできません。</span><span class="sxs-lookup"><span data-stu-id="a042e-141">The printing of the string "Top-level context" is not part of the function.</span></span> <span data-ttu-id="a042e-142">したがって、最初に出力されます、初期化中に、静的な関数が呼び出される前にします。</span><span class="sxs-lookup"><span data-stu-id="a042e-142">Therefore, it is printed first, during the static initialization, before the function is called.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/code-formatting/snippet1.fs)]

<span data-ttu-id="a042e-143">出力は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="a042e-143">The output is as follows.</span></span>

```
Top-level context

(Negative number) Zero 1 2 3 Done!
```

<span data-ttu-id="a042e-144">長い行を中断したときは、それを囲むコンストラクトよりも行の継続をインデントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a042e-144">When you break long lines, the continuation of the line must be indented farther than the enclosing construct.</span></span> <span data-ttu-id="a042e-145">たとえば、次のコードに示すように、関数名の最初の文字よりも関数の引数をインデントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a042e-145">For example, function arguments must be indented farther than the first character of the function name, as shown in the following code.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/code-formatting/snippet2.fs)]

<span data-ttu-id="a042e-146">これらの規則の例外があるように、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="a042e-146">There are exceptions to these rules, as described in the next section.</span></span>


## <a name="indentation-in-modules"></a><span data-ttu-id="a042e-147">モジュールのインデント</span><span class="sxs-lookup"><span data-stu-id="a042e-147">Indentation in Modules</span></span>
<span data-ttu-id="a042e-148">モジュールを基準としたローカル モジュール内のコードのインデントを設定する必要がありますが、最上位レベルのモジュール内のコードにインデントを解除するがないです。</span><span class="sxs-lookup"><span data-stu-id="a042e-148">Code in a local module must be indented relative to the module, but code in a top-level module does not have to be indented.</span></span> <span data-ttu-id="a042e-149">Namespace 要素は、インデントする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="a042e-149">Namespace elements do not have to be indented.</span></span>

<span data-ttu-id="a042e-150">次のコード例では、この問題を説明します。</span><span class="sxs-lookup"><span data-stu-id="a042e-150">The following code examples illustrate this.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/code-formatting/snippet3.fs)]
[!code-fsharp[Main](../../../samples/snippets/fsharp/code-formatting/snippet4.fs)]

<span data-ttu-id="a042e-151">詳細については、次を参照してください。[モジュール](modules.md)です。</span><span class="sxs-lookup"><span data-stu-id="a042e-151">For more information, see [Modules](modules.md).</span></span>


## <a name="exceptions-to-the-basic-indentation-rules"></a><span data-ttu-id="a042e-152">基本的なインデント規則の例外</span><span class="sxs-lookup"><span data-stu-id="a042e-152">Exceptions to the Basic Indentation Rules</span></span>
<span data-ttu-id="a042e-153">一般的な規則、コンストラクトの最初の行のインデントの基準とした複数行の構造体でコードをインデントする必要があります、最初のオフサイド ラインが発生すると、コンストラクトの末尾がによって決定されるを前のセクションで説明したです。</span><span class="sxs-lookup"><span data-stu-id="a042e-153">The general rule, as described in the previous section, is that code in multiline constructs must be indented relative to the indentation of the first line of the construct, and that the end of the construct is determined by when the first offside line occurs.</span></span> <span data-ttu-id="a042e-154">コンテキストの末尾が、一部を構築などの場合は、規則の例外、`try...with`式では、`if...then...else`式、および使用する`and`再帰関数や型を一緒に宣言するための構文には、複数の一部が含まれています。</span><span class="sxs-lookup"><span data-stu-id="a042e-154">An exception to the rule about when contexts end is that some constructs, such as the `try...with` expression, the `if...then...else` expression, and the use of `and` syntax for declaring mutually recursive functions or types, have multiple parts.</span></span> <span data-ttu-id="a042e-155">など、後の部分をインデントする`then`と`else`で、`if...then...else`式、同時に、トークンとレベルを開始されますが、式がコンテキストの終了を示すではなく、同じコンテキストの次の部分を表します。</span><span class="sxs-lookup"><span data-stu-id="a042e-155">You indent the later parts, such as `then` and `else` in an `if...then...else` expression, at the same level as the token that starts the expression, but instead of indicating an end to the context, it represents the next part of the same context.</span></span> <span data-ttu-id="a042e-156">したがって、`if...then...else`式は、次のコード例のように記述できます。</span><span class="sxs-lookup"><span data-stu-id="a042e-156">Therefore, an `if...then...else` expression can be written as in the following code example.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/code-formatting/snippet5.fs)]

<span data-ttu-id="a042e-157">オフサイド規則の例外にのみ適用され、`then`と`else`キーワード。</span><span class="sxs-lookup"><span data-stu-id="a042e-157">The exception to the offside rule applies only to the `then` and `else` keywords.</span></span> <span data-ttu-id="a042e-158">したがって、インデントを設定すると、エラーではありませんが、`then`と`else`内のコードの行をインデントするさらに、失敗している、`then`ブロックは、警告を生成します。</span><span class="sxs-lookup"><span data-stu-id="a042e-158">Therefore, although it is not an error to indent the `then` and `else` further, failing to indent the lines of code in a `then` block produces a warning.</span></span> <span data-ttu-id="a042e-159">これは、次のコード行に示します。</span><span class="sxs-lookup"><span data-stu-id="a042e-159">This is illustrated in the following lines of code.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/code-formatting/snippet6.fs)]
[!code-fsharp[Main](../../../samples/snippets/fsharp/code-formatting/snippet7.fs)]

<span data-ttu-id="a042e-160">コードに、`else`ブロック、その他の特別な規則が適用されます。</span><span class="sxs-lookup"><span data-stu-id="a042e-160">For code in an `else` block, an additional special rule applies.</span></span> <span data-ttu-id="a042e-161">内のコードでのみ、前の例で警告が発生した、`then`内のコードではなく、ブロック、`else`ブロックします。</span><span class="sxs-lookup"><span data-stu-id="a042e-161">The warning in the previous example occurs only on the code in the `then` block, not on the code in the `else` block.</span></span> <span data-ttu-id="a042e-162">これにより、関数の場合に可能性のあるコードの残りの部分を強制することがなく、関数の先頭にさまざまな条件をチェックするコードを記述するため、`else`ブロックをインデントされます。</span><span class="sxs-lookup"><span data-stu-id="a042e-162">This allows you to write code that checks for various conditions at the beginning of a function without forcing the rest of the code for the function, which might be in an `else` block, to be indented.</span></span> <span data-ttu-id="a042e-163">したがって、警告が生成されず、次を記述できます。</span><span class="sxs-lookup"><span data-stu-id="a042e-163">Thus, you can write the following without producing a warning.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/code-formatting/snippet8.fs)]

<span data-ttu-id="a042e-164">別の例外として前の行は挿入演算子など、行はインデントされないときにコンテキストを終了するルールを`+`と`|>`です。</span><span class="sxs-lookup"><span data-stu-id="a042e-164">Another exception to the rule that contexts end when a line is not indented as far as a previous line is for infix operators, such as `+` and `|>`.</span></span> <span data-ttu-id="a042e-165">挿入演算子で始まる行は、開始を許可する`(1 + oplength)`、コンテキストの終了をトリガーすることがなく通常の位置の前に列を`oplength`演算子文字の数です。</span><span class="sxs-lookup"><span data-stu-id="a042e-165">Lines that start with infix operators are permitted to begin `(1 + oplength)` columns before the normal position without triggering an end to the context, where `oplength` is the number of characters that make up the operator.</span></span> <span data-ttu-id="a042e-166">これにより、前の行に合うように演算子の後に最初のトークンが原因です。</span><span class="sxs-lookup"><span data-stu-id="a042e-166">This causes the first token after the operator to align with the previous line.</span></span>

<span data-ttu-id="a042e-167">たとえば、次のコードで、`+`記号の前の行未満のインデントされた 2 つの列では許可されています。</span><span class="sxs-lookup"><span data-stu-id="a042e-167">For example, in the following code, the `+` symbol is permitted to be indented two columns less than the previous line.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/code-formatting/snippet9.fs)]

<span data-ttu-id="a042e-168">インデントは、通常、入れ子のレベルが高くなり、向上しますが、コンパイラが低い列の位置にインデントをリセットすることに、いくつかの構造があります。</span><span class="sxs-lookup"><span data-stu-id="a042e-168">Although indentation usually increases as the level of nesting becomes higher, there are several constructs in which the compiler allows you to reset the indentation to a lower column position.</span></span>

<span data-ttu-id="a042e-169">列の位置をリセットできる構成要素は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="a042e-169">The constructs that permit a reset of column position are as follows:</span></span>


- <span data-ttu-id="a042e-170">匿名関数の本体。</span><span class="sxs-lookup"><span data-stu-id="a042e-170">Bodies of anonymous functions.</span></span> <span data-ttu-id="a042e-171">次のコードでは、印刷式はよりもよりも左にある列の位置から始まり、`fun`キーワード。</span><span class="sxs-lookup"><span data-stu-id="a042e-171">In the following code, the print expression starts at a column position that is farther to the left than the `fun` keyword.</span></span> <span data-ttu-id="a042e-172">ただし、行は、前のインデント レベルの開始の左側の列で開始する必要がありますされません (つまりの左側に、`L`で`List`)。</span><span class="sxs-lookup"><span data-stu-id="a042e-172">However, the line must not start at a column to the left of the start of the previous indentation level (that is, to the left of the `L` in `List`).</span></span>
[!code-fsharp[Main](../../../samples/snippets/fsharp/code-formatting/snippet10.fs)]

- <span data-ttu-id="a042e-173">構成要素を囲む丸かっこまたは`begin`と`end`で、`then`または`else`のブロック、`if...then...else`インデントいいえよりも小さいかの列の位置、式が提供される、`if`キーワード。</span><span class="sxs-lookup"><span data-stu-id="a042e-173">Constructs enclosed by parentheses or by `begin` and `end` in a `then` or `else` block of an `if...then...else` expression, provided the indentation is no less than the column position of the `if` keyword.</span></span> <span data-ttu-id="a042e-174">コーディング スタイルでは、この例外開きかっこを入力または`begin`後の行の最後に使用される`then`または`else`です。</span><span class="sxs-lookup"><span data-stu-id="a042e-174">This exception allows for a coding style in which an opening parenthesis or `begin` is used at the end of a line after `then` or `else`.</span></span>


- <span data-ttu-id="a042e-175">モジュール、クラス、インターフェイス、およびで区切られた構造体の本体`begin...end`、 `{...}`、 `class...end`、または`interface...end`です。</span><span class="sxs-lookup"><span data-stu-id="a042e-175">Bodies of modules, classes, interfaces, and structures delimited by `begin...end`, `{...}`, `class...end`, or `interface...end`.</span></span> <span data-ttu-id="a042e-176">これによりを型定義の開始キーワードできる型名と同じ行に始めキーワードよりもインデントする本文全体を強制することがなくスタイル。</span><span class="sxs-lookup"><span data-stu-id="a042e-176">This allows for a style in which the opening keyword of a type definition can be on the same line as the type name without forcing the whole body to be indented farther than the opening keyword.</span></span>
[!code-fsharp[Main](../../../samples/snippets/fsharp/code-formatting/snippet13.fs)]


## <a name="see-also"></a><span data-ttu-id="a042e-177">関連項目</span><span class="sxs-lookup"><span data-stu-id="a042e-177">See Also</span></span>
[<span data-ttu-id="a042e-178">F# 言語リファレンス</span><span class="sxs-lookup"><span data-stu-id="a042e-178">F# Language Reference</span></span>](index.md)