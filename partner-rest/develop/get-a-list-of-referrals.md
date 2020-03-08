---
title: 获取引荐列表
description: 如何使用合作伙伴 API 获取引荐列表。
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7daa7a1989a5832f58d555b1f8bb3d7681024dba
ms.sourcegitcommit: 50d18c96d24755174beb4fcb694223325a7fe450
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "74556527"
---
# <a name="get-a-list-of-referrals"></a>获取引荐列表

适用范围：

- 合作伙伴 API

本主题说明了如何获取引荐列表。

## <a name="prerequisites"></a>先决条件

- [Partner API authentication](api-authentication.md)（合作伙伴 API 身份验证）中所述的凭据。 此方案支持使用应用凭据和用户凭据进行身份验证。

## <a name="rest-request"></a>REST 请求

### <a name="request-syntax"></a>请求语法

| 方法  | 请求 URI                                                  |
|---------|--------------------------------------------------------------|
| **GET** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### <a name="supported-odata-operations"></a>支持的 OData 操作

| 名称     | 说明            | 示例                                                                    |
|:---------|:-----------------------|:---------------------------------------------------------------------------|
| $filter  | 筛选结果（行） |`/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` |
| $orderby | 将结果排序         |`/referrals?$orderby=createdDateTime desc`                                  |

#### <a name="supported-filter-parameters"></a>支持的筛选器参数

使用以下筛选器参数获取引荐列表

| 名称         | 类型   | 必需 | 说明                                                                             |
|--------------|--------|----------|-----------------------------------------------------------------------------------------|
| engagementId | string | 是       | 一个参与 ID。                                                                       |
| status       | string | 是       | 一个表示 [ReferralStatus](referral-resources.md#referralstatus) 的字符串       |
| substatus    | string | 是       | 一个表示 [ReferralSubstatus](referral-resources.md#referralsubstatus) 的字符串 |
| updatedDateTime     | string | 是       | 引荐的 UpdatedDatetime |
| 电子邮件     | string | 是       | 引荐的团队联系人电子邮件 |

#### <a name="supported-orderby-parameters"></a>支持的排序方式参数

使用以下排序方式参数获取引荐列表

| 名称           | 类型     | 必需 | 说明                        |
|----------------|----------|----------|------------------------------------|
|createdDateTime | DateTime | 是      | 引荐创建日期和时间 |

### <a name="request-headers"></a>请求标头

- 有关详细信息，请参阅 [Partner REST headers](headers.md)（合作伙伴 REST 标头）。

### <a name="request-body"></a>请求正文

无。

### <a name="request-example"></a>请求示例

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

```

## <a name="rest-response"></a>REST 响应

如果请求成功，则响应正文包含[引荐资源](referral-resources.md)的集合。

### <a name="response-success-and-error-codes"></a>响应的成功和错误代码

每个响应都带有一个 [HTTP 状态代码](error-codes.md)，用于指示成功或失败以及其他调试信息。 请使用网络跟踪工具来读取此代码、错误类型和其他参数。

### <a name="response-example"></a>响应示例

``` http
{
    "@odata.context": "http://api.partner.microsoft.com/v1.0/$metadata#Referrals",
    "@odata.count": 100,
    "value": [
        {
            "id": "c5fbb3b6-be74-4795-9fb5-4324c73fed37",  
            "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
            "organizationName": "Contoso Company",
            "engagementId": "65edc0b5-3485-41b7-a17e-dfa9ef4706e2",
            "externalReferenceId": "",
            "createdDateTime": "2018-10-30T21:03:42.4579542Z",
            "updatedDateTime": "2018-10-30T21:03:42.4579542Z",
            "expirationDateTime": "2018-11-13T00:00:00Z",
            "status": "New",
            "substatus": "Pending",
            "qualification": "Direct",
            "type": "Independent",
            "target": [
                    {
                        "type": "BusinessProfileLocation",
                        "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
                    }
            ],
            "customerProfile": {
                "name": "Fabrikam Customer Inc",
                "address": {
                    "addressLine1": "One Microsoft Way",
                    "addressLine2": "",
                    "city": "Redmond",
                    "state": "WA",
                    "postalCode": "98052",
                    "country": "US"
                },
                "size": "1to9employees",
                "team": [
                    {
                        "contactPreference": {
                            "locale": "en-US",
                            "disableNotifications": false
                        },
                        "firstName": "Sue",
                        "lastName": "Smith",
                        "phoneNumber": "1234567890",
                        "email": "sue.smith@fabrikam.com"
                    }
                ],
                "ids": {}
            },
            "consent": {
                "consentToContact": true
            },
            "details": {
                "notes": "We are interested in deploying Microsoft 365 and are looking for support in training our employees. Can you help?",
                "requirements": {
                    "industries": [
                        {
                            "id": "Education"
                        }
                    ],
                    "products": [
                        {
                            "id": "Microsoft365"
                        }
                    ],
                    "services": [
                        {
                            "id": "LearningAndCertification"
                        }
                    ]
                }
            }
            "links": {
                "relatedReferrals":
                    {
                       "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
                        "method": "GET"
                    },
                "self":
                    {
                       "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals/c5fbb3b6-be74-4795-9fb5-4324c73fed37",
                        "method": "GET"
                    }
            },
        },
        {
            "id": "61c65491-2f2c-461a-84b4-3654499bc1d9",
            "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
            "organizationName": "Contoso Company",
            "engagementId": "b1c40bb4-6d36-4eca-baa3-e1460cf2a454",
            "createdDateTime": "2018-10-29T21:24:52.040469Z",
            "updatedDateTime": "2018-10-29T21:24:52.040469Z",
            "expirationDateTime": "2018-11-06T00:00:00Z",
            "status": "New",
            "substatus": "Pending",
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
                            "locale": "en-US",
                            "disableNotifications": false
                        },
                        "firstName": "Sue",
                        "lastName": "Smith",
                        "phoneNumber": "1234567890",
                        "email": "sue.smith@contoso.com"
                    },
                    {
                        "contactPreference": {
                            "locale": "en-US",
                            "disableNotifications": false
                        },
                        "firstName": "Joe",
                        "lastName": "Hansen",
                        "phoneNumber": "4035698759",
                        "email": "joe.hansen@contoso.com"
                    }
                ],
                "ids": {}
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
                        "locale": "en-US",
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
                    "organizationId": "msft",
                    "organizationName": "Microsoft"
                }
            },
            "links": {
                "relatedReferrals":
                    {
                       "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=engagementId eq 'b1c40bb4-6d36-4eca-baa3-e1460cf2a454'",
                        "method": "GET"
                    },
                "self":
                    {
                       "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals/61c65491-2f2c-461a-84b4-3654499bc1d9",
                        "method": "GET"
                    }
            }
        }
    ],
  
 "@odata.nextLink": "http://api.partner.microsoft.com/v1.0/referrals?$skiptoken=k181pEdP0ykypkieJfcxXIN4ARsee8%2fFUEbbvZaoTUZRLJ3o7TADYve12iEDrlgVevJO5J0ftNkTY5FZepU1sh1m8fRNuUD4YPGazoaywpAqoRAd43JuVJV8fwmcJFTFAH4Wg2%2fQFWkxT6PWujvkj%2biqLMDsU8CI6x3k0CHZWhLiw4inmd3Ib8wVoA4wygjONBhcEegyySiZa85H59pWHQoNFA%2fYP6tyw3%2f0CgcSwa%2fh%2bDf7Ygm0MaOhBZbYmkhRITbgRT1LWDLBGpNzLJN%2fB%2basQXEojDL7tZRLB%2bGlfPJ%2fojPBTctFqEp13TVZta2jdJmC917IhR5fGt91%2blwuxd83Y5PwCjXpg%2fYn8JKna10%2bVe4Devy21pryas%2bu3oGKmbqaXKMBIUCQU8D7cFy59R90Tzcogte05QSSiN6U1KP%2bY1oPchrKmvqt8S6jNoy%2bTaR3Bc9AtzVNpuaEGGkfO9g3SFlLuBv%2bd4aG50iFjmOKCAPIRr76JVUzYsJ76oyUv0AOZ%2bW5lqgtyQQwN%2b%2baEkF3HDebb6%2byTqdagjI86faTAi4YOOn0oVmmGIWZJnp5MuG38P8VHqK4ZdZ5OpKkpMrigLqYrU%2fFliGbBgnTP4Y7Pp%2fai9JzxYF1%2fajIYsE0OdyojAG2GtzNzlyHj1g9e9Tgz2%2fy5BfHrk4asYRcSvQfN%2bdaO1NVWCraMvhxjsr5Twcg9z%2bAETNVqXZMp5qKBsPGxPFcnWGx6OY296kmIzuTnDd2igIoye8wj57xO4WEBIW3%2bFIHrBlzh3bV0ljNHBb%2f5eDF68GK6AMmwusqjleiW3iHmZRPeTiMU2oPuzx5"
}
```

如果集合中的项超出 100 个，请使用 `@odata.nextLink` 获取下一页结果。

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json
```
