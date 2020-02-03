---
title: クラウドネイティブアプリケーションでのキャッシュ
description: クラウドネイティブアプリケーションでのキャッシュ戦略について説明します。
author: robvet
ms.date: 01/22/2020
ms.openlocfilehash: 2da61a01fc53233d1934df813fcba3b91a495c43
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2020
ms.locfileid: "76795117"
---
# <a name="caching-in-a-cloud-native-app"></a><span data-ttu-id="22ee0-103">クラウドネイティブアプリでのキャッシュ</span><span class="sxs-lookup"><span data-stu-id="22ee0-103">Caching in a cloud-native app</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="22ee0-104">キャッシュの利点はよく理解されています。</span><span class="sxs-lookup"><span data-stu-id="22ee0-104">The benefits of caching are well understood.</span></span> <span data-ttu-id="22ee0-105">この手法は、頻繁にアクセスされるデータをバックエンドデータストアから、アプリケーションの近くにある*高速ストレージ*に一時的にコピーすることによって機能します。</span><span class="sxs-lookup"><span data-stu-id="22ee0-105">The technique works by temporarily copying frequently accessed data from a backend data store to *fast storage* that's located closer to the application.</span></span> <span data-ttu-id="22ee0-106">キャッシュは、多くの場合に実装されます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-106">Caching is often implemented where...</span></span>

- <span data-ttu-id="22ee0-107">データは比較的静的なままです。</span><span class="sxs-lookup"><span data-stu-id="22ee0-107">Data remains relatively static.</span></span>
- <span data-ttu-id="22ee0-108">特にキャッシュの速度と比較して、データアクセスは低速です。</span><span class="sxs-lookup"><span data-stu-id="22ee0-108">Data access is slow, especially compared to the speed of the cache.</span></span>
- <span data-ttu-id="22ee0-109">データは高レベルの競合の影響を受けます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-109">Data is subject to high levels of contention.</span></span>

## <a name="why"></a><span data-ttu-id="22ee0-110">その理由については、</span><span class="sxs-lookup"><span data-stu-id="22ee0-110">Why?</span></span>

<span data-ttu-id="22ee0-111">「 [Microsoft キャッシュのガイダンス](https://docs.microsoft.com/azure/architecture/best-practices/caching)」で説明されているように、キャッシュを使用すると、個々のマイクロサービスとシステム全体のパフォーマンス、スケーラビリティ、および可用性を向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-111">As discussed in the [Microsoft caching guidance](https://docs.microsoft.com/azure/architecture/best-practices/caching), caching can increase performance, scalability, and availability for individual microservices and the system as a whole.</span></span> <span data-ttu-id="22ee0-112">これにより、データストアに対する大量の同時要求を処理する際の待機時間と競合が軽減されます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-112">It reduces the latency and contention of handling large volumes of concurrent requests to a data store.</span></span> <span data-ttu-id="22ee0-113">データ量とユーザー数が増えるにつれて、キャッシュの利点が大きくなります。</span><span class="sxs-lookup"><span data-stu-id="22ee0-113">As data volume and the number of users increase, the greater the benefits of caching become.</span></span>

<span data-ttu-id="22ee0-114">キャッシュは、不変のデータまたは変更頻度の低いデータをクライアントが繰り返し読み取る場合に最も効果的です。</span><span class="sxs-lookup"><span data-stu-id="22ee0-114">Caching is most effective when a client repeatedly reads data that is immutable or that changes infrequently.</span></span> <span data-ttu-id="22ee0-115">例としては、製品や価格情報などの参照情報や、構築するのにコストがかかる共有静的リソースなどがあります。</span><span class="sxs-lookup"><span data-stu-id="22ee0-115">Examples include reference information such as product and pricing information, or shared static resources that are costly to construct.</span></span>

<span data-ttu-id="22ee0-116">マイクロサービスはステートレスである必要がありますが、分散キャッシュは、必要に応じてセッション状態データへの同時アクセスをサポートできます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-116">While microservices should be stateless, a distributed cache can support concurrent access to session state data when absolutely required.</span></span>

<span data-ttu-id="22ee0-117">また、繰り返し計算が行われないようにキャッシュを検討してください。</span><span class="sxs-lookup"><span data-stu-id="22ee0-117">Also consider caching to avoid repetitive computations.</span></span> <span data-ttu-id="22ee0-118">操作でデータを変換したり、複雑な計算を実行したりする場合は、後続の要求の結果をキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="22ee0-118">If an operation transforms data or performs a complicated calculation, cache the result for subsequent requests.</span></span>

## <a name="caching-architecture"></a><span data-ttu-id="22ee0-119">キャッシュアーキテクチャ</span><span class="sxs-lookup"><span data-stu-id="22ee0-119">Caching architecture</span></span>

<span data-ttu-id="22ee0-120">クラウドネイティブアプリケーションは、通常、分散キャッシュアーキテクチャを実装します。</span><span class="sxs-lookup"><span data-stu-id="22ee0-120">Cloud native applications typically implement a distributed caching architecture.</span></span> <span data-ttu-id="22ee0-121">キャッシュは、マイクロサービスとは別に、クラウドベースの[バッキングサービス](./definition.md#backing-services)としてホストされます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-121">The cache is hosted as a cloud-based [backing service](./definition.md#backing-services), separate from the microservices.</span></span> <span data-ttu-id="22ee0-122">図5-20 にアーキテクチャを示します。</span><span class="sxs-lookup"><span data-stu-id="22ee0-122">Figure 5-20 shows the architecture.</span></span>

![クラウドネイティブアプリでのキャッシュ](media/caching-in-a-cloud-native-app.png)

<span data-ttu-id="22ee0-124">**図 5-19**: クラウドネイティブアプリでのキャッシュ</span><span class="sxs-lookup"><span data-stu-id="22ee0-124">**Figure 5-19**: Caching in a cloud native app</span></span>

<span data-ttu-id="22ee0-125">前の図では、キャッシュがマイクロサービスに依存せず、共有されていることに注目してください。</span><span class="sxs-lookup"><span data-stu-id="22ee0-125">In the previous figure, note how the cache is independent of and shared by the microservices.</span></span> <span data-ttu-id="22ee0-126">このシナリオでは、キャッシュは[API ゲートウェイ](./front-end-communication.md)によって呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-126">In this scenario, the cache is invoked by the [API Gateway](./front-end-communication.md).</span></span> <span data-ttu-id="22ee0-127">第4章で説明したように、ゲートウェイはすべての受信要求のフロントエンドとして機能します。</span><span class="sxs-lookup"><span data-stu-id="22ee0-127">As discussed in chapter 4, the gateway serves as a front end for all incoming requests.</span></span> <span data-ttu-id="22ee0-128">分散キャッシュは、可能な限りキャッシュされたデータを返すことによって、システムの応答性を高めます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-128">The distributed cache increases system responsiveness by returning cached data whenever possible.</span></span> <span data-ttu-id="22ee0-129">さらに、サービスからキャッシュを分離することで、増加したトラフィック要求に合わせてキャッシュを個別にスケールアップまたはスケールアウトすることができます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-129">Additionally, separating the cache from the services allows the cache to scale up or out independently to meet increased traffic demands.</span></span>

<span data-ttu-id="22ee0-130">この図は、[キャッシュアサイドパターン](https://docs.microsoft.com/azure/architecture/patterns/cache-aside)と呼ばれる一般的なキャッシュパターンを示しています。</span><span class="sxs-lookup"><span data-stu-id="22ee0-130">The figure presents a common caching pattern known as the [cache-aside pattern](https://docs.microsoft.com/azure/architecture/patterns/cache-aside).</span></span> <span data-ttu-id="22ee0-131">受信要求の場合は、最初にキャッシュを照会し (手順 \#1)、応答を確認します。</span><span class="sxs-lookup"><span data-stu-id="22ee0-131">For an incoming request, you first query the cache (step \#1) for a response.</span></span> <span data-ttu-id="22ee0-132">見つかった場合は、すぐにデータが返されます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-132">If found, the data is returned immediately.</span></span> <span data-ttu-id="22ee0-133">データがキャッシュに存在しない場合 ([キャッシュミス](https://www.techopedia.com/definition/6308/cache-miss)とも呼ばれます)、ダウンストリームサービスのローカルデータベースから取得されます (手順 \#2)。</span><span class="sxs-lookup"><span data-stu-id="22ee0-133">If the data doesn't exist in the cache (known as a [cache miss](https://www.techopedia.com/definition/6308/cache-miss)), it's retrieved from a local database in a downstream service (step \#2).</span></span> <span data-ttu-id="22ee0-134">その後、後続の要求のためにキャッシュに書き込まれ (ステップ \#3)、呼び出し元に返されます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-134">It's then written to the cache for future requests (step \#3), and returned to the caller.</span></span> <span data-ttu-id="22ee0-135">キャッシュされたデータを定期的に削除して、システムが適時かつ一貫した状態になるように注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="22ee0-135">Care must be taken to periodically evict cached data so that the system remains timely and consistent.</span></span>

<span data-ttu-id="22ee0-136">共有キャッシュが大きくなるにつれて、データを複数のノードにパーティション分割する方が有益な場合があります。</span><span class="sxs-lookup"><span data-stu-id="22ee0-136">As a shared cache grows, it might prove beneficial to partition its data across multiple nodes.</span></span> <span data-ttu-id="22ee0-137">これにより、競合を最小限に抑えてスケーラビリティを向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-137">Doing so can help minimize contention and improve scalability.</span></span> <span data-ttu-id="22ee0-138">多くのキャッシュサービスでは、ノードを動的に追加および削除したり、パーティション間でデータを再調整したりする機能がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="22ee0-138">Many Caching services support the ability to dynamically add and remove nodes and rebalance data across partitions.</span></span> <span data-ttu-id="22ee0-139">このアプローチには、通常、クラスタリングが含まれます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-139">This approach typically involves clustering.</span></span> <span data-ttu-id="22ee0-140">クラスタリングでは、シームレスな単一のキャッシュとして、フェデレーションノードのコレクションが公開されます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-140">Clustering exposes a collection of federated nodes as a seamless, single cache.</span></span> <span data-ttu-id="22ee0-141">ただし、内部的には、負荷を均等に分散する定義済みのディストリビューション戦略に従って、データがノード間で分散されます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-141">Internally, however, the data is dispersed across the nodes following a predefined distribution strategy that balances the load evenly.</span></span>

## <a name="azure-cache-for-redis"></a><span data-ttu-id="22ee0-142">Redis 用 Azure キャッシュ</span><span class="sxs-lookup"><span data-stu-id="22ee0-142">Azure Cache for Redis</span></span>

<span data-ttu-id="22ee0-143">[Redis 用 Azure cache](https://azure.microsoft.com/services/cache/)は、セキュリティで保護されたデータキャッシュとメッセージングブローカーサービスであり、Microsoft によって完全に管理されています。</span><span class="sxs-lookup"><span data-stu-id="22ee0-143">[Azure Cache for Redis](https://azure.microsoft.com/services/cache/) is a secure data caching and messaging broker service, fully managed by Microsoft.</span></span> <span data-ttu-id="22ee0-144">サービスとしてのプラットフォーム (PaaS) として使用され、データへの高スループットと待機時間の短いアクセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="22ee0-144">Consumed as a Platform as a Service (PaaS) offering, it provides high throughput and low-latency access to data.</span></span> <span data-ttu-id="22ee0-145">Azure の内部または外部のアプリケーションは、サービスにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-145">The service is accessible to any application within or outside of Azure.</span></span>

<span data-ttu-id="22ee0-146">Redis サービス用の Azure キャッシュは、Azure データセンター間でホストされているオープンソースの Redis サーバーへのアクセスを管理します。</span><span class="sxs-lookup"><span data-stu-id="22ee0-146">The Azure Cache for Redis service manages access to open-source Redis servers hosted across Azure data centers.</span></span> <span data-ttu-id="22ee0-147">このサービスは、管理、アクセス制御、およびセキュリティを提供するファサードとして機能します。</span><span class="sxs-lookup"><span data-stu-id="22ee0-147">The service acts as a facade providing management, access control, and security.</span></span> <span data-ttu-id="22ee0-148">サービスは、文字列、ハッシュ、リスト、セットなどの豊富なデータ構造のセットをネイティブでサポートしています。</span><span class="sxs-lookup"><span data-stu-id="22ee0-148">The service natively supports a rich set of data structures, including strings, hashes, lists, and sets.</span></span> <span data-ttu-id="22ee0-149">アプリケーションが既に Redis を使用している場合、Redis の Azure Cache と同様に動作します。</span><span class="sxs-lookup"><span data-stu-id="22ee0-149">If your application already uses Redis, it will work as-is with Azure Cache for Redis.</span></span>

<span data-ttu-id="22ee0-150">Redis の Azure Cache は、単純なキャッシュサーバーを超えています。</span><span class="sxs-lookup"><span data-stu-id="22ee0-150">Azure Cache for Redis is more than a simple cache server.</span></span> <span data-ttu-id="22ee0-151">マイクロサービスアーキテクチャを強化するためのさまざまなシナリオをサポートできます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-151">It can support a number of scenarios to enhance a microservices architecture:</span></span>

- <span data-ttu-id="22ee0-152">メモリ内データストア</span><span class="sxs-lookup"><span data-stu-id="22ee0-152">An in-memory data store</span></span>
- <span data-ttu-id="22ee0-153">分散型の非リレーショナルデータベース</span><span class="sxs-lookup"><span data-stu-id="22ee0-153">A distributed non-relational database</span></span>
- <span data-ttu-id="22ee0-154">メッセージブローカー</span><span class="sxs-lookup"><span data-stu-id="22ee0-154">A message broker</span></span>
- <span data-ttu-id="22ee0-155">構成サーバーまたは検出サーバー</span><span class="sxs-lookup"><span data-stu-id="22ee0-155">A configuration or discovery server</span></span>
  
<span data-ttu-id="22ee0-156">高度なシナリオでは、キャッシュされたデータのコピーを[ディスクに保存](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-premium-persistence)できます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-156">For advanced scenarios, a copy of the cached data can be [persisted to disk](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-premium-persistence).</span></span> <span data-ttu-id="22ee0-157">致命的なイベントがプライマリキャッシュとレプリカキャッシュの両方を無効にすると、キャッシュは最新のスナップショットから再構築されます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-157">If a catastrophic event disables both the primary and replica caches, the cache is reconstructed from the most recent snapshot.</span></span>

<span data-ttu-id="22ee0-158">Azure Redis Cache は、いくつかの定義済みの構成と価格レベルで利用できます。</span><span class="sxs-lookup"><span data-stu-id="22ee0-158">Azure Redis Cache is available across a number of predefined configurations and pricing tiers.</span></span>  <span data-ttu-id="22ee0-159">[Premium](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-premium-tier-intro)レベルでは、クラスタリング、データの永続性、geo レプリケーション、仮想ネットワークの分離など、多くのエンタープライズレベルの機能が機能します。</span><span class="sxs-lookup"><span data-stu-id="22ee0-159">The [Premium tier](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-premium-tier-intro) features many enterprise-level features such as clustering, data persistence, geo-replication, and virtual-network isolation.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="22ee0-160">[前へ](relational-vs-nosql-data.md)
>[次へ](elastic-search-in-azure.md)</span><span class="sxs-lookup"><span data-stu-id="22ee0-160">[Previous](relational-vs-nosql-data.md)
[Next](elastic-search-in-azure.md)</span></span>