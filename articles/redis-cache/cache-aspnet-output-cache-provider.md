<properties
    pageTitle="缓存 ASP.NET 输出缓存提供程序"
    description="了解如何使用 Azure Redis 缓存来缓存 ASP.NET 页面输出"
    services="redis-cache"
    documentationcenter="na"
    author="steved0x"
    manager="douge"
    editor="tysonn" />
<tags
    ms.assetid="78469a66-0829-484f-8660-b2598ec60fbf"
    ms.service="cache"
    ms.devlang="na"
    ms.topic="article"
    ms.tgt_pltfrm="cache-redis"
    ms.workload="tbd"
    ms.date="02/14/2017"
    wacn.date="03/03/2017"
    ms.author="sdanie" />  


# Azure Redis 缓存的 ASP.NET 输出缓存提供程序

[AZURE.INCLUDE [azure-sdk-developer-differences](../../includes/azure-sdk-developer-differences.md)]

Redis 输出缓存提供程序是用于输出缓存数据的进程外存储机制。此数据专门用于完整 HTTP 响应（页面输出缓存）。此提供程序会插入 ASP.NET 4 中引入的新输出缓存提供程序扩展点。

要使用 Redis 输出缓存提供程序，首先配置你的缓存，然后使用 Redis 输出缓存提供程序 NuGet 包配置 ASP.NET 应用程序。本主题提供有关配置应用程序以使用 Redis 输出缓存提供程序的指南。有关创建和配置 Azure Redis 缓存实例的详细信息，请参阅[创建缓存](/documentation/articles/cache-dotnet-how-to-use-azure-redis-cache/#create-a-cache)。

## 在缓存中存储 ASP.NET 页面输出
若要在 Visual Studio 中使用 Redis 输出缓存提供程序 NuGet 包配置客户端应用程序，请在“解决方案资源管理器”中右键单击项目，然后选择“管理 NuGet 包”。

[AZURE.INCLUDE [azure-sdk-developer-differences](../../includes/azure-visual-studio-login-guide.md)]

![Azure Redis 缓存管理 NuGet 包](./media/cache-aspnet-output-cache-provider/redis-cache-manage-nuget-menu.png)  


在搜索文本框中键入 **RedisOutputCacheProvider**，从结果中选择它，然后单击“安装”。

![Azure Redis 缓存输出缓存提供程序](./media/cache-aspnet-output-cache-provider/redis-cache-page-output-provider.png)  


Redis 输出缓存提供程序 NuGet 包依赖于 StackExchange.Redis.StrongName 包。如果项目中没有 StackExchange.Redis.StrongName 包，则会安装它。

>[AZURE.NOTE]
除了强命名的 StackExchange.Redis.StrongName 包外，还有 StackExchange.Redis 非强命名版本。如果项目使用非强命名的 StackExchange.Redis 版本，则必须将其卸载，否则会在项目中出现命名冲突。有关这些包的详细信息，请参阅[配置 .NET 缓存客户端](/documentation/articles/cache-dotnet-how-to-use-azure-redis-cache/#configure-the-cache-clients)。
>
>

NuGet 包会下载并添加所需的程序集引用，并将以下节添加到 web.config 文件中。此节包含的配置是 ASP.NET 应用程序使用 Redis 输出缓存提供程序所必需的。

    <caching>
      <outputCachedefault Provider="MyRedisOutputCache">
        <providers>
          <!--
          <add name="MyRedisOutputCache"
            host = "127.0.0.1" [String]
            port = "" [number]
            accessKey = "" [String]
            ssl = "false" [true|false]
            databaseId = "0" [number]
            applicationName = "" [String]
            connectionTimeoutInMilliseconds = "5000" [number]
            operationTimeoutInMilliseconds = "5000" [number]
          />
          -->
          <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
        </providers>
      </outputCache>
    </caching>

注释部分提供了属性及每个属性的示例设置的一个示例。

使用来自 Azure 门户预览中的缓存边栏选项卡的值配置属性，并根据需要配置其他值。有关访问缓存属性的说明，请参阅[配置 Redis 缓存设置](/documentation/articles/cache-configure/#configure-redis-cache-settings)。

* **host** - 指定缓存终结点。
* **port** - 使用非 SSL 端口或 SSL 端口，具体取决于 SSL 设置。
* **accessKey** - 使用缓存的主密钥或辅助密钥。
* **ssl** - 如果要使用 SSL 保护缓存/客户端通信，则为 true；否则为 false。请务必指定正确的端口。
    * 默认情况下，将为新缓存禁用非 SSL 端口。为此设置指定 true 可使用 SSL 端口。有关启用非 SSL 端口的详细信息，请参阅[配置缓存](/documentation/articles/cache-configure/)主题中的[访问端口](/documentation/articles/cache-configure/#access-ports)部分。
* **databaseId** - 指定要用于缓存输出数据的数据库。如果未指定，则使用默认值 0。
* **applicationName** - 密钥存储在 redis 中作为 `<AppName>_<SessionId>_Data`。此命名方案使多个应用程序可以共享同一密钥。此参数是可选的，如果未提供它，则使用默认值。
* **connectionTimeoutInMilliseconds** - 此设置允许你覆盖 StackExchange.Redis 客户端中的 connectTimeout 设置。如果未指定，则使用默认 connectTimeout 设置 5000。有关详细信息，请参阅 [StackExchange.Redis 配置模型](http://go.microsoft.com/fwlink/?LinkId=398705)。
* **operationTimeoutInMilliseconds** - 此设置允许你覆盖 StackExchange.Redis 客户端中的 syncTimeout 设置。如果未指定，则使用默认 syncTimeout 设置 1000。有关详细信息，请参阅 [StackExchange.Redis 配置模型](http://go.microsoft.com/fwlink/?LinkId=398705)。

将 OutputCache 指令添加到希望为其缓存输出的每个页面中。

    <%@ OutputCache Duration="60" VaryByParam="*" %>

在上面的示例中，缓存的页面数据保留在缓存中 60 秒，并且为每个参数组合缓存不同版本的页面。有关 OutputCache 指令的详细信息，请参阅 [@OutputCache](https://msdn.microsoft.com/zh-cn/library/hdxfb6cy(v=vs.100).aspx)。

执行这些步骤后，你的应用程序已配置为使用 Redis 输出缓存提供程序。

## 后续步骤
了解 [Azure Redis 缓存的 ASP.NET 会话状态提供程序](/documentation/articles/cache-aspnet-session-state-provider/)。

<!---HONumber=Mooncake_0227_2017-->
<!--Update_Description: wording update-->