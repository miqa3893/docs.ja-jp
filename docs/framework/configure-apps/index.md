---
title: "構成ファイルを使用してアプリを構成する方法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "AutoGeneratedOrientationPage"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - ".NET Framework アプリケーション構成, 構成ファイル"
  - "< runtime > 要素"
  - "アプリケーション構成ファイル"
  - "アプリケーション構成ファイル, バージョン情報"
  - "アプリケーション構成ファイル, format"
  - "アプリケーション構成ファイル, マシン"
  - "アプリケーション構成ファイル, セキュリティ"
  - "アプリケーション [.NET Framework], 構成ファイル"
  - "ASP.NET, 構成"
  - "構成ファイル [.NET Framework]"
  - "構成ファイル [.NET Framework], アプリケーション"
  - "構成ファイル [.NET Framework], format"
  - "構成ファイル [.NET Framework], マシン"
  - "構成ファイル [.NET Framework], セキュリティ"
  - "終了タグ"
  - "ホスト, アプリケーション"
  - "マシン構成ファイル"
  - "セキュリティ構成ファイル"
  - "開始タグ"
ms.assetid: 86bd26d3-737e-4484-9782-19b17f34cd1f
caps.latest.revision: 28
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 28
---
# 構成ファイルを使用してアプリを構成する方法
.NET Framework を使用すると、開発者および管理者は、構成ファイルを使用することにより、アプリケーションの実行方法を制御し、アプリケーションの実行に柔軟性を持たせることができます。  構成ファイルは XML ファイルで、必要に応じて変更できます。  管理者は、アプリケーションからアクセスできるプロテクト リソース、アプリケーションが使用するアセンブリのバージョン、およびリモート アプリケーションやオブジェクトの配置場所を制御できます。  開発者は、構成ファイル内に設定を格納できます。これにより、設定変更のたびにアプリケーションを再コンパイルする必要がなくなります。  このセクションでは、設定できる内容と、アプリケーションを設定することが有益である理由を説明します。  
  
> [!NOTE]
>  マネージ コードは、<xref:System.Configuration> 名前空間のクラスを使用して、構成ファイルから設定を読み込むことができます。設定をファイルへ書き込むことはありません。  
  
 ここでは、構成ファイルの構文を説明し、3 種類の構成ファイル \(マシン構成ファイル、アプリケーション構成ファイル、およびセキュリティ構成ファイル\) について情報を提供します。  
  
## 構成ファイルの形式  
 構成ファイルには、構成情報を設定する論理データ構造体である要素が含まれます。  構成ファイル内では、タグを使用して、それらの要素の先頭と末尾を示します。  たとえば、`<runtime>` 要素は `<runtime>`*child elements*`</runtime>` で構成されます。  空の要素は `<runtime/>` または `<runtime>``</runtime>` として書き込まれます。  
  
 XML ファイルと同様に、構成ファイル内の構文では、大文字と小文字が区別されます。  
  
 構成設定は、要素の開始タグの内部に、定義済みの属性の名前と値を組み合わせて使用することで指定します。  `version` 要素に 2 つの属性 \(`href` および `<codeBase>`\) を指定して、ランタイムがアセンブリを検索する場所を指定する例を次に示します。詳細については、「[アセンブリの場所の指定](../../../docs/framework/configure-apps/specify-assembly-location.md)」を参照してください。  
  
```  
<codeBase version="2.0.0.0"  
          href="http://www.litwareinc.com/myAssembly.dll"/>  
```  
  
## マシン構成ファイル  
 マシン構成ファイル Machine.config には、コンピューター全体に適用する設定を含めます。  このファイルは、%*runtime install path*%\\Config ディレクトリに含まれています。  Machine.config には、マシン全体のアセンブリ バインディング、組み込みの[リモート処理チャネル](http://msdn.microsoft.com/ja-jp/6e9b60e0-9bc0-47b4-a8ef-3b78585f9a18)、および ASP.NET に関する構成設定が含まれます。  
  
 構成システムは、まずマシン構成ファイル内で、[appSettings 要素](http://msdn.microsoft.com/ja-jp/0d65a3f1-c522-423d-89b6-44921b6daebb)と、開発者が定義したその他の構成セクションを調べます。  次に、アプリケーション構成ファイルを調べます。  マシン構成ファイルを管理しやすくするには、これらの設定をアプリケーション構成ファイルに配置するのが最適です。  しかし、それらの設定をマシン構成ファイル内に配置した方が、システムの保守が簡単になります。  たとえば、クライアント アプリケーションとサーバー アプリケーションの両方で使用されるサードパーティ コンポーネントがある場合、そのコンポーネントの設定を 1 か所に設まとめた方が簡単です。  この場合、同じ設定を 2 つのファイルに配置する必要がなくなるという点から、設定を格納するのに適した場所はマシン構成ファイルになります。  
  
> [!NOTE]
>  XCOPY を使用してアプリケーションを配置しても、マシン構成ファイル内の設定はコピーされません。  
  
 共通言語ランタイムがアセンブリ バインディングに関してマシン構成ファイルを使用する方法の詳細については、「[ランタイムがアセンブリを検索する方法](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)」を参照してください。  
  
## アプリケーション構成ファイル  
 アプリケーション構成ファイルは、アプリケーション固有の設定を含みます。  このファイルには、アセンブリ バインディング ポリシー、リモート処理オブジェクトなど、共通言語ランタイムが読み取る構成設定と、アプリケーションが読み取ることのできる設定を含めます。  
  
 アプリケーション構成ファイルの名前と場所は、アプリケーションのホストによって異なり、次のいずれかの場合が考えられます。  
  
-   実行可能ファイルによってホストされるアプリケーション。  
  
     これらのアプリケーションには構成ファイルが 2 つあります。開発中に開発者によって変更されるソース構成ファイルと、アプリケーションと共に配布される出力構成ファイルです。  
  
     Visual Studio で開発するときは、プロジェクト ディレクトリにアプリケーションのソース構成ファイルを配置し、その **\[出力ディレクトリにコピー\]** プロパティを **\[常にコピーする\]** または **\[新しい場合はコピーする\]** に設定します。  この構成ファイルの名前は、アプリケーション名に拡張子 .config を付けた名前になります。  たとえば、myApp.exe という名前のアプリケーションは、myApp.exe.config という名前のソース構成ファイルを持ちます。  
  
     Visual Studio は、コンパイル済みアセンブリが格納されるディレクトリに自動的にソース構成ファイルをコピーして、アプリケーションと共に配置される出力構成ファイルを作成します。  場合によっては、Visual Studio が出力構成ファイルを変更することがあります。詳細については、「[アセンブリ バージョンのリダイレクト](../../../docs/framework/configure-apps/redirect-assembly-versions.md)」の「[アプリ レベルでのアセンブリ バージョンのリダイレクト](../../../docs/framework/configure-apps/redirect-assembly-versions.md#BKMK_Redirectingassemblyversionsattheapplevel)」を参照してください。  
  
-   ASP.NET によってホストされるアプリケーション。  
  
     ASP.NET 構成ファイルの詳細については、「[ASP.NET 構成設定](http://msdn.microsoft.com/ja-jp/116608f3-c03d-4413-9fc7-978703e18b0f)」を参照してください。  
  
-   Internet Explorer によってホストされるアプリケーション。  
  
     Internet Explorer でホストされるアプリケーションに構成ファイルが関連付けられている場合、そのファイルの場所は、`<link>` タグ内に次の構文で指定します。  
  
     \<link rel\="*ConfigurationFileName*" href\="*location*"\>  
  
     このタグ内の `location` は、構成ファイルの場所を示す URL です。  これにより、アプリケーション ベースが設定されます。  構成ファイルは、アプリケーションと同じ Web サイトに配置する必要があります。  
  
## セキュリティ構成ファイル  
 セキュリティ構成ファイルには、コード グループ階層構造に関する情報と、ポリシー レベルに関連付けたアクセス許可セットを含めます。  セキュリティ ポリシーを変更するときは、ポリシーの変更によってセキュリティ構成ファイルが破損しないように、[コード アクセス セキュリティ ポリシー ツール \(Caspol.exe\)](../../../docs/framework/tools/caspol-exe-code-access-security-policy-tool.md) を使用することを強くお勧めします。  
  
> [!NOTE]
>  [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 以降では、セキュリティ構成ファイルはセキュリティ ポリシーが変更された場合にのみ存在します。  
  
 セキュリティ構成ファイルは次の場所にあります。  
  
-   エンタープライズ ポリシー構成ファイル: %*runtime\-install\-path*%\\Config\\Enterprisesec.config  
  
-   コンピューター ポリシー構成ファイル: %*runtime\-install\-path*%\\Config\\Security.config  
  
-   ユーザー ポリシー構成ファイル: %USERPROFILE%\\Application data\\Microsoft\\CLR security config\\v*xx.xx*\\Security.config  
  
## このセクションの内容  
 [方法 : DEVPATH を使用してアセンブリを指定する](../../../docs/framework/configure-apps/how-to-locate-assemblies-by-using-devpath.md)  
 アセンブリ検索のときに DEVPATH 環境変数を使用するようにランタイムに指示する方法を説明します。  
  
 [アセンブリ バージョンのリダイレクト](../../../docs/framework/configure-apps/redirect-assembly-versions.md)  
 アセンブリの場所および使用するアセンブリ バージョンを指定する方法を説明します。  
  
 [アセンブリの場所の指定](../../../docs/framework/configure-apps/specify-assembly-location.md)  
 ランタイムがどの場所でアセンブリを検索するかを指定する方法を説明します。  
  
 [暗号化クラスの設定](../../../docs/framework/configure-apps/configure-cryptography-classes.md)  
 暗号化クラスにアルゴリズム名を割り当てる方法と、暗号化アルゴリズムにオブジェクト ID を割り当てる方法を説明します。  
  
 [方法 : 発行者ポリシーを作成する](../../../docs/framework/configure-apps/how-to-create-a-publisher-policy.md)  
 アセンブリのリダイレクトやコード ベース設定を指定する発行者ポリシー ファイルを追加する状況や方法を説明します。  
  
 [構成ファイル スキーマ](../../../docs/framework/configure-apps/file-schema/index.md)  
 スキーマ、起動時の階層、ランタイム、ネットワーク、およびその他の種類の構成設定を説明します。  
  
## 参照  
 [構成ファイル スキーマ](../../../docs/framework/configure-apps/file-schema/index.md)   
 [アセンブリの場所の指定](../../../docs/framework/configure-apps/specify-assembly-location.md)   
 [アセンブリ バージョンのリダイレクト](../../../docs/framework/configure-apps/redirect-assembly-versions.md)   
 [構成ファイルを使用したリモート オブジェクトの登録](http://msdn.microsoft.com/ja-jp/bc503ee1-c811-4f82-9525-470343326adc)   
 [ASP.NET Web Site Administration](../Topic/ASP.NET%20Web%20Site%20Administration.md)   
 [NIB: Security Policy Management](http://msdn.microsoft.com/ja-jp/d754e05d-29dc-4d3a-a2c2-95eaaf1b82b9)   
 [Caspol.exe \(コード アクセス セキュリティ ポリシー ツール\)](../../../docs/framework/tools/caspol-exe-code-access-security-policy-tool.md)   
 [共通言語ランタイムのアセンブリ](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)   
 [リモート オブジェクト](http://msdn.microsoft.com/ja-jp/515686e6-0a8d-42f7-8188-73abede57c58)