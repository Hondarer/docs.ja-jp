---
title: '方法: .NET Framework シングルファイル アセンブリをビルドする'
ms.date: 08/20/2019
helpviewer_keywords:
- assembly manifest, single-file assemblies
- library assemblies
- command-line compilers
- assemblies [.NET Framework], single-file
- output file name for assemblies
- code modules
- single-file assemblies
dev_langs:
- csharp
- vb
ms.assetid: a6063221-43a5-4d3e-814c-288a4ec69aec
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 98f06e62e1070f78faa77ef7d83fd80a62984684
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991243"
---
# <a name="how-to-build-a-net-framework-single-file-assembly"></a><span data-ttu-id="b09b6-102">方法: .NET Framework シングルファイル アセンブリをビルドする</span><span class="sxs-lookup"><span data-stu-id="b09b6-102">How to: Build a .NET Framework single-file assembly</span></span>

<span data-ttu-id="b09b6-103">アセンブリの最も単純な形式であるシングルファイル アセンブリには、型の情報、実装、[アセンブリ マニフェスト](../../standard/assembly/manifest.md)が含まれています。</span><span class="sxs-lookup"><span data-stu-id="b09b6-103">A single-file assembly, which is the simplest type of assembly, contains type information and implementation, as well as the [assembly manifest](../../standard/assembly/manifest.md).</span></span> <span data-ttu-id="b09b6-104">コマンド ライン コンパイラや Visual Studio を利用し、.NET Framework を対象とするシングルファイル アセンブリを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b09b6-104">You can use command-line compilers or Visual Studio to create a single-file assembly that targets the .NET Framework.</span></span> <span data-ttu-id="b09b6-105">既定では、コンパイラでは *.exe* 拡張子でアセンブリ ファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="b09b6-105">By default, the compiler creates an assembly file with an *.exe* extension.</span></span>

> [!NOTE]
> <span data-ttu-id="b09b6-106">C# と Visual Basic の Visual Studio は、シングルファイル アセンブリの作成にのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="b09b6-106">Visual Studio for C# and Visual Basic can be used only to create single-file assemblies.</span></span> <span data-ttu-id="b09b6-107">マルチファイル アセンブリを作成する場合は、コマンド ライン コンパイラまたは Visual C++ を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b09b6-107">If you want to create multifile assemblies, you must use command-line compilers or Visual C++.</span></span>

<span data-ttu-id="b09b6-108">次の手順は、コマンド ライン コンパイラでシングルファイル アセンブリを作成する方法です。</span><span class="sxs-lookup"><span data-stu-id="b09b6-108">The following procedures show how to create single-file assemblies using command-line compilers.</span></span>

## <a name="create-an-assembly-with-an-exe-extension"></a><span data-ttu-id="b09b6-109">拡張子が .exe のアセンブリを作成する</span><span class="sxs-lookup"><span data-stu-id="b09b6-109">Create an assembly with an .exe extension</span></span>

<span data-ttu-id="b09b6-110">コマンド プロンプトに次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="b09b6-110">At the command prompt, type the following command:</span></span>

<span data-ttu-id="b09b6-111">\<*コンパイラ コマンド*> \<*モジュール名*></span><span class="sxs-lookup"><span data-stu-id="b09b6-111">\<*compiler command*> \<*module name*></span></span>

<span data-ttu-id="b09b6-112">このコマンドでは、*コンパイラ コマンド*はお使いのコード モジュールで使用されている言語のコンパイラ コマンドで、*モジュール名*はアセンブリにコンパイルするコード モジュールの名前です。</span><span class="sxs-lookup"><span data-stu-id="b09b6-112">In this command, *compiler command* is the compiler command for the language used in your code module, and *module name* is the name of the code module to compile into the assembly.</span></span>

<span data-ttu-id="b09b6-113">次の例では、`myCode` というコード モジュールから *myCode.exe* という名前のアセンブリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="b09b6-113">The following example creates an assembly named *myCode.exe* from a code module called `myCode`.</span></span>

```csharp
csc myCode.cs
```

```vb
vbc myCode.vb
```

## <a name="create-an-assembly-with-an-exe-extension-and-specify-the-output-file-name"></a><span data-ttu-id="b09b6-114">拡張子が .exe のアセンブリを作成し、出力ファイル名を指定する</span><span class="sxs-lookup"><span data-stu-id="b09b6-114">Create an assembly with an .exe extension and specify the output file name</span></span>

<span data-ttu-id="b09b6-115">コマンド プロンプトに次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="b09b6-115">At the command prompt, type the following command:</span></span>

<span data-ttu-id="b09b6-116">\<*コンパイラ コマンド*>  **/out:** \<*ファイル名*> \<*モジュール名*></span><span class="sxs-lookup"><span data-stu-id="b09b6-116">\<*compiler command*> **/out:**\<*file name*> \<*module name*></span></span>

<span data-ttu-id="b09b6-117">このコマンドでは、*コンパイラ コマンド*はお使いのコード モジュールで使用されている言語のコンパイラ コマンド、*ファイル名*は出力ファイル名、*モジュール名*はアセンブリにコンパイルするコード モジュールの名前です。</span><span class="sxs-lookup"><span data-stu-id="b09b6-117">In this command, *compiler command* is the compiler command for the language used in your code module, *file name* is the output file name, and *module name* is the name of the code module to compile into the assembly.</span></span>

<span data-ttu-id="b09b6-118">次の例では、`myCode` というコード モジュールから *myAssembly.exe* という名前のアセンブリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="b09b6-118">The following example creates an assembly named *myAssembly.exe* from a code module called `myCode`.</span></span>

```csharp
csc -out:myAssembly.exe myCode.cs
```

```vb
vbc -out:myAssembly.exe myCode.vb
```

## <a name="create-library-assemblies"></a><span data-ttu-id="b09b6-119">ライブラリ アセンブリを作成する</span><span class="sxs-lookup"><span data-stu-id="b09b6-119">Create library assemblies</span></span>
 <span data-ttu-id="b09b6-120">ライブラリ アセンブリはクラス ライブラリに似ています。</span><span class="sxs-lookup"><span data-stu-id="b09b6-120">A library assembly is similar to a class library.</span></span> <span data-ttu-id="b09b6-121">他のアセンブリにより参照される型が含まれますが、実行を開始するためのエントリ ポイントがありません。</span><span class="sxs-lookup"><span data-stu-id="b09b6-121">It contains types that will be referenced by other assemblies, but it has no entry point to begin execution.</span></span>

<span data-ttu-id="b09b6-122">ライブラリ アセンブリを作成するには、コマンド プロンプトで次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="b09b6-122">To create a library assembly, at the command prompt, type the following command:</span></span>

<span data-ttu-id="b09b6-123">\<*コンパイラ コマンド*>  **/t:library** \<*モジュール名*></span><span class="sxs-lookup"><span data-stu-id="b09b6-123">\<*compiler command*> **-t:library** \<*module name*></span></span>

<span data-ttu-id="b09b6-124">このコマンドでは、*コンパイラ コマンド*はお使いのコード モジュールで使用されている言語のコンパイラ コマンドで、*モジュール名*はアセンブリにコンパイルするコード モジュールの名前です。</span><span class="sxs-lookup"><span data-stu-id="b09b6-124">In this command, *compiler command* is the compiler command for the language used in your code module, and *module name* is the name of the code module to compile into the assembly.</span></span> <span data-ttu-id="b09b6-125">**/out:** オプションなど、他のコンパイラ オプションも使用できます。</span><span class="sxs-lookup"><span data-stu-id="b09b6-125">You can also use other compiler options, such as the **-out:** option.</span></span>

<span data-ttu-id="b09b6-126">次の例では、`myCode` というコード モジュールから *myCodeAssembly.dll* という名前のライブラリ アセンブリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="b09b6-126">The following example creates a library assembly named *myCodeAssembly.dll* from a code module called `myCode`.</span></span>

```csharp
csc -out:myCodeLibrary.dll -t:library myCode.cs
```

```vb
vbc -out:myCodeLibrary.dll -t:library myCode.vb
```

## <a name="see-also"></a><span data-ttu-id="b09b6-127">関連項目</span><span class="sxs-lookup"><span data-stu-id="b09b6-127">See also</span></span>

- [<span data-ttu-id="b09b6-128">アセンブリを作成する</span><span class="sxs-lookup"><span data-stu-id="b09b6-128">Create assemblies</span></span>](../../standard/assembly/create.md)
- [<span data-ttu-id="b09b6-129">マルチファイル アセンブリ</span><span class="sxs-lookup"><span data-stu-id="b09b6-129">Multifile assemblies</span></span>](multifile-assemblies.md)
- [<span data-ttu-id="b09b6-130">方法: マルチファイル アセンブリをビルドする</span><span class="sxs-lookup"><span data-stu-id="b09b6-130">How to: Build a multifile assembly</span></span>](build-multifile-assembly.md)
- [<span data-ttu-id="b09b6-131">アセンブリを使用したプログラム</span><span class="sxs-lookup"><span data-stu-id="b09b6-131">Program with assemblies</span></span>](../../standard/assembly/program.md)