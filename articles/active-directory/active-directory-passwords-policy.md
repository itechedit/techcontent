<properties
    pageTitle="Azure Active Directory 中的密码策略和限制 | Azure"
    description="介绍适用于 Azure Active Directory 中密码的策略，包括允许的字符、长度和过期"
    services="active-directory"
    documentationcenter=""
    author="curtand"
    manager="femila"
    editor="" />
<tags
    ms.assetid="e7cae5cf-e0ee-467b-9a90-db6fdf56cd52"
    ms.service="active-directory"
    ms.workload="identity"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="02/22/2017"
    wacn.date="04/11/2017"
    ms.author="curtand" />  


# Azure Active Directory 中的密码策略和限制
本文介绍与 Azure AD 目录中存储的用户帐户关联的各种密码策略和复杂性要求。

> [AZURE.IMPORTANT]
**你是否因登录时遇到问题而浏览至此？** 如果是这样，[可按以下方式更改和重置你的密码](/documentation/articles/active-directory-passwords-update-your-own-password/#how-to-reset-your-password/)。
>
>

## 适用于所有用户帐户的 UserPrincipalName 策略
需要登录到 Azure AD 身份验证系统的每个用户帐户都必须有唯一的用户主体名称 (UPN) 属性值与该帐户相关联。下表概要列出了同时适用于本地 Active Directory 来源的用户帐户（同步到云）和仅限云的用户帐户的策略。

| 属性 | UserPrincipalName 要求 |
| --- | --- |
| 允许的字符 |<ul> <li>A - Z</li> <li>a - z</li><li>0 - 9</li> <li> . - \_ ! # ^ ~</li></ul> |
| 不允许的字符 |<ul> <li>任何并非分隔用户名和域的“@”字符。</li> <li>不能紧靠在“@”符号前面添加句点字符“.”</li></ul> |
| 长度约束 |<ul> <li>总长度不能超过 113 个字符</li><li>“@”符号前面可以有 64 个字符</li><li>“@”符号后面可以有 48 个字符</li></ul> |

## 仅适用于云用户帐户的密码策略
下表描述了可用于在 Azure AD 中创建和管理的用户帐户的密码策略设置。

| 属性 | 要求 |
| --- | --- |
| 允许的字符 |<ul><li>A - Z</li><li>a - z</li><li>0 - 9</li> <li>@ # $ % ^ & * - \_ ! + = [ ] { } | \\ : ‘ , . ? / ` ~ “ ( ) ;</li></ul> |
| 不允许的字符 |<ul><li>Unicode 字符</li><li>空格</li><li>**仅限强密码**：不能紧靠在“@”符号前面添加点字符“.”</li></ul> |
| 密码限制 |<ul><li>至少 8 个字符，最多 16 个字符</li><li>**仅限强密码**：要求包含以下 4 种字符中的 3 种：<ul><li>小写字符</li><li>大写字符</li><li>数字 (0-9)</li><li>符号（请参阅上面的密码限制）</li></ul></li></ul> |
| 密码过期期限 |<ul><li>默认值：**90** 天</li><li>可通过 Windows PowerShell 的 Azure Active Directory 模块中的 Set-MsolPasswordPolicy cmdlet 来配置该值。</li></ul> |
| 密码过期通知 |<ul><li>默认值：**14** 天（密码过期前）</li><li>可使用 Set-MsolPasswordPolicy cmdlet 配置该值。</li></ul> |
| 密码过期 |<ul><li>默认值：**false** 天（指示已启用密码过期）</li><li>可以使用 Set-MsolUser cmdlet 为单个用户帐户配置该值。</li></ul> |
| 密码**更改**历史记录 |**更改**密码时，**不能**再次使用上次的密码。 |
| 密码**重置**历史记录 | **重置**遗忘的密码时，**可以**再次使用上次的密码。 |
| 帐户锁定 |10 次登录尝试失败（错误密码）之后，用户会被锁定一分钟。后续的错误登录尝试会增加用户被锁定的时间。 |

## 后续步骤
- **你是否因登录时遇到问题而浏览至此？** 如果是这样，[可按以下方式更改和重置你的密码](/documentation/articles/active-directory-passwords-update-your-own-password/#how-to-reset-your-password/)。
- [从任意位置管理密码](/documentation/articles/active-directory-passwords/)

<!---HONumber=Mooncake_0327_2017-->
<!---Update_Description: link update -->