---
title: 如何：引用具有强名称的程序集
ms.date: 08/20/2019
helpviewer_keywords:
- strong-named assemblies, compile-time references
- compile-time assembly referencing
- assemblies [.NET Framework], strong-named
- assembly binding, strong-named
ms.assetid: 4c6a406a-b5eb-44fa-b4ed-4e95bb95a813
author: rpetrusha
ms.author: ronpet
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 324cd42a2781202f19e7e1cb5055d571f0c58cf5
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972611"
---
# <a name="how-to-reference-a-strong-named-assembly"></a><span data-ttu-id="66a4d-102">如何：引用具有强名称的程序集</span><span class="sxs-lookup"><span data-stu-id="66a4d-102">How to: Reference a strong-named assembly</span></span>
<span data-ttu-id="66a4d-103">引用强名称程序集中的类型或资源的过程通常是透明的。</span><span class="sxs-lookup"><span data-stu-id="66a4d-103">The process for referencing types or resources in a strong-named assembly is usually transparent.</span></span> <span data-ttu-id="66a4d-104">可在编译时（早期绑定）或在运行时进行引用。</span><span class="sxs-lookup"><span data-stu-id="66a4d-104">You can make the reference either at compile time (early binding) or at run time.</span></span>  
  
<span data-ttu-id="66a4d-105">向编译器指示要编译的程序集显式引用另一程序集时，会发生编译时引用。</span><span class="sxs-lookup"><span data-stu-id="66a4d-105">A compile-time reference occurs when you indicate to the compiler that the assembly to be compiled explicitly references another assembly.</span></span> <span data-ttu-id="66a4d-106">使用编译时引用时，编译器会自动获取目标强名称程序集的公钥，并将其放在正在编译的程序集的程序集引用中。</span><span class="sxs-lookup"><span data-stu-id="66a4d-106">When you use compile-time referencing, the compiler automatically gets the public key of the targeted strong-named assembly and places it in the assembly reference of the assembly being compiled.</span></span>
  
> [!NOTE]
> <span data-ttu-id="66a4d-107">具有强名称的程序集只能使用其他具有强名称的程序集的类型。</span><span class="sxs-lookup"><span data-stu-id="66a4d-107">A strong-named assembly can only use types from other strong-named assemblies.</span></span> <span data-ttu-id="66a4d-108">否则，将会危害具有强名称的程序集的安全性。</span><span class="sxs-lookup"><span data-stu-id="66a4d-108">Otherwise, the security of the strong-named assembly would be compromised.</span></span>  
  
## <a name="make-a-compile-time-reference-to-a-strong-named-assembly"></a><span data-ttu-id="66a4d-109">对具有强名称的程序集进行编译时引用</span><span class="sxs-lookup"><span data-stu-id="66a4d-109">Make a compile-time reference to a strong-named assembly</span></span>  

<span data-ttu-id="66a4d-110">在命令提示符下，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="66a4d-110">At a command prompt, type the following command:</span></span>  

<span data-ttu-id="66a4d-111">\<compiler command> /reference:\<assembly name></span><span class="sxs-lookup"><span data-stu-id="66a4d-111">\<*compiler command*> **/reference:**\<*assembly name*></span></span>  

<span data-ttu-id="66a4d-112">在此命令中，compiler command 是所用语言的编译器命令，assembly name 是引用的强名称程序集的名称。</span><span class="sxs-lookup"><span data-stu-id="66a4d-112">In this command, *compiler command* is the compiler command for the language you are using, and *assembly name* is the name of the strong-named assembly being referenced.</span></span> <span data-ttu-id="66a4d-113">还可使用其他编译器选项，如用于创建库程序集的 /t:library 选项。</span><span class="sxs-lookup"><span data-stu-id="66a4d-113">You can also use other compiler options, such as the **/t:library** option for creating a library assembly.</span></span>  

<span data-ttu-id="66a4d-114">以下示例创建名为 myAssembly.dll 的程序集，该程序集从名为 myAssembly.cs 的代码模块中引用名为 myLibAssembly.dll 的强名称程序集。</span><span class="sxs-lookup"><span data-stu-id="66a4d-114">The following example creates an assembly called *myAssembly.dll* that references a strong-named assembly called *myLibAssembly.dll* from a code module called *myAssembly.cs*.</span></span>  

```cmd
csc /t:library myAssembly.cs /reference:myLibAssembly.dll  
```  

## <a name="make-a-run-time-reference-to-a-strong-named-assembly"></a><span data-ttu-id="66a4d-115">对强名称程序集进行运行时引用</span><span class="sxs-lookup"><span data-stu-id="66a4d-115">Make a run-time reference to a strong-named assembly</span></span>  
  
<span data-ttu-id="66a4d-116">对强名称程序集进行运行时引用（例如使用 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 或 <xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType> 方法）时，必须使用引用的强名称程序集的显示名称。</span><span class="sxs-lookup"><span data-stu-id="66a4d-116">When you make a run-time reference to a strong-named assembly, for example by using the <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> or <xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType> method, you must use the display name of the referenced strong-named assembly.</span></span> <span data-ttu-id="66a4d-117">显示名称的语法如下：</span><span class="sxs-lookup"><span data-stu-id="66a4d-117">The syntax of a display name is as follows:</span></span>  

<span data-ttu-id="66a4d-118">\<assembly name>, \<version number>, \<culture>, \<public key token></span><span class="sxs-lookup"><span data-stu-id="66a4d-118">\<*assembly name*>**,** \<*version number*>**,** \<*culture*>**,** \<*public key token*></span></span>  

<span data-ttu-id="66a4d-119">例如:</span><span class="sxs-lookup"><span data-stu-id="66a4d-119">For example:</span></span>  

```console
myDll, Version=1.1.0.0, Culture=en, PublicKeyToken=03689116d3a4ae33   
```  

<span data-ttu-id="66a4d-120">在此示例中，`PublicKeyToken` 是十六进制格式的公钥标记。</span><span class="sxs-lookup"><span data-stu-id="66a4d-120">In this example, `PublicKeyToken` is the hexadecimal form of the public key token.</span></span> <span data-ttu-id="66a4d-121">如果没有区域性值，请使用 `Culture=neutral`。</span><span class="sxs-lookup"><span data-stu-id="66a4d-121">If there is no culture value, use `Culture=neutral`.</span></span>  

<span data-ttu-id="66a4d-122">下面的代码示例演示如何将此信息用于 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="66a4d-122">The following code example shows how to use this information with the <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method.</span></span>  

```cpp
Assembly^ myDll =
    Assembly::Load("myDll, Version=1.0.0.1, Culture=neutral, PublicKeyToken=9b35aa32c18d4fb1");
```

```csharp
Assembly myDll =
    Assembly.Load("myDll, Version=1.0.0.1, Culture=neutral, PublicKeyToken=9b35aa32c18d4fb1");
```

```vb
Dim myDll As Assembly = _
    Assembly.Load("myDll, Version=1.0.0.1, Culture=neutral, PublicKeyToken=9b35aa32c18d4fb1")
```

<span data-ttu-id="66a4d-123">可使用以下[强名称 (Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md) 命令为特定程序集打印十六进制格式的公钥和公钥标记：</span><span class="sxs-lookup"><span data-stu-id="66a4d-123">You can print the hexadecimal format of the public key and public key token for a specific assembly by using the following [Strong Name (Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md) command:</span></span>  

<span data-ttu-id="66a4d-124">sn -Tp \< assembly ></span><span class="sxs-lookup"><span data-stu-id="66a4d-124">**sn -Tp \<** *assembly* **>**</span></span>  

<span data-ttu-id="66a4d-125">如果有公钥文件，则可改用以下命令（请注意命令行选项大小写的区别）：</span><span class="sxs-lookup"><span data-stu-id="66a4d-125">If you have a public key file, you can use the following command instead (note the difference in case on the command-line option):</span></span>  

<span data-ttu-id="66a4d-126">**sn -tp \<** *公钥文件* **>**</span><span class="sxs-lookup"><span data-stu-id="66a4d-126">**sn -tp \<** *public key file* **>**</span></span>  

## <a name="see-also"></a><span data-ttu-id="66a4d-127">请参阅</span><span class="sxs-lookup"><span data-stu-id="66a4d-127">See also</span></span>

- [<span data-ttu-id="66a4d-128">创建和使用具有强名称的程序集</span><span class="sxs-lookup"><span data-stu-id="66a4d-128">Create and use strong-named assemblies</span></span>](create-use-strong-named.md)