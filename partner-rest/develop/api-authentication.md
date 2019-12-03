---
title: 合作伙伴 API 身份验证
description: 配置身份验证设置，以便将合作伙伴 API 与 Azure AD 配合用于身份验证。
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: cd0aca43ad243a17779fe76edd107c5156d4a040
ms.sourcegitcommit: f7918b7775ca8c6192b2a3e61edb74547730672d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "74556437"
---
# <a name="partner-api-authentication"></a>合作伙伴 API 身份验证

适用于：

- 合作伙伴 API

合作伙伴 API 利用 Azure Active Directory (Azure AD) 进行身份验证。 与合作伙伴 API 交互时，必须正确配置 Azure AD 应用程序并获取访问令牌。 获取的访问令牌可以进行[应用程序和用户访问](#application-and-user-access)，也可以进行[仅限应用程序的访问](#application-only-access)。

## <a name="application-and-user-access"></a>应用程序和用户访问

建议使用此方法来设置对 API 的**应用程序和用户访问**。

1. 登录 [Azure 门户](https://portal.azure.com/)。
2. 选择 **Azure Active Directory** 服务。
3. 选择“应用注册”，然后选择“新建应用程序注册”   。
4. 创建新应用程序。 对于“应用程序类型”，请选择“本机”   。 提供名称和 URL，然后选择“创建”  。
5. 选择应用程序的“API 权限”。  在“请求 API 权限”屏幕上，选择“添加权限”，然后选择“我的组织使用的 API”   
6. 搜索“Microsoft 合作伙伴  (Microsoft 开发人员中心  ) API (`4990cffe-04e8-4e8b-808a-1175604b879f`)”。

    ![“请求 API 权限”屏幕的屏幕截图，其中包含对 Microsoft 合作伙伴 API 的搜索](../images/SearchGatewayApi.png)

7. 将“委托权限”设置为“合作伙伴中心”。  

    ![Microsoft 合作伙伴 API 的委托权限配置屏幕的屏幕截图](../images/SelectUserPermission.png)

## <a name="application-only-access"></a>仅限应用程序的访问

建议使用此方法来设置对 API 的**仅限应用程序的访问**。

> [!IMPORTANT]
> 必须提供来自 Azure AD 应用程序的应用程序 ID、应用程序密钥和目录 ID。

1. 登录 [Azure 门户](https://portal.azure.com/)。
2. 选择 **Azure Active Directory** 服务。
3. 选择“应用注册”，然后选择“新建应用程序注册”   。
4. 创建新应用程序。 选择“Web 应用/API”作为“应用程序类型”   。 输入应用程序**名称**和 **URL**。 然后，选择“创建”  。
5. 选择应用程序的“API 权限”。  选择“添加权限”，然后选择“我的组织使用的 API”  
6. 搜索“Microsoft 合作伙伴  (Microsoft 开发人员中心  ) API (`4990cffe-04e8-4e8b-808a-1175604b879f`)”。

    ![“请求 API 权限”屏幕的屏幕截图，其中包含对 Microsoft 合作伙伴 API 的搜索](../images/SearchGatewayApi.png)

7. 将“委托权限”设置为“合作伙伴中心”。  

    ![Microsoft 合作伙伴 API 的委托权限配置屏幕的屏幕截图](../images/SelectUserPermission.png)

8. 对于已注册的应用程序，请选择“属性”，然后选择“复制应用程序 ID”。  
9. 选择“设置”，然后选择“证书和机密”。   选择“新建客户端机密”，然后将“过期”设置为“永不过期”。    然后选择“保存”。 
10. 在“密钥”菜单上，选择“复制密钥值”。   保存此值的副本。

> [!WARNING]
> 对于已创建的密钥，请务必保存密钥值的副本。 稍后需使用该密钥值来获取令牌。

## <a name="partner-consent"></a>合作伙伴许可

在 Azure 管理门户中，选择“企业应用程序”。  搜索在上一部分创建的应用程序，然后选择该应用程序。 选择“权限”  ，然后选择“为合作伙伴帐户授予管理员许可”  。