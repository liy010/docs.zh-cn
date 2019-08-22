---
title: 云优化应用程序中的 Microsoft 技术
description: 通过 Azure 云和 Windows 容器实现现有 .NET 应用程序的现代化 |云优化应用程序中的 Microsoft 技术
ms.date: 04/28/2018
ms.openlocfilehash: 915aa99d2331c5b9c46eabef3335fb809baa9370
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "69578220"
---
# <a name="microsoft-technologies-in-cloud-optimized-applications"></a><span data-ttu-id="d7d1c-103">云优化应用程序中的 Microsoft 技术</span><span class="sxs-lookup"><span data-stu-id="d7d1c-103">Microsoft technologies in cloud-optimized applications</span></span>

<span data-ttu-id="d7d1c-104">以下列表描述了可识别为云优化应用程序要求的工具、技术和解决方案。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-104">The following list describes the tools, technologies, and solutions that are recognized as requirements for Cloud-Optimized apps.</span></span> <span data-ttu-id="d7d1c-105">您可以根据自己的优先级有选择地或逐步地采用云优化的元素。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-105">You can adopt Cloud-Optimized elements selectively or gradually, depending on your priorities.</span></span>

- <span data-ttu-id="d7d1c-106">**云基础结构**:提供计算平台、操作系统、网络和存储的基础结构。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-106">**Cloud infrastructure**: The infrastructure that provides the compute platform, operating system, network, and storage.</span></span> <span data-ttu-id="d7d1c-107">Microsoft Azure 位于此级别。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-107">Microsoft Azure is positioned at this level.</span></span>

- <span data-ttu-id="d7d1c-108">**运行时**:此层提供应用程序运行的环境。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-108">**Runtime**: This layer provides the environment for the application to run.</span></span> <span data-ttu-id="d7d1c-109">如果使用的是容器, 则该层通常基于[Docker 引擎](https://docs.docker.com/engine/), 该引擎在 Linux 主机或 Windows 主机上运行。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-109">If you are using containers, this layer usually is based on [Docker Engine](https://docs.docker.com/engine/), running either on Linux hosts or on Windows hosts.</span></span> <span data-ttu-id="d7d1c-110">(从 Windows Server 2016 开始支持[Windows 容器](https://docs.microsoft.com/virtualization/windowscontainers/about/)。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-110">([Windows Containers](https://docs.microsoft.com/virtualization/windowscontainers/about/) are supported beginning with Windows Server 2016.</span></span> <span data-ttu-id="d7d1c-111">Windows 容器是在 Windows 上运行的现有 .NET Framework 应用程序的最佳选择。)</span><span class="sxs-lookup"><span data-stu-id="d7d1c-111">Windows Containers is the best choice for existing .NET Framework applications that run on Windows.)</span></span>

- <span data-ttu-id="d7d1c-112">**托管云**:选择托管云选项后, 你可以避免管理和支持底层基础结构、Vm、OS 修补程序和网络配置的开销和复杂性。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-112">**Managed cloud**: When you choose a managed cloud option, you can avoid the expense and complexity of managing and supporting the underlying infrastructure, VMs, OS patches, and networking configuration.</span></span> <span data-ttu-id="d7d1c-113">如果选择使用 IaaS 进行迁移, 则需要负责所有这些任务以及相关的成本。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-113">If you choose to migrate by using IaaS, you are responsible for all of these tasks, and for associated costs.</span></span> <span data-ttu-id="d7d1c-114">在托管云选项中, 只管理你开发的应用程序和服务。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-114">In a managed cloud option, you manage only the applications and services that you develop.</span></span> <span data-ttu-id="d7d1c-115">云服务提供商通常会管理其他所有内容。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-115">The cloud service provider typically manages everything else.</span></span> <span data-ttu-id="d7d1c-116">Azure 中托管云服务的示例包括[AZURE SQL 数据库](https://azure.microsoft.com/services/sql-database)、 [azure Redis 缓存](https://azure.microsoft.com/services/cache/)、 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)、 [azure 存储](https://azure.microsoft.com/services/storage/)、 [Azure Database for MySQL](https://azure.microsoft.com/services/mysql/)、 [Azure Database for PostgreSQL](https://azure.microsoft.com/services/postgresql/)、 [azure Active目录](https://azure.microsoft.com/services/active-directory/)和托管计算服务, 例如[VM 规模集](https://azure.microsoft.com/services/virtual-machine-scale-sets/)、 [Azure App Service](https://azure.microsoft.com/services/app-service/)和[Azure Kubernetes 服务](https://azure.microsoft.com/services/container-service/)。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-116">Examples of managed cloud services in Azure include [Azure SQL Database](https://azure.microsoft.com/services/sql-database), [Azure Redis Cache](https://azure.microsoft.com/services/cache/), [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), [Azure Storage](https://azure.microsoft.com/services/storage/), [Azure Database for MySQL](https://azure.microsoft.com/services/mysql/), [Azure Database for PostgreSQL](https://azure.microsoft.com/services/postgresql/), [Azure Active Directory](https://azure.microsoft.com/services/active-directory/), and managed compute services like [VM scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Azure App Service](https://azure.microsoft.com/services/app-service/), and [Azure Kubernetes Service](https://azure.microsoft.com/services/container-service/).</span></span>

- <span data-ttu-id="d7d1c-117">**应用程序开发**:生成在容器中运行的应用程序时, 可以选择多种语言。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-117">**Application development**: You can choose from many languages when you build applications that run in containers.</span></span> <span data-ttu-id="d7d1c-118">本指南重点介绍[.net](https://www.microsoft.com/net), 但你可以使用其他语言 (如 Node.js、Python、弹簧/Java 或中转) 来开发基于容器的应用。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-118">This guide focuses on [.NET](https://www.microsoft.com/net), but, you can develop container-based apps by using other languages, like Node.js, Python, Spring/Java, or Go.</span></span>

- <span data-ttu-id="d7d1c-119">**监视、遥测、日志记录和审核**:在云中运行的应用程序和容器的监视和审核功能对于任何云优化的应用程序而言至关重要。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-119">**Monitoring, telemetry, logging, and auditing**: The ability to monitor and audit applications and containers that are running in the cloud is critical for any Cloud-Optimized application.</span></span> <span data-ttu-id="d7d1c-120">[Azure 应用程序 Insights](https://azure.microsoft.com/services/application-insights/)和[Microsoft Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite)是为云优化应用提供监视和审核的主要 Microsoft 工具。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-120">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) and [Microsoft Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite) are the main Microsoft tools that provide monitoring and auditing for Cloud-Optimized apps.</span></span>

- <span data-ttu-id="d7d1c-121">**预配**:自动化工具可帮助你预配基础结构和将应用程序部署到多个环境 (生产、测试、过渡)。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-121">**Provisioning**: Automation tools help you provision the infrastructure and deploy an application to multiple environments (production, testing, staging).</span></span> <span data-ttu-id="d7d1c-122">你可以使用 Chef 和 Puppet 之类的工具来管理应用程序的配置和环境。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-122">You can use tools like Chef and Puppet to manage an application's configuration and environment.</span></span> <span data-ttu-id="d7d1c-123">此层还可以通过使用更简单、更直接的方法来实现。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-123">This layer also can be implemented by using simpler and more direct approaches.</span></span> <span data-ttu-id="d7d1c-124">例如, 你可以使用 Azure 命令行接口 (Azure CLI) 工具直接部署, 然后在[Azure DevOps Services](https://azure.microsoft.com/services/devops/)中使用连续部署和发布管理管道。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-124">For example, you can deploy directly by using Azure command-line interface (Azure CLI) tooling, and then use the continuous deployment and release management pipelines in [Azure DevOps Services](https://azure.microsoft.com/services/devops/).</span></span>

- <span data-ttu-id="d7d1c-125">**应用程序生命周期**:[Azure DevOps Services](https://azure.microsoft.com/services/devops/)和其他工具 (如 Jenkins) 都是构建自动化服务器, 可帮助你实现 CI/CD 管道, 包括 release management。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-125">**Application lifecycle**: [Azure DevOps Services](https://azure.microsoft.com/services/devops/) and other tools, like Jenkins, are built automation servers that help you implement CI/CD pipelines, including release management.</span></span>

<span data-ttu-id="d7d1c-126">本章的后续部分以及相关演练专门针对有关运行时层 (Windows 容器) 的详细信息。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-126">The next sections of this chapter, and the related walkthroughs, focus specifically on details about the runtime layer (Windows Containers).</span></span> <span data-ttu-id="d7d1c-127">本指南介绍了在 Windows Server 2016 (及更高版本) Vm 和 Azure 容器实例上部署 Windows 容器的方式。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-127">The guidance describes the ways you can deploy Windows Containers on Windows Server 2016 (and later versions) VMs and Azure Container Instances.</span></span> <span data-ttu-id="d7d1c-128">它还介绍了更高级的 PaaS 平台, 如 Azure App Service 和 orchestrator, 如 Azure Kubernetes Service。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-128">It also covers more advanced PaaS platforms like Azure App Service and orchestrator like Azure Kubernetes Service.</span></span>

## <a name="monolithic-applications-can-be-cloud-optimized"></a><span data-ttu-id="d7d1c-129">单个应用程序*可以*进行云优化</span><span class="sxs-lookup"><span data-stu-id="d7d1c-129">Monolithic applications *can* be Cloud-Optimized</span></span>

<span data-ttu-id="d7d1c-130">重要的是, 重点强调单一应用程序 (不基于微服务的应用程序)*可以*是云优化的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-130">It's important to highlight that monolithic applications (applications that are not based on microservices) *can* be Cloud-Optimized applications.</span></span> <span data-ttu-id="d7d1c-131">你可以使用容器、持续交付和 DevOps 的组合来构建和运行利用云计算模型的单一应用程序。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-131">You can build and operate monolithic applications that take advantage of the cloud computing model by using a combination of containers, continuous delivery, and DevOps.</span></span> <span data-ttu-id="d7d1c-132">如果现有的单一应用程序适用于你的业务目标, 则可以将其现代化, 并使其成为云优化的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-132">If an existing monolithic application is right for your business goals, you can modernize it and make it Cloud-Optimized.</span></span>

<span data-ttu-id="d7d1c-133">同样, 如果单一应用程序可以是云优化的应用程序, 其他更复杂的体系结构 (如 N 层应用程序) 也可以现代化为云优化的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d7d1c-133">Similarly, if monolithic applications can be Cloud-Optimized applications, other, more complex architectures like N-Tier applications can also be modernized as Cloud-Optimized applications.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="d7d1c-134">[上一页](reasons-to-modernize-existing-net-apps-to-cloud-optimized-applications.md)
>[下一页](what-about-cloud-native-applications.md)</span><span class="sxs-lookup"><span data-stu-id="d7d1c-134">[Previous](reasons-to-modernize-existing-net-apps-to-cloud-optimized-applications.md)
[Next](what-about-cloud-native-applications.md)</span></span>