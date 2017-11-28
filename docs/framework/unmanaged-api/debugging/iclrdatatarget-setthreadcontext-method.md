---
title: "ICLRDataTarget::SetThreadContext メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICLRDataTarget.SetThreadContext
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICLRDataTarget::SetThreadContext
helpviewer_keywords:
- SetThreadContext method, ICLRDataTarget interface [.NET Framework debugging]
- ICLRDataTarget::SetThreadContext method [.NET Framework debugging]
ms.assetid: 103c8502-81fe-40d7-9c1e-9008d8fb19e1
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: e51cbafda76933d58bd60be8db7dd163a2dd59d3
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="iclrdatatargetsetthreadcontext-method"></a><span data-ttu-id="fcff8-102">ICLRDataTarget::SetThreadContext メソッド</span><span class="sxs-lookup"><span data-stu-id="fcff8-102">ICLRDataTarget::SetThreadContext Method</span></span>
<span data-ttu-id="fcff8-103">ターゲット プロセスで指定されたスレッドの現在のコンテキストを設定します。</span><span class="sxs-lookup"><span data-stu-id="fcff8-103">Sets the current context of the specified thread in the target process.</span></span> <span data-ttu-id="fcff8-104">このメソッドは、共通言語ランタイム (CLR) データ アクセス サービスによって呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="fcff8-104">This method is called by the common language runtime (CLR) data access services.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fcff8-105">構文</span><span class="sxs-lookup"><span data-stu-id="fcff8-105">Syntax</span></span>  
  
```  
HRESULT SetThreadContext (  
    [in] ULONG32            threadID,  
    [in] ULONG32            contextSize,  
    [in, size_is(contextSize)]   
         BYTE               *context  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="fcff8-106">パラメーター</span><span class="sxs-lookup"><span data-stu-id="fcff8-106">Parameters</span></span>  
 `threadID`  
 <span data-ttu-id="fcff8-107">[in]ターゲット プロセス内のスレッドのオペレーティング システムの識別子です。</span><span class="sxs-lookup"><span data-stu-id="fcff8-107">[in] The operating system identifier of a thread in the target process.</span></span>  
  
 `contextSize`  
 <span data-ttu-id="fcff8-108">[in]コンテキストのサイズ。</span><span class="sxs-lookup"><span data-stu-id="fcff8-108">[in] The size of the context.</span></span>  
  
 `context`  
 <span data-ttu-id="fcff8-109">[in]コンテキストを格納するバッファーへのポインター。</span><span class="sxs-lookup"><span data-stu-id="fcff8-109">[in] Pointer to a buffer containing the context.</span></span>  
  
 <span data-ttu-id="fcff8-110">内のデータ、`context`バッファーは、Win32 の形式である`CONTEXT`構造体。</span><span class="sxs-lookup"><span data-stu-id="fcff8-110">The data in the `context` buffer will be in the format of the Win32 `CONTEXT` structure.</span></span> <span data-ttu-id="fcff8-111">コンテキストはプロセッサ固有のレジスタのデータを指定するので、Win32 の定義`CONTEXT`構造は、プロセッサのアーキテクチャによって異なります。</span><span class="sxs-lookup"><span data-stu-id="fcff8-111">The context specifies processor-specific register data, so the definition of the Win32 `CONTEXT` structure depends on the processor's architecture.</span></span> <span data-ttu-id="fcff8-112">Win32 の定義については、WinNT.h ヘッダー ファイルを参照してください`CONTEXT`構造体。</span><span class="sxs-lookup"><span data-stu-id="fcff8-112">Refer to the WinNT.h header file for the definition of the Win32 `CONTEXT` structure.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="fcff8-113">コメント</span><span class="sxs-lookup"><span data-stu-id="fcff8-113">Remarks</span></span>  
 <span data-ttu-id="fcff8-114">このメソッドは、デバッグ アプリケーションの作成者によって実装されます。</span><span class="sxs-lookup"><span data-stu-id="fcff8-114">This method is implemented by the writer of the debugging application.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="fcff8-115">要件</span><span class="sxs-lookup"><span data-stu-id="fcff8-115">Requirements</span></span>  
 <span data-ttu-id="fcff8-116">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="fcff8-116">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="fcff8-117">**ヘッダー:** ClrData.idl、ClrData.h</span><span class="sxs-lookup"><span data-stu-id="fcff8-117">**Header:** ClrData.idl, ClrData.h</span></span>  
  
 <span data-ttu-id="fcff8-118">**ライブラリ:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="fcff8-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="fcff8-119">**.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="fcff8-119">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fcff8-120">関連項目</span><span class="sxs-lookup"><span data-stu-id="fcff8-120">See Also</span></span>  
 [<span data-ttu-id="fcff8-121">ICLRDataTarget インターフェイス</span><span class="sxs-lookup"><span data-stu-id="fcff8-121">ICLRDataTarget Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget-interface.md)