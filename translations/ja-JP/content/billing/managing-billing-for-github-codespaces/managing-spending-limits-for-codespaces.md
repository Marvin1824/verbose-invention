---
title: Managing spending limits for Codespaces
intro: '{% data variables.product.prodname_codespaces %} の使用に対して利用上限を設定できます。'
versions:
  fpt: '*'
type: how_to
product: '{% data reusables.gated-features.codespaces %}'
topics:
  - Codespaces
  - Enterprise
  - Organizations
  - Spending limits
  - User account
  - Billing
shortTitle: 利用上限
---

## {% data variables.product.prodname_codespaces %} の利用上限について

{% data reusables.codespaces.codespaces-spending-limit-requirement %}

Once you've reached your spending limit, your organization or repository will no longer be able to create new codespaces, and won't be able to start existing codespaces. Any existing codespaces that are still running will not be shutdown; if you don't change the spending limit, you will not be charged for the amount that exceeds the limit.

{% data variables.product.prodname_codespaces %}の価格に関する詳細な情報については、「[{% data variables.product.prodname_codespaces %}の支払いについて](/billing/managing-billing-for-github-codespaces/about-billing-for-codespaces)」を参照してください。

## Using your Azure Subscription
If you purchased {% data variables.product.prodname_enterprise %} through a Microsoft Enterprise Agreement, you can connect your Azure Subscription ID to your enterprise account to enable and pay for {% data variables.product.prodname_codespaces %} usage. 詳しい情報については、「[Azure サブスクリプションを Enterprise に接続する](/github/setting-up-and-managing-your-enterprise/connecting-an-azure-subscription-to-your-enterprise)」を参照してください。

## Organizationの {% data variables.product.prodname_codespaces %} に対する利用上限を管理する

Organization の {% data variables.product.prodname_codespaces %} については、Organizationのオーナーと支払いマネージャーが利用上限を管理できます。

{% data reusables.organizations.billing-settings %}
{% data reusables.dotcom_billing.manage-spending-limit %}
{% data reusables.dotcom_billing.monthly-spending-limit-codespaces %}
{% data reusables.dotcom_billing.update-spending-limit %}

## Enterprise アカウントの {% data variables.product.prodname_codespaces %} に対する利用上限を管理する

Enterprise アカウントの {% data variables.product.prodname_codespaces %} の利用上限は、Enterprise オーナーと支払いマネージャーが管理できます。

{% data reusables.enterprise-accounts.access-enterprise %}
{% data reusables.enterprise-accounts.settings-tab %}
{% data reusables.enterprise-accounts.billing-tab %}
1. Above "{% data variables.product.prodname_codespaces %} monthly usage", click **Spending Limit**. ![Spending limit tab](/assets/images/help/settings/spending-limit-tab-enterprise.png)
{% data reusables.dotcom_billing.monthly-spending-limit %}
{% data reusables.dotcom_billing.update-spending-limit %}

## Exporting changes when you have reached your spending limit

{% data reusables.codespaces.exporting-changes %}
## Managing usage and spending limit email notifications

Email notifications are sent to account owners and billing managers when spending reaches 50%, 75%, and 90% of your account's spending limit.

You can disable these notifications anytime by navigating to the bottom of the **Spending Limit** page.
