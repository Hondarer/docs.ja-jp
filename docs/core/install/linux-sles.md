---
title: SLES に .NET Core をインストールする - .NET Core
description: SLES に .NET Core SDK と .NET Core ランタイムをインストールするさまざまな方法を示します。
author: adegeo
ms.author: adegeo
ms.date: 06/04/2020
ms.openlocfilehash: 8f64efcc8206b47855871104e5b6914570c06da0
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619417"
---
# <a name="install-net-core-sdk-or-net-core-runtime-on-sles"></a><span data-ttu-id="d5722-103">SLES に .NET Core SDK または .NET Core ランタイムをインストールする</span><span class="sxs-lookup"><span data-stu-id="d5722-103">Install .NET Core SDK or .NET Core Runtime on SLES</span></span>

<span data-ttu-id="d5722-104">.NET Core は SLES でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d5722-104">.NET Core is supported on SLES.</span></span> <span data-ttu-id="d5722-105">この記事では、SLES に .NET Core をインストールする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d5722-105">This article describes how to install .NET Core on SLES.</span></span>

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

## <a name="supported-distributions"></a><span data-ttu-id="d5722-106">サポートされているディストリビューション</span><span class="sxs-lookup"><span data-stu-id="d5722-106">Supported distributions</span></span>

<span data-ttu-id="d5722-107">次の表は、SLES 12 SP2 と SLES 15 の両方で現在サポートされている .NET Core リリースの一覧です。</span><span class="sxs-lookup"><span data-stu-id="d5722-107">The following table is a list of currently supported .NET Core releases on both SLES 12 SP2 and SLES 15.</span></span> <span data-ttu-id="d5722-108">これらのバージョンは、[.NET Core のバージョンがサポート終了になる](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)か、SLES のバージョンがサポート終了になるまでサポートされます。</span><span class="sxs-lookup"><span data-stu-id="d5722-108">These versions remain supported until either the version of [.NET Core reaches end-of-support](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) or the version of SLES is no longer supported.</span></span>

- <span data-ttu-id="d5722-109">✔️ は、SLES または .NET Core のバージョンがまだサポートされていることを示します。</span><span class="sxs-lookup"><span data-stu-id="d5722-109">A ✔️ indicates that the version of SLES or .NET Core is still supported.</span></span>
- <span data-ttu-id="d5722-110">❌ は、SLES または .NET Core のバージョンがその SLES のリリースではサポートされていないことを示しています。</span><span class="sxs-lookup"><span data-stu-id="d5722-110">A ❌ indicates that the version of SLES or .NET Core isn't supported on that SLES release.</span></span>
- <span data-ttu-id="d5722-111">SLES のバージョンと .NET Core のバージョンの両方に ✔️ が付いている場合、その OS と .NET の組み合わせはサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d5722-111">When both a version of SLES and a version of .NET Core have ✔️, that OS and .NET combination are supported.</span></span>

| <span data-ttu-id="d5722-112">SLES</span><span class="sxs-lookup"><span data-stu-id="d5722-112">SLES</span></span>                   | <span data-ttu-id="d5722-113">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="d5722-113">.NET Core 2.1</span></span> | <span data-ttu-id="d5722-114">.NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="d5722-114">.NET Core 3.1</span></span> | <span data-ttu-id="d5722-115">.NET 5 Preview (手動インストールのみ)</span><span class="sxs-lookup"><span data-stu-id="d5722-115">.NET 5 Preview (manual install only)</span></span> |
|------------------------|---------------|---------------|----------------|
| <span data-ttu-id="d5722-116">✔️ [15](#sles-15-)</span><span class="sxs-lookup"><span data-stu-id="d5722-116">✔️ [15](#sles-15-)</span></span>     | <span data-ttu-id="d5722-117">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="d5722-117">✔️ 2.1</span></span>        | <span data-ttu-id="d5722-118">✔️ 3.1</span><span class="sxs-lookup"><span data-stu-id="d5722-118">✔️ 3.1</span></span>        | <span data-ttu-id="d5722-119">✔️ 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="d5722-119">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="d5722-120">✔️ [12 SP2](#sles-12-)</span><span class="sxs-lookup"><span data-stu-id="d5722-120">✔️ [12 SP2](#sles-12-)</span></span> | <span data-ttu-id="d5722-121">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="d5722-121">✔️ 2.1</span></span>        | <span data-ttu-id="d5722-122">✔️ 3.1</span><span class="sxs-lookup"><span data-stu-id="d5722-122">✔️ 3.1</span></span>        | <span data-ttu-id="d5722-123">✔️ 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="d5722-123">✔️ 5.0 Preview</span></span> |

<span data-ttu-id="d5722-124">次のバージョンの .NET Core は、サポート対象外となりました。</span><span class="sxs-lookup"><span data-stu-id="d5722-124">The following versions of .NET Core are no longer supported.</span></span> <span data-ttu-id="d5722-125">これらのダウンロードは、まだ公開されています。</span><span class="sxs-lookup"><span data-stu-id="d5722-125">The downloads for these still remain published:</span></span>

- <span data-ttu-id="d5722-126">3.0</span><span class="sxs-lookup"><span data-stu-id="d5722-126">3.0</span></span>
- <span data-ttu-id="d5722-127">2.2</span><span class="sxs-lookup"><span data-stu-id="d5722-127">2.2</span></span>
- <span data-ttu-id="d5722-128">2.0</span><span class="sxs-lookup"><span data-stu-id="d5722-128">2.0</span></span>

## <a name="how-to-install-other-versions"></a><span data-ttu-id="d5722-129">その他のバージョンをインストールする方法</span><span class="sxs-lookup"><span data-stu-id="d5722-129">How to install other versions</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="sles-15-"></a><span data-ttu-id="d5722-130">SLES 15 ✔️</span><span class="sxs-lookup"><span data-stu-id="d5722-130">SLES 15 ✔️</span></span>

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/sles/15/packages-microsoft-prod.rpm
```

<span data-ttu-id="d5722-131">現時点では、SLES 15 Microsoft リポジトリ セットアップ パッケージによって "*microsoft-prod.repo*" ファイルが間違ったディレクトリにインストールされるため、zypper が .NET Core パッケージを見つけることができません。</span><span class="sxs-lookup"><span data-stu-id="d5722-131">Currently, the SLES 15 Microsoft repository setup package installs the *microsoft-prod.repo* file to the wrong directory, preventing zypper from finding the .NET Core packages.</span></span> <span data-ttu-id="d5722-132">この問題を解決するには、正しいディレクトリにシンボリックリンクを作成します。</span><span class="sxs-lookup"><span data-stu-id="d5722-132">To fix this problem, create a symlink in the correct directory.</span></span>

```bash
sudo ln -s /etc/yum.repos.d/microsoft-prod.repo /etc/zypp/repos.d/microsoft-prod.repo
```

[!INCLUDE [linux-zyp-install-31](includes/linux-install-31-zyp.md)]

## <a name="sles-12-"></a><span data-ttu-id="d5722-133">SLES 12 ✔️</span><span class="sxs-lookup"><span data-stu-id="d5722-133">SLES 12 ✔️</span></span>

<span data-ttu-id="d5722-134">.NET Core では、SLES 12 ファミリの最小要件として SP2 が必要です。</span><span class="sxs-lookup"><span data-stu-id="d5722-134">.NET Core requires SP2 as a minimum for the SLES 12 family.</span></span>

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/sles/12/packages-microsoft-prod.rpm
```

[!INCLUDE [linux-zyp-install-31](includes/linux-install-31-zyp.md)]

## <a name="troubleshoot-the-package-manager"></a><span data-ttu-id="d5722-135">パッケージ マネージャーのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="d5722-135">Troubleshoot the package manager</span></span>

<span data-ttu-id="d5722-136">このセクションでは、パッケージ マネージャーを使用して .NET Core をインストールするときに発生する可能性のある一般的なエラーについて説明します。</span><span class="sxs-lookup"><span data-stu-id="d5722-136">This section provides information on common errors you may get while using the package manager to install .NET Core.</span></span>

### <a name="failed-to-fetch"></a><span data-ttu-id="d5722-137">フェッチできない</span><span class="sxs-lookup"><span data-stu-id="d5722-137">Failed to fetch</span></span>

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]

## <a name="dependencies"></a><span data-ttu-id="d5722-138">依存関係</span><span class="sxs-lookup"><span data-stu-id="d5722-138">Dependencies</span></span>

<span data-ttu-id="d5722-139">パッケージ マネージャーを使用してインストールする場合、次のライブラリが自動的にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="d5722-139">When you install with a package manager, these libraries are installed for you.</span></span> <span data-ttu-id="d5722-140">ただし、手動で .NET Core をインストールする場合、または自己完結型アプリを公開する場合は、次のライブラリがインストールされていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5722-140">But, if you manually install .NET Core or you publish a self-contained app, you'll need to make sure these libraries are installed:</span></span>

- <span data-ttu-id="d5722-141">krb5</span><span class="sxs-lookup"><span data-stu-id="d5722-141">krb5</span></span>
- <span data-ttu-id="d5722-142">libicu</span><span class="sxs-lookup"><span data-stu-id="d5722-142">libicu</span></span>
- <span data-ttu-id="d5722-143">libopenssl1_1</span><span class="sxs-lookup"><span data-stu-id="d5722-143">libopenssl1_1</span></span>

<span data-ttu-id="d5722-144">ターゲット ランタイム環境の OpenSSL バージョンが 1.1 以降である場合は、**compat-openssl10** をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5722-144">If the target runtime environment's OpenSSL version is 1.1 or newer, you'll need to install **compat-openssl10**.</span></span>

<span data-ttu-id="d5722-145">依存関係の詳細については、「[Self-contained Linux applications](https://github.com/dotnet/core/blob/master/Documentation/self-contained-linux-apps.md)」(自己完結型 Linux アプリケーション) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="d5722-145">For more information about the dependencies, see [Self-contained Linux apps](https://github.com/dotnet/core/blob/master/Documentation/self-contained-linux-apps.md).</span></span>

<span data-ttu-id="d5722-146">*System.Drawing.Common* アセンブリを使用する .NET Core アプリの場合は、次の依存関係も必要です。</span><span class="sxs-lookup"><span data-stu-id="d5722-146">For .NET Core apps that use the *System.Drawing.Common* assembly, you'll also need the following dependency:</span></span>

- [<span data-ttu-id="d5722-147">libgdiplus (バージョン 6.0.1 以降)</span><span class="sxs-lookup"><span data-stu-id="d5722-147">libgdiplus (version 6.0.1 or later)</span></span>](https://www.mono-project.com/docs/gui/libgdiplus/)

  > [!WARNING]
  > <span data-ttu-id="d5722-148">最新バージョンの *libgdiplus* をインストールするには、システムに Mono リポジトリを追加します。</span><span class="sxs-lookup"><span data-stu-id="d5722-148">You can install a recent version of *libgdiplus* by adding the Mono repository to your system.</span></span> <span data-ttu-id="d5722-149">詳細については、「<https://www.mono-project.com/download/stable/>」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d5722-149">For more information, see <https://www.mono-project.com/download/stable/>.</span></span>

## <a name="scripted-install"></a><span data-ttu-id="d5722-150">スクリプトでのインストール</span><span class="sxs-lookup"><span data-stu-id="d5722-150">Scripted install</span></span>

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a><span data-ttu-id="d5722-151">手動インストール</span><span class="sxs-lookup"><span data-stu-id="d5722-151">Manual install</span></span>

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a><span data-ttu-id="d5722-152">次の手順</span><span class="sxs-lookup"><span data-stu-id="d5722-152">Next steps</span></span>

- [<span data-ttu-id="d5722-153">チュートリアル: Visual Studio Code を使用して .NET Core SDK でコンソール アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="d5722-153">Tutorial: Create a console application with .NET Core SDK using Visual Studio Code</span></span>](../tutorials/with-visual-studio-code.md)