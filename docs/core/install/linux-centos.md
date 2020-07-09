---
title: CentOS に .NET Core をインストールする - .NET Core
description: CentOS に .NET Core SDK と .NET Core ランタイムをインストールするさまざまな方法を示します。
author: adegeo
ms.author: adegeo
ms.date: 06/04/2020
ms.openlocfilehash: 6b1bad3a6c967483bb683866de84c9e5077a336f
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619508"
---
# <a name="install-net-core-sdk-or-net-core-runtime-on-centos"></a><span data-ttu-id="469c2-103">CentOS に .NET Core SDK または .NET Core ランタイムをインストールする</span><span class="sxs-lookup"><span data-stu-id="469c2-103">Install .NET Core SDK or .NET Core Runtime on CentOS</span></span>

<span data-ttu-id="469c2-104">.NET Core は CentOS でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="469c2-104">.NET Core is supported on CentOS.</span></span> <span data-ttu-id="469c2-105">この記事では、CentOS に .NET Core をインストールする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="469c2-105">This article describes how to install .NET Core on CentOS.</span></span>

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="supported-distributions"></a><span data-ttu-id="469c2-106">サポートされているディストリビューション</span><span class="sxs-lookup"><span data-stu-id="469c2-106">Supported distributions</span></span>

<span data-ttu-id="469c2-107">次の表は、CentOS 7 と CentOS 8 の両方で現在サポートされている .NET Core リリースの一覧です。</span><span class="sxs-lookup"><span data-stu-id="469c2-107">The following table is a list of currently supported .NET Core releases on both CentOS 7 and CentOS 8.</span></span> <span data-ttu-id="469c2-108">これらのバージョンは、[.NET Core のバージョンがサポート終了になる](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)か、CentOS のバージョンがサポート終了になるまでサポートされます。</span><span class="sxs-lookup"><span data-stu-id="469c2-108">These versions remain supported until either the version of [.NET Core reaches end-of-support](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) or the version of CentOS is no longer supported.</span></span>

- <span data-ttu-id="469c2-109">✔️ は、CentOS または .NET Core のバージョンがまだサポートされていることを示します。</span><span class="sxs-lookup"><span data-stu-id="469c2-109">A ✔️ indicates that the version of CentOS or .NET Core is still supported.</span></span>
- <span data-ttu-id="469c2-110">❌ は、CentOS または .NET Core のバージョンがその CentOS のリリースではサポートされていないことを示しています。</span><span class="sxs-lookup"><span data-stu-id="469c2-110">A ❌ indicates that the version of CentOS or .NET Core isn't supported on that CentOS release.</span></span>
- <span data-ttu-id="469c2-111">CentOS のバージョンと .NET Core のバージョンの両方に ✔️ が付いている場合、その OS と .NET の組み合わせはサポートされています。</span><span class="sxs-lookup"><span data-stu-id="469c2-111">When both a version of CentOS and a version of .NET Core have ✔️, that OS and .NET combination are supported.</span></span>

| <span data-ttu-id="469c2-112">CentOS</span><span class="sxs-lookup"><span data-stu-id="469c2-112">CentOS</span></span>                   | <span data-ttu-id="469c2-113">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="469c2-113">.NET Core 2.1</span></span> | <span data-ttu-id="469c2-114">.NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="469c2-114">.NET Core 3.1</span></span> | <span data-ttu-id="469c2-115">.NET 5 Preview (手動インストールのみ)</span><span class="sxs-lookup"><span data-stu-id="469c2-115">.NET 5 Preview (manual install only)</span></span> |
|--------------------------|---------------|---------------|----------------|
| <span data-ttu-id="469c2-116">✔️ [8](#centos-8-)</span><span class="sxs-lookup"><span data-stu-id="469c2-116">✔️ [8](#centos-8-)</span></span> | <span data-ttu-id="469c2-117">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="469c2-117">✔️ 2.1</span></span>        | <span data-ttu-id="469c2-118">✔️ 3.1</span><span class="sxs-lookup"><span data-stu-id="469c2-118">✔️ 3.1</span></span>        | <span data-ttu-id="469c2-119">✔️ 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="469c2-119">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="469c2-120">✔️ [7](#centos-7-)</span><span class="sxs-lookup"><span data-stu-id="469c2-120">✔️ [7](#centos-7-)</span></span> | <span data-ttu-id="469c2-121">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="469c2-121">✔️ 2.1</span></span>        | <span data-ttu-id="469c2-122">✔️ 3.1</span><span class="sxs-lookup"><span data-stu-id="469c2-122">✔️ 3.1</span></span>        | <span data-ttu-id="469c2-123">✔️ 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="469c2-123">✔️ 5.0 Preview</span></span> |

<span data-ttu-id="469c2-124">次のバージョンの .NET Core は、サポート対象外となりました。</span><span class="sxs-lookup"><span data-stu-id="469c2-124">The following versions of .NET Core are no longer supported.</span></span> <span data-ttu-id="469c2-125">これらのダウンロードは、まだ公開されています。</span><span class="sxs-lookup"><span data-stu-id="469c2-125">The downloads for these still remain published:</span></span>

- <span data-ttu-id="469c2-126">3.0</span><span class="sxs-lookup"><span data-stu-id="469c2-126">3.0</span></span>
- <span data-ttu-id="469c2-127">2.2</span><span class="sxs-lookup"><span data-stu-id="469c2-127">2.2</span></span>
- <span data-ttu-id="469c2-128">2.0</span><span class="sxs-lookup"><span data-stu-id="469c2-128">2.0</span></span>

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="how-to-install-other-versions"></a><span data-ttu-id="469c2-129">その他のバージョンをインストールする方法</span><span class="sxs-lookup"><span data-stu-id="469c2-129">How to install other versions</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="centos-8-"></a><span data-ttu-id="469c2-130">CentOS 8 ✔️</span><span class="sxs-lookup"><span data-stu-id="469c2-130">CentOS 8 ✔️</span></span>

<span data-ttu-id="469c2-131">.NET Core 3.1 は CentOS 8 の既定のパッケージ リポジトリで利用できます。</span><span class="sxs-lookup"><span data-stu-id="469c2-131">.NET Core 3.1 is available in the default package repositories for CentOS 8.</span></span>

[!INCLUDE [linux-dnf-install-31](includes/linux-install-31-dnf.md)]

## <a name="centos-7-"></a><span data-ttu-id="469c2-132">CentOS 7 ✔️</span><span class="sxs-lookup"><span data-stu-id="469c2-132">CentOS 7 ✔️</span></span>

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
```

[!INCLUDE [linux-yum-install-31](includes/linux-install-31-yum.md)]

## <a name="troubleshoot-the-package-manager"></a><span data-ttu-id="469c2-133">パッケージ マネージャーのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="469c2-133">Troubleshoot the package manager</span></span>

<span data-ttu-id="469c2-134">このセクションでは、パッケージ マネージャーを使用して .NET Core をインストールするときに発生する可能性のある一般的なエラーについて説明します。</span><span class="sxs-lookup"><span data-stu-id="469c2-134">This section provides information on common errors you may get while using the package manager to install .NET Core.</span></span>

### <a name="failed-to-fetch"></a><span data-ttu-id="469c2-135">フェッチできない</span><span class="sxs-lookup"><span data-stu-id="469c2-135">Failed to fetch</span></span>

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]

## <a name="snap"></a><span data-ttu-id="469c2-136">Snap</span><span class="sxs-lookup"><span data-stu-id="469c2-136">Snap</span></span>

[!INCLUDE [linux-install-snap](includes/linux-install-snap.md)]

## <a name="dependencies"></a><span data-ttu-id="469c2-137">依存関係</span><span class="sxs-lookup"><span data-stu-id="469c2-137">Dependencies</span></span>

[!INCLUDE [linux-rpm-install-dependencies](includes/linux-rpm-install-dependencies.md)]

## <a name="scripted-install"></a><span data-ttu-id="469c2-138">スクリプトでのインストール</span><span class="sxs-lookup"><span data-stu-id="469c2-138">Scripted install</span></span>

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a><span data-ttu-id="469c2-139">手動インストール</span><span class="sxs-lookup"><span data-stu-id="469c2-139">Manual install</span></span>

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a><span data-ttu-id="469c2-140">次の手順</span><span class="sxs-lookup"><span data-stu-id="469c2-140">Next steps</span></span>

- [<span data-ttu-id="469c2-141">チュートリアル: Visual Studio Code を使用して .NET Core SDK でコンソール アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="469c2-141">Tutorial: Create a console application with .NET Core SDK using Visual Studio Code</span></span>](../tutorials/with-visual-studio-code.md)