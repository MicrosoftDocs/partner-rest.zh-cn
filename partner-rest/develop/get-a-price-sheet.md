---
title: 获取价目表
description: 获取给定市场和视图的价格表。 支持筛选器以按月获取历史记录。
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d6f1fbd39e7bdb30bdaef19cbf632cc87a2ea4ff
ms.sourcegitcommit: dbb0a0d2b928eaacbae0795166b3e51547fb0bf6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223310"
---
# <a name="get-a-price-sheet"></a>获取价目表

适用于：

- 合作伙伴 API

本主题说明如何获取给定市场和视图的价目表。 此方法支持按月份获取历史记录的筛选器。

## <a name="prerequisites"></a>必备条件

- [Partner API authentication](api-authentication.md)（合作伙伴 API 身份验证）中所述的凭据。 此方案仅支持应用程序用户身份验证。 目前尚不支持只能。

## <a name="details"></a>详细信息

- Current 只为 Azure 计划消耗和预订产品返回数据。
- 当前[定价](pricing.md)包括当前月份内可用的所有计量和产品，以及调用 API 的日期。 上个月包含给定月份可用的所有计量和产品。
- 消耗计量价仅为 USD，合作伙伴将使用外币汇率 API 来计算本地货币成本。
- 消耗计量价格是预计零售价格。 合作伙伴折扣通过合作伙伴获得的[信用额度](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation)提供。
- 预订计量价格包括 CSP 合作伙伴折扣。 可从合作伙伴中心的 "定价和优惠" 页中获取预订的预计零售价格。
- 有关 Azure 计划定价的详细信息，请参阅[azure 计划定价文档](https://docs.microsoft.com/partner-center/azure-plan-price-list)。
- 合作伙伴定价和外国汇率 Api 不属于[合作伙伴中心 SDK](https://docs.microsoft.com/partner-center/develop/get-started)。
- 此方法将价目表作为文件流返回。 文件流是 .csv 文件或 .csv 的压缩版本。 下面提供了有关如何请求压缩的文件的详细信息。

## <a name="rest-request"></a>REST 请求

### <a name="request-syntax"></a>请求语法

| 方法   | 请求 URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **GET** | https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market="{marketplace}"，PricesheetView = "{view}"）/$value                                     |

### <a name="uri-required-parameters"></a>URI 必需参数

使用以下路径参数来请求所需的市场和价目表类型。

| 名称                   | 类型     | 必需 | 说明                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|市场                      | 字符串   | 是       | 请求的市场的双字母国家/地区代码       |
|PricesheetView | 字符串   | 是       | 请求的价目表类型，可以是 azure_consumption 或 azure_reservations       |

### <a name="uri-filter-parameters"></a>URI 筛选器参数

使用以下筛选器参数。

| 名称                   | 类型     | 必需 | 说明                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|时间线| 字符串   | 否| 如果未通过，则默认值为 "当前"。 可能的值包括历史记录、当前和未来。       |
|月份| 字符串   | 否| 仅在请求历史记录时是必需的，对于所请求的价目表，必须遵循 YYYYMM。       |

### <a name="request-headers"></a>请求标头

- 有关详细信息，请参阅 [Partner REST headers](headers.md)（合作伙伴 REST 标头）。

除了上述标头外，还可以将定价文件作为压缩的缩减带宽和下载时间来检索。 默认情况下，不压缩文件。 若要获取文件的压缩版本，可以包含下面的标头值。 请注意，压缩的工作表仅在2020年4月之后可用，4月2020之前的所有工作表都只能提供为未压缩。

| Header                   | 值类型     | 值 | 描述                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| 字符串   | deflate| 可选。 如果未压缩省略的文件流，则为。       |

### <a name="request-example"></a>请求示例

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST 响应

如果成功，则此方法将价目表作为文件流返回。 文件流是 .csv 文件或 .csv 的压缩版本。

### <a name="response-success-and-error-codes"></a>响应的成功和错误代码

每个响应都带有一个 HTTP 状态代码，用于指示成功或失败以及其他调试信息。 请使用网络跟踪工具来读取此代码、错误类型和其他参数。 有关完整列表，请参阅[错误代码](error-codes.md)。

### <a name="response-example"></a>响应示例

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=pricesheet
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Oct 2019 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","MeterIds","MeterType","Tags“
"Advanced Data Security - SQL Database","DZH318Z0C16V","001J","Advanced Data Security - SQL Database - Standard - US East 2","Microsoft","Advanced Data Security - SQL Database - Standard - US East 2","1 Node/Month","payG-1","US","USD","15","","","3/1/2018 12:00:00 AM","11/30/9999 11:59:59 PM","cb0969aa-aaaa-4d6c-ab4b-7e182fa06aff","1 Node/Month","Azure“
======= Truncated ==============

```
