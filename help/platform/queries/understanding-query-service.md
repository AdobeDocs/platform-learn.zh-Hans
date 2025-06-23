---
title: 查询服务和数据Distiller概述
description: Adobe Experience Platform查询服务使用户能够使用SQL浏览、验证和转换存储在Data Lake中的客户体验数据，并通过数据Distiller加载项提供增强的功能，如数据输出和计划。 此视频概述了一些核心功能，以帮助用户了解如何跨各种基于平台的应用程序利用查询服务。
feature: Queries
role: Data Engineer, Developer
level: Beginner
jira: KT-3139
last-substantial-update: 2025-06-23T00:00:00Z
exl-id: 988bc316-9eec-4dca-8049-95c2d613379d
source-git-commit: b0466e114d657c2584b23bfd76e4f6c185c83c06
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 13%

---

# 查询服务和数据Distiller概述

Adobe Experience Platform查询服务使用户能够使用SQL浏览、验证和转换存储在Data Lake中的客户体验数据，并通过数据Distiller加载项提供增强的功能，如数据输出和计划。 此视频概述了一些核心功能，以帮助用户了解如何跨各种基于平台的应用程序利用查询服务。 有关详细信息，请访问[查询服务文档](https://experienceleague.adobe.com/en/docs/experience-platform/query/home)。

>[!VIDEO](https://video.tv.adobe.com/v/29795?learn=on&enablevpops)

## 基本用法

<!-- CARDS
* query-service-ui.md
* query-service-api.md
* adobe-defined-functions.md
* run-queries.md
* understanding-data-usage-patterns-with-query-service.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Query Service UI">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="query-service-ui.md" title="查询服务UI" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333403?format=jpeg&nocache=1740415310696" alt="查询服务UI"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="query-service-ui.md" target="_blank" rel="referrer" title="查询服务UI">查询服务UI</a>
                    </p>
                    <p class="is-size-6">了解如何在 Adobe Experience Platform 查询服务中编写和执行查询、查看以前执行的查询以及访问由 IMS 组织内的其他用户保存的查询。</p>
                </div>
                <a href="query-service-ui.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Query Service API">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="query-service-api.md" title="查询服务API" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333700?format=jpeg&nocache=1740415310716" alt="查询服务API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="query-service-api.md" target="_blank" rel="referrer" title="查询服务API">查询服务API</a>
                    </p>
                    <p class="is-size-6">了解如何使用Adobe Experience Platform查询服务API编写和执行查询、创建计划查询以及创建查询模板。</p>
                </div>
                <a href="query-service-api.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Adobe Defined Functions">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="adobe-defined-functions.md" title="Adobe定义的函数" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333701?format=jpeg&nocache=1740415310668" alt="Adobe定义的函数"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="adobe-defined-functions.md" target="_blank" rel="referrer" title="Adobe定义的函数">Adobe定义的函数</a>
                    </p>
                    <p class="is-size-6">了解如何在Adobe Experience Platform查询服务中使用Adobe定义的函数来对体验事件数据执行常见的业务相关任务。</p>
                </div>
                <a href="adobe-defined-functions.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Run Queries with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="run-queries.md" title="使用查询服务运行查询" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29796?format=jpeg&nocache=1740415310683" alt="使用查询服务运行查询"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="run-queries.md" target="_blank" rel="referrer" title="使用查询服务运行查询">使用查询服务运行查询</a>
                    </p>
                    <p class="is-size-6">本视频说明如何在Adobe Experience Platform界面和PSQL客户端中运行查询。 此外，还演示了在XDM对象中使用单个属性、使用Adobe定义的函数以及使用CREATE TABLE AS SELECT (CTAS)。</p>
                </div>
                <a href="run-queries.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Understanding Data Usage Patterns with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="understanding-data-usage-patterns-with-query-service.md" title="了解使用查询服务的数据使用模式" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29811?format=jpeg&nocache=1740415310706" alt="了解使用查询服务的数据使用模式"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" title="了解使用查询服务的数据使用模式">了解查询服务的数据使用模式</a>
                    </p>
                    <p class="is-size-6">此视频分享有关在查询编辑器界面、PSQL客户端、商业智能(BI)解决方案和HTTP API中运行查询的提示和最佳实践。</p>
                </div>
                <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 数据验证和探索

<!-- CARDS
* explore-data.md
* validate-data-in-the-datalake.md
* 
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Explore data">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="explore-data.md" title="浏览数据" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333415?format=jpeg&nocache=1740415312087" alt="浏览数据"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="explore-data.md" target="_blank" rel="referrer" title="浏览数据">浏览数据</a>
                    </p>
                    <p class="is-size-6">了解如何使用 SQL 函数验证提取的数据、预览数据以及探索数据的统计和分析属性。</p>
                </div>
                <a href="explore-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Validate data in the datalake with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="validate-data-in-the-datalake.md" title="使用查询服务验证Datalake中的数据" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3416130?format=jpeg&nocache=1740415312076" alt="使用查询服务验证Datalake中的数据"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="validate-data-in-the-datalake.md" target="_blank" rel="referrer" title="使用查询服务验证Datalake中的数据">使用查询服务验证datalake中的数据</a>
                    </p>
                    <p class="is-size-6">了解如何使用Adobe Experience Platform的查询服务验证数据是否已成功引入datalake。</p>
                </div>
                <a href="validate-data-in-the-datalake.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 使用Data Distiller进行数据转换

<!-- CARDS
* 
* prepare-data.md
* 
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Prepare data">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="prepare-data.md" title="准备数据" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333699?format=jpeg&nocache=1740415313086" alt="准备数据"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="prepare-data.md" target="_blank" rel="referrer" title="准备数据">准备数据</a>
                    </p>
                    <p class="is-size-6">了解如何清理、准备和合并来自多个数据集的数据，以使用CTAS(Create Table AS)和Spark SQL函数创建新的数据集以用于报告和仪表板。</p>
                </div>
                <a href="prepare-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 用例

<!-- CARDS
* understanding-data-usage-patterns-with-query-service.md
* psql-client-tableau.md
* analyze-and-visualize.md
* recharge-your-customer-data.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Understanding Data Usage Patterns with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="understanding-data-usage-patterns-with-query-service.md" title="了解使用查询服务的数据使用模式" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29811?format=jpeg&nocache=1740415313190" alt="了解使用查询服务的数据使用模式"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" title="了解使用查询服务的数据使用模式">了解查询服务的数据使用模式</a>
                    </p>
                    <p class="is-size-6">此视频分享有关在查询编辑器界面、PSQL客户端、商业智能(BI)解决方案和HTTP API中运行查询的提示和最佳实践。</p>
                </div>
                <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Connect Tableau to Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="psql-client-tableau.md" title="将Tableau连接到查询服务" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333702?format=jpeg&nocache=1740415313229" alt="将Tableau连接到查询服务"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="psql-client-tableau.md" target="_blank" rel="referrer" title="将Tableau连接到查询服务">将 Tableau 连接到查询服务</a>
                    </p>
                    <p class="is-size-6">了解如何从各种支持PostgreSQL协议的桌面客户端应用程序连接到查询服务，以及如何使用PostgreSQL工具和驱动程序连接和写入查询。</p>
                </div>
                <a href="psql-client-tableau.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Analyze and visualize omni-channel insights in Tableau using Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="analyze-and-visualize.md" title="在Tableau中使用查询服务分析和可视化全渠道洞察" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/342115?format=jpeg&nocache=1740415313204" alt="在Tableau中使用查询服务分析和可视化全渠道洞察"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="analyze-and-visualize.md" target="_blank" rel="referrer" title="在Tableau中使用查询服务分析和可视化全渠道洞察">使用查询服务在 Tableau 中分析和可视化全渠道洞察</a>
                    </p>
                    <p class="is-size-6">通过客户流失分析示例，了解如何将 Adobe Experience Platform 的查询服务与外部数据可视化工具结合使用。</p>
                </div>
                <a href="analyze-and-visualize.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Recharge your customer data to deliver electrifying experiences">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="recharge-your-customer-data.md" title="为您的客户数据重新充电，以提供令人振奋的体验" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/342533?format=jpeg&nocache=1740415313218" alt="为您的客户数据重新充电，以提供令人振奋的体验"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="recharge-your-customer-data.md" target="_blank" rel="referrer" title="为您的客户数据重新充电，以提供令人振奋的体验">为您的客户数据重新充电，以提供令人振奋的体验</a>
                    </p>
                    <p class="is-size-6">了解如何减轻低质量数据的影响，缩短实现价值的时间，并通过在多种用例中使用相同的数据来提高ROI。</p>
                </div>
                <a href="recharge-your-customer-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
