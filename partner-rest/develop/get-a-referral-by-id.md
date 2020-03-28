---
title: 按 ID 获取引荐
description: 按 ID 获取引荐。
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 39ee62de740f3aa73c3fe8ca86d0da47ebb96334
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2020
ms.locfileid: "80342258"
---
# <a name="get-a-referral-by-id"></a>按 ID 获取引荐

适用范围：

- 合作伙伴 API

本主题说明了如何按 ID 获取引荐。

## <a name="prerequisites"></a>先决条件

- [Partner API authentication](api-authentication.md)（合作伙伴 API 身份验证）中所述的凭据。 此方案支持使用应用凭据和用户凭据进行身份验证。

## <a name="rest-request"></a>REST 请求

### <a name="request-syntax"></a>请求语法

| 方法   | 请求 URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **GET** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}>                                     |

### <a name="uri-parameter"></a>URI 参数

在 URL 中使用以下 ID

| 名称                   | 类型     | 必需 | 说明                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|ID                      | string   | 是       | 引荐 ID       |

### <a name="request-headers"></a>请求标头

- 有关详细信息，请参阅 [Partner REST headers](headers.md)（合作伙伴 REST 标头）。

### <a name="request-body"></a>请求正文

下表说明了请求正文中的[引荐](referral-resources.md)属性。

### <a name="request-example"></a>请求示例

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals/0d43414c-fb9f-4ca0-9b8d-29deb70364cf HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

```

## <a name="rest-response"></a>REST 响应

如果成功，此方法会在响应正文中返回填充的[引荐](referral-resources.md)资源。

### <a name="response-success-and-error-codes"></a>响应的成功和错误代码

每个响应都带有一个 HTTP 状态代码，用于指示成功或失败以及其他调试信息。 请使用网络跟踪工具来读取此代码、错误类型和其他参数。 有关完整列表，请参阅[错误代码](error-codes.md)。

### <a name="response-example"></a>响应示例

``` http
{
    "@odata.context": "https://api.partner.microsoft.com/v1.0/engagments/referrals/$metadata#Referrals/$entity",
    "id": "61c65491-2f2c-461a-84b4-3654499bc1d9",
    "engagementId": "b1c40bb4-6d36-4eca-baa3-e1460cf2a454",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "createdDateTime": "2018-10-29T21:24:52.040469Z",
    "updatedDateTime": "2018-10-29T21:24:52.040469Z",
    "expirationDateTime": "2018-11-06T00:00:00Z",
    "status": "New",
    "substatus": "Pending",
    "statusReason": null,
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
            "region": "Washington"
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
        "ids": [
                {
                "profileType": "Duns",
                "id": "795986822"
                }
            ]
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
        "notes": "Hi ABC Partner, Can you help this customer? Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq 'b1c40bb4-6d36-4eca-baa3-e1460cf2a454'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/61c65491-2f2c-461a-84b4-3654499bc1d9",
            "method": "GET"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\""
}
```