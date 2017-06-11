---
title: "フェデレーションと信頼 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "フェデレーション [WCF], 信頼"
ms.assetid: 4bdec4f2-f8a2-4512-bdcf-14ef54b5877a
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# フェデレーションと信頼
ここでは、[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] におけるフェデレーション アプリケーション、信頼の境界と構成、および発行済みトークンの使用に関連したさまざまな側面について説明します。  
  
## サービス、セキュリティ トークン サービス、および信頼  
 フェデレーション エンドポイントを公開するサービスを使用する場合、通常、特定の発行者によって提供されたトークンを使用してクライアント認証を行う必要があります。そのため、発行者の正しい資格情報を使用してサービスが構成されていることが重要です。そうでないと、サービスは発行済みトークンの署名を検証することができず、クライアントはサービスと通信できません。サービスで発行者の資格情報を構成する方法[!INCLUDE[crabout](../../../../includes/crabout-md.md)]、「[方法 : フェデレーション サービスで資格情報を設定する](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)」を参照してください。  
  
 同様に、対称キーを使用する場合も、キーがターゲット サービス用に暗号化されるため、セキュリティ トークン サービスがターゲット サービスの正しい資格情報で構成される必要があります。そうでないと、セキュリティ トークン サービスはターゲット サービス用にキーを暗号化できないため、この場合も、クライアントはサービスと通信できなくなります。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] サービスでは、[SecurityBindingElement](../../../../docs/framework/wcf/diagnostics/wmi/securitybindingelement.md) にある <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxClockSkew%2A> プロパティの値を使用してクライアントとサービスとの間の時刻のずれを許可します。フェデレーションでは、`MaxClockSkew` 設定が、クライアントと、クライアントが発行済みトークンを取得したセキュリティ トークン サービスの両方の時刻のずれに対して適用されます。そのため、発行済みトークンの有効期間の開始時刻と終了時刻が設定する際、セキュリティ トークン サービスで時刻のずれを許可する必要はありません。  
  
> [!NOTE]
>  時刻のずれの重要性は、発行済みトークンの有効期間が短くなるほど大きくなります。トークンの有効期間が 30 分以上あれば、多くの場合、時刻のずれは大きな問題にはなりません。短い有効期間が使用されるシナリオやトークンの正確な有効時間が重要となるシナリオでは、時刻のずれを考慮に入れて設計する必要があります。  
  
## フェデレーション エンドポイントとタイムアウト  
 クライアントがフェデレーション エンドポイントと通信するときは、最初にセキュリティ トークン サービスから適切なトークンを取得する必要があります。このセキュリティ トークン サービスがフェデレーション エンドポイントを公開している場合、クライアントは最初にそのエンドポイントの発行者からトークンを取得する必要があります。それぞれのトークンの取得には時間がかかり、この時間が実際のメッセージを最終的なエンドポイントに送信するときの全体的なタイムアウトの影響を受けます。  
  
 たとえば、クライアント側チャネルのタイムアウトが 30 秒に設定されているとします。またメッセージを最終的なエンドポイントに送信する前に、トークンを取得するために 2 つのトークン発行者を呼び出す必要があり、それぞれのトークンの発行に 15 秒を要するとします。この場合、この試行は失敗し、<xref:System.TimeoutException> がスローされます。したがって、クライアント チャネルの <xref:System.ServiceModel.IContextChannel.OperationTimeout%2A> 値は、すべての発行済みトークンを取得するのにかかる時間を含めた、十分大きな値に設定する必要があります。<xref:System.ServiceModel.IContextChannel.OperationTimeout%2A> プロパティの値が指定されていない場合、<xref:System.ServiceModel.Channels.Binding.OpenTimeout%2A> プロパティ、または <xref:System.ServiceModel.Channels.Binding.SendTimeout%2A> プロパティ \(あるいはその両方\) を、すべての発行済みトークンを取得するのにかかる時間を含めた、十分大きな値に設定する必要があります。  
  
## トークンの有効期間と更新  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] クライアントは、サービスへの最初の要求を行う際に発行済みトークンのチェックを行いません。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] では、セキュリティ トークン サービスによって適切な有効期間を持つトークンが発行されることが信頼されています。トークンがクライアントによってキャッシュされて再使用される場合は、トークンの有効期間が、後続する要求によってチェックされ、クライアントは必要に応じてトークンを自動的に更新します。トークンのキャッシュ[!INCLUDE[crabout](../../../../includes/crabout-md.md)]、「[方法 : フェデレーション クライアントを作成する](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)」を参照してください。  
  
 発行済みトークンまたはセキュリティ コンテキスト トークンに対して、30 秒以下などの短い有効期間を指定すると、発行済みトークンを要求したり、セキュリティ コンテキスト トークンのネゴシエーションや更新を行ったりした場合に、ネゴシエーションのタイムアウトやその他の例外が [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] クライアントによってスローされることがあります。  
  
## 発行済みトークンと InclusionMode  
 クライアントからフェデレーション エンドポイントに送信されたメッセージで発行済みトークンがシリアル化されるかどうかは、<xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters> クラスの <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.InclusionMode%2A> プロパティを設定することによって制御します。このプロパティは <xref:System.ServiceModel.Security.Tokens.SecurityTokenInclusionMode> 列挙値のいずれかに設定できますが、これはほとんどのフェデレーション シナリオでは役に立ちません。`SecurityTokenInclusionMode.Never` 値および `SecurityTokenInclusionMode.AlwaysToInitiator` 値を設定すると、クライアントによって、セキュリティ トークンサービスによって発行されたトークンへの参照が証明書利用者に送信されます。証明書利用者がこの発行済みトークンのコピーを持っていない限り、トークン参照が解決されないため、認証は失敗します。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] では `SecurityTokenInclusionMode.Once` を `SecurityTokenInclusionMode.AlwaysToRecipient` と等価のものとして扱います。  
  
## 参照  
 <xref:System.ServiceModel.Security.Tokens.SecurityTokenInclusionMode>   
 [方法 : フェデレーション クライアントを作成する](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)   
 [方法 : フェデレーション サービスで資格情報を設定する](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)   
 [方法 : WSFederationHttpBinding を作成する](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)