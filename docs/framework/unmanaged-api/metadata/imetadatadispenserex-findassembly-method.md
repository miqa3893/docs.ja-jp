---
title: "IMetaDataDispenserEx::FindAssembly メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMetaDataDispenserEx.FindAssembly
api_location: mscoree.dll
api_type: COM
f1_keywords: IMetaDataDispenserEx::FindAssembly
helpviewer_keywords:
- FindAssembly method [.NET Framework metadata]
- IMetaDataDispenserEx::FindAssembly method [.NET Framework metadata]
ms.assetid: 3afe7252-5f28-48d9-a74d-1927566c404c
topic_type: apiref
caps.latest.revision: "10"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 7a70d1e2b3636a405fe28b84c2e76dd7264df4f3
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="imetadatadispenserexfindassembly-method"></a><span data-ttu-id="87af6-102">IMetaDataDispenserEx::FindAssembly メソッド</span><span class="sxs-lookup"><span data-stu-id="87af6-102">IMetaDataDispenserEx::FindAssembly Method</span></span>
<span data-ttu-id="87af6-103">このメソッドは実装されていません。</span><span class="sxs-lookup"><span data-stu-id="87af6-103">This method is not implemented.</span></span> <span data-ttu-id="87af6-104">呼び出された場合、E_NOTIMPL を返します。</span><span class="sxs-lookup"><span data-stu-id="87af6-104">If called, it returns E_NOTIMPL.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="87af6-105">構文</span><span class="sxs-lookup"><span data-stu-id="87af6-105">Syntax</span></span>  
  
```  
HRESULT FindAssembly(  
    [in]  LPCWSTR  szAppBase,  
    [in]  LPCWSTR  szPrivateBin,  
    [in]  LPCWSTR  szGlobalBin,  
    [in]  LPCWSTR  szAssemblyName,  
    [out] LPCWSTR  szName,  
    [in]  ULONG    cchName,  
    [out] ULONG    *pcName  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="87af6-106">パラメーター</span><span class="sxs-lookup"><span data-stu-id="87af6-106">Parameters</span></span>  
 `szAppBase`  
 <span data-ttu-id="87af6-107">[in]使用しません。</span><span class="sxs-lookup"><span data-stu-id="87af6-107">[in] Not used.</span></span>  
  
 `szPrivateBin`  
 <span data-ttu-id="87af6-108">[in]使用しません。</span><span class="sxs-lookup"><span data-stu-id="87af6-108">[in] Not used.</span></span>  
  
 `szGlobalBin`  
 <span data-ttu-id="87af6-109">[in]使用しません。</span><span class="sxs-lookup"><span data-stu-id="87af6-109">[in] Not used.</span></span>  
  
 `szAssemblyName`  
 <span data-ttu-id="87af6-110">[in]検索するアセンブリ。</span><span class="sxs-lookup"><span data-stu-id="87af6-110">[in] The assembly to be found.</span></span>  
  
 `szName`  
 <span data-ttu-id="87af6-111">[out]アセンブリの簡易名。</span><span class="sxs-lookup"><span data-stu-id="87af6-111">[out] The simple name of the assembly.</span></span>  
  
 `cchName`  
 <span data-ttu-id="87af6-112">[in]サイズをバイト単位での`szName`します。</span><span class="sxs-lookup"><span data-stu-id="87af6-112">[in] The size, in bytes, of `szName`.</span></span>  
  
 `pcName`  
 <span data-ttu-id="87af6-113">[out]実際に返される文字数`szName`です。</span><span class="sxs-lookup"><span data-stu-id="87af6-113">[out] The number of characters actually returned in `szName`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="87af6-114">要件</span><span class="sxs-lookup"><span data-stu-id="87af6-114">Requirements</span></span>  
 <span data-ttu-id="87af6-115">**Platform:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="87af6-115">**Platform:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="87af6-116">**ヘッダー:** Cor.h</span><span class="sxs-lookup"><span data-stu-id="87af6-116">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="87af6-117">**ライブラリ:** MsCorEE.dll にリソースとして使用</span><span class="sxs-lookup"><span data-stu-id="87af6-117">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="87af6-118">**.NET framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="87af6-118">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="87af6-119">関連項目</span><span class="sxs-lookup"><span data-stu-id="87af6-119">See Also</span></span>  
 [<span data-ttu-id="87af6-120">IMetaDataDispenserEx インターフェイス</span><span class="sxs-lookup"><span data-stu-id="87af6-120">IMetaDataDispenserEx Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-interface.md)  
 [<span data-ttu-id="87af6-121">IMetaDataDispenser インターフェイス</span><span class="sxs-lookup"><span data-stu-id="87af6-121">IMetaDataDispenser Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-interface.md)