---
title: 合作伙伴 API REST 标头
description: 合作伙伴 REST API 支持以下 HTTP 请求和响应标头。
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 955cab07da7f3a386690e18042165015906d864a
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2020
ms.locfileid: "80342227"
---
# <a name="partner-rest-api-headers"></a>合作伙伴 REST API 标头

合作伙伴 REST API 支持以下 HTTP 请求和响应标头。

> [!NOTE]
> 并非所有 API 调用都接受所有标头。

## <a name="request-headers"></a>请求标头

合作伙伴 REST API 支持以下 HTTP 请求标头。

| 标头                       | 值类型 | 说明                                                                            |
|------------------------------|------------|----------------------------------------------------------------------------------------|
| 授权           | string     | 必需。 Authorization 标头采用 Bearer &lt;token&gt; 形式。                    |
| 接受                  | string     | 指定请求和响应类型“应用程序/json”。                           |
| client-request-id         | GUID       | 必需。 调用的唯一标识符，在日志和网络跟踪中用于排查错误。 应重置每个调用的此值。 所有操作都应包含此标头。 |
| If-Match:                    | string     | 用于并发控制。 某些 API 调用要求通过 If-Match 标头来传递 ETag。 ETag 通常出现在资源上，因此，需要获取最新的。 |

## <a name="response-headers"></a>响应标头

合作伙伴 REST API 可能返回以下 HTTP 响应标头。

| 标头                    | 值    类型 | 说明                                                                                                               |
|-------------------|------------|--------------------------------------------------------------------------------------------------|
| 接受                | string     | 指定请求和响应类型“应用程序/json”。                                     |
| request-id        | GUID       | 调用的唯一标识符，用于确保 ID 强度。 在超时情况下，重试调用应包含同一值。 收到响应（业务成功或失败）后，应针对下一次调用重置此值。 |
| client-request-id| GUID| 调用的唯一标识符，在日志和网络跟踪中用于排查错误。 应重置每个调用的此值。 所有操作都应包含此标头。                                                |
| x-ms-ags-diagnostic   | string | 一个字符串，其中包含来自服务的诊断信息。
| timestamp|string | 请求命中 API 时的时间戳。
|ETag |string | 资源的 ETag。
