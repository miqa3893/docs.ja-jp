---
title: キューに置かれたアプリケーションの Web ホスト
ms.date: 03/30/2017
ms.assetid: c7a539fa-e442-4c08-a7f1-17b7f5a03e88
ms.openlocfilehash: f396ffadeca81d86d867842b63cad3c63d67ff3a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33505050"
---
# <a name="web-hosting-a-queued-application"></a>キューに置かれたアプリケーションの Web ホスト
Windows プロセス アクティブ化サービス (WAS) は、ライセンス認証とアプリケーションを含む Windows Communication Foundation (WCF) サービスをホストするワーカー プロセスの有効期間を管理します。 WAS プロセス モデルは HTTP の依存関係を取り除くことにより、HTTP サーバーの [!INCLUDE[iis601](../../../../includes/iis601-md.md)] プロセス モデルを一般化します。 これにより、HTTP と net.msmq や msmq.formatname、メッセージ ベースのアクティブ化をサポートし、多数の特定のコンピューター上のアプリケーションをホストする機能を提供するホスト環境でなどの非 HTTP プロトコルの両方を使用する WCF サービスです。  
  
 WAS にはメッセージ キュー (MSMQ) アクティブ化サービスが含まれており、アプリケーションで使用されるキューのいずれかに 1 つ以上のメッセージが置かれると、キュー アプリケーションがアクティブ化されます。 MSMQ アクティブ化サービスは、既定で自動的に開始される NT サービスです。  
  
 WAS と利点の詳細については、次を参照してください。 [Windows Process Activation Service でのホスティング](../../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md)です。 MSMQ の詳細については、次を参照してください[キューの概要。](../../../../docs/framework/wcf/feature-details/queues-overview.md)  
  
## <a name="queue-addressing-in-was"></a>WAS でのキュー アドレス指定  
 WAS アプリケーションには URI (Uniform Resource Identifier) アドレスがあります。 アプリケーション アドレスは、ベース URI プレフィックスとアプリケーション固有の相対アドレス (パス) の 2 つの部分に分かれます。 この 2 つの部分を結合すると、アプリケーションの外部アドレスになります。 ベース URI プレフィックスは、サイトのバインドから構築され、たとえば、"net.msmq://localhost"、"msmq.formatname://localhost"、または"net.tcp://localhost など"のサイトの下のすべてのアプリケーションのために使用します。 アプリケーション アドレスは、アプリケーション固有のパス フラグメントを作成し (など"/されて")、ベース uri プレフィックスに追加アプリケーションの完全 URI、たとえば、/applicationone"net.msmq://localhost/applicationone など"とします。  
  
 MSMQ アクティブ化サービスは、アプリケーション URI を使用して、MSMQ アクティブ化サービスでメッセージを監視する必要のあるキューを照会します。 MSMQ アクティブ化サービスを起動すると、受信するように設定したコンピューターのすべてのパブリック キューとプライベート キューが列挙され、そのキューのメッセージが監視されます。 MSMQ アクティブ化サービスは、10 分おきに監視対象のキュー リストを更新します。 キューでメッセージが検出されると、アクティブ化サービスは、キュー名を net.msmq バインディングで一致する最長のアプリケーション URI と一致させ、アプリケーションをアクティブ化します。  
  
> [!NOTE]
>  アクティブ化するアプリケーションは、キュー名のプレフィックスに一致 (最長一致) する必要があります。  
  
 たとえば、msmqWebHost/orderProcessing/service.svc という名前のキューがあるとします。 アプリケーション 1 に仮想ディレクトリ /msmqWebHost/orderProcessing がありその下に service.svc が格納されており、アプリケーション 2 に仮想ディレクトリ /msmqWebHost がありその下に orderProcessing.svc が格納されている場合、アプリケーション 1 がアクティブ化されます。 アプリケーション 1 が削除されると、アプリケーション 2 がアクティブ化されます。  
  
> [!NOTE]
>  キューが作成され、メッセージがそのキューに送信されても、MSMQ アクティブ化サービスがそのキュー リストを更新するまで、アプリケーションはアクティブ化されません。キュー リストが更新されるまでの時間は、キューが作成されてから最大で 10 分です。 アクティブ化サービスを再起動した場合も、キュー リストは更新されます。  
  
### <a name="the-effect-of-private-and-public-queues-on-addressing"></a>アドレスに対するプライベート キューとパブリック キューの影響  
 MSMQ アクティブ化サービスでは、プライベート キューの監視とパブリック キューの監視が区別されません。 したがって、パブリック キューとプライベート キューを同じ名前にすることはできません。 同じ名前の場合、いずれかのキューを読み込んで、Web ホスト アプリケーションがアクティブ化される場合があります。  
  
### <a name="queue-configuration-for-activation"></a>アクティブ化のためのキュー構成  
 MSMQ アクティブ化サービスは、NETWORK SERVICE として動作します。 これは、アプリケーションをアクティブ化するキューを監視するサービスです。 キューからアプリケーションをアクティブ化するようにするには、アクセス制御リスト (ACL) に NETWORK SERVICE アクセス用のキューを指定し、メッセージをピークする必要があります。  
  
### <a name="poison-messaging"></a>有害メッセージ処理  
 有害メッセージ処理 WCF では、だけでなく検出メッセージは有害しますが、ユーザーの構成に基づいて処置を選択すると、チャネルによって処理されます。 そのため、キューには 1 つのメッセージが存在します。 Web ホスト アプリケーションが連続的に中断されると、このメッセージは再試行キューに移動されます。 再試行サイクル遅延により指定された時点で、メッセージは再試行キューからメイン キューに移動されて再試行されます。 ただし、この場合、キューに置かれたチャネルがアクティブである必要があります。 アプリケーションが WAS により再利用される場合、メッセージは、別のメッセージがメイン キューに到着してキューに置かれたアプリケーションがアクティブ化されるまで再試行キューに残ります。 この場合の回避策は、メッセージを再試行キューからメイン キューに手動で戻し、アプリケーションを再アクティブ化することです。  
  
### <a name="subqueue-and-system-queue-caveat"></a>サブキューとシステム キューに関する注意  
 WAS によりホストされるアプリケーションを、システム キュー (システム全体の配信不能キューなど) 内や、サブキュー (有害サブキューなど) 内のメッセージに基づいてアクティブ化することはできません。 これはこのバージョンの製品の制限です。  
  
## <a name="see-also"></a>関連項目  
 [有害メッセージ処理](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)  
 [サービス エンドポイントとキューのアドレス指定](../../../../docs/framework/wcf/feature-details/service-endpoints-and-queue-addressing.md)
