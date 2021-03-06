[适用于 .NET 的 Microsoft Azure Configuration Manager 库](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) 提供用于分析配置文件中连接字符串的类。 [CloudConfigurationManager 类](https://msdn.microsoft.com/library/azure/mt634650.aspx) 分析配置设置，而不考虑客户端应用程序是在台式机、移动设备、Azure 虚拟机还是 Azure 云服务中运行。

若要引用 CloudConfigurationManager 包，请将以下 `using` 语句添加到你的类：

    using Microsoft.Azure;    //Namespace for CloudConfigurationManager

下面的示例演示了如何检索配置文件中的连接字符串：

    // Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("StorageConnectionString"));

不一定要使用 Azure Configuration Manager。 还可以使用 API，例如 .NET Framework 的 [ConfigurationManager 类](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx)。



<!--HONumber=Nov16_HO2-->


