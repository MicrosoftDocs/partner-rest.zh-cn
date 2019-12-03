---
title: 引荐连接器。
description: 使用 Microsoft Flow 将合作伙伴引荐与 Dynamics 365 CRM 潜在客户同步。
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e1197b00202bcf299579a285208026bffe3ab12c
ms.sourcegitcommit: f7918b7775ca8c6192b2a3e61edb74547730672d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "74556647"
---
# <a name="referral-connectors"></a>引荐连接器

可以使用引荐连接器将合作伙伴引荐与客户关系管理 (CRM) 潜在客户同步。 可以创建引荐连接器，使用 [Microsoft Flow](https://flow.microsoft.com) 作为 HTTPS 终结点来接收合作伙伴引荐。 然后，可以将流接收的引荐作为潜在客户写入 CRM 系统。

## <a name="prerequisites"></a>必备条件

* Microsoft Flow 订阅
  * 可以通过管理员身份访问此订阅的帐户
* Azure Active Directory (Azure AD) 应用程序 ID、用户 ID、密码和租户 ID（用于访问合作伙伴 API）。 有关设置说明，请参阅[合作伙伴身份验证](api-authentication.md)。
* [Azure 函数应用](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-function-app-portal)订阅。
* [合作伙伴中心 Webhook 事件](https://docs.microsoft.com/en-us/partner-center/develop/partner-center-webhook-events)订阅（针对[引荐创建的](https://docs.microsoft.com/en-us/partner-center/develop/partner-center-webhook-events#referral-created-event)和[引荐更新的](https://docs.microsoft.com/en-us/partner-center/develop/partner-center-webhook-events#referral-updated-event)事件）。
* [Microsoft Dynamics 365](https://dynamics.microsoft.com) 订阅
  * 已启用的销售模块
  * 可以通过管理员身份访问此订阅的帐户

## <a name="flow-overview"></a>流概述

使用以下流将引荐导入 CRM：

1. 合作伙伴设置一个 Webhook 来接收引荐通知。
2. 合作伙伴将 Webhook 注册到合作伙伴中心。 合作伙伴还订阅创建或更新引荐时的 Webhook 事件。
3. 引荐客户端创建或更新引荐。
4. 合作伙伴中心 Webhook 系统会检查合作伙伴的注册并向 Webhook 发送通知。
5. Webhook 接收通知。
6. Microsoft Flow 中的流文档使用令牌来调用合作伙伴中心引荐 API。
7. 流终结点获取引荐。
8. 流终结点创建 CRM 潜在客户。

![流程图，显示此部分中将合作伙伴引荐导入 CRM 的步骤。](../images/referralwebhook.png)

## <a name="flow-document-process"></a>流文档流程

引荐连接器的流文档会将合作伙伴引荐与 Dynamics 365 中的 CRM 潜在客户同步。

1. 连接器获取一个用于连接到 `https://api.partner.microsoft.com/v1.0/engagements/referrals` 的令牌。
2. 连接器使用 `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}` 获取触发了连接器的引荐。
3. 连接器连接到 Dynamics 365。
4. 连接器创建新的潜在客户，或使用有关引荐的最新信息更新现有的潜在客户。
5. 连接器使用来自 CRM 潜在客户的最新更新对引荐进行更新。

![流程图，显示此部分中适用于流文档流程的步骤。](../images/ReferralFlowSteps.png)

## <a name="sample-referral-connector"></a>示例引荐连接器

以下示例引荐连接器显示了如何将合作伙伴中心引荐同步到  Dynamics 365 中的 CRM 潜在客户。

> [!IMPORTANT]
> 可以通过替换示例代码中的[流连接器](https://flow.microsoft.com/en-us/connectors/)将数据写入不同的 CRM。

### <a name="import-flow-synchronization-package"></a>导入流同步包

请将示例代码包下载并导入  Microsoft Flow，然后连接到 Dynamics 365：

1. 从 [GitHub 存储库](https://github.com/microsoft/Partner-Center-Referrals)下载[流同步包](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true)。
2. 使用适当的凭据登录 [Microsoft Flow](https://flow.microsoft.com)。
3. 在导航菜单中选择“我的流”。  然后，选择“导入”。 
4. 在“导入包”页上，选择已下载的流同步包  。 然后，选择“上传”。 

    ![包文件的“导入包”屏幕](../images/importPackage.png)

5. 完成包上传操作以后，在“查看包内容”中找到上传的包。 

    ![“导入包”屏幕的详细信息](../images/importPackageDetails.png)

6. 选择已上传包的“操作”按钮（铅笔图标）。  这会打开“导入设置”边栏选项卡。 
7. 选择你的“设置”  类型。

    * 若要创建新流，请选择“作为新的创建”，然后输入新的“资源名称”  。 
    * 若要使用同一名称更新现有流，请选择“更新”。 

    ![“创建或更新新包”屏幕](../images/CreateNewConnection.png)

8. 在“导入包”页上，在“查看包内容”部分的“相关资源”下找到你的 Dynamics 365 连接。   
9. 选择 Dynamics 365 连接的“操作”按钮（铅笔图标）。  这会打开该相关资源的“导入设置”边栏选项卡。 
10. 选择“新建”以创建新的 Dynamics 365 连接，或者选择现有的连接。 
11. 验证“导入包”页现在是否显示所选流设置类型和 Dynamics 365 连接。  然后，选择“导入”。 

    ![“导入包”状态屏幕](../images/importStatus.png)

12. 验证流资源现在是否已创建或更新。

### <a name="configure-flow-parameters"></a>配置流参数

配置流资源的参数：

1. 在 [Microsoft Flow](https://flow.microsoft.com) 的导航菜单中选择“我的流”。 
2. 选择在上一部分创建或更新的流资源。
3. 在流页面上，选择“编辑流”。 
4. 选择“AAD-Application (客户端) ID”变量并输入 Azure AD 应用程序的 ID。 
5. 选择 **UserId** 变量并输入用户 ID。
6. 选择 **UserPassword** 变量并输入用户密码。
7. 选择“AAD-Directory (租户) ID”变量。  输入 Azure AD 应用程序的租户 ID。
8. 选择“保存”以保存流。 

    ![流变量设置屏幕](../images/SetFlowVariables.png)

### <a name="authenticate-the-callback"></a>验证回调

验证来自合作伙伴中心的回调事件：

> [!TIP]
> 有关示例，请参阅以下部分的[示例函数应用代码](#sample-function-app-code)。

1. [创建 Azure 函数应用](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-function-app-portal)，用于[验证来自合作伙伴中心的回调事件](https://docs.microsoft.com/en-us/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback)。

    1. 验证所需标头（**Authorization**、**x-ms-certificate-url** 和 **x-ms-signature-algorithm**）是否存在。
    2. 下载用于对内容进行签名的证书 (**x-ms-certificate-url**)。
    3. 验证证书链。
    4. 验证证书的“组织”。 
    5. 将使用 UTF-8 编码的内容读取到缓冲区中。
    6. 创建 RSA 加密提供程序。
    7. [验证签名](https://docs.microsoft.com/en-us/partner-center/develop/partner-center-webhooks#example-for-signature-validation)是否与使用指定哈希算法（例如 SHA256）签名的内容匹配。
    8. 如果验证成功，则会返回一条“正常”消息。 

2. 请注意为函数应用的 HTTP 终结点生成的回调 URI。 创建函数应用时，会显示该 URI。 也可在函数应用的 Azure 资源页上找到该 URI。
3. 在 [Microsoft Flow](https://flow.microsoft.com) 中，编辑你在[导入流同步包](#import-flow-synchronization-package)  部分导入的“合作伙伴对 Microsoft Dynamics CRM 潜在客户的引荐”流。

    1. 将函数应用的 URI 的值添加到“Webhook 证书验证”步骤。
    2. 复制函数应用的回调 URI 并将其粘贴到流文档中。
    3. 保存流文档。

#### <a name="sample-function-app-code"></a>示例函数应用代码

```csharp
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using Microsoft.Azure.WebJobs;
using Microsoft.Extensions.Logging;
using System;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Security.Cryptography.X509Certificates;
using System.Text;
using System.Threading.Tasks;

public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
    string requestBody = null;
    if (!string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-certificate-url")) && !string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-signature-algorithm")))
    {
        var certificateUrl = req?.Headers["x-ms-certificate-url"].First();
        try
        {
            string resultContent = null;
            using (var client = new HttpClient())
            {
                var result = await client.GetAsync(req.Headers["x-ms-certificate-url"].First());
                resultContent = await result.Content.ReadAsStringAsync();
                log.LogInformation(resultContent);
            }
            if (!string.IsNullOrEmpty(resultContent))
            {
                var certificate = new X509Certificate2(Encoding.UTF8.GetBytes(resultContent));
                var validationResult = certificate.Verify() && certificate.Issuer.Contains("O=Microsoft Corporation");
                if (validationResult)
                {
                    return new OkResult();
                }
                else
                {
                    return new BadRequestResult();
                }
            }
        }
        catch (Exception)
        {
            new BadRequestObjectResult("Certificate could not be retrieved, invalid caller to flow");
        }

        requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
    }
    else
    {
        new BadRequestObjectResult("Missing headers");
    }

    return new BadRequestObjectResult("Certificate validation failed");
}

private static string GetFirstValueFromHeader(HttpRequest request, string headerName)
{
    StringValues matchingHeaderValues;
    request.Headers.TryGetValue(headerName, out matchingHeaderValues);
    return matchingHeaderValues.Count != 0 ? matchingHeaderValues.First() : string.Empty;
}
```

### <a name="register-flow-with-partner-center"></a>将流注册到合作伙伴中心

将流资源注册到合作伙伴中心即可触发流和接收 Webhook 事件：

1. 在 [Microsoft Flow](https://flow.microsoft.com) 的导航菜单中选择“我的流”。 
2. 选择已创建或更新的流。
3. 在流页面上，选择“编辑流”。 
4. 复制并保存流的 **HTTP POST URL**。 需使用此 URL 来触发流。
5. [注册以接收 Webhook 事件](https://docs.microsoft.com/en-us/partner-center/develop/partner-center-webhooks#register-to-receive-events)（创建或更新引荐时的）。 请使用以下正文格式：

```json
{
    "WebhookUrl": "<<FlowUrl>>",
    "WebhookEvents": [
        "referral-created",
        "referral-updated"
    ],
    "signatureTokenToMsSignatureHeader": true
}
```
