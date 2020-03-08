---
title: 获取外币汇率
description: 获取给定月的外币汇率。
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0d044c36a94c521fbfb980017e0503e78826ffd1
ms.sourcegitcommit: 50d18c96d24755174beb4fcb694223325a7fe450
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "76796616"
---
# <a name="get-foreign-exchange-rates"></a>获取外币汇率

适用范围：

- 合作伙伴 API

本主题说明如何获取给定月份的外币汇率。

## <a name="prerequisites"></a>先决条件

- [Partner API authentication](api-authentication.md)（合作伙伴 API 身份验证）中所述的凭据。 此方案仅支持应用程序用户身份验证。 目前尚不支持应用程序。


## <a name="details"></a>详细信息

- 当前与 "[获取价目表" API](get-a-price-sheet.md)一起用于计算 AZURE 计划 CSP 本地货币的预计费用。
- 外国汇率在整个月发布后均为 true。
- 有关 Azure 计划[定价](pricing.md)的详细信息，请参阅[azure 计划定价文档](https://docs.microsoft.com/partner-center/azure-plan-price-list)。
- 合作伙伴定价和外国汇率 Api 不属于[合作伙伴中心 SDK](https://docs.microsoft.com/partner-center/develop/get-started)。

## <a name="rest-request"></a>REST 请求

### <a name="request-syntax"></a>请求语法

| 方法   | 请求 URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **GET** | https://api.partner.microsoft.com/v1.0/sales/fxrates(Month="{month}"）/$value                                  |

### <a name="uri-required-parameters"></a>URI 必需参数

使用以下路径参数来请求所需的外币汇率的月份。

| 名称                   | 类型     | 必需 | 说明                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|月                      | string   | 是       | 必须采用 YYYMM 格式。 如果省略，则默认为当前月份。       |

### <a name="request-headers"></a>请求标头

- 有关详细信息，请参阅 [Partner REST headers](headers.md)（合作伙伴 REST 标头）。

### <a name="request-example"></a>请求示例

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer 
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST 响应

如果成功，则此方法返回作为文件流的外部汇率。

### <a name="response-success-and-error-codes"></a>响应的成功和错误代码

每个响应都带有一个 HTTP 状态代码，用于指示成功或失败以及其他调试信息。 请使用网络跟踪工具来读取此代码、错误类型和其他参数。 有关完整列表，请参阅[错误代码](error-codes.md)。

### <a name="response-example"></a>响应示例

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 18548
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=fxrates
Request-ID: 65fb6e59-051b-42f7-8771-c8c139b3c901
Date: Wed, 02 Oct 2019 03:42:54 GMT

"CurrencyCode","USDPerUnit","Month"
"AED","0.27224589249009701","2019”
======= Truncated ==============

```
