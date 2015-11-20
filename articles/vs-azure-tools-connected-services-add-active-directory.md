<properties 
   pageTitle="在 Visual Studio 中使用连接服务添加 Azure Active Directory"
   description="使用 Visual Studio 中“添加连接的服务”对话框添加 Azure Active Directory"
   services="visual-studio-online"
   documentationCenter="n/a"
   authors="patshea123"
   manager="douge"
   editor="tlee" />
<tags  
ms.service="visual-studio-online"" 
ms.date="08/12/2015" 
wacn.date=""/>

# 在 Visual Studio 中使用连接服务添加 Azure Active Directory 

##概述
通过使用 Azure Active Directory (Azure AD)，您可以对 ASP.NET MVC Web 应用程序或 Web API 服务中的 AD 身份验证支持单一登录 (SSO)。通过 Azure AD 身份验证，您的用户可以使用其帐户从 Azure AD 连接到您的 Web 应用程序。通过 Web API 的 Azure AD 身份验证的优点包括，从 Web 应用程序公开 API 时提供增强的数据安全性。通过 Azure AD，您不需要使用其自己的帐户和用户管理来管理单独的身份验证系统。

## 支持的项目类型

您可以在以下项目类型中使用“连接服务”对话框连接到 Azure AD。

- ASP.NET MVC 项目

- ASP.NET Web API 项目


### 使用“连接服务”对话框连接到 Azure AD

1. 确保您具有 Azure 帐户。如果您没有 Azure 帐户，可以注册[免费试用版](http://go.microsoft.com/fwlink/?LinkId=518146)。

1. 在 Visual Studio 中，打开项目中“引用”节点的快捷菜单，然后选择“添加连接服务”。
1. 选择“Azure AD 身份验证”，然后选择“配置”。

    ![选择“添加 Azure AD 身份验证”](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. 在“配置 Azure AD 身份验证”的第一页上，选中“使用 Azure AD 配置单一登录”。

    如果您的项目是使用另一个身份验证配置进行配置的，向导将警告您继续操作将禁用以前的配置。

    ![在向导中配置 Azure AD](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1.  在第二页上，从“域”下拉列表中选择一个域。域列表包含在“帐户设置”对话框中列出的帐户可以访问的所有域。如果没有找到您要查找的域，作为替代方法，您可以输入域名，如 mydomain.onmicrosoft.com。您可以选择用于创建一个新 Azure AD 应用程序的选项，也可以使用现有 Azure AD 应用程序中的设置。

    ![在向导中配置 Azure AD](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)


1. 在向导的第三页上，确保已选中“读取目录数据”。该向导将填写“客户端密码”。

    ![在向导中配置 Azure AD](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. 单击“完成”按钮。对话框将添加必要的配置代码和引用，以便为 Azure AD 身份验证启用项目。您可以在 Azure 门户上看到 AD 域。

    ![在 Azure 管理门户中查找域](./media/vs-azure-tools-connected-services-add-active-directory/IC765882.png)

1. 查看浏览器中显示的“入门”页可了解有关后续步骤的内容，查看“发生了什么”页可查看您的项目的修改情况。如果您想要查看状态是否正常，请打开其中一个修改过的配置文件，并验证“发生了什么”中提到的设置确实存在。例如，ASP.NET MVC 项目中的主 web.config 会添加这些设置：

        <appSettings> 
            <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
            <add key="ida:AADInstance" value="https://login.windows.net/" />
            <add key="ida:Domain" value="Your selected domain" />
            <add key="ida:TenantId" value="The Id of your selected Azure AD Tenant" />
            <add key="ida:PostLogoutRedirectUri" value="The default redirect URI from the project" />
        </appSettings>

## 您的项目的修改情况

当运行向导时，Visual Studio 会将 Azure AD 和关联的引用添加到您的项目。还会修改您项目中的配置文件和代码文件以添加对 Azure AD 的支持。Visual Studio 所做的特定修改取决于项目类型。有关 ASP.NET MVC 项目修改情况的详细信息，请参阅[发生了什么 – MVC 项目](http://go.microsoft.com/fwlink/p/?LinkID=513809)。对于 Web API 项目，请参阅[发生了什么 – Web API 项目](http://go.microsoft.com/fwlink/p/?LinkId=513810)。

##后续步骤

提出问题并获得帮助。

 - [MSDN 论坛：Azure AD](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)

 - [Azure AD 文档](http://azure.microsoft.com/documentation/services/active-directory/)

 - [博客文章：Azure AD 简介](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)

<!---HONumber=71-->