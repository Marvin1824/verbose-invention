---
title: 其他身份验证方法
intro: 您可以在非生产环境中使用基本身份验证进行测试。
redirect_from:
  - /v3/auth
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
topics:
  - API
shortTitle: 其他身份验证方法
---


{% ifversion fpt or ghes %}
虽然 API 提供多种身份验证方法，但我们强烈建议对生产应用程序使用 [OAuth](/apps/building-integrations/setting-up-and-registering-oauth-apps/)。 提供的其他方法旨在用于脚本或测试（即没有必要使用完整 OAuth 方法的情况）。 依赖
{% data variables.product.product_name %} 进行身份验证的第三方应用程序不应要求或收集 {% data variables.product.product_name %} 凭据。
它们应该使用 [OAuth web 工作流程](/apps/building-oauth-apps/authorizing-oauth-apps/)。

{% endif %}

{% ifversion ghae %}

要验证身份，我们建议使用 [OAuth](/apps/building-integrations/setting-up-and-registering-oauth-apps/) 令牌，这种个人访问令牌通过 [OAuth web 流程](/apps/building-oauth-apps/authorizing-oauth-apps/)验证。

{% endif %}

## 基本身份验证

API 支持在 [RFC2617](http://www.ietf.org/rfc/rfc2617.txt) 中定义的基本身份验证，但有一些细微区别。 主要区别在于 RFC 要求使用 `401 Unauthorized` 响应来回复未经验证的请求。 在很多情况下这会暴露用户数据的存在。 对于此类请求，{% data variables.product.product_name %} API 的响应是 `404 Not Found`。 这可能导致 HTTP 库假定返回 `401 Unauthorized` 的问题。 解决方案是手动创建 `Authorization` 标头。

### 通过 OAuth 和个人访问令牌

我们建议您使用 OAuth 令牌向 GitHub API 验证。 OAuth 令牌包含[个人访问令牌][personal-access-tokens]，允许用户随时撤销访问权限。

```shell
$ curl -u <em>username</em>:<em>token</em> {% data variables.product.api_url_pre %}/user
```

如果您的工具只支持基本身份验证，但您想要利用 OAuth 访问令牌的安全功能，这个方法非常有用。

### 通过用户名和密码

{% ifversion fpt %}

{% note %}

**注意：**自 2020 年 11 月 13 日开始，对于所有 {% data variables.product.prodname_dotcom_the_website %} 帐户（包括 {% data variables.product.prodname_free_user %}、{% data variables.product.prodname_pro %}、{% data variables.product.prodname_team %} 或 {% data variables.product.prodname_ghe_cloud %} 计划上的帐户），{% data variables.product.prodname_dotcom %} 已停止对 API 的密码验证。 现在，您必须使用 API 令牌（如 OAuth 访问令牌、GitHub 应用程序安装访问令牌或个人访问令牌，具体取决于您需要使用令牌执行的操作）向 {% data variables.product.prodname_dotcom %} API 验证。 更多信息请参阅“[疑难排解](/rest/overview/troubleshooting#basic-authentication-errors)”。

{% endnote %}

{% endif %}

{% ifversion ghes %}
要将基本身份验证用于
{% data variables.product.product_name %} API，只需发送帐户相关的用户名和
密码。

例如，如果您通过 [cURL][curl] 访问 API，则将 `<username>` 替换为您的 {% data variables.product.product_name %} 用户名后，以下命令将对您进行身份验证。 （cURL 将提示您输入密码。）

```shell
$ curl -u <em>username</em> {% data variables.product.api_url_pre %}/user
```
如果您启用了双重身份验证，请务必了解如何[使用双重身份验证](/rest/overview/other-authentication-methods#working-with-two-factor-authentication)。

{% endif %}

{% ifversion fpt %}
### SAML SSO 身份验证

{% note %}

**注：**代表其他工具生成令牌的集成和 OAuth 应用程序将自动获得授权。

{% endnote %}

如果您要使用 API 访问实施 [SAML SSO][saml-sso] 身份验证的组织，您需要创建个人访问令牌 (PAT) 并[授权该令牌][allowlist]访问组织。 访问 `X-GitHub-SO` 中指定的 URL 以授权令牌访问组织。

```shell
$ curl -v -H "Authorization: token <em>TOKEN</em>" {% data variables.product.api_url_pre %}/repos/octodocs-test/test

> X-GitHub-SSO: required; url=https://github.com/orgs/octodocs-test/sso?authorization_request=AZSCKtL4U8yX1H3sCQIVnVgmjmon5fWxks5YrqhJgah0b2tlbl9pZM4EuMz4
{
  "message": "Resource protected by organization SAML enforcement. You must grant your personal token access to this organization.",
  "documentation_url": "https://docs.github.com"
}
```

在请求可能来自多个组织的数据时（例如，[请求由用户创建的议题列表][user-issues]），`X-GitHub-SSO` 标头将指示哪些组织需要您授权个人访问令牌：

```shell
$ curl -v -H "Authorization: token <em>TOKEN</em>" {% data variables.product.api_url_pre %}/user/issues

> X-GitHub-SSO: partial-results; organizations=21955855,20582480
```

`organizations` 的值是需要您授权个人访问令牌的组织列表，用逗号分隔。
{% endif %}

{% ifversion fpt or ghes %}
## 使用双重身份验证

启用双重身份验证后，REST API 中_大多数_端点的[基本身份验证](#basic-authentication)均要求您使用个人访问令牌{% ifversion ghes %} 或 OAuth 令牌，而不是用户名和密码{% endif %}。

您可以使用 [{% data variables.product.product_name %}开发者设置{% endif %}{% ifversion ghes %}来生成新的个人访问令牌，{% ifversion fpt %}或者使用 OAuth 授权 API 中的“\[创建新授权\]\[/rest/reference/oauth-authorizations#create-a-new-authorization\]”](https://github.com/settings/tokens/new)端点来生成新的 OAuth 令牌{% endif %}。 更多信息请参阅“[创建用于命令行的个人访问令牌](/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line)”。 然后，您将使用这些令牌以通过 {% data variables.product.prodname_dotcom %} API [使用 OAuth 令牌进行身份验证][oauth-auth]。{% ifversion ghes %} 仅当您创建 OAuth 令牌或使用 OAuth 授权 API 时才需要通过用户名和密码进行身份验证。{% endif %}

{% endif %}

{% ifversion ghes %}
### 结合使用 OAuth 授权 API 与双重身份验证

当您调用 OAuth 授权 API 时，基本身份验证会要求您使用一次性密码 (OTP) 以及您的用户名和密码，而不是令牌。 当您尝试使用 OAuth 授权 API 进行身份验证时，服务器将响应 `401 Unauthorized` 和以下标头之一，以指示需要使用双重身份验证代码：

`X-GitHub-OTP: required; SMS` 或 `X-GitHub-OTP: required; app`.

此标头指示您的帐户如何接收其双重身份验证代码。 您将通过 SMS 接收 OTP 代码，或者使用 Google Authenticator 或 1Password 等应用程序，具体取决于您的帐户设置。 更多信息请参阅“[配置双重身份验证](/articles/configuring-two-factor-authentication)”。 在标头中传递 OTP：

```shell
$ curl --request POST \
  --url https://api.github.com/authorizations \
  --header 'authorization: Basic <em>PASSWORD</em>' \
  --header 'content-type: application/json' \
  --header 'x-github-otp: <em>OTP</em>' \
  --data '{"scopes": ["public_repo"], "note": "test"}'
```
{% endif %}

[curl]: http://curl.haxx.se/
[oauth-auth]: /rest#authentication
[personal-access-tokens]: /articles/creating-a-personal-access-token-for-the-command-line
[saml-sso]: /articles/about-identity-and-access-management-with-saml-single-sign-on
[allowlist]: /github/authenticating-to-github/authorizing-a-personal-access-token-for-use-with-saml-single-sign-on
[user-issues]: /rest/reference/issues#list-issues-assigned-to-the-authenticated-user
