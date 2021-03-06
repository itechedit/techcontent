<properties
    pageTitle="SQL 数据库性能：服务层 | Azure"
    description="比较 SQL 数据库服务层。"
    keywords="数据库选项,数据库性能"
    services="sql-database"
    documentationcenter=""
    author="janeng"
    manager="jhubbard"
    editor="" />
<tags
    ms.assetid="f5c5c596-cd1e-451f-92a7-b70d4916e974"
    ms.service="sql-database"
    ms.custom="overview"
    ms.devlang="na"
    ms.topic="article"
    ms.tgt_pltfrm="na"
    ms.workload="data-management"
    ms.date="02/09/2017"
    wacn.date="03/24/2017"
    ms.author="janeng" />

# SQL 数据库选项和性能：了解每个服务层提供的功能
[Azure SQL 数据库](/documentation/articles/sql-database-technical-overview/)提供了三个具有多个性能级别的服务层（**基本**、**标准**、**高级**和**高级 RS**），用于处理不同的工作负荷。更高的性能级别提供不断增加的资源，旨在递增式提供更高的吞吐量。无需停机[即可动态更改服务层和性能级别](/documentation/articles/sql-database-service-tiers/)。基本、标准和高级服务层都提供 99.99% 的运行时间 SLA、灵活的业务连续性选项、安全功能和按小时计费。高级 RS 服务层提供和高级服务层相同的性能级别、安全功能和业务连续性，以及相对低的 SLA。

>[AZURE.IMPORTANT]高级 RS 数据库运行的冗余副本的数量比标准和高级层的数据库低。所以当遇到服务失败时，你可能需要通过一个最多滞后5分钟的备份来恢复数据库。

可以在所选[性能级别](/documentation/articles/sql-database-service-tiers/#single-database-service-tiers-and-performance-levels)上使用专用资源创建单一数据库。还可以在资源在数据库之间共享的[弹性池](/documentation/articles/sql-database-service-tiers/#elastic-pool-service-tiers-and-performance-in-edtus)中管理多个数据库。可用于单一数据库的资源以数据库事务单位 (DTU) 表示，可用于弹性池的资源则用弹性 DTU (eDTU) 表示。有关 DTU 和 eDTU 的详细信息，请参阅[什么是 DTU？](/documentation/articles/sql-database-what-is-a-dtu/)。

在这两种情况下，服务层包括“基本”、“标准”和“高级”。

## 选择服务层
下表提供了最适用于不同应用程序工作负荷的层的示例。

| 服务层 | 目标工作负荷 |
| :--- | --- |
| **基本** | 最适合小型数据库，通常支持在给定时间执行一个活动操作。示例包括用于开发或测试的数据库，或不常使用的小型应用程序。 |
| **标准** |云应用程序的转到选项，提供低到中等的 IO 性能要求，并支持多个并发查询。示例包括工作组或 Web 应用程序。 |
| **高级** | 专为高事务量设计，提供高 IO 性能要求，并支持许多并发用户。示例包括支持任务关键型应用程序的数据库。 |
| **高级 RS** | 专为具有 IO 密集型工作负载但不需要最高可用性保证的客户设计。示例包括测试高性能工作负载，或分析数据库不是记录系统的工作负载。 |

首先确定是要运行单一数据库，还是要运行共享资源的组数据库。查看[弹性池注意事项](/documentation/articles/sql-database-elastic-pool-guidance/)。若要确定服务层，首先确定所需的最小数据库功能：

| **服务层功能** | **基本** | **标准** | **高级** | **高级 RS**|
| :-- | --: | --: | --: | --: |
| 单个数据库的最大数据库大小 | 2 GB | 250 GB | 4 TB*  | 500 GB  |
| 弹性池的最大总存储 | 117 GB | 1200 GB | 750 GB | 750 GB |
| 每个池的最大数据库数 | 400  | 400 | 50 | 50 |
| 数据库备份保留期 | 7 days | 35 days | 35 days | 35 days |
||||||


确定最低服务层后，就可以确定数据库的性能级别（DTU 数）。通常情况下，一开始可以使用标准 S2 和 S3 性能级别。对于具有较高 CPU 或 IO 要求的数据库，高级性能级别是合适的起点。与最高的标准性能级别相比，高级性能级别提供更多 CPU 和至少高 10 倍的 IO。



##<a name="standalone-database-service-tiers-and-performance-levels"></a> 单一数据库服务层和性能级别
对于单一数据库，每个服务层内都具有多个性能级别。你可以灵活选择最能满足你的工作负荷需求的级别。如果你需要增加或减少工作负荷，可以轻松更改数据库层。有关详细信息，请参阅[更改数据库服务层和性能级别](/documentation/articles/sql-database-service-tiers/)。

尽管有多个托管的数据库，你的数据库仍可确保获得一组资源，并且数据库的预期性能特征不受影响。

[AZURE.INCLUDE [SQL 数据库服务层表](../../includes/sql-database-service-tiers-table.md)]


>[AZURE.NOTE] 如需本服务层表中所有其他行的详细说明，请参阅[服务层功能和限制](/documentation/articles/sql-database-performance-guidance/#service-tier-capabilities-and-limits)。

## 上下缩放单一数据库

在一开始选取服务层和性能级别以后，即可根据实际经验对单一数据库动态地进行上下缩放。


更改数据库的服务层和/或性能级别将在新的性能级别创建原始数据库的副本，然后将连接切换到副本。在此过程中不会丢失任何数据，但在切换到副本的短暂瞬间，将禁用与数据库的连接，因此可能回滚某些处于进行状态的事务。此时间范围因具体情况而异，但平均低于 4 秒，并且在超过 99%的情况下低于 30 秒。在禁用连接的瞬间有大量事务正在进行时，此时间范围可能更长。

整个扩展过程的持续时间同时取决于更改前后数据库的大小和服务层。例如，250 GB 的数据库以标准服务层为源和/或目标的更改应在 6 小时内完成。而同样大小的数据库在高级服务层内更改性能级别应在 3 小时内完成。

* 若要对数据库进行降级，数据库应小于目标服务层允许的最大大小。
* 在启用了[异地复制](/documentation/articles/sql-database-geo-replication-portal/)的情况下升级数据库时，必须先将次要数据库升级到所需的性能层，然后再升级主数据库。
* 从高级服务层降级时，必须先终止所有异地复制关系。可以按照[在中断后恢复](/documentation/articles/sql-database-disaster-recovery/)主题中所述的步骤，停止主数据库与活动次要数据库之间的复制过程。
* 各服务层的还原服务不同。如果降级，可能无法再还原到某个时间点，或者备份保留期变短。有关详细信息，请参阅 [Azure SQL 数据库备份和还原](/documentation/articles/sql-database-business-continuity/)。
* 更改完成前不会应用数据库的新属性。

> [AZURE.IMPORTANT]
有关详细步骤，请参阅[使用 Azure 门户管理单一数据库](/documentation/articles/sql-database-manage-single-databases-portal/)、[使用 Powershell 管理单一数据库](/documentation/articles/sql-database-manage-single-databases-powershell/)或[使用 Transact-SQL 管理单一数据库](/documentation/articles/sql-database-manage-single-databases-tsql/)。
>

##<a name="elastic-pool-service-tiers-and-performance-in-edtus"></a><a name="elastic-database-pool-service-tiers-and-performance-in-edtus"></a><a name="single-database-service-tiers-and-performance-levels"></a> 弹性池服务层和性能 (eDTU)

池允许数据库共享和使用 eDTU 资源，而无需为该池中的每个数据库分配特定性能级别。例如，标准池中的单一数据库可使用 0 个 eDTU 到最大数据库 eDTU 数（配置池时设置的）运转。弹性池允许多个具有不同工作负荷的数据库有效地使用在整个池中都可用的 eDTU 资源。有关详细信息，请参阅[弹性池的价格和性能注意事项](/documentation/articles/sql-database-elastic-pool-guidance/)。

下表描述了池服务层的特征。

[AZURE.INCLUDE [用于弹性池的 SQL 数据库服务层表](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

池中的每个数据库也遵循该层的单一数据库特征。例如，基本池具有每池最大会话数为 4800 - 28800 的限制，但该基本池中单个数据库具有 300 个会话数的数据库限制。

## 上下缩放弹性池

在一开始选取服务层和性能级别以后，即可根据实际经验对弹性池动态地进行上下缩放。

* 更改每个数据库的最小 eDTU 数或每个数据库的最大 eDTU 数通常可在五分钟或更少的时间内完成。
* 更改池大小 (eDTU) 所需的时间取决于池中所有数据库的总大小。每 100 GB 的更改平均需要 90 分钟或更短的时间。例如，如果池中所有数据库的总空间为 200 GB，则更改每个池的池 eDTU 时，预计延迟为 3 小时或更短的时间。

> [AZURE.IMPORTANT]
有关详细步骤，请参阅[使用 Azure 门户管理弹性池](/documentation/articles/sql-database-elastic-pool-manage-portal/)、[使用 Powershell 管理弹性池](/documentation/articles/sql-database-elastic-pool-manage-powershell/)、[使用 Transact-SQL 管理弹性池](/documentation/articles/sql-database-elastic-pool-manage-tsql/)或[使用 C# 管理弹性池](/documentation/articles/sql-database-elastic-pool-manage-csharp/)。
>

## 后续步骤

* 了解有关[弹性池](/documentation/articles/sql-database-elastic-pool-guidance/)和[弹性池的价格和性能注意事项](/documentation/articles/sql-database-elastic-pool-guidance/)的详细信息。
* 了解如何[监视、管理弹性池和调整其大小](/documentation/articles/sql-database-elastic-pool-manage-portal/)以及如何[监视单个数据库的性能](/documentation/articles/sql-database-single-database-monitor/)。
* 现在，你已了解有关 SQL 数据库层的信息，可使用 [1 元帐户](/pricing/1rmb-trial/)来试用这些层，并了解[如何创建你的第一个 SQL 数据库](/documentation/articles/sql-database-get-started/)。
* 对于迁移方案，请使用 [DTU 计算器](http://dtucalculator.azurewebsites.net/)估计所需的 DTU 数。

<!---HONumber=Mooncake_0320_2017-->
<!--Update_Description: add introduction about scaling up/scaling down single database and elastic pool  -->