---
title: "ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugAppDomain3.GetCachedWinRTTypesForIIDs
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs
helpviewer_keywords:
- ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs method, [.NET Framework debugging]
- GetCachedWinRTTypesForIIDs method, ICorDebugAppDomain3 interface [.NET Framework debugging]
ms.assetid: 23682ca0-1bcf-48e6-996e-69f7ba337682
topic_type: apiref
caps.latest.revision: "5"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 84b58e3a016431eba10710ea384338cb388404ff
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugappdomain3getcachedwinrttypesforiids-method"></a><span data-ttu-id="c35df-102">ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs メソッド</span><span class="sxs-lookup"><span data-stu-id="c35df-102">ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs Method</span></span>
<span data-ttu-id="c35df-103">キャッシュされた列挙子を取得[!INCLUDE[wrt](../../../../includes/wrt-md.md)]アプリケーション ドメイン内の型、インターフェイスの id に基づいています。</span><span class="sxs-lookup"><span data-stu-id="c35df-103">Gets an enumerator for cached [!INCLUDE[wrt](../../../../includes/wrt-md.md)] types in an application domain based on their interface identifiers.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c35df-104">構文</span><span class="sxs-lookup"><span data-stu-id="c35df-104">Syntax</span></span>  
  
```  
HRESULT GetCachedWinRTTypesForIIDs (   
    [in]  ULONG32            cReqTypes,  
    [in]  GUID                *iidsToResolve,  
    [out] ICorDebugTypeEnum   **ppTypesEnum  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="c35df-105">パラメーター</span><span class="sxs-lookup"><span data-stu-id="c35df-105">Parameters</span></span>  
 `cReqTypes`  
 <span data-ttu-id="c35df-106">[in]必要な種類の数。</span><span class="sxs-lookup"><span data-stu-id="c35df-106">[in] The number of required types.</span></span>  
  
 `iidsToResolve`  
 <span data-ttu-id="c35df-107">[in]管理対象の形式に対応するインターフェイスの id を格納している配列へのポインター、[!INCLUDE[wrt](../../../../includes/wrt-md.md)]を取得する型。</span><span class="sxs-lookup"><span data-stu-id="c35df-107">[in] A pointer to an array that contains the interface identifiers corresponding to the managed representations of the [!INCLUDE[wrt](../../../../includes/wrt-md.md)] types to be retrieved.</span></span>  
  
 `ppTypesEnum`  
 <span data-ttu-id="c35df-108">[out]マネージの表現をキャッシュの列挙体をできるようにする"ICorDebugTypeEnum"インターフェイス オブジェクトのアドレスへのポインター、[!INCLUDE[wrt](../../../../includes/wrt-md.md)]にインターフェイス識別子に基づいて、型が取得`iidsToResolve`です。</span><span class="sxs-lookup"><span data-stu-id="c35df-108">[out] A pointer to the address of an "ICorDebugTypeEnum" interface object that allows enumeration of the cached managed representations of the [!INCLUDE[wrt](../../../../includes/wrt-md.md)] types retrieved, based on the interface identifiers in `iidsToResolve`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="c35df-109">コメント</span><span class="sxs-lookup"><span data-stu-id="c35df-109">Remarks</span></span>  
 <span data-ttu-id="c35df-110">"ICorDebugTypeEnum"コレクション内の対応するエントリがの型を持つメソッドは、特定のインターフェイスの識別子の情報を取得できなかった場合、`ELEMENT_TYPE_END`データ取得に関する問題によるエラーのまたは`ELEMENT_TYPE_VOID`の不明なインターフェイス識別子。</span><span class="sxs-lookup"><span data-stu-id="c35df-110">If the method fails to retrieve information for a specific interface identifier, the corresponding entry in the "ICorDebugTypeEnum" collection will have a type of `ELEMENT_TYPE_END` for errors due to data retrieval issues, or `ELEMENT_TYPE_VOID` for unknown interface identifiers.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c35df-111">要件</span><span class="sxs-lookup"><span data-stu-id="c35df-111">Requirements</span></span>  
 <span data-ttu-id="c35df-112">**プラットフォーム:**[!INCLUDE[wrt](../../../../includes/wrt-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c35df-112">**Platforms:** [!INCLUDE[wrt](../../../../includes/wrt-md.md)]</span></span>  
  
 <span data-ttu-id="c35df-113">**ヘッダー:** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="c35df-113">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="c35df-114">**ライブラリ:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="c35df-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="c35df-115">**.NET framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c35df-115">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c35df-116">関連項目</span><span class="sxs-lookup"><span data-stu-id="c35df-116">See Also</span></span>  
 [<span data-ttu-id="c35df-117">ICorDebugAppDomain3 インターフェイス</span><span class="sxs-lookup"><span data-stu-id="c35df-117">ICorDebugAppDomain3 Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain3-interface.md)