---
title: Configurar uma versão de avaliação do GitHub Enterprise Cloud
intro: 'Você pode avaliar o {% data variables.product.prodname_ghe_cloud %} gratuitamente.'
redirect_from:
  - /articles/setting-up-a-trial-of-github-enterprise-cloud
  - /github/getting-started-with-github/setting-up-a-trial-of-github-enterprise-cloud
  - /github/getting-started-with-github/signing-up-for-github/setting-up-a-trial-of-github-enterprise-cloud
versions:
  fpt: '*'
  ghes: '*'
topics:
  - Accounts
shortTitle: Desafio da nuvem corporativa
---

{% data reusables.enterprise.ghec-cta-button %}


## Sobre o {% data variables.product.prodname_ghe_cloud %}

{% data reusables.organizations.about-organizations %}

You can use organizations for free with {% data variables.product.prodname_free_team %}, which includes limited features. For additional features, such as SAML single sign-on (SSO), access control for {% data variables.product.prodname_pages %}, and included {% data variables.product.prodname_actions %} minutes, you can upgrade to {% data variables.product.prodname_ghe_cloud %}. For a detailed list of the features available with {% data variables.product.prodname_ghe_cloud %}, see our [Pricing](https://github.com/pricing) page.

{% data reusables.saml.saml-accounts %} Para obter mais informações, consulte "<a href="/organizations/managing-saml-single-sign-on-for-your-organization/about-identity-and-access-management-with-saml-single-sign-on" class="dotcom-only">Sobre identidade e gerenciamento de acesso com o logon único SAML</a>".

{% data reusables.products.which-product-to-use %}

## Sobre as versões de avaliação do {% data variables.product.prodname_ghe_cloud %}

You can set up a 14-day trial to evaluate {% data variables.product.prodname_ghe_cloud %}. Não há necessidade de fornecer um método de pagamento durante a avaliação, a menos que você adicione à sua organização aplicativos do {% data variables.product.prodname_marketplace %} que exijam um método de pagamento. Para obter mais informações, consulte "<a href="/articles/about-billing-for-github-marketplace/" class="dotcom-only">Sobre a cobrança do {% data variables.product.prodname_marketplace %}</a>".

Sua versão de avaliação inclui 50 estações. Se precisar de mais estações para avaliar o {% data variables.product.prodname_ghe_cloud %}, entre em contato com {% data variables.contact.contact_enterprise_sales %}. Ao final da avaliação, você poderá escolher um número diferente de estações.

As versões de avaliação também estão disponíveis para o {% data variables.product.prodname_ghe_server %}. Para obter mais informações, consulte "[Configurar uma versão de avaliação do {% data variables.product.prodname_ghe_server %}](/articles/setting-up-a-trial-of-github-enterprise-server)".

## Configurar a versão de avaliação do {% data variables.product.prodname_ghe_cloud %}

Before you can try {% data variables.product.prodname_ghe_cloud %}, you must be signed into a user account. If you don't already have a user account on {% data variables.product.prodname_dotcom_the_website %}, you must create one. Para obter mais informações, consulte "<a href="/articles/signing-up-for-a-new-github-account" class="dotcom-only">Inscrever-se em uma nova conta do {% data variables.product.prodname_dotcom %}</a>".

1. Navigate to [{% data variables.product.prodname_dotcom %} for enterprises](https://github.com/enterprise).
1. Click **Start a free trial**. !["Start a free trial" button](/assets/images/help/organizations/start-a-free-trial-button.png)
1. Click **Enterprise Cloud**. !["Enterprise Cloud" button](/assets/images/help/organizations/enterprise-cloud-trial-option.png)
1. Follow the prompts to configure your trial.

## Explorar o {% data variables.product.prodname_ghe_cloud %}

Depois de configurar sua versão de avaliação, você pode explorar o {% data variables.product.prodname_ghe_cloud %} seguindo o [Guia de Ativação Enterprise](https://resources.github.com/enterprise-onboarding/).

{% data reusables.products.product-roadmap %}

## Finalizar a versão de avaliação

Você pode comprar o {% data variables.product.prodname_enterprise %} ou fazer downgrade para o {% data variables.product.prodname_team %} em qualquer momento de sua avaliação.

Se você não comprar o {% data variables.product.prodname_enterprise %} ou o {% data variables.product.prodname_team %} antes de expirar sua versão de avaliação, sua organização será rebaixada para o {% data variables.product.prodname_free_team %} e perder acesso a ferramentas e recursos avançados incluídos apenas em produtos pagos, incluindo sites {% data variables.product.prodname_pages %} publicados a partir desses repositórios privados. Se você não planeja atualizar, para evitar a perda de acesso aos recursos avançados, transforme-os em repositórios públicos antes de sua versão de avaliação expirar. Para obter mais informações, consulte "[Configurar visibilidade do repositório](/articles/setting-repository-visibility)".

Fazer downgrade para o {% data variables.product.prodname_free_team %} para organizações também desabilita quaisquer configurações SAML feitas durante o período de avaliação. Ao adquirir o {% data variables.product.prodname_enterprise %} ou o {% data variables.product.prodname_team %}, suas configurações SAML serão habilitadas novamente para os usuários da organização se autenticarem.

{% data reusables.profile.access_org %}
{% data reusables.profile.org_settings %}
{% data reusables.organizations.billing_plans %}
5. Em "{% data variables.product.prodname_ghe_cloud %} Free Trial" (Versão de avaliação grátis do {% data variables.product.prodname_ghe_cloud %}) clique em **Buy Enterprise** (Comprar versão Enterprise) ou **Downgrade to Team** (Fazer downgrade para versão Team). ![Botões comprar versão Enterprise e fazer downgrade para versão Team](/assets/images/help/organizations/finish-trial-buttons.png)
6. Siga as instruções para inserir seu método de pagamento e clique em **Submit** (Enviar).
