---
title: 配置有漏洞依赖项的通知
shortTitle: 配置通知
intro: '优化接收 {% data variables.product.prodname_dependabot %} 相关警报的通知的方式。'
redirect_from:
  - /github/managing-security-vulnerabilities/configuring-notifications-for-vulnerable-dependencies
  - /code-security/supply-chain-security/configuring-notifications-for-vulnerable-dependencies
versions:
  fpt: '*'
  ghes: '>=3.0'
type: how_to
topics:
  - Dependabot
  - Alerts
  - Notifications
  - Vulnerabilities
  - Dependencies
  - Repositories
---

<!--For this article in earlier GHES versions, see /content/github/managing-security-vulnerabilities-->

## 关于有漏洞依赖项的通知

当 {% data variables.product.prodname_dependabot %} 在您的仓库中检测到有漏洞依赖项时，我们将生成 {% data variables.product.prodname_dependabot %} 警报，并将其显示在仓库的“Security（安全）”选项卡中。 {% data variables.product.product_name %} 根据通知首选项将新警报通知受影响仓库的维护员。{% ifversion fpt %} {% data variables.product.prodname_dependabot %} 在所有公共仓库上默认启用。 对于 {% data variables.product.prodname_dependabot_alerts %}，默认情况下，您将通过电子邮件收到按特定漏洞分组的 {% data variables.product.prodname_dependabot_alerts %}。
{% endif %}

{% ifversion fpt %}如果您是组织所有者，您可以对组织中的所有仓库一键启用或禁用 {% data variables.product.prodname_dependabot_alerts %}。 您也可以设置是否对新建的仓库启用或禁用有漏洞依赖项检测。 更多信息请参阅“[管理组织的安全和分析设置](/organizations/keeping-your-organization-secure/managing-security-and-analysis-settings-for-your-organization#enabling-or-disabling-a-feature-for-all-new-repositories-when-they-are-added)”。
{% endif %}

{% ifversion ghes %}
默认情况下，如果站点管理员为您企业上的通知配置了电子邮件，您将通过电子邮件收到 {% data variables.product.prodname_dependabot_alerts %}。{% endif %}

{% ifversion ghes %}站点管理员还可以启用无通知 {% data variables.product.prodname_dependabot_alerts %}。 更多信息请参阅“[为 {% data variables.product.prodname_ghe_server %} 上的有漏洞依赖项启用 {% data variables.product.prodname_dependabot_alerts %}](/admin/configuration/enabling-alerts-for-vulnerable-dependencies-on-github-enterprise-server#enabling-dependabot-alerts)”。{% endif %}

## 配置 {% data variables.product.prodname_dependabot_alerts %} 的通知

{% ifversion fpt or ghes > 3.1 %}
When a new {% data variables.product.prodname_dependabot %} alert is detected, {% data variables.product.product_name %} notifies all users with access to {% data variables.product.prodname_dependabot_alerts %} for the repository according to their notification preferences. You will receive alerts if you are watching the repository, have enabled notifications for security alerts or for all the activity on the repository, and are not ignoring the repository. 更多信息请参阅“[配置通知](/github/managing-subscriptions-and-notifications-on-github/configuring-notifications#configuring-your-watch-settings-for-an-individual-repository)”。
{% endif %}

您可以从每个页面顶部显示的管理通知下拉菜单 {% octicon "bell" aria-label="The notifications bell" %} 为您自己或您的组织配置通知设置。 更多信息请参阅“[配置通知](/github/managing-subscriptions-and-notifications-on-github/configuring-notifications#choosing-your-notification-settings)”。

{% data reusables.notifications.vulnerable-dependency-notification-delivery-method-customization2 %}
{% data reusables.notifications.vulnerable-dependency-notification-options %}

  ![{% data variables.product.prodname_dependabot_alerts %} 选项](/assets/images/help/notifications-v2/dependabot-alerts-options.png)

{% note %}

**注：** 您可以过滤 {% data variables.product.company_short %} 上的通知以显示{% data variables.product.prodname_dependabot %} 警报。 更多信息请参阅“[从收件箱管理通知](/github/managing-subscriptions-and-notifications-on-github/managing-notifications-from-your-inbox#dependabot-custom-filters)”。

{% endnote %}

{% data reusables.repositories.security-alerts-x-github-severity %} 更多信息请参阅“[配置通知](/github/managing-subscriptions-and-notifications-on-github/configuring-notifications#filtering-email-notifications)”。

## 如何减少有漏洞依赖项通知的干扰

如果您想要收到太多 {% data variables.product.prodname_dependabot_alerts %} 的通知，我们建议您选择加入每周的电子邮件摘要，或者在保持 {% data variables.product.prodname_dependabot_alerts %} 启用时关闭通知。 您仍可导航到仓库的 Security（安全性）选项卡查看 {% data variables.product.prodname_dependabot_alerts %}。 更多信息请参阅“[查看和更新仓库中的漏洞依赖项](/github/managing-security-vulnerabilities/viewing-and-updating-vulnerable-dependencies-in-your-repository)”。

## 延伸阅读

- "[配置通知](/github/managing-subscriptions-and-notifications-on-github/configuring-notifications)"
- “[从收件箱管理通知](/github/managing-subscriptions-and-notifications-on-github/managing-notifications-from-your-inbox#supported-is-queries)”。
