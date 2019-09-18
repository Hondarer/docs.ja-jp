---
title: '方法: アセンブリをグローバル アセンブリ キャッシュにインストールする'
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- Gacutil.exe
- strong-named assemblies, global assembly cache
- global assembly cache, installing assemblies
- Global Assembly Cache tool
- windows installer, global assembly cache
ms.assetid: a7e6f091-d02c-49ba-b736-7295cb0eb743
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: de5ae03ab885c4368e39b6339b5a14d1082e6df5
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972871"
---
# <a name="how-to-install-an-assembly-into-the-global-assembly-cache"></a><span data-ttu-id="1cf69-102">方法: アセンブリをグローバル アセンブリ キャッシュにインストールする</span><span class="sxs-lookup"><span data-stu-id="1cf69-102">How to: Install an assembly into the global assembly cache</span></span>

<span data-ttu-id="1cf69-103">グローバル アセンブリ キャッシュ (GAC) には、複数のアプリケーションで共有されるアセンブリが格納されています。</span><span class="sxs-lookup"><span data-stu-id="1cf69-103">The global assembly cache (GAC) stores assemblies that several applications share.</span></span> <span data-ttu-id="1cf69-104">次のコンポーネントのいずれかを使用して、アセンブリを[グローバル アセンブリ キャッシュ](gac.md)にインストールします。</span><span class="sxs-lookup"><span data-stu-id="1cf69-104">Install an assembly into the [global assembly cache](gac.md) with one of the following components:</span></span> 

- [<span data-ttu-id="1cf69-105">Windows インストーラー</span><span class="sxs-lookup"><span data-stu-id="1cf69-105">Windows Installer</span></span>](#windows-installer)
- [<span data-ttu-id="1cf69-106">グローバル アセンブリ キャッシュ ツール</span><span class="sxs-lookup"><span data-stu-id="1cf69-106">Global Assembly Cache tool</span></span>](#global-assembly-cache-tool)

> [!IMPORTANT]
> <span data-ttu-id="1cf69-107">グローバル アセンブリ キャッシュにインストールできるのは、厳密な名前のアセンブリだけです。</span><span class="sxs-lookup"><span data-stu-id="1cf69-107">You can install only strong-named assemblies into the global assembly cache.</span></span> <span data-ttu-id="1cf69-108">厳密な名前付きのアセンブリを作成する方法については、「[方法:厳密な名前でアセンブリに署名する](../../standard/assembly/sign-strong-name.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1cf69-108">For information about how to create a strong-named assembly, see [How to: Sign an assembly with a strong name](../../standard/assembly/sign-strong-name.md).</span></span>

## <a name="windows-installer"></a><span data-ttu-id="1cf69-109">Windows インストーラー</span><span class="sxs-lookup"><span data-stu-id="1cf69-109">Windows Installer</span></span>

<span data-ttu-id="1cf69-110">アセンブリをグローバル アセンブリ キャッシュに追加するための推奨する方法は、[Windows インストーラー](/windows/desktop/Msi/installation-of-assemblies-to-the-global-assembly-cache)(Windows インストール エンジン) です。</span><span class="sxs-lookup"><span data-stu-id="1cf69-110">[Windows Installer](/windows/desktop/Msi/installation-of-assemblies-to-the-global-assembly-cache), the Windows installation engine, is the recommended way to add assemblies to the global assembly cache.</span></span> <span data-ttu-id="1cf69-111">Windows インストーラーを使用すると、グローバル アセンブリ キャッシュ内のアセンブリの参照カウントが示されるなどの利点があります。</span><span class="sxs-lookup"><span data-stu-id="1cf69-111">Windows Installer provides reference counting of assemblies in the global assembly cache and other benefits.</span></span> <span data-ttu-id="1cf69-112">Windows インストーラー用のインストーラー パッケージを作成するには、[Visual Studio 2017 用 WiX Toolset 拡張機能](https://marketplace.visualstudio.com/items?itemName=RobMensching.WixToolsetVisualStudio2017Extension)を使用します。</span><span class="sxs-lookup"><span data-stu-id="1cf69-112">To create an installer package for Windows Installer, use the [WiX toolset extension for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=RobMensching.WixToolsetVisualStudio2017Extension).</span></span>

## <a name="global-assembly-cache-tool"></a><span data-ttu-id="1cf69-113">グローバル アセンブリ キャッシュ ツール</span><span class="sxs-lookup"><span data-stu-id="1cf69-113">Global Assembly Cache tool</span></span>

<span data-ttu-id="1cf69-114">[.NET グローバル アセンブリ キャッシュ ユーティリティ (gacutil.exe)](../tools/gacutil-exe-gac-tool.md) を使用して、アセンブリをグローバル アセンブリ キャッシュに追加したり、グローバル アセンブリ キャッシュの内容を表示したりできます。</span><span class="sxs-lookup"><span data-stu-id="1cf69-114">You can use the [.NET Global Assembly Cache utility (gacutil.exe)](../tools/gacutil-exe-gac-tool.md) to add assemblies to the global assembly cache and to view the contents of the global assembly cache.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1cf69-115">*Gacutil.exe* は、開発のみを目的としています。</span><span class="sxs-lookup"><span data-stu-id="1cf69-115">*Gacutil.exe* is for development purposes only.</span></span> <span data-ttu-id="1cf69-116">これは運用環境のアセンブリをグローバル アセンブリ キャッシュにインストールするのには使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="1cf69-116">Don't use it to install production assemblies into the global assembly cache.</span></span>

<span data-ttu-id="1cf69-117">*gacutil.exe* を使用して GAC にアセンブリをインストールするための構文は、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="1cf69-117">The syntax for using *gacutil.exe* to install an assembly in the GAC is as follows:</span></span>

```cmd
gacutil -i <assembly name>
```

<span data-ttu-id="1cf69-118">このコマンドの *\<assembly name>* は、グローバル アセンブリ キャッシュにインストールされるアセンブリの名前です。</span><span class="sxs-lookup"><span data-stu-id="1cf69-118">In this command, *\<assembly name>* is the name of the assembly to install in the global assembly cache.</span></span>

<span data-ttu-id="1cf69-119">システム パスに *gacutil.exe* が含まれていない場合は、[開発者コマンド プロンプト for VS *\<バージョン>* ](../tools/developer-command-prompt-for-vs.md) を使用します。</span><span class="sxs-lookup"><span data-stu-id="1cf69-119">If *gacutil.exe* isn't in your system path, use the [Developer command prompt for VS *\<version>*](../tools/developer-command-prompt-for-vs.md).</span></span>

<span data-ttu-id="1cf69-120">ファイル名 *hello.dll* のアセンブリをグローバル アセンブリ キャッシュにインストールする例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="1cf69-120">The following example installs an assembly with the file name *hello.dll* into the global assembly cache.</span></span>

```cmd
gacutil -i hello.dll
```

> [!NOTE]
> <span data-ttu-id="1cf69-121">以前のバージョンの .NET Framework では、Windows のシェル拡張機能である *Shfusion.dll* により、ファイル エクスプローラーにアセンブリをドラッグしてインストールすることができました。</span><span class="sxs-lookup"><span data-stu-id="1cf69-121">In earlier versions of the .NET Framework, the *Shfusion.dll* Windows shell extension let you install assemblies by dragging them to File Explorer.</span></span> <span data-ttu-id="1cf69-122">.NET Framework 4 以降では、*Shfusion.dll* は廃止されました。</span><span class="sxs-lookup"><span data-stu-id="1cf69-122">Beginning with .NET Framework 4, *Shfusion.dll* is obsolete.</span></span>

## <a name="see-also"></a><span data-ttu-id="1cf69-123">関連項目</span><span class="sxs-lookup"><span data-stu-id="1cf69-123">See also</span></span>

- [<span data-ttu-id="1cf69-124">アセンブリとグローバル アセンブリ キャッシュの使用</span><span class="sxs-lookup"><span data-stu-id="1cf69-124">Work with assemblies and the global assembly cache</span></span>](working-with-assemblies-and-the-gac.md)
- [<span data-ttu-id="1cf69-125">方法: グローバル アセンブリ キャッシュからアセンブリを削除する</span><span class="sxs-lookup"><span data-stu-id="1cf69-125">How to: Remove an assembly from the global assembly cache</span></span>](how-to-remove-an-assembly-from-the-gac.md)
- [<span data-ttu-id="1cf69-126">Gacutil.exe (グローバル アセンブリ キャッシュ ツール)</span><span class="sxs-lookup"><span data-stu-id="1cf69-126">Gacutil.exe (Global Assembly Cache tool)</span></span>](../tools/gacutil-exe-gac-tool.md)
- [<span data-ttu-id="1cf69-127">方法: 厳密な名前でアセンブリに署名する</span><span class="sxs-lookup"><span data-stu-id="1cf69-127">How to: Sign an assembly with a strong name</span></span>](../../standard/assembly/sign-strong-name.md)