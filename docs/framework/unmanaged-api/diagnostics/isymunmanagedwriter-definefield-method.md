---
title: "ISymUnmanagedWriter::DefineField メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ISymUnmanagedWriter.DefineField
api_location: diasymreader.dll
api_type: COM
f1_keywords: ISymUnmanagedWriter::DefineField
helpviewer_keywords:
- ISymUnmanagedWriter::DefineField method [.NET Framework debugging]
- DefineField method, ISymUnmanagedWriter interface [.NET Framework debugging]
ms.assetid: c6a1f797-dbf4-40f5-ab99-d9b4bfb26148
topic_type: apiref
caps.latest.revision: "9"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: c44c4ba4a2fd8959299bce6c9f3b4dc361174922
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="isymunmanagedwriterdefinefield-method"></a><span data-ttu-id="fdcbf-102">ISymUnmanagedWriter::DefineField メソッド</span><span class="sxs-lookup"><span data-stu-id="fdcbf-102">ISymUnmanagedWriter::DefineField Method</span></span>
<span data-ttu-id="fdcbf-103">メソッド内ではない 1 つの変数を定義します。</span><span class="sxs-lookup"><span data-stu-id="fdcbf-103">Defines a single variable that is not within a method.</span></span> <span data-ttu-id="fdcbf-104">このメソッドは、使用されるクラス内の特定のフィールド、ビット フィールドです。</span><span class="sxs-lookup"><span data-stu-id="fdcbf-104">This method is used for certain fields in classes, bit fields, and so on.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fdcbf-105">構文</span><span class="sxs-lookup"><span data-stu-id="fdcbf-105">Syntax</span></span>  
  
```  
HRESULT DefineField(  
    [in] mdTypeDef    parent,  
    [in] const WCHAR  *name,  
    [in] ULONG32      attributes,  
    [in] ULONG32      cSig,  
    [in, size_is(cSig)] unsigned char signature[],  
    [in] ULONG32      addrKind,  
    [in] ULONG32      addr1,  
    [in] ULONG32      addr2,  
    [in] ULONG32      addr3);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="fdcbf-106">パラメーター</span><span class="sxs-lookup"><span data-stu-id="fdcbf-106">Parameters</span></span>  
 `parent`  
 <span data-ttu-id="fdcbf-107">[in]メタデータ型またはメソッド トークンです。</span><span class="sxs-lookup"><span data-stu-id="fdcbf-107">[in] The metadata type or method token.</span></span>  
  
 `name`  
 <span data-ttu-id="fdcbf-108">[in]フィールド名です。</span><span class="sxs-lookup"><span data-stu-id="fdcbf-108">[in] The field name.</span></span>  
  
 `attributes`  
 <span data-ttu-id="fdcbf-109">[in]フィールドの属性。</span><span class="sxs-lookup"><span data-stu-id="fdcbf-109">[in] The field attributes.</span></span>  
  
 `cSig`  
 <span data-ttu-id="fdcbf-110">[in]A`ULONG32`フィールド シグネチャの格納に必要なバッファーの文字のサイズはします。</span><span class="sxs-lookup"><span data-stu-id="fdcbf-110">[in] A `ULONG32` that is the size, in characters, of the buffer required to contain the field signature.</span></span>  
  
 `signature`  
 <span data-ttu-id="fdcbf-111">[in]フィールド シグネチャの配列です。</span><span class="sxs-lookup"><span data-stu-id="fdcbf-111">[in] The array of field signatures.</span></span>  
  
 `addrKind`  
 <span data-ttu-id="fdcbf-112">[in]アドレスの種類。</span><span class="sxs-lookup"><span data-stu-id="fdcbf-112">[in] The address type.</span></span>  
  
 `addr1`  
 <span data-ttu-id="fdcbf-113">[in]フィールド定義の最初のアドレス。</span><span class="sxs-lookup"><span data-stu-id="fdcbf-113">[in] The first address for the field specification.</span></span>  
  
 `addr2`  
 <span data-ttu-id="fdcbf-114">[in]フィールド定義の 2 番目のアドレス。</span><span class="sxs-lookup"><span data-stu-id="fdcbf-114">[in] The second address for the field specification.</span></span>  
  
 `addr3`  
 <span data-ttu-id="fdcbf-115">[in]フィールドの仕様の 3 番目のアドレス。</span><span class="sxs-lookup"><span data-stu-id="fdcbf-115">[in] The third address for the field specification.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="fdcbf-116">戻り値</span><span class="sxs-lookup"><span data-stu-id="fdcbf-116">Return Value</span></span>  
 <span data-ttu-id="fdcbf-117">メソッドが成功した場合は S_OK、それ以外の場合、E_FAIL またはその他のエラー コード。</span><span class="sxs-lookup"><span data-stu-id="fdcbf-117">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="fdcbf-118">要件</span><span class="sxs-lookup"><span data-stu-id="fdcbf-118">Requirements</span></span>  
 <span data-ttu-id="fdcbf-119">**ヘッダー:** CorSym.idl、CorSym.h</span><span class="sxs-lookup"><span data-stu-id="fdcbf-119">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fdcbf-120">関連項目</span><span class="sxs-lookup"><span data-stu-id="fdcbf-120">See Also</span></span>  
 [<span data-ttu-id="fdcbf-121">ISymUnmanagedWriter インターフェイス</span><span class="sxs-lookup"><span data-stu-id="fdcbf-121">ISymUnmanagedWriter Interface</span></span>](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-interface.md)