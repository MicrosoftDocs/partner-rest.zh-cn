---
title: 引荐资源
description: 引荐资源表示直接来自客户、Microsoft 或其他合作伙伴的销售线索。
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 1fdb539835ae6aaa662407270393ae1ad81ed309
ms.sourcegitcommit: f7918b7775ca8c6192b2a3e61edb74547730672d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "74556677"
---
# <a name="referral-resources"></a>引荐资源

适用于：

- 合作伙伴中心

这些资源表示直接来自客户、Microsoft 或其他合作伙伴的销售线索。

## <a name="referral"></a>引荐

表示引荐。

| 属性              | 在任务栏的搜索框中键入                                              | 描述                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| ID                    | 字符串                                            | 此引荐的 ID。                                                                                         |
| EngagementId          | 字符串                                            | 此引荐的 EngagementID。 可以将多个引荐关联到单个 EngagementID                 |
| 名称                  | 字符串                                            | 引荐的名称。                 |
| ExternalReferenceId   | 字符串                                            | 引荐的外部标识符。 示例：存储自己的 Dynamics 365 潜在客户/机会 ID                    |
| CreatedDateTime       | 采用 UTC 日期/时间格式的字符串                    | 创建引荐的日期。                                                                                |
| UpdatedDateTime       | 采用 UTC 日期/时间格式的字符串                    | 上次更新引荐的日期。                                                                           |
| ExpirationDateTime    | 采用 UTC 日期/时间格式的字符串                    | 引荐将过期的日期。                                                                                |
| 状态                | [ReferralStatus](referral-resources.md#referralstatus)      | 一个 [Enum](https://docs.microsoft.com/dotnet/api/system.enum)，其值指示引荐状态。 |
| Substatus          | [ReferralSubstatus](referral-resources.md#referralsubstatus)      | 一个 [Enum](https://docs.microsoft.com/dotnet/api/system.enum)，其值指示引荐子状态。 |
| StatusReason          | 字符串                                            | 一条有关状态的说明性消息。 示例：为什么引荐丢失了? |
| ReferralType          | [ReferralType](referral-resources.md#referraltype)          | 表示引荐类型。                                                                                     |
| Qualification         | [ReferralQualification](referral-resources.md#referralqualification)| 表示引荐的质量。                                                                           |
| CustomerProfile       | [CustomerProfile](referral-resources.md#customerprofile)    | 有关客户的信息。                                                                                     |
| Consent               | [许可](referral-resources.md#consent)                    | 如果要与其他组织共享信息并允许其联系用户，则使用许可标记。         |
| 详细信息               | [ReferralDetails](referral-resources.md#referraldetails)    | 客户详细信息、说明、交易值、货币结账日期。                                                                |
| 组                  | [成员](referral-resources.md#member)                      | 表示涉及的组织中的用户。                                |
| InviteContext         | [InviteContext](referral-resources.md#invitecontext)        | 表示用户在邀请其他组织参与合作伙伴计划时可以提供的其他信息。  |
| ETag                  | 字符串                                            | ETag 用于更新资源时的并发检查，是必需项。 |
| 目标         | [ReferralTarget](referral-resources.md#target)        | 表示用户在邀请其他组织参与合作伙伴计划时可以提供的其他信息。  |

## <a name="referralstatus"></a>ReferralStatus

一个 [Enum](https://docs.microsoft.com/dotnet/api/system.enum)，其值指示引荐状态。

| 值           | 描述                                                                                |
|-----------------|---------------------------------------------------------------------------------------------|
| 无            |                                                                                             |
| 新增             | 表示新的引荐。                                                                 |
| 活跃          | 表示活跃的引荐。                                                             |
| 关闭          | 表示关闭的引荐。                                                              |

## <a name="referralsubstatus"></a>ReferralSubstatus

一个 [Enum](https://docs.microsoft.com/dotnet/api/system.enum)，其值指示引荐状态。

| 值           | 描述                                                                                |
|-----------------|--------------------------------------------------------------------------------------------|
| 无            |                                                                                            |
| Pending         | 表示挂起的新引荐。                                                 |
| 已接收        | 表示已接收的新引荐。                   |
| 接受        | 表示已接受的活跃引荐。                                                    |
| Won             | 表示赢得的已关闭引荐。                                            |
| Lost            | 表示丢失的已关闭引荐。                                           |
| 已拒绝        | 表示被拒绝的已关闭引荐。                                       |
| 过期         | 表示过期的已关闭引荐。                                             |

### <a name="status--substatus-transition-states"></a>状态和子状态转换状态

| 状态                | 允许的状态转换     | 允许的子状态                |
|-----------------------|-------------------------------|---------------------------------------|
| 新增                   | 新增、活跃、已关闭           | 挂起、已接收                     |
| 活跃                | 活跃、已关闭                | 接受                              |
| 关闭                | 关闭                        | 赢得、丢失、已拒绝、已过期          |

## <a name="referraltype"></a>ReferralType

一个 [Enum](https://docs.microsoft.com/dotnet/api/system.enum)，其值指示引荐类型。

| 属性              | 描述                                                                     |
|-----------------------|---------------------------------------------------------------------------------|
| 共享                | 表示一个引荐，其中涉及的各方会通过协作方式进行关闭。  |
| Independent           | 表示一个引荐，其中的双方方会通过协作方式进行关闭。           |

## <a name="referralqualification"></a>ReferralQualification

一个 [Enum](https://docs.microsoft.com/dotnet/api/system.enum)，其值指示引荐状态。

| 值                | 描述                                                                                 |
|----------------------|---------------------------------------------------------------------------------------------|
| 无                 | 表示一个没有关联的质量衡量标准的引荐。                               |
| Direct               | 表示一个已经直接由客户创建的引荐。                         |
| MarketingQualified   | 表示一个已经通过 Microsoft 营销自动化系统生成的引荐。   |
| SalesQualified       | 表示一个来自 Microsoft 营销代理的引荐。                                         |

## <a name="customerprofile"></a>CustomerProfile

包含客户联系人信息。

| 属性 | 在任务栏的搜索框中键入                                                   | 描述                                            |
|----------|--------------------------------------------------------|--------------------------------------------------------|
| 名称     | 字符串                                                 | 客户组织名称。                        |
| 地址  | [地址](referral-resources.md#address)                         | 客户的地址。                           |
| 尺寸     | 字符串                                                 | 客户组织的员工数。 |
| 组     | [成员](referral-resources.md#member)                           | 客户组织的联系人。            |
| Ids      | [CustomerProfileType](referral-resources.md#customerprofiletype) | 一个 [Array](https://docs.microsoft.com/en-us/dotnet/api/system.array)，其中的值指示客户的外部 ID。                        |

## <a name="customerprofiletype"></a>CustomerProfileType

包含客户的外部 ID。

| 属性 | 在任务栏的搜索框中键入   | 描述                                                                           |
|----------|--------|---------------------------------------------------------------------------------------|
| Duns     | 字符串 | 客户的 [Dun 和 Bradstreet 编码](https://www.dnb.com/duns-number.html)。 |
| 外部 | 字符串 | 你的组织特有的客户 ID。                                            |

## <a name="address"></a>地址

一个用于客户的地址。

| 属性     | 在任务栏的搜索框中键入   | 描述                                                |
|--------------|--------|------------------------------------------------------------|
| 地址行 1 | 字符串 | 地址的第一行。                             |
| 地址行 2 | 字符串 | 地址的第二行。 此属性为可选项。 |
| 城市         | 字符串 | 城市。                                                  |
| 状态        | 字符串 | 省/市/自治区。                                                 |
| 邮政编码   | 字符串 | 邮政编码或邮编                                |
| 国家/地区      | 字符串 | 国家/地区，采用 [ISO 国家/地区代码格式](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.regioninfo.threeletterisoregionname?view=netframework-4.7.2)。             |
| Region       | 字符串 | 区域。                                                |

## <a name="member"></a>成员

描述特定个人的联系人信息。

| 属性    | 在任务栏的搜索框中键入   | 描述                  |
|-------------|--------|------------------------------|
| FirstName   | 字符串 | 联系人的名字。    |
| LastName    | 字符串 | 联系人的姓氏。     |
| PhoneNumber | 字符串 | 联系人的电话号码。  |
| 电子邮件       | 字符串 | 联系人的电子邮件地址。 |
| ContactPreference       | [ContactPreference](referral-resources.md#contactpreference) | 联系人的有关如何接收电子邮件通知的首选项。 |

## <a name="contactpreference"></a>ContactPreference

描述联系人的有关如何接收电子邮件通知的首选项。

| 属性    | 在任务栏的搜索框中键入   | 描述                  |
|-------------|--------|------------------------------|
| 区域设置   | 字符串 | 电子邮件通知的区域设置。 支持 [AllCultures](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_AllCultures)、[NeutralCultures](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_NeutralCultures) 和 [SpecificCultures](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_SpecificCultures)  |
| DisableNotifications    | 布尔 | 会禁用用户的电子邮件通知。     |

## <a name="consent"></a>Consent

如果要与其他组织共享信息并允许其联系用户，则使用许可标记。

| 属性                                         | 在任务栏的搜索框中键入      | 描述                                                                                |
|--------------------------------------------------|-----------|--------------------------------------------------------------------------------------------|
| ConsentToToShareInfoWithOthers                   | 布尔值   | 表示同意与他人共享个人身份信息 (PII)。             |
| ConsentToContact                                 | 布尔值   | 表示同意与用户联系。  |

## <a name="invitecontext"></a>InviteContext

邀请其他组织时可能被共享的其他信息。

| 属性              | 在任务栏的搜索框中键入                                                       | 描述                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| 注释                 | 字符串                                                     | 针对接收组织的其他说明。                |
| InvitedBy | [InvitedBy](referral-resources.md#invitedby)                                     | 发送了引荐的组织 ID。                                   |

## <a name="invitedby"></a>InvitedBy

邀请其他组织时可能被共享的其他信息。

| 属性              | 在任务栏的搜索框中键入                                                       | 描述                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| OrganizationId        | 字符串                                                     | 发送了引荐的组织 ID。                |
| 组织名称      | 字符串                                                     | 发送了引荐的组织名称。                                   |

## <a name="referraldetails"></a>ReferralDetails

表示引荐详细信息。

| 属性              | 在任务栏的搜索框中键入                                                       | 描述                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| 注释                 | 字符串                                                     | 针对接收组织的其他说明。                |
| DealValue             | 十进制                                                    | 引荐的值。                                    |
| 货币              | 字符串                                                    | [ISO 4217 货币符号](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.regioninfo.isocurrencysymbol?view=netframework-4.7.2)                                   |
| ClosingDateTime       | 采用 UTC 日期/时间格式的字符串                         | 客户预期关闭的日期。                           |
| 要求          | [ReferralRequirements](referral-resources.md#referralrequirements)   | 客户感兴趣的行业、产品、服务类型和解决方案。|

## <a name="referralrequirements"></a>ReferralRequirements

包含客户要求。

| 属性        | 在任务栏的搜索框中键入                                                         | 描述                                          |
|-----------------|--------------------------------------------------------------|------------------------------------------------------|
| Industries      | [标记](referral-resources.md#tag)                                       | 客户感兴趣的行业。        |
| 产品        | [标记](referral-resources.md#tag)                                       | 客户感兴趣的产品。          |
| 服务        | [标记](referral-resources.md#tag)                                       | 客户感兴趣的服务。          |
| 解决方案       | [SolutionTag](referral-resources.md#solutiontag)                       | 客户感兴趣的解决方案。                             |

## <a name="solutiontag"></a>SolutionTag

包含解决方案详细信息。

| 属性        | 在任务栏的搜索框中键入                                         | 描述                                          |
|-----------------|----------------------------------------------|------------------------------------------------------|
| ID              | 字符串                                       | 解决方案的 ID。        |
| 名称            | 字符串                                       | 解决方案的名称。          |
| SolutionType    | [SolutionType](referral-resources.md#solutiontype)     | 解决方案的类型。          |

## <a name="solutiontype"></a>SolutionType

一个 [Enum](https://docs.microsoft.com/dotnet/api/system.enum)，其值指示解决方案类型。

| 属性        | 描述                                                     |
|-----------------|-----------------------------------------------------------------|
| 无            |                                                                  |
| 类别        |  利用预定义的解决方案名称。                            |
| 名称            |  从 Microsoft 目录引用解决方案的功能。 |

## <a name="target"></a>目标

描述引荐目标。

| 属性                  | 在任务栏的搜索框中键入                                                  | 描述                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| ID                        | 字符串                                                | 引荐目标的 ID。 |
| 在任务栏的搜索框中键入                      | [ReferralTargetType](referral-resources.md#targettype) | 引荐目标类型 |

## <a name="targettype"></a>TargetType

一个 [Enum](https://docs.microsoft.com/dotnet/api/system.enum)，其值指示解决方案类型。

| 属性        | 描述                                                     |
|-----------------|-----------------------------------------------------------------|
| 无            |                                                                  |
| BusinessProfileLocation         |  合作伙伴业务配置文件中的配置文件位置。                            |
| SolutionProfile            |  合作伙伴的解决方案配置文件。 |

## <a name="tag"></a>Tag

描述标记。

| 属性                  | 在任务栏的搜索框中键入                                                  | 描述                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| ID                        | 字符串                                                | 此标记的 ID。                                          |

### <a name="products"></a>产品

| 值        |
|-----------------|
|Azure|
|EnterpriseMobilityAndSecurity|
|Exchange|
|DeveloperTools|
|Dynamics365Business|
|Dynamics365Enterprise|
|DynamicsAX,GP,NAV,SL|
|Microsoft365|
|Office|
|PowerBI|
|项目|
|SharePoint|
|SkypeForBusiness|
|Surface|
|SurfaceHub|
|SQL|
|Teams|
|Visio|
|Windows|
|Yammer|

### <a name="services"></a>服务

| 值        |
|-----------------|
|ConsultingAndProfessional|
|CustomSolution(ISV)|
|DeploymentOrMigration|
|硬件|
|集成|
|IPServices(ISV)|
|LearningAndCertification|
|授权|
|ManagedServices|
|ProjectServices|

### <a name="industries"></a>Industries

| 值        |
|-----------------|
|农、林、渔|
|通信和媒体|
|教育版|
|金融服务|
|政策|
|医疗业|
|餐饮业|
|制造|
|电力设施|
|公共安全和国家安全|
|零售和消费品|
|服务|
|旅游和运输业|
|批发和分销|

### <a name="solutions"></a>解决方案

| 值        |
|-----------------|
|AdvancedAnalytics|
|ApplicationIntegration|
|ArtificialIntelligence|
|AzureSecurityOperationManagement|
    |AzureStack|
    |BackupDisasterRecovery|
    |BigData|
    |区块链|
    |聊天机器人|
    |CloudDatabaseMigration|
    |CloudMigration|
    |CloudVoice|
    |CognitiveServices|
    |CompetitiveDatabaseMigration|
    |容器|
    |DataWarehouse|
    |DatabaseonLinux|
    |DevelopmentandTest|
    |DevOps|
    |DigitalMedia|
    |Dynamics365forCustomerService|
    |Dynamics365forFieldService|
    |Dynamics365forFinanceOperations|
    |Dynamics365forRetail|
    |Dynamics365forSales|
    |Dynamics365forTalent|
    |DynamicsonAzure|
    |EnterpriseBusinessIntelligence|
    |游戏|
    |HighPerformanceComputing|
    |HybridStorage|
    |IdentityandAccessManagement|
    |InformationManagement|
    |InternetofThings|
    |MachineLearning|
    |Microserviceapplications|
    |MobileApplications|
    |MySQLPostgresMigrationtoAzure|
    |网络|
    |NoSQLMigration|
    |RedhatonAzure|
    |RegulatoryComplianceGDPR|
    |SAPonAzure|
    |ServerlessComputing|
    |SharepointonAzure|
    |SQLServerUpgrade|
    |ThreatProtection|
    |WebDevelopment|

### <a name="customer-size"></a>客户规模

| 值        |
|-----------------|
|    1to50employees|
|    51to500employees|
|    Morethan500employees|
|    1to9employees|
|    10to50employees|
|    51to250employees|
|    251to1000employees|
|    1001to5000employees|
|    5001to10000employees|
|    10001to20000employees|
|    Morethan20000employees|