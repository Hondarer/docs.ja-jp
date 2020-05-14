---
ms.openlocfilehash: 7a05f60cf1c04d3d73dadb54541254a83b4ea855
ms.sourcegitcommit: 1cb64b53eb1f253e6a3f53ca9510ef0be1fd06fe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82507088"
---
### <a name="signalr-messagepack-hub-protocol-options-type-changed"></a><span data-ttu-id="d70b8-101">SignalR:MessagePack ハブ プロトコル オプションの種類を変更</span><span class="sxs-lookup"><span data-stu-id="d70b8-101">SignalR: MessagePack Hub Protocol options type changed</span></span>

<span data-ttu-id="d70b8-102">ASP.NET Core SignalR MessagePack ハブ プロトコルのオプションの型が `IList<MessagePack.IFormatterResolver>` から [MessagePack](https://www.nuget.org/packages/MessagePack) ライブラリの `MessagePackSerializerOptions` 型に変更されました。</span><span class="sxs-lookup"><span data-stu-id="d70b8-102">The ASP.NET Core SignalR MessagePack Hub Protocol options type has changed from `IList<MessagePack.IFormatterResolver>` to the [MessagePack](https://www.nuget.org/packages/MessagePack) library's `MessagePackSerializerOptions` type.</span></span>

<span data-ttu-id="d70b8-103">この変更のディスカッションについては、[dotnet/aspnetcore#20506](https://github.com/dotnet/aspnetcore/issues/20506) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d70b8-103">For discussion on this change, see [dotnet/aspnetcore#20506](https://github.com/dotnet/aspnetcore/issues/20506).</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="d70b8-104">導入されたバージョン</span><span class="sxs-lookup"><span data-stu-id="d70b8-104">Version introduced</span></span>

<span data-ttu-id="d70b8-105">5.0 Preview 4</span><span class="sxs-lookup"><span data-stu-id="d70b8-105">5.0 Preview 4</span></span>

#### <a name="old-behavior"></a><span data-ttu-id="d70b8-106">以前の動作</span><span class="sxs-lookup"><span data-stu-id="d70b8-106">Old behavior</span></span>

<span data-ttu-id="d70b8-107">次の例に示されているようにオプションを増やすことができます。</span><span class="sxs-lookup"><span data-stu-id="d70b8-107">You can add to the options as shown in the following example:</span></span>

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.FormatterResolvers.Add(MessagePack.Resolvers.StandardResolver.Instance);
    });
```

<span data-ttu-id="d70b8-108">次のようにオプションを置換してください。</span><span class="sxs-lookup"><span data-stu-id="d70b8-108">And replace the options as follows:</span></span>

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.FormatterResolvers = new List<MessagePack.IFormatterResolver>()
        {
            MessagePack.Resolvers.StandardResolver.Instance
        };
    });
```

#### <a name="new-behavior"></a><span data-ttu-id="d70b8-109">新しい動作</span><span class="sxs-lookup"><span data-stu-id="d70b8-109">New behavior</span></span>

<span data-ttu-id="d70b8-110">次の例に示されているようにオプションを増やすことができます。</span><span class="sxs-lookup"><span data-stu-id="d70b8-110">You can add to the options as shown in the following example:</span></span>

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.SerializerOptions =
            options.SerializeOptions.WithResolver(MessagePack.Resolvers.StandardResolver.Instance);
    });
```

<span data-ttu-id="d70b8-111">次のようにオプションを置換してください。</span><span class="sxs-lookup"><span data-stu-id="d70b8-111">And replace the options as follows:</span></span>

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.SerializerOptions = MessagePackSerializerOptions
                .Standard
                .WithResolver(MessagePack.Resolvers.StandardResolver.Instance)
                .WithSecurity(MessagePackSecurity.UntrustedData);
    });
```

#### <a name="reason-for-change"></a><span data-ttu-id="d70b8-112">変更理由</span><span class="sxs-lookup"><span data-stu-id="d70b8-112">Reason for change</span></span>

<span data-ttu-id="d70b8-113">この変更は [aspnet/Announcements#404](https://github.com/aspnet/Announcements/issues/404) で告知した MessagePack v2.x への以降の一環です。</span><span class="sxs-lookup"><span data-stu-id="d70b8-113">This change is part of moving to MessagePack v2.x, which was announced in [aspnet/Announcements#404](https://github.com/aspnet/Announcements/issues/404).</span></span> <span data-ttu-id="d70b8-114">v2.x ライブラリで追加されたオプション API は使いやすく、以前に公開されていた `MessagePack.IFormatterResolver` のリストより機能が多くなっています。</span><span class="sxs-lookup"><span data-stu-id="d70b8-114">The v2.x library has added an options API that's easier to use and provides more features than the list of `MessagePack.IFormatterResolver` that was exposed before.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="d70b8-115">推奨アクション</span><span class="sxs-lookup"><span data-stu-id="d70b8-115">Recommended action</span></span>

<span data-ttu-id="d70b8-116">この重大な変更は、<xref:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions> で値を構成しているユーザーに影響します。</span><span class="sxs-lookup"><span data-stu-id="d70b8-116">This breaking change affects anyone who is configuring values on <xref:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions>.</span></span> <span data-ttu-id="d70b8-117">ASP.NET Core SignalR MessagePack ハブ プロトコルを使用しているとき、このオプションを変更する場合、上の画像のように新しいオプション API を使用するように使用状況を更新します。</span><span class="sxs-lookup"><span data-stu-id="d70b8-117">If you're using the ASP.NET Core SignalR MessagePack Hub Protocol and modifying the options, update your usage to use the new options API as shown above.</span></span>

#### <a name="category"></a><span data-ttu-id="d70b8-118">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="d70b8-118">Category</span></span>

<span data-ttu-id="d70b8-119">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d70b8-119">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="d70b8-120">影響を受ける API</span><span class="sxs-lookup"><span data-stu-id="d70b8-120">Affected APIs</span></span>

<xref:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions?displayProperty=nameWithType>

<!--

#### Affected APIs

`T:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions`

-->