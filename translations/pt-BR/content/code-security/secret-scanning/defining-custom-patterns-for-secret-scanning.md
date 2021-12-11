---
title: Definindo padrões personalizados para varredura de segredo
shortTitle: Defina padrões personalizados
intro: 'Você pode definir padrões personalizados para {% data variables.product.prodname_secret_scanning %} em organizações e repositórios privados.'
product: '{% data reusables.gated-features.secret-scanning %}'
redirect_from:
  - /code-security/secret-security/defining-custom-patterns-for-secret-scanning
versions:
  fpt: '*'
  ghes: '>=3.2'
  ghae: next
topics:
  - Repositories
---

{% ifversion ghes < 3.3 or ghae %}
{% note %}

**Observação:** Os padrões personalizados para {% data variables.product.prodname_secret_scanning %} estão atualmente em fase beta e sujeitos a alterações.

{% endnote %}
{% endif %}

## Sobre padrões personalizados para {% data variables.product.prodname_secret_scanning %}

{% data variables.product.company_short %} executa {% data variables.product.prodname_secret_scanning %} nos repositórios {% ifversion fpt %}públicos e privados{% endif %} para padrões de segredo fornecidos por parceiros de {% data variables.product.company_short %} e {% data variables.product.company_short %}. Para obter mais informações sobre o programa de parceria de {% data variables.product.prodname_secret_scanning %}, consulte "<a href="/developers/overview/secret-scanning-partner-program" class="dotcom-only">Programa de varredura de segredo de parceiros</a>".

No entanto, pode haver situações em que você deverá pesquisar outros padrões secretos nos seus repositórios {% ifversion fpt %}privados{% endif %}. Por exemplo, você pode ter um padrão de segredo que é interno da sua organização. Para esses casos, você pode definir padrões personalizados de {% data variables.product.prodname_secret_scanning %} na sua empresa, organização ou {% ifversion fpt %}repositório{% endif %} privado em {% data variables.product.product_name %}. É possível definir até 100 padrões personalizados para cada conta da organização ou empresa e até 20 padrões personalizados por repositório {% ifversion fpt %}privado{% endif %}.

{% ifversion ghes < 3.3 or ghae %}
{% note %}

**Observação:** No beta, existem algumas limitações ao usar padrões personalizados para {% data variables.product.prodname_secret_scanning %}:

* Não há nenhuma funcionalidade de exercício de simulação.
* Você não pode editar padrões personalizados depois que forem criados. Para alterar um padrão, você deve excluí-lo e recriá-lo.
* Não há API para criar, editar ou excluir padrões personalizados. No entanto, os resultados de padrões personalizados são retornados na [API de alertas de segredos](/rest/reference/secret-scanning).

{% endnote %}
{% endif %}

## Sintaxe de expressão regular para padrões personalizados

Os padrões personalizados para {% data variables.product.prodname_secret_scanning %} são especificados como expressões regulares. {% data variables.product.prodname_secret_scanning_caps %} usa a [biblioteca Hyperscan](https://github.com/intel/hyperscan) e é compatível apenas os construtores regex do Hyperscan, que são um subconjunto da sintaxe PCRE. Os modificadores de opções de huperscan não são compatíveis.  Para obter mais informações sobre construções de padrões do Hyperscan, consulte "[suporte do padrão](http://intel.github.io/hyperscan/dev-reference/compilation.html#pattern-support)na documentação do Hyperscan.

## Definindo um padrão personalizado para um repositório

Antes de definir um padrão personalizado, você deve garantir que {% data variables.product.prodname_secret_scanning %} está habilitado no seu repositório. Para obter mais informações, consulte "[Configurar {% data variables.product.prodname_secret_scanning %} para os seus repositórios](/code-security/secret-security/configuring-secret-scanning-for-your-repositories)".

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.sidebar-settings %}
{% data reusables.repositories.navigate-to-security-and-analysis %}
{% data reusables.repositories.navigate-to-ghas-settings %}
{% data reusables.advanced-security.secret-scanning-new-custom-pattern %}
{% data reusables.advanced-security.secret-scanning-add-custom-pattern-details %}

Após a criação do seu padrão, {% data reusables.secret-scanning.secret-scanning-process %} Para mais informações sobre visualização de alertas {% data variables.product.prodname_secret_scanning %}, consulte "[Gerenciando alertas de {% data variables.product.prodname_secret_scanning %}](/code-security/secret-security/managing-alerts-from-secret-scanning)".

## Definindo um padrão personalizado para uma organização

Antes de definir um padrão personalizado, você deverá habilitar {% data variables.product.prodname_secret_scanning %} para os repositórios {% ifversion fpt %}privaivados{% endif %} que você deseja fazer a varredura na organização. Para habilitar {% data variables.product.prodname_secret_scanning %} em todos os repositórios {% ifversion fpt %}privados {% endif %} na sua organização, consulte "[Gerenciar as configurações de segurança e análise da sua organização](/organizations/keeping-your-organization-secure/managing-security-and-analysis-settings-for-your-organization)".

{% note %}

**Observação:** Como não há nenhuma funcionalidade de teste, recomendamos que você teste seus padrões personalizados em um repositório antes de defini-los para toda a organização. Dessa forma, você pode evitar criar alertas falsos-positivos de {% data variables.product.prodname_secret_scanning %}.

{% endnote %}

{% data reusables.profile.access_org %}
{% data reusables.profile.org_settings %}
{% data reusables.organizations.security-and-analysis %}
{% data reusables.repositories.navigate-to-ghas-settings %}
{% data reusables.advanced-security.secret-scanning-new-custom-pattern %}
{% data reusables.advanced-security.secret-scanning-add-custom-pattern-details %}

Depois que o padrão for criado, {% data variables.product.prodname_secret_scanning %} irá verificar todos os segredos nos repositórios {% ifversion fpt %}privados {% endif %} na sua organização, incluindo todo seu histórico do Git em todos os branches. Os proprietários da organização e administradores do repositório receberão um alerta sobre todos os segredos encontrados e poderão revisar o alerta no repositório onde o segredo for encontrado. Para obter mais informações sobre a visualização de alertas de {% data variables.product.prodname_secret_scanning %}, consulte "[Gerenciar alertas de {% data variables.product.prodname_secret_scanning %}](/code-security/secret-security/managing-alerts-from-secret-scanning)".

## Definir um padrão personalizado para uma conta corporativa

Antes de definir um padrão personalizado, você deverá garantir que você habilite a digitalização de segredo para a sua conta corporativa. Para obter mais informações, consulte "[Habilitar {% data variables.product.prodname_GH_advanced_security %} para a sua empresa](/admin/advanced-security/enabling-github-advanced-security-for-your-enterprise)."

{% note %}

**Observação:** Como não há nenhuma funcionalidade de teste, recomendamos que você teste seus padrões personalizados em um repositório antes de defini-los para toda sua empresa. Dessa forma, você pode evitar criar alertas falsos-positivos de {% data variables.product.prodname_secret_scanning %}.

{% endnote %}

{% data reusables.enterprise-accounts.access-enterprise %}
{% data reusables.enterprise-accounts.policies-tab %}
{% data reusables.enterprise-accounts.advanced-security-policies %}
{% data reusables.enterprise-accounts.advanced-security-security-features %}
1. Em "Padrões personalizados de digitalização de segredos", clique em {% ifversion fpt or ghes > 3.2 or ghae-next %}**Novo padrão**{% elsif ghes = 3.2 %}**Novo padrão personalizado**{% endif %}.
{% data reusables.advanced-security.secret-scanning-add-custom-pattern-details %}

Depois que seu padrão for criado, {% data variables.product.prodname_secret_scanning %} irá verificar se há segredos em repositórios {% ifversion fpt %}privados{% endif %} dentro das organizações da sua empresa com {% data variables.product.prodname_GH_advanced_security %} habilitado, incluindo toda a sua história de Git em todos os branches. Os proprietários da organização e administradores do repositório receberão um alerta sobre todos os segredos encontrados e poderão revisar o alerta no repositório onde o segredo for encontrado. Para obter mais informações sobre a visualização de alertas de {% data variables.product.prodname_secret_scanning %}, consulte "[Gerenciar alertas de {% data variables.product.prodname_secret_scanning %}](/code-security/secret-security/managing-alerts-from-secret-scanning)".

{% ifversion fpt or ghes > 3.2 %}
## Editando um padrão personalizado

Ao salvar uma alteração em um padrão personalizado, isso irá fechar todos os alertas de {% data variables.product.prodname_secret_scanning %} que foram criados usando a versão anterior do padrão.
1. Acesse o local onde o padrão personalizado foi criado. Um padrão personalizado pode ser criado na conta de um repositório, organização ou empresa.
   * Para um repositório ou organização, exiba as configurações "Segurança & análise" do repositório ou organização onde o padrão personalizado foi criado. Para mais informações consulte "[Definir um padrão personalizado para um repositório](#defining-a-custom-pattern-for-a-repository)" ou "[Definir um padrão personalizado para uma organização](#defining-a-custom-pattern-for-an-organization)" acima.
   * Para uma empresa, em "Políticas" exiba a área "Segurança Avançada" e, em seguida, clique em **Funcionalidades de segurança**. Para obter mais informações, consulte "[Definindo um padrão personalizado para uma conta corporativa](#defining-a-custom-pattern-for-an-enterprise-account)" acima.
2. Em "{% data variables.product.prodname_secret_scanning_caps %}", à direita do padrão personalizado que você deseja editar, clique em {% octicon "pencil" aria-label="The edit icon" %}.
3. Ao revisar e testar suas alterações, clique em **Salvar alterações**.
{% endif %}

## Removendo um padrão personalizado

1. Acesse o local onde o padrão personalizado foi criado. Um padrão personalizado pode ser criado na conta de um repositório, organização ou empresa.

   * Para um repositório ou organização, exiba as configurações "Segurança & análise" do repositório ou organização onde o padrão personalizado foi criado. Para mais informações consulte "[Definir um padrão personalizado para um repositório](#defining-a-custom-pattern-for-a-repository)" ou "[Definir um padrão personalizado para uma organização](#defining-a-custom-pattern-for-an-organization)" acima.
   * Para uma empresa, em "Políticas" exiba a área "Segurança Avançada" e, em seguida, clique em **Funcionalidades de segurança**.  Para obter mais informações, consulte "[Definindo um padrão personalizado para uma conta corporativa](#defining-a-custom-pattern-for-an-enterprise-account)" acima.
{%- ifversion fpt or ghes > 3.2 or ghae-next %}
1. À direita do padrão personalizado que você deseja remover, clique em {% octicon "trash" aria-label="The trash icon" %}.
1. Revise a confirmação e selecione um método para lidar com todos os alertas abertos relacionados ao padrão personalizado.
1. Clique em **Sim, excluir este padrão**.

   ![Confirmando a exclusão de um padrão {% data variables.product.prodname_secret_scanning %} personalizado ](/assets/images/help/repository/secret-scanning-confirm-deletion-custom-pattern.png)
{%- elsif ghes = 3.2 %}
1. À direita do padrão personalizado que você deseja remover, clique em **Remover**.
1. Revise a confirmação e clique em **Remover padrão personalizado**.
{%- endif %}
