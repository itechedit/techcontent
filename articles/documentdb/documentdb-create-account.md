<properties
    pageTitle="如何创建 DocumentDB 帐户 | Azure"
    description="使用 Azure DocumentDB 创建 NoSQL 数据库。遵循本说明文档创建 DocumentDB 帐户，并开始构建运行速度飞快且可全局缩放的 NoSQL 数据库。"
    keywords="构建数据库"
    services="documentdb"
    documentationcenter=""
    author="mimig1"
    manager="jhubbard"
    editor="monicar" />
<tags
    ms.assetid="0e7f8488-7bb7-463e-b6fd-3ae91a02c03a"
    ms.service="documentdb"
    ms.workload="data-services"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="get-started-article"
    ms.date="02/10/2017"
    wacn.date="03/22/2017"
    ms.author="mimig" />  


# 如何使用 Azure 门户预览创建 DocumentDB NoSQL 帐户
> [AZURE.SELECTOR]
- [Azure 门户预览](/documentation/articles/documentdb-create-account/)
- [Azure CLI 和 Azure资源管理器](/documentation/articles/documentdb-automation-resource-manager-cli/)

若要使用 Azure DocumentDB 构建数据库，必须：

- 有一个 Azure 帐户。如果没有 Azure 帐户，可以获取 [Azure 帐户](/pricing/1rmb-trial/)。
- 创建一个 DocumentDB 帐户。

可以使用 Azure 门户预览、Azure 资源管理器模板或 Azure 命令行接口 (CLI) 来创建 DocumentDB 帐户。本文说明如何使用 Azure 门户预览创建 DocumentDB 帐户。若要使用 Azure资源管理器或 Azure CLI 创建帐户，请参阅[自动创建 DocumentDB 数据库帐户](/documentation/articles/documentdb-automation-resource-manager-cli/)。

1. 登录到 [Azure 门户预览](https://portal.azure.cn/)。
2. 在左侧导航窗格中，依次单击“新建”、“数据库”、“NoSQL (DocumentDB)”。

	![屏幕截图：Azure 门户预览，其中突出显示“更多服务”和 NoSQL (DocumentDB)](./media/documentdb-create-account/create-nosql-db-databases-json-tutorial-1.png)  

3. 在“新建帐户”边栏选项卡中，为 DocumentDB 帐户指定所需的配置。

    ![“新建 DocumentDB”边栏选项卡的屏幕截图](./media/documentdb-create-account/create-nosql-db-databases-json-tutorial-2.png)  


   - 在“ID”框中，输入一个名称用于标识 DocumentDB 帐户。对“ID”进行验证后，“ID”框中会出现一个绿色的复选标记。该“ID”值将成为 URI 中的主机名。“ID”只能包含小写字母、数字及“-”字符，且长度必须为 3 到 50 个字符。请注意，*documents.azure.com* 会追加到所选终结点名称后面，其结果将成为 DocumentDB 帐户终结点。
   - 在“NoSQL API”框中，选择要使用的编程模型：

     - **DocumentDB**：DocumentDB API 可通过 .NET、Java、Node.js、Python 和 JavaScript [SDK](/documentation/articles/documentdb-sdk-dotnet/) 以及 HTTP [REST](https://msdn.microsoft.com/zh-cn/library/azure/dn781481.aspx) 获得，并提供对所有 DocumentDB 功能的编程访问方式。
     - **MongoDB**：DocumentDB 还为 **MongoDB** API 提供了[协议级别支持](/documentation/articles/documentdb-protocol-mongodb/)。选择“MongoDB API”选项时，可以使用现有的 MongoDB SDK 和[工具](/documentation/articles/documentdb-mongodb-mongochef/)与 DocumentDB 交互。[无需更改代码](/documentation/articles/documentdb-connect-mongodb-account/)即可将现有的 MongoDB 应用[转](/documentation/articles/documentdb-import-data/)为使用 DocumentDB，并利用完全托管的数据库作为一种服务，且具有无限缩放、全局复制等功能。
   - 对于“订阅”，请选择要用于 DocumentDB 帐户的 Azure 订阅。如果帐户只有一个订阅，则默认为选择该帐户。
   - 在“资源组”中，为 DocumentDB 帐户选择或创建资源组。默认创建新的资源组。有关详细信息，请参阅[使用 Azure 门户预览管理 Azure 资源](/documentation/articles/resource-group-portal/)。
   - 使用“位置”指定在其中托管 DocumentDB 帐户的地理位置。
4. 配置了新的 DocumentDB 帐户后，单击“创建”。若要检查部署状态，请查看“通知中心”。

	![快速创建数据库 — 通知中心的屏幕截图，其中显示正在创建 DocumentDB 帐户](./media/documentdb-create-account/create-nosql-db-databases-json-tutorial-4.png)  


	![通知中心的屏幕截图，其中显示 DocumentDB 帐户已成功创建并且部署到资源组 — 在线数据库创建者通知](./media/documentdb-create-account/create-nosql-db-databases-json-tutorial-5.png)  

5. 创建 DocumentDB 帐户之后，即可使用其默认设置。DocumentDB 帐户的默认一致性设置为“会话”。可单击资源菜单中的“默认一致性”调整默认一致性。若要了解有关 DocumentDB 提供的一致性级别的详细信息，请参阅 [DocumentDB 中的一致性级别](/documentation/articles/documentdb-consistency-levels/)。

	![“资源组”边栏选项卡的屏幕截图 — 开始应用程序开发](./media/documentdb-create-account/create-nosql-db-databases-json-tutorial-6.png)  


	![“一致性级别”边栏选项卡的屏幕截图 — 会话一致性](./media/documentdb-create-account/create-nosql-db-databases-json-tutorial-7.png)

[How to: Create a DocumentDB account]: #Howto
[Next steps]: #NextSteps


## 后续步骤
创建 DocumentDB 帐户后，下一步是创建 DocumentDB 集合与数据库。

可以使用以下方法之一创建新的集合和数据库：

- Azure 门户预览。请参阅[使用 Azure 门户预览创建 DocumentDB 集合](/documentation/articles/documentdb-create-collection/)。
- 包含示例数据的全面教程：[.NET](/documentation/articles/documentdb-get-started/)、[.NET MVC](/documentation/articles/documentdb-dotnet-application/)、[Java](/documentation/articles/documentdb-java-application/)、[Node.js](/documentation/articles/documentdb-nodejs-application/) 或 [Python](/documentation/articles/documentdb-python-application/)。
- 可在 GitHub 中找到 [.NET](/documentation/articles/documentdb-dotnet-samples/#database-examples/)、[Node.js](/documentation/articles/documentdb-nodejs-samples/#database-examples/) 或 [Python](/documentation/articles/documentdb-python-samples/#database-examples/) 示例代码。
- [.NET](/documentation/articles/documentdb-sdk-dotnet/)、[.NET Core](/documentation/articles/documentdb-sdk-dotnet-core/)、[Node.js](/documentation/articles/documentdb-sdk-node/)、[Java](/documentation/articles/documentdb-sdk-java/)、[Python](/documentation/articles/documentdb-sdk-python/) 和 [REST](https://msdn.microsoft.com/zh-cn/library/azure/mt489072.aspx) SDK。

创建数据库和集合后，需要在集合中[添加文档](/documentation/articles/documentdb-view-json-document-explorer/)。

集合中有文档后，可以使用 [DocumentDB SQL](/documentation/articles/documentdb-sql-query/) 对这些文档[执行查询](/documentation/articles/documentdb-sql-query/#executing-sql-queries/)。可以使用门户中的[查询浏览器](/documentation/articles/documentdb-query-collections-query-explorer/)、[REST API](https://msdn.microsoft.com/zh-cn/library/azure/dn781481.aspx) 或其中一个 [SDK](/documentation/articles/documentdb-sdk-dotnet/) 执行查询。

### 了解详细信息
若要详细了解 DocumentDB，请浏览以下资源：

- [DocumentDB 分层资源模型和概念](/documentation/articles/documentdb-resources/)

<!---HONumber=Mooncake_0313_2017-->
<!---Update_Description: wording update -->