---
title: 创建引荐
description: 在合作伙伴 API 中创建独立的或共享的引荐。
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6aab4b5f45030c3c16294b2929b1a6d3086fb951
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2020
ms.locfileid: "80342289"
---
# <a name="create-a-referral"></a>创建引荐

适用于：

- 合作伙伴 API

本主题说明了如何创建引荐。 有两种类型的 [ReferralType](referral-resources.md#referraltype)：

1. 独立：引荐对一个合作伙伴可见。
2. 共享：引荐对一起工作的双方可见。 例如，如果 Microsoft 和某个合作伙伴进行合作销售，则可在双方之间共享引荐。 有关详细信息，请参阅[创建共享引荐](#create-a-shared-referral)部分。

## <a name="prerequisites"></a>必备条件

- [Partner API authentication](api-authentication.md)（合作伙伴 API 身份验证）中所述的凭据。 此方案支持使用应用凭据和用户凭据进行身份验证。

## <a name="rest-request"></a>REST 请求

### <a name="request-syntax"></a>请求语法

| 方法  | 请求 URI                                                  |
|---------|--------------------------------------------------------------|
| **POST** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

### <a name="request-headers"></a>请求标头

- 有关详细信息，请参阅 [Partner API REST headers](headers.md)（合作伙伴 API REST 标头）。

### <a name="request-body"></a>请求正文

下表说明了请求正文中适用于全新引荐的[引荐](referral-resources.md)属性。

| 属性            | 类型                                                                 | 说明                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| 名称                | 字符串                                                               | 引荐的名称。                                                                                            |
| ExternalReferenceId | 字符串                                                               | 引荐的外部标识符。 例如，你自己的 Dynamics 365 潜在客户或机会 ID。                   |
| 状态              | [ReferralStatus](referral-resources.md#referralstatus)               | 一个 [Enum](https://docs.microsoft.com/dotnet/api/system.enum)，其值指示引荐状态。          |
| Substatus           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | 一个 [Enum](https://docs.microsoft.com/dotnet/api/system.enum)，其值指示引荐子状态。       |
| StatusReason        | 字符串                                                               | 一条有关状态的说明性消息。 例如，说明为什么丢失了引荐。                            |
| ReferralType        | [ReferralType](referral-resources.md#referraltype)                   | 表示引荐类型。 **必填。**                                                                                        |
| Qualification       | [ReferralQualification](referral-resources.md#referralqualification) | 表示引荐的质量。                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | 客户联系人信息。  **必填。**                                                                                      |
| Consent             | [许可](referral-resources.md#consent)                             | 如果要与其他组织共享信息并允许其联系用户，则使用许可标记。**必填。**               |
| 详细信息             | [ReferralDetails](referral-resources.md#referraldetails)             | 客户详细信息、说明、交易值、货币结账日期。 **必填。**                                                           |
| 组                | [成员](referral-resources.md#member)                               | 表示涉及合作伙伴参与计划的组织中的用户。                                   |
| InviteContext       | [InviteContext](referral-resources.md#invitecontext)                 | 表示用户在邀请其他组织参与合作伙伴计划时可以提供的其他信息。 |
| 目标         | [ReferralTarget](referral-resources.md#target)        | 表示用户在邀请其他组织参与合作伙伴计划时可以提供的其他信息。  |

#### <a name="status--substatus-transition-states"></a>状态和子状态转换状态

| 状态 | 允许的状态转换 | 允许的子状态            |
|--------|---------------------------|------------------------------|
| “新建”    | 新增、活跃、已关闭       | 挂起、已接收            |
| Active | 活跃、已关闭            | 接受                     |
| 关闭 | 关闭                    | 赢得、丢失、已拒绝、已过期 |

### <a name="request-example"></a>请求示例

```http
POST https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "name": "Test Cosell Invite_20",
    "status": "New",
    "substatus": "Pending",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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
    }
}
```

## <a name="rest-response"></a>REST 响应

如果成功，此方法会在响应正文中返回填充的[引荐](referral-resources.md)资源。

### <a name="response-success-and-error-codes"></a>响应的成功和错误代码

每个响应都带有一个 HTTP 状态代码，用于指示成功或失败以及其他调试信息。 请使用网络跟踪工具来读取此代码、错误类型和其他参数。 有关完整列表，请参阅[错误代码](error-codes.md)。

### <a name="response-example"></a>响应示例

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "name": "Test Cosell Invite_20",
    "externalReferenceId": null,
    "createdDateTime": "2019-02-23T02:05:23.2931817Z",
    "updatedDateTime": "2019-02-23T02:05:23.2931817Z",
    "expirationDateTime": null,
    "status": "Active",
    "substatus": "Accepted",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "eTag": "\"00006d10-0000-0000-0000-5c70aa630000\"",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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

## <a name="create-a-shared-referral"></a>创建共享的引荐

可以通过两个步骤创建“共享”  [引荐类型](referral-resources.md#referraltype)的引荐。

1. [创建共享的引荐](#create-your-referral)
2. [创建第二方的连接引荐](#create-a-connected-referral)

以下流程图展示了在创建共享引荐过程中使用的这两个步骤。

![显示共享引荐的流程图，其中的 2 个引荐通过 Microsoft 合作伙伴 API 连接](../images/SharedReferral.png)

### <a name="create-your-referral"></a>创建引荐

1. 创建引荐，将 [ReferralType](referral-resources.md#referraltype) 设置为 shared。
2. 从返回响应中复制 **engagementId**。

适用于引荐的 [ReferralTarget](referral-resources.md#target) 示例

```json
"target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-ABC-DEF"
        }
    ]
```

### <a name="create-a-connected-referral"></a>创建连接的引荐

1. 为 Microsoft 创建另一引荐。
2. 包括引荐中的 **enagementId**，使之绑定在一起。

适用于 Microsoft 引荐的 [ReferralTarget](referral-resources.md#target) 示例

```json
"target": [
        {
            "type": "BusinessProfileLocation",
            "id": "msft"
        }
    ]
```