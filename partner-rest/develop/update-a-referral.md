---
title: 更新引荐
description: 使用合作伙伴 API 更新引荐。
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: cae08ddffc7fd97682a009a430b4cd1114f8e761
ms.sourcegitcommit: f7918b7775ca8c6192b2a3e61edb74547730672d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "74556767"
---
# <a name="update-a-referral"></a>更新引荐

适用于：

- 合作伙伴 API

本主题说明了如何更新引荐。

## <a name="prerequisites"></a>必备条件

- [Partner API authentication](api-authentication.md)（合作伙伴 API 身份验证）中所述的凭据。 此方案支持使用应用凭据和用户凭据进行身份验证。

## <a name="rest-request"></a>REST 请求

### <a name="request-syntax"></a>请求语法

| 方法  | 请求 URI                                                       |
|---------|-------------------------------------------------------------------|
| **PUT** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="request-headers"></a>请求标头

- 有关详细信息，请参阅 [Partner API REST headers](headers.md)（合作伙伴 API REST 标头）。

> [!IMPORTANT]
> 请务必设置 **If-Match** 标头。

### <a name="request-body"></a>请求正文

下表说明了请求正文中的[引荐](referral-resources.md)属性。

| 属性            | 在任务栏的搜索框中键入                                                                 | 描述                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| ID                  | 字符串                                                               | 此引荐的 ID。                                                                                            |
| EngagementId        | 字符串                                                               | 此引荐的 EngagementID。 可以将多个引荐关联到单个 EngagementID                    |
| 名称                | 字符串                                                               | 引荐的名称。                                                                                            |
| ExternalReferenceId | 字符串                                                               | 引荐的外部标识符。 示例：存储自己的 Dynamics 365 潜在客户/机会 ID                    |
| CreatedDateTime     | 采用 UTC 日期/时间格式的字符串                                       | 创建引荐的日期。                                                                                   |
| UpdatedDateTime     | 采用 UTC 日期/时间格式的字符串                                       | 上次更新引荐的日期。                                                                              |
| ExpirationDateTime  | 采用 UTC 日期/时间格式的字符串                                       | 引荐将过期的日期。                                                                                   |
| 状态              | [ReferralStatus](referral-resources.md#referralstatus)               | 一个 [Enum](https://docs.microsoft.com/dotnet/api/system.enum)，其值指示引荐状态。          |
| Substatus           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | 一个 [Enum](https://docs.microsoft.com/dotnet/api/system.enum)，其值指示引荐子状态。      |
| StatusReason        | 字符串                                                               | 一条有关状态的说明性消息。 例如，说明为什么丢失了引荐。                              |
| ReferralType        | [ReferralType](referral-resources.md#referraltype)                   | 表示引荐类型。                                                                                        |
| Qualification       | [ReferralQualification](referral-resources.md#referralqualification) | 表示引荐的质量。                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | 客户联系人信息。                                                                                        |
| Consent             | [许可](referral-resources.md#consent)                             | 如果要与其他组织共享信息并允许其联系用户，则使用许可标记。                |
| 详细信息             | [ReferralDetails](referral-resources.md#referraldetails)             | 客户详细信息、说明、交易值、货币结账日期。                                                          |
| 组                | [成员](referral-resources.md#member)                               | 表示涉及合作伙伴参与计划的组织中的用户。                                   |
| InviteContext       | [InviteContext](referral-resources.md#invitecontext)                 | 表示用户在邀请其他组织参与合作伙伴计划时可以提供的其他信息。 |
| 目标         | [ReferralTarget](referral-resources.md#target)        | 表示用户在邀请其他组织参与合作伙伴计划时可以提供的其他信息。  |

### <a name="status-and-substatus-transition-states"></a>状态和子状态转换状态

| 状态 | 允许的状态转换 | 允许的子状态            |
|--------|---------------------------|------------------------------|
| 新增    | 新增、活跃、已关闭       | 挂起、已接收            |
| 活跃 | 活跃、已关闭            | 接受                     |
| 关闭 | 关闭                    | 赢得、丢失、已拒绝、已过期 |

### <a name="request-example"></a>请求示例

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "closingDateTime": "2018-11-14T00:00:00Z",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",

}
```

> [!IMPORTANT]
> 从 PUT 资源中删除 `"links": { }` 对象。

## <a name="rest-response"></a>REST 响应

如果成功，此方法会在响应正文中返回填充的[引荐](referral-resources.md)资源。

### <a name="response-success-and-error-codes"></a>响应的成功和错误代码

每个响应都带有一个 HTTP 状态代码，用于指示成功或失败以及其他调试信息。 请使用网络跟踪工具来读取此代码、错误类型和其他参数。 有关完整列表，请参阅[错误代码](error-codes.md)。

### <a name="response-example"></a>响应示例

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq '37ef26aa-1d15-4533-9f93-a69bd33ab1e5'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/4111fffc-f9ee-4d53-bba6-569135228642",
            "method": "GET"
        }
    }
}
```