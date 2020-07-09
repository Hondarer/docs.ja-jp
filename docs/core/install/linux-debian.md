---
title: Debian に .NET Core をインストールする - .NET Core
description: Debian に .NET Core SDK と .NET Core ランタイムをインストールするさまざまな方法を示します。
author: adegeo
ms.author: adegeo
ms.date: 06/04/2020
ms.openlocfilehash: 68a3e848b3d80806e875dfb2fb7e2cbf223f8ad5
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619495"
---
# <a name="install-net-core-sdk-or-net-core-runtime-on-debian"></a><span data-ttu-id="9a29b-103">Debian に .NET Core SDK または .NET Core ランタイムをインストールする</span><span class="sxs-lookup"><span data-stu-id="9a29b-103">Install .NET Core SDK or .NET Core Runtime on Debian</span></span>

<span data-ttu-id="9a29b-104">この記事では、Debian に .NET Core をインストールする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="9a29b-104">This article describes how to install .NET Core on Debian.</span></span> <span data-ttu-id="9a29b-105">Debian のバージョンがサポート対象外である場合、.NET Core もそのバージョンでサポート対象外となります。</span><span class="sxs-lookup"><span data-stu-id="9a29b-105">When a Debian version falls out of support, .NET Core is no longer supported with that version.</span></span> <span data-ttu-id="9a29b-106">ただし、サポートされていない場合でも、以下の手順はそれらのバージョンで実行される .NET Core の取得に役立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="9a29b-106">However, these instructions may help you to get .NET Core running on those versions, even though it isn't supported.</span></span>

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="supported-distributions"></a><span data-ttu-id="9a29b-107">サポートされているディストリビューション</span><span class="sxs-lookup"><span data-stu-id="9a29b-107">Supported distributions</span></span>

<span data-ttu-id="9a29b-108">次の表は、現在サポートされている .NET Core リリースと、それらがサポートされている Debian のバージョンの一覧です。</span><span class="sxs-lookup"><span data-stu-id="9a29b-108">The following table is a list of currently supported .NET Core releases and the versions of Debian they're supported on.</span></span> <span data-ttu-id="9a29b-109">これらのバージョンは、[.NET Core のバージョンがサポート終了になる](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)か、[Debian のバージョンがサポート終了になる](https://wiki.debian.org/DebianReleases)までサポートされます。</span><span class="sxs-lookup"><span data-stu-id="9a29b-109">These versions remain supported until either the version of [.NET Core reaches end-of-support](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) or the version of [Debian reaches end-of-life](https://wiki.debian.org/DebianReleases).</span></span>

- <span data-ttu-id="9a29b-110">✔️ は、Debian または .NET Core のバージョンがまだサポートされていることを示します。</span><span class="sxs-lookup"><span data-stu-id="9a29b-110">A ✔️ indicates that the version of Debian or .NET Core is still supported.</span></span>
- <span data-ttu-id="9a29b-111">❌ は、Debian または .NET Core のバージョンがその Debian のリリースではサポートされていないことを示しています。</span><span class="sxs-lookup"><span data-stu-id="9a29b-111">A ❌ indicates that the version of Debian or .NET Core isn't supported on that Debian release.</span></span>
- <span data-ttu-id="9a29b-112">Debian のバージョンと .NET Core のバージョンの両方に ✔️ が付いている場合、その OS と .NET の組み合わせはサポートされています。</span><span class="sxs-lookup"><span data-stu-id="9a29b-112">When both a version of Debian and a version of .NET Core have ✔️, that OS and .NET combination are supported.</span></span>

| <span data-ttu-id="9a29b-113">Debian</span><span class="sxs-lookup"><span data-stu-id="9a29b-113">Debian</span></span>                   | <span data-ttu-id="9a29b-114">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="9a29b-114">.NET Core 2.1</span></span> | <span data-ttu-id="9a29b-115">.NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="9a29b-115">.NET Core 3.1</span></span> | <span data-ttu-id="9a29b-116">.NET 5 Preview (手動インストールのみ)</span><span class="sxs-lookup"><span data-stu-id="9a29b-116">.NET 5 Preview (manual install only)</span></span> |
|--------------------------|---------------|---------------|----------------|
| <span data-ttu-id="9a29b-117">✔️ [10](#debian-10-)</span><span class="sxs-lookup"><span data-stu-id="9a29b-117">✔️ [10](#debian-10-)</span></span>     | <span data-ttu-id="9a29b-118">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="9a29b-118">✔️ 2.1</span></span>        | <span data-ttu-id="9a29b-119">✔️ 3.1</span><span class="sxs-lookup"><span data-stu-id="9a29b-119">✔️ 3.1</span></span>        | <span data-ttu-id="9a29b-120">✔️ 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="9a29b-120">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="9a29b-121">✔️ [9](#debian-9-)</span><span class="sxs-lookup"><span data-stu-id="9a29b-121">✔️ [9](#debian-9-)</span></span>       | <span data-ttu-id="9a29b-122">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="9a29b-122">✔️ 2.1</span></span>        | <span data-ttu-id="9a29b-123">✔️ 3.1</span><span class="sxs-lookup"><span data-stu-id="9a29b-123">✔️ 3.1</span></span>        | <span data-ttu-id="9a29b-124">✔️ 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="9a29b-124">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="9a29b-125">❌ [8](#debian-8-)</span><span class="sxs-lookup"><span data-stu-id="9a29b-125">❌ [8](#debian-8-)</span></span>       | <span data-ttu-id="9a29b-126">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="9a29b-126">✔️ 2.1</span></span>        | <span data-ttu-id="9a29b-127">❌ 3.1</span><span class="sxs-lookup"><span data-stu-id="9a29b-127">❌ 3.1</span></span>        | <span data-ttu-id="9a29b-128">❌ 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="9a29b-128">❌ 5.0 Preview</span></span> |

<span data-ttu-id="9a29b-129">次のバージョンの .NET Core は、サポート対象外となりました。</span><span class="sxs-lookup"><span data-stu-id="9a29b-129">The following versions of .NET Core are no longer supported.</span></span> <span data-ttu-id="9a29b-130">これらのダウンロードは、まだ公開されています。</span><span class="sxs-lookup"><span data-stu-id="9a29b-130">The downloads for these still remain published:</span></span>

- <span data-ttu-id="9a29b-131">3.0</span><span class="sxs-lookup"><span data-stu-id="9a29b-131">3.0</span></span>
- <span data-ttu-id="9a29b-132">2.2</span><span class="sxs-lookup"><span data-stu-id="9a29b-132">2.2</span></span>
- <span data-ttu-id="9a29b-133">2.0</span><span class="sxs-lookup"><span data-stu-id="9a29b-133">2.0</span></span>

## <a name="how-to-install-other-versions"></a><span data-ttu-id="9a29b-134">その他のバージョンをインストールする方法</span><span class="sxs-lookup"><span data-stu-id="9a29b-134">How to install other versions</span></span>

[!INCLUDE [hack-pkgname](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="debian-10-"></a><span data-ttu-id="9a29b-135">Debian 10 ✔️</span><span class="sxs-lookup"><span data-stu-id="9a29b-135">Debian 10 ✔️</span></span>

[!INCLUDE [linux-prep-intro-apt](includes/linux-prep-intro-apt.md)]

```bash
wget https://packages.microsoft.com/config/debian/10/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
dpkg -i packages-microsoft-prod.deb
```

[!INCLUDE [linux-apt-install-31](includes/linux-install-31-apt.md)]

## <a name="debian-9-"></a><span data-ttu-id="9a29b-136">Debian 9 ✔️</span><span class="sxs-lookup"><span data-stu-id="9a29b-136">Debian 9 ✔️</span></span>

[!INCLUDE [linux-prep-intro-apt](includes/linux-prep-intro-apt.md)]

```bash
wget -O - https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg
sudo mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/
wget https://packages.microsoft.com/config/debian/9/prod.list
sudo mv prod.list /etc/apt/sources.list.d/microsoft-prod.list
sudo chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg
sudo chown root:root /etc/apt/sources.list.d/microsoft-prod.list
```

[!INCLUDE [linux-apt-install-31](includes/linux-install-31-apt.md)]

## <a name="debian-8-"></a><span data-ttu-id="9a29b-137">Debian 8 ❌</span><span class="sxs-lookup"><span data-stu-id="9a29b-137">Debian 8 ❌</span></span>

[!INCLUDE [linux-not-supported](includes/linux-not-supported-debian.md)]

[!INCLUDE [linux-prep-intro-apt](includes/linux-prep-intro-apt.md)]

```bash
wget -O - https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg
sudo mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/
wget https://packages.microsoft.com/config/debian/8/prod.list
sudo mv prod.list /etc/apt/sources.list.d/microsoft-prod.list
sudo chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg
sudo chown root:root /etc/apt/sources.list.d/microsoft-prod.list
```

[!INCLUDE [linux-apt-install-21](includes/linux-install-21-apt.md)]

## <a name="apt-update-sdk-or-runtime"></a><span data-ttu-id="9a29b-138">APT での SDK またはランタイムの更新</span><span class="sxs-lookup"><span data-stu-id="9a29b-138">APT update SDK or runtime</span></span>

<span data-ttu-id="9a29b-139">.NET Core で新しい修正プログラムのリリースを利用できる場合は、次のコマンドを使用して、APT で簡単にアップグレードすることができます。</span><span class="sxs-lookup"><span data-stu-id="9a29b-139">When a new patch release is available for .NET Core, you can simply upgrade it through APT with the following commands:</span></span>

```bash
sudo apt-get update
sudo apt-get upgrade
```

## <a name="apt-troubleshooting"></a><span data-ttu-id="9a29b-140">APT のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="9a29b-140">APT troubleshooting</span></span>

<span data-ttu-id="9a29b-141">このセクションでは、APT を使用して .NET Core をインストールするときに発生する可能性のある一般的なエラーについて説明します。</span><span class="sxs-lookup"><span data-stu-id="9a29b-141">This section provides information on common errors you may get while using APT to install .NET Core.</span></span>

### <a name="unable-to-locate"></a><span data-ttu-id="9a29b-142">見つからない</span><span class="sxs-lookup"><span data-stu-id="9a29b-142">Unable to locate</span></span>

[!INCLUDE [package-manager-failed-to-find-deb](includes/package-manager-failed-to-find-deb.md)]

```bash
sudo apt-get install -y gpg
wget -O - https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor -o microsoft.asc.gpg
sudo mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/
wget https://packages.microsoft.com/config/debian/{os-version}/prod.list
sudo mv prod.list /etc/apt/sources.list.d/microsoft-prod.list
sudo chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg
sudo chown root:root /etc/apt/sources.list.d/microsoft-prod.list
sudo apt-get update; \
  sudo apt-get install -y apt-transport-https && \
  sudo apt-get update && \
  sudo apt-get install -y {dotnet-package}
```

### <a name="failed-to-fetch"></a><span data-ttu-id="9a29b-143">フェッチできない</span><span class="sxs-lookup"><span data-stu-id="9a29b-143">Failed to fetch</span></span>

[!INCLUDE [package-manager-failed-to-fetch-deb](includes/package-manager-failed-to-fetch-deb.md)]

## <a name="snap"></a><span data-ttu-id="9a29b-144">Snap</span><span class="sxs-lookup"><span data-stu-id="9a29b-144">Snap</span></span>

[!INCLUDE [linux-install-snap](includes/linux-install-snap.md)]

## <a name="dependencies"></a><span data-ttu-id="9a29b-145">依存関係</span><span class="sxs-lookup"><span data-stu-id="9a29b-145">Dependencies</span></span>

<span data-ttu-id="9a29b-146">パッケージ マネージャーを使用してインストールする場合、次のライブラリが自動的にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="9a29b-146">When you install with a package manager, these libraries are installed for you.</span></span> <span data-ttu-id="9a29b-147">ただし、手動で .NET Core をインストールする場合、または自己完結型アプリを公開する場合は、次のライブラリがインストールされていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9a29b-147">But, if you manually install .NET Core or you publish a self-contained app, you'll need to make sure these libraries are installed:</span></span>

- <span data-ttu-id="9a29b-148">libc6</span><span class="sxs-lookup"><span data-stu-id="9a29b-148">libc6</span></span>
- <span data-ttu-id="9a29b-149">libgcc1</span><span class="sxs-lookup"><span data-stu-id="9a29b-149">libgcc1</span></span>
- <span data-ttu-id="9a29b-150">libgssapi-krb5-2</span><span class="sxs-lookup"><span data-stu-id="9a29b-150">libgssapi-krb5-2</span></span>
- <span data-ttu-id="9a29b-151">libicu52 (8.x 用)</span><span class="sxs-lookup"><span data-stu-id="9a29b-151">libicu52 (for 8.x)</span></span>
- <span data-ttu-id="9a29b-152">libicu57 (9.x 用)</span><span class="sxs-lookup"><span data-stu-id="9a29b-152">libicu57 (for 9.x)</span></span>
- <span data-ttu-id="9a29b-153">libicu63 (10.x 用)</span><span class="sxs-lookup"><span data-stu-id="9a29b-153">libicu63 (for 10.x)</span></span>
- <span data-ttu-id="9a29b-154">libicu67 (11.x 用)</span><span class="sxs-lookup"><span data-stu-id="9a29b-154">libicu67 (for 11.x)</span></span>
- <span data-ttu-id="9a29b-155">libssl1.0.0 (8.x 用)</span><span class="sxs-lookup"><span data-stu-id="9a29b-155">libssl1.0.0 (for 8.x)</span></span>
- <span data-ttu-id="9a29b-156">libssl1.1 (9.x - 11.x 用)</span><span class="sxs-lookup"><span data-stu-id="9a29b-156">libssl1.1 (for 9.x-11.x)</span></span>
- <span data-ttu-id="9a29b-157">libstdc++6</span><span class="sxs-lookup"><span data-stu-id="9a29b-157">libstdc++6</span></span>
- <span data-ttu-id="9a29b-158">zlib1g</span><span class="sxs-lookup"><span data-stu-id="9a29b-158">zlib1g</span></span>

<span data-ttu-id="9a29b-159">*System.Drawing.Common* アセンブリを使用する .NET Core アプリの場合は、次の依存関係も必要です。</span><span class="sxs-lookup"><span data-stu-id="9a29b-159">For .NET Core apps that use the *System.Drawing.Common* assembly, you also need the following dependency:</span></span>

- <span data-ttu-id="9a29b-160">libgdiplus (バージョン 6.0.1 以降)</span><span class="sxs-lookup"><span data-stu-id="9a29b-160">libgdiplus (version 6.0.1 or later)</span></span>

  > [!WARNING]
  > <span data-ttu-id="9a29b-161">最新バージョンの *libgdiplus* をインストールするには、システムに Mono リポジトリを追加します。</span><span class="sxs-lookup"><span data-stu-id="9a29b-161">You can install a recent version of *libgdiplus* by adding the Mono repository to your system.</span></span> <span data-ttu-id="9a29b-162">詳細については、「<https://www.mono-project.com/download/stable/>」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9a29b-162">For more information, see <https://www.mono-project.com/download/stable/>.</span></span>

## <a name="scripted-install"></a><span data-ttu-id="9a29b-163">スクリプトでのインストール</span><span class="sxs-lookup"><span data-stu-id="9a29b-163">Scripted install</span></span>

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a><span data-ttu-id="9a29b-164">手動インストール</span><span class="sxs-lookup"><span data-stu-id="9a29b-164">Manual install</span></span>

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a><span data-ttu-id="9a29b-165">次の手順</span><span class="sxs-lookup"><span data-stu-id="9a29b-165">Next steps</span></span>

- [<span data-ttu-id="9a29b-166">チュートリアル: Visual Studio Code を使用して .NET Core SDK でコンソール アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="9a29b-166">Tutorial: Create a console application with .NET Core SDK using Visual Studio Code</span></span>](../tutorials/with-visual-studio-code.md)