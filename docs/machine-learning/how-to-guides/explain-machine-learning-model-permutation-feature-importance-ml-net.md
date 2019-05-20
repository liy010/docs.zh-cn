---
title: 使用排列特征重要性解释模型预测
description: 在 ML.NET 中使用排列功能的重要性来理解模型功能的重要性
ms.date: 05/02/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc,how-to
ms.openlocfilehash: 2f444508990a902a1c61b72b1be2263d8d93ba70
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65065640"
---
# <a name="explain-model-predictions-using-permutation-feature-importance"></a><span data-ttu-id="39604-103">使用排列特征重要性解释模型预测</span><span class="sxs-lookup"><span data-stu-id="39604-103">Explain model predictions using Permutation Feature Importance</span></span>

<span data-ttu-id="39604-104">借助排列特征重要性 (PFI) 理解特征对预测的贡献，了解如何解释 ML.NET 机器学习模型预测。</span><span class="sxs-lookup"><span data-stu-id="39604-104">Learn how to explain ML.NET machine learning model predictions by understanding the contribution features have to predictions using Permutation Feature Importance (PFI).</span></span>

<span data-ttu-id="39604-105">机器学习模型通常被视为黑盒，它们接收输入并生成输出。</span><span class="sxs-lookup"><span data-stu-id="39604-105">Machine learning models are often thought of as black boxes that take inputs and generate an output.</span></span> <span data-ttu-id="39604-106">人们对影响输出的中间步骤或特征之间的交互了解甚少。</span><span class="sxs-lookup"><span data-stu-id="39604-106">The intermediate steps or interactions among the features that influence the output are rarely understood.</span></span> <span data-ttu-id="39604-107">随着机器学习被引入日常生活的更多方面（例如医疗保健），理解机器学习模型为何做出其决策变得至关重要。</span><span class="sxs-lookup"><span data-stu-id="39604-107">As machine learning is introduced into more aspects of everyday life such as healthcare, it's of utmost importance to understand why a machine learning model makes the decisions it does.</span></span> <span data-ttu-id="39604-108">例如，如果诊断由机器学习模型做出，则医疗保健专业人员需要查看影响做出诊断的因素的方法。</span><span class="sxs-lookup"><span data-stu-id="39604-108">For example, if diagnoses are made by a machine learning model, healthcare professionals need a way to look into the factors that went into making that diagnoses.</span></span> <span data-ttu-id="39604-109">提供正确的诊断可以对患者是否快速康复产生重大影响。</span><span class="sxs-lookup"><span data-stu-id="39604-109">Providing the right diagnosis could make a great difference on whether a patient has a speedy recovery or not.</span></span> <span data-ttu-id="39604-110">因此，模型的可解释性水平越高，医疗保健专业人员就越有信心接受或拒绝模型做出的决策。</span><span class="sxs-lookup"><span data-stu-id="39604-110">Therefore the higher the level of explainability in a model, the greater confidence healthcare professionals have to accept or reject the decisions made by the model.</span></span>

<span data-ttu-id="39604-111">有各种技术被用于解释模型，其中之一是 PFI。</span><span class="sxs-lookup"><span data-stu-id="39604-111">Various techniques are used to explain models, one of which is PFI.</span></span> <span data-ttu-id="39604-112">PFI 是一种用于解释分类和回归模型的技术，其灵感来自 [Breima 的 *Random Forests*（随机森林）论文](https://www.stat.berkeley.edu/~breiman/randomforest2001.pdf)（参见第 10 部分）。</span><span class="sxs-lookup"><span data-stu-id="39604-112">PFI is a technique used to explain classification and regression models that is inspired by [Breiman's *Random Forests* paper](https://www.stat.berkeley.edu/~breiman/randomforest2001.pdf)(see section 10).</span></span> <span data-ttu-id="39604-113">概括而言，其工作原理是一次随机为整个数据集随机抽取数据的一个特征，并计算关注性能指标的下降程度。</span><span class="sxs-lookup"><span data-stu-id="39604-113">At a high level, the way it works is by randomly shuffling data one feature at a time for the entire dataset and calculating how much the performance metric of interest decreases.</span></span> <span data-ttu-id="39604-114">变化越大，特征就越重要。</span><span class="sxs-lookup"><span data-stu-id="39604-114">The larger the change, the more important that feature is.</span></span> 

<span data-ttu-id="39604-115">此外，通过突出显示最重要的特征，模型生成器可以专注于使用一组更有意义的特征，这可能会减少干扰和训练时间。</span><span class="sxs-lookup"><span data-stu-id="39604-115">Additionally, by highlighting the most important features, model builders can focus on using a subset of more meaningful features which can potentially reduce noise and training time.</span></span>

## <a name="load-the-data"></a><span data-ttu-id="39604-116">加载数据</span><span class="sxs-lookup"><span data-stu-id="39604-116">Load the data</span></span>

<span data-ttu-id="39604-117">数据集中用于此示例的特征位于列 1-12 中。</span><span class="sxs-lookup"><span data-stu-id="39604-117">The features in the dataset being used for this sample are in columns 1-12.</span></span> <span data-ttu-id="39604-118">目标在于预测 `Price`。</span><span class="sxs-lookup"><span data-stu-id="39604-118">The goal is to predict `Price`.</span></span> 

| <span data-ttu-id="39604-119">列</span><span class="sxs-lookup"><span data-stu-id="39604-119">Column</span></span> | <span data-ttu-id="39604-120">功能</span><span class="sxs-lookup"><span data-stu-id="39604-120">Feature</span></span> | <span data-ttu-id="39604-121">说明</span><span class="sxs-lookup"><span data-stu-id="39604-121">Description</span></span> 
| --- | --- | --- |
| <span data-ttu-id="39604-122">1</span><span class="sxs-lookup"><span data-stu-id="39604-122">1</span></span> | <span data-ttu-id="39604-123">CrimeRate</span><span class="sxs-lookup"><span data-stu-id="39604-123">CrimeRate</span></span> | <span data-ttu-id="39604-124">人均犯罪率</span><span class="sxs-lookup"><span data-stu-id="39604-124">Per capita crime rate</span></span>
| <span data-ttu-id="39604-125">2</span><span class="sxs-lookup"><span data-stu-id="39604-125">2</span></span> | <span data-ttu-id="39604-126">ResidentialZones</span><span class="sxs-lookup"><span data-stu-id="39604-126">ResidentialZones</span></span> | <span data-ttu-id="39604-127">城镇住宅区</span><span class="sxs-lookup"><span data-stu-id="39604-127">Residential zones in town</span></span>
| <span data-ttu-id="39604-128">3</span><span class="sxs-lookup"><span data-stu-id="39604-128">3</span></span> | <span data-ttu-id="39604-129">CommercialZones</span><span class="sxs-lookup"><span data-stu-id="39604-129">CommercialZones</span></span> | <span data-ttu-id="39604-130">城镇非住宅区</span><span class="sxs-lookup"><span data-stu-id="39604-130">Non-residential zones in town</span></span>
| <span data-ttu-id="39604-131">4</span><span class="sxs-lookup"><span data-stu-id="39604-131">4</span></span> | <span data-ttu-id="39604-132">NearWater</span><span class="sxs-lookup"><span data-stu-id="39604-132">NearWater</span></span> | <span data-ttu-id="39604-133">距水体的距离</span><span class="sxs-lookup"><span data-stu-id="39604-133">Proximity to body of water</span></span>
| <span data-ttu-id="39604-134">5</span><span class="sxs-lookup"><span data-stu-id="39604-134">5</span></span> | <span data-ttu-id="39604-135">ToxicWasteLevels</span><span class="sxs-lookup"><span data-stu-id="39604-135">ToxicWasteLevels</span></span> | <span data-ttu-id="39604-136">毒性程度 (PPM)</span><span class="sxs-lookup"><span data-stu-id="39604-136">Toxicity levels (PPM)</span></span>
| <span data-ttu-id="39604-137">6</span><span class="sxs-lookup"><span data-stu-id="39604-137">6</span></span> | <span data-ttu-id="39604-138">AverageRoomNumber</span><span class="sxs-lookup"><span data-stu-id="39604-138">AverageRoomNumber</span></span> | <span data-ttu-id="39604-139">房屋平均房间数量</span><span class="sxs-lookup"><span data-stu-id="39604-139">Average number of rooms in house</span></span>
| <span data-ttu-id="39604-140">7</span><span class="sxs-lookup"><span data-stu-id="39604-140">7</span></span> | <span data-ttu-id="39604-141">HomeAge</span><span class="sxs-lookup"><span data-stu-id="39604-141">HomeAge</span></span> | <span data-ttu-id="39604-142">楼龄</span><span class="sxs-lookup"><span data-stu-id="39604-142">Age of home</span></span>
| <span data-ttu-id="39604-143">8</span><span class="sxs-lookup"><span data-stu-id="39604-143">8</span></span> | <span data-ttu-id="39604-144">BusinessCenterDistance</span><span class="sxs-lookup"><span data-stu-id="39604-144">BusinessCenterDistance</span></span> | <span data-ttu-id="39604-145">与最近商业区的距离</span><span class="sxs-lookup"><span data-stu-id="39604-145">Distance to nearest business district</span></span>
| <span data-ttu-id="39604-146">9</span><span class="sxs-lookup"><span data-stu-id="39604-146">9</span></span> | <span data-ttu-id="39604-147">HighwayAccess</span><span class="sxs-lookup"><span data-stu-id="39604-147">HighwayAccess</span></span> | <span data-ttu-id="39604-148">距公路的距离</span><span class="sxs-lookup"><span data-stu-id="39604-148">Proximity to highways</span></span>
| <span data-ttu-id="39604-149">10</span><span class="sxs-lookup"><span data-stu-id="39604-149">10</span></span> | <span data-ttu-id="39604-150">TaxRate</span><span class="sxs-lookup"><span data-stu-id="39604-150">TaxRate</span></span> | <span data-ttu-id="39604-151">财产税率</span><span class="sxs-lookup"><span data-stu-id="39604-151">Property tax rate</span></span>
| <span data-ttu-id="39604-152">11</span><span class="sxs-lookup"><span data-stu-id="39604-152">11</span></span> | <span data-ttu-id="39604-153">StudentTeacherRatio</span><span class="sxs-lookup"><span data-stu-id="39604-153">StudentTeacherRatio</span></span> | <span data-ttu-id="39604-154">师生比率</span><span class="sxs-lookup"><span data-stu-id="39604-154">Ratio of students to teachers</span></span>
| <span data-ttu-id="39604-155">12</span><span class="sxs-lookup"><span data-stu-id="39604-155">12</span></span> | <span data-ttu-id="39604-156">PercentPopulationBelowPoverty</span><span class="sxs-lookup"><span data-stu-id="39604-156">PercentPopulationBelowPoverty</span></span> | <span data-ttu-id="39604-157">贫困线以下人口百分比</span><span class="sxs-lookup"><span data-stu-id="39604-157">Percent of population living below poverty</span></span>
| <span data-ttu-id="39604-158">13</span><span class="sxs-lookup"><span data-stu-id="39604-158">13</span></span> | <span data-ttu-id="39604-159">Price</span><span class="sxs-lookup"><span data-stu-id="39604-159">Price</span></span> | <span data-ttu-id="39604-160">住宅价格</span><span class="sxs-lookup"><span data-stu-id="39604-160">Price of the home</span></span>

<span data-ttu-id="39604-161">数据集的示例如下所示：</span><span class="sxs-lookup"><span data-stu-id="39604-161">A sample of the dataset is shown below:</span></span>

```text
1,24,13,1,0.59,3,96,11,23,608,14,13,32
4,80,18,1,0.37,5,14,7,4,346,19,13,41
2,98,16,1,0.25,10,5,1,8,689,13,36,12
```

<span data-ttu-id="39604-162">此示例中的数据可以由 `HousingPriceData` 等类进行建模：</span><span class="sxs-lookup"><span data-stu-id="39604-162">The data in this sample can be modeled by a class like `HousingPriceData`:</span></span>

```csharp
class HousingPriceData
{
    [LoadColumn(0)]
    public float CrimeRate { get; set; }

    [LoadColumn(1)]
    public float ResidentialZones { get; set; }

    [LoadColumn(2)]
    public float CommercialZones { get; set; }

    [LoadColumn(3)]
    public float NearWater { get; set; }

    [LoadColumn(4)]
    public float ToxicWasteLevels { get; set; }

    [LoadColumn(5)]
    public float AverageRoomNumber { get; set; }

    [LoadColumn(6)]
    public float HomeAge { get; set; }

    [LoadColumn(7)]
    public float BusinessCenterDistance { get; set; }

    [LoadColumn(8)]
    public float HighwayAccess { get; set; }

    [LoadColumn(9)]
    public float TaxRate { get; set; }

    [LoadColumn(10)]
    public float StudentTeacherRatio { get; set; }

    [LoadColumn(11)]
    public float PercentPopulationBelowPoverty { get; set; }

    [LoadColumn(12)]
    [ColumnName("Label")]
    public float Price { get; set; }
}
```

<span data-ttu-id="39604-163">将数据加载到 [`IDataView`](xref:Microsoft.ML.IDataView) 中。</span><span class="sxs-lookup"><span data-stu-id="39604-163">Load the data into an [`IDataView`](xref:Microsoft.ML.IDataView).</span></span>

## <a name="train-the-model"></a><span data-ttu-id="39604-164">定型模型</span><span class="sxs-lookup"><span data-stu-id="39604-164">Train the model</span></span>

<span data-ttu-id="39604-165">下面的代码示例演示了训练线性回归模型用于预测房屋价格的过程。</span><span class="sxs-lookup"><span data-stu-id="39604-165">The code sample below illustrates the process of training a linear regression model to predict house prices.</span></span>

```csharp
// 1. Get the column name of input features.
string[] featureColumnNames = 
    data.Schema
        .Select(column => column.Name)
        .Where(columnName => columnName != "Label").ToArray();

// 2. Define estimator with data pre-processing steps
IEstimator<ITransformer> dataPrepEstimator =
    mlContext.Transforms.Concatenate("Features", featureColumnNames)
        .Append(mlContext.Transforms.NormalizeMinMax("Features"));

// 3. Create transformer using the data pre-processing estimator
ITransformer dataPrepTransformer = dataPrepEstimator.Fit(data);

// 4. Pre-process the training data
IDataView preprocessedTrainData = dataPrepTransformer.Transform(data);

// 5. Define Stochastic Dual Coordinate Ascent machine learning estimator
var sdcaEstimator = mlContext.Regression.Trainers.Sdca();

// 6. Train machine learning model
var sdcaModel = sdcaEstimator.Fit(preprocessedTrainData);
```

## <a name="explain-the-model-with-permutation-feature-importance-pfi"></a><span data-ttu-id="39604-166">使用排列特征重要性 (PFI) 解释模型</span><span class="sxs-lookup"><span data-stu-id="39604-166">Explain the model with Permutation Feature Importance (PFI)</span></span>

<span data-ttu-id="39604-167">在 ML.NET 中，为相应的任务使用 [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) 方法。</span><span class="sxs-lookup"><span data-stu-id="39604-167">In ML.NET use the [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) method for your respective task.</span></span>

```csharp
ImmutableArray<RegressionMetricsStatistics> permutationFeatureImportance = 
    mlContext
        .Regression
        .PermutationFeatureImportance(sdcaModel, preprocessedTrainData, permutationCount:3);
```

<span data-ttu-id="39604-168">在训练数据集上使用 [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) 的结果是 [`RegressionMetricsStatistics`](xref:Microsoft.ML.Data.RegressionMetricsStatistics) 对象的 [`ImmutableArray`](xref:System.Collections.Immutable.ImmutableArray)。</span><span class="sxs-lookup"><span data-stu-id="39604-168">The result of using [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) on the training dataset is an [`ImmutableArray`](xref:System.Collections.Immutable.ImmutableArray) of [`RegressionMetricsStatistics`](xref:Microsoft.ML.Data.RegressionMetricsStatistics) objects.</span></span> <span data-ttu-id="39604-169">[`RegressionMetricsStatistics`](xref:Microsoft.ML.Data.RegressionMetricsStatistics) 提供 [`RegressionMetrics`](xref:Microsoft.ML.Data.RegressionMetrics) 的多个观测值的均值和标准差等摘要统计信息，观测值数量等于 `permutationCount` 参数指定的排列数。</span><span class="sxs-lookup"><span data-stu-id="39604-169">[`RegressionMetricsStatistics`](xref:Microsoft.ML.Data.RegressionMetricsStatistics) provides summary statistics like mean and standard deviation for multiple observations of [`RegressionMetrics`](xref:Microsoft.ML.Data.RegressionMetrics) equal to the number of permutations specified by the `permutationCount` parameter.</span></span>

<span data-ttu-id="39604-170">重要性（在本例中，由 [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) 计算的 R 平方指标的绝对平均下降）可随后按从最重要到最不重要的顺序排序。</span><span class="sxs-lookup"><span data-stu-id="39604-170">The importance, or in this case, the absolute average decrease in R-squared metric calculated by [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) can then be ordered from most important to least important.</span></span>  

```csharp
// Order features by importance
var featureImportanceMetrics =
    permutationFeatureImportance
        .Select((metric, index) => new { index, metric.RSquared })
        .OrderByDescending(myFeatures => Math.Abs(myFeatures.RSquared.Mean));

Console.WriteLine("Feature\tPFI");

foreach (var feature in featureImportanceMetrics)
{
    Console.WriteLine($"{featureColumnNames[feature.index],-20}|\t{feature.RSquared.Mean:F6}");
}
```

<span data-ttu-id="39604-171">打印 `featureImportanceMetrics` 中每个特征的值将生成类似如下的输出。</span><span class="sxs-lookup"><span data-stu-id="39604-171">Printing the values for each of the features in `featureImportanceMetrics` would generate output similar to that below.</span></span> <span data-ttu-id="39604-172">请记住，应该预期看到不同的结果，因为这些值根据其获得的数据而有所不同。</span><span class="sxs-lookup"><span data-stu-id="39604-172">Keep in mind that you should expect to see different results because these values vary based on the data that they are given.</span></span>  

| <span data-ttu-id="39604-173">功能</span><span class="sxs-lookup"><span data-stu-id="39604-173">Feature</span></span> | <span data-ttu-id="39604-174">R 平方的变化</span><span class="sxs-lookup"><span data-stu-id="39604-174">Change to R-Squared</span></span> |
|:--|:--:|
<span data-ttu-id="39604-175">HighwayAccess</span><span class="sxs-lookup"><span data-stu-id="39604-175">HighwayAccess</span></span>       |   <span data-ttu-id="39604-176">-0.042731</span><span class="sxs-lookup"><span data-stu-id="39604-176">-0.042731</span></span>
<span data-ttu-id="39604-177">StudentTeacherRatio</span><span class="sxs-lookup"><span data-stu-id="39604-177">StudentTeacherRatio</span></span> |   <span data-ttu-id="39604-178">-0.012730</span><span class="sxs-lookup"><span data-stu-id="39604-178">-0.012730</span></span>
<span data-ttu-id="39604-179">BusinessCenterDistance</span><span class="sxs-lookup"><span data-stu-id="39604-179">BusinessCenterDistance</span></span>| <span data-ttu-id="39604-180">-0.010491</span><span class="sxs-lookup"><span data-stu-id="39604-180">-0.010491</span></span>
<span data-ttu-id="39604-181">TaxRate</span><span class="sxs-lookup"><span data-stu-id="39604-181">TaxRate</span></span>             |   <span data-ttu-id="39604-182">-0.008545</span><span class="sxs-lookup"><span data-stu-id="39604-182">-0.008545</span></span>
<span data-ttu-id="39604-183">AverageRoomNumber</span><span class="sxs-lookup"><span data-stu-id="39604-183">AverageRoomNumber</span></span>   |   <span data-ttu-id="39604-184">-0.003949</span><span class="sxs-lookup"><span data-stu-id="39604-184">-0.003949</span></span>
<span data-ttu-id="39604-185">CrimeRate</span><span class="sxs-lookup"><span data-stu-id="39604-185">CrimeRate</span></span>           |   <span data-ttu-id="39604-186">-0.003665</span><span class="sxs-lookup"><span data-stu-id="39604-186">-0.003665</span></span>
<span data-ttu-id="39604-187">CommercialZones</span><span class="sxs-lookup"><span data-stu-id="39604-187">CommercialZones</span></span>     |   <span data-ttu-id="39604-188">0.002749</span><span class="sxs-lookup"><span data-stu-id="39604-188">0.002749</span></span>
<span data-ttu-id="39604-189">HomeAge</span><span class="sxs-lookup"><span data-stu-id="39604-189">HomeAge</span></span>             |   <span data-ttu-id="39604-190">-0.002426</span><span class="sxs-lookup"><span data-stu-id="39604-190">-0.002426</span></span>
<span data-ttu-id="39604-191">ResidentialZones</span><span class="sxs-lookup"><span data-stu-id="39604-191">ResidentialZones</span></span>    |   <span data-ttu-id="39604-192">-0.002319</span><span class="sxs-lookup"><span data-stu-id="39604-192">-0.002319</span></span>
<span data-ttu-id="39604-193">NearWater</span><span class="sxs-lookup"><span data-stu-id="39604-193">NearWater</span></span>           |   <span data-ttu-id="39604-194">0.000203</span><span class="sxs-lookup"><span data-stu-id="39604-194">0.000203</span></span>
<span data-ttu-id="39604-195">PercentPopulationLivingBelowPoverty</span><span class="sxs-lookup"><span data-stu-id="39604-195">PercentPopulationLivingBelowPoverty</span></span>|    <span data-ttu-id="39604-196">0.000031</span><span class="sxs-lookup"><span data-stu-id="39604-196">0.000031</span></span>
<span data-ttu-id="39604-197">ToxicWasteLevels</span><span class="sxs-lookup"><span data-stu-id="39604-197">ToxicWasteLevels</span></span>    |   <span data-ttu-id="39604-198">-0.000019</span><span class="sxs-lookup"><span data-stu-id="39604-198">-0.000019</span></span>

<span data-ttu-id="39604-199">查看此数据集最重要的五个特征，此模型预测的房屋价格受其与公路的距离、该区域学校的师生比率、与主要就业中心的距离、资产税率和房屋平均房间数量的影响。</span><span class="sxs-lookup"><span data-stu-id="39604-199">Taking a look at the the five most important features for this dataset, the price of a house predicted by this model is influenced by its proximity to highways, student teacher ratio of schools in the area, proximity to major employment centers, property tax rate and average number of rooms in the home.</span></span>