---
title: 合作伙伴 API REST 错误代码
description: 合作伙伴 REST API 会返回一个 JSON 对象，其中的状态代码会指示请求是成功还是失败。
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0829f48e5028b4a19e8a6f7b89fbb41d83a50cab
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2020
ms.locfileid: "80342294"
---
# <a name="partner-api-rest-error-codes"></a>合作伙伴 API REST 错误代码

适用范围：

- 合作伙伴 API

合作伙伴 REST API 中的错误使用标准 HTTP 状态代码和 JSON 错误响应对象返回。

## <a name="http-status-codes"></a>HTTP 状态代码

下表列出并介绍了可能返回的 HTTP 状态代码。

| 状态代码 | 状态消息                  | 说明                                                                                                                            |
|:------------|:--------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| 400         | 错误的请求                     | 无法处理请求，因为它的格式错误，或者它不正确。                                                                       |
| 401         | Unauthorized                    | 所需身份验证信息缺失或者对资源来说无效。                                                   |
| 403         | 已禁止                       | 访问请求的资源时被拒绝。 用户可能没有足够的权限。 **重要：如果将条件访问策略应用到某个资源，可能会返回 `HTTP 403; Forbidden error=insufficent_claims`。** 有关 Microsoft Graph 和条件访问的更多详细信息，请参阅 [Azure Active Directory 条件访问开发人员指南](https://docs.microsoft.com/azure/active-directory/develop/active-directory-conditional-access-developer)  |
| 404         | 未找到                       | 请求的资源不存在。                                                                                                  |
| 405         | 不允许使用的方法              | 资源上不允许请求中的 HTTP 方法。                                                                         |
| 406         | 不可接受                  | 此服务不支持在 Accept 标头中请求的格式。                                                                |
| 409         | 冲突                        | 当前状态与请求预期的状态冲突。 例如，指定的父文件夹可能不存在。                   |
| 410         | 不存在                            | 请求的资源在服务器上不再可用。                                               |
| 411         | 需要的长度                 | 请求中需要 Content-Length 标头。                                                                                    |
| 412         | 不满足前提条件             | 请求中提供的前提条件（例如 if-match 标头）与资源的当前状态不匹配。                       |
| 413         | 请求实体太大        | 请求大小超出最大限制。                                                                                            |
| 415         | 不支持的介质类型          | 请求的内容类型是服务不支持的格式。                                                      |
| 416         | 请求的范围无法满足 | 指定的字节范围无效或不可用。                                                                                    |
| 422         | 无法处理的实体            | 无法处理请求，因为它在语义上不正确。                                                                        |
| 423         | Locked                          | 所访问的资源已锁定。                                                                                          |
| 429         | 请求过多               | 客户端应用程序已受限，请过一段时间后再尝试重复该请求。                |
| 500         | 内部服务器错误           | 处理请求时出现内部服务器错误。                                                                       |
| 501         | 未实现                 | 未实现请求的功能。                                                                                               |
| 503         | 服务不可用             | 此服务因维护而暂时不可用，或者已过载。 可以在延迟一段时间后重复此请求，延迟的时间长度可以在 Retry-After 标头中指定。|
| 504         | 网关超时                 | 充当代理时，服务器在尝试完成请求时没有从需要访问的上游服务器接收到及时的响应。 可能与 503 一起出现。 |
| 507         | 存储不足            | 已达到最大存储配额。                                                                                            |
| 509         | 超出带宽限制        | 应用已因超出最大带宽限制而受限。 应用可以在更长时间过后重试请求。 |

错误响应是单个 JSON 对象，其中包含单个名为 **error** 的属性。 此对象包含错误的所有详细信息。 可以使用此处返回的信息，而 HTTP 状态代码则既可使用，也可不使用。 下面是完整 JSON 错误正文的示例。

## <a name="error-resource-type"></a>错误资源类型

错误响应是单个 JSON 对象，其中包含单个名为 **error** 的属性。 此对象包含错误的所有详细信息。 可以使用此处返回的信息，而 HTTP 状态代码则既可使用，也可不使用。 下面是完整 JSON 错误正文的示例。

下面的表和代码示例介绍错误响应的架构。

| 名称        | 类型   | 说明                                                                                    |
|-------------|--------|------------------------------------------------------------------------------------------------|
| 代码        | string | 始终返回。 指示已发生的错误的类型。 非 null。                          |
| message | string | 始终返回。 详细描述错误，并提供其他调试信息。 非 null，非空。 最大长度为 1024 个字符。 |
| innerError        | 对象  | 可选。 其他错误对象，可能比顶级错误更具体。                                   |
| target      | string | 错误一开始出现时所在的目标。                                                      |

### <a name="code-property"></a>Code 属性

`code` 属性包含下述可能值之一。 应用应准备好处理下述任何错误。

| 代码                      | 说明
|:--------------------------|:--------------
| **accessDenied**          | 调用方没有执行此操作的权限。
| **generalException**      | 发生了错误。
| **invalidRequest**        | 请求的格式错误，或者请求不正确。
| **itemNotFound**          | 找不到资源。
|**preconditionFailed**     | 请求中提供的前提条件（例如 if-match 标头）与资源的当前状态不匹配。
| **resourceModified**      | 要更新的资源自调用方上次读取它以后已变化，通常是 eTag 不匹配。
| **serviceNotAvailable**   | 服务不可用。 请在延迟一段时间后重新尝试此请求。 可能有 Retry-After 标头。
| **unauthenticated**       | 调用方未进行身份验证。

### <a name="message-property"></a>Message 属性

根中的 `message` 属性包含一条供开发人员阅读的错误消息。 错误消息未本地化，不应直接显示给用户。 当处理错误时，你的代码不应对 `message` 值进行检查，因为它们可以随时更改，并且通常包含特定于失败请求的动态信息。 只应针对 `code` 属性中返回的错误代码进行编码。

### <a name="innererror-object"></a>InnerError 对象

`innererror` 对象可能会以递归方式包含更多 `innererror` 对象，其中有其他更具体的错误代码。 处理错误时，应用应循环访问所有可用的错误代码，使用能够理解的、最详细的错误代码。

应用可能会在嵌套的 `innererror` 对象中遇到一些其他的错误。 应用不需要处理这些错误，但可以选择这样做。 服务可能会随时添加新的错误代码或停止返回旧的错误代码，因此，必须确保所有应用能够处理[基本的错误代码]

```json
{
  "error": {
    "code": "unAuthorized",
    "message": "Caller is not authorized to access the resource.",
    "target": "referral",
    "innerError": {
      "code": "innerErrorCode",
      "message": "Unauthorized referral access"
    }
  }
}
```
