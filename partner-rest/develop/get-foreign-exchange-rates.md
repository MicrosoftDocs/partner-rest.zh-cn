---
title: 获取外币汇率
description: 获取给定月的外币汇率。
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1e718624db54dcc2ed2b5d2d93dfd1cef0e6f96f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "88001673"
---
# <a name="get-foreign-exchange-rates"></a>获取外币汇率

适用于：

- 合作伙伴 API

本主题说明如何获取给定月份的外币汇率。

## <a name="prerequisites"></a>必备条件

- [Partner API authentication](api-authentication.md)（合作伙伴 API 身份验证）中所述的凭据。 此方案仅支持应用程序用户身份验证。 目前尚不支持应用程序。
- 此 API 目前仅支持用户访问权限，其中合作伙伴必须属于以下角色之一：全局管理员、管理代理或销售代理。


## <a name="details"></a>详细信息

- 当前与 "[获取价目表" API](get-a-price-sheet.md)一起用于计算 AZURE 计划 CSP 本地货币的预计费用。
- 外国汇率在整个月发布后均为 true。
- 有关 Azure 计划[定价](pricing.md)的详细信息，请参阅[azure 计划定价文档](https://docs.microsoft.com/partner-center/azure-plan-price-list)。
- 合作伙伴定价和外国汇率 Api 不属于[合作伙伴中心 SDK](https://docs.microsoft.com/partner-center/develop/get-started)。
- 此方法以文件流的形式返回结果。 文件流是 .csv 文件或 .csv 的压缩版本。 下面提供了有关如何请求压缩的文件的详细信息。

## <a name="rest-request"></a>REST 请求

### <a name="request-syntax"></a>请求语法

| 方法   | 请求 URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **GET** | https://api.partner.microsoft.com/v1.0/sales/fxrates(Month="{month}" ) /$value                                  |

### <a name="uri-required-parameters"></a>URI 必需参数

使用以下路径参数来请求所需的外币汇率的月份。

| 名称                   | 类型     | 必选 | 描述                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|月份                      | 字符串   | 是       | 必须采用 YYYMM 格式。 如果省略，则默认为当前月份。       |

### <a name="request-headers"></a>请求标头

- 有关详细信息，请参阅 [Partner REST headers](headers.md)（合作伙伴 REST 标头）。

除了上述标头外，还可以将文件检索为压缩后的带宽和下载时间。 默认情况下，不压缩文件。 若要获取文件的压缩版本，可以包含下面的标头值。 请注意，压缩的工作表仅在2020年4月提供，2020年4月之前的所有请求仅可用于未压缩。

| 标头                   | 值类型     | “值” | 描述                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| 字符串   | deflate| 可选。 如果未压缩省略的文件流，则为。       |

### <a name="request-example"></a>请求示例

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST 响应

如果成功，则此方法返回作为文件流的外部汇率。 文件流是 .csv 文件或 .csv 的压缩版本。

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
