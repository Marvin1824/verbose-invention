---
title: Funcionalidades de segurança do GitHub
intro: 'Uma visão geral das funcionalidades de segurança de {% data variables.product.prodname_dotcom %}'
versions:
  fpt: '*'
  ghes: '>=3.0'
  ghae: '*'
type: overview
topics:
  - Repositories
  - Dependencies
  - Vulnerabilities
  - Advanced Security
---

## Sobre as funcionalidades de segurança de {% data variables.product.prodname_dotcom %}

{% data variables.product.prodname_dotcom %} tem funcionalidades de segurança que ajudam a manter códigos e segredos seguros nos repositórios e entre organizações. Algumas funcionalidades estão disponíveis para todos os repositórios e outras estão disponíveis apenas {% ifversion fpt %}para repositórios públicos e repositórios {% endif %}com uma licença de {% data variables.product.prodname_GH_advanced_security %}.

O {% data variables.product.prodname_advisory_database %} contém uma lista de vulnerabilidades de segurança que você pode visualizar, pesquisar e filtrar. {% data reusables.security-advisory.link-browsing-advisory-db %}

{% ifversion fpt or ghes > 2.22 %}
## Disponível para todos os repositórios

{% ifversion fpt or ghes > 3.0 or ghae-next %}
### Política de segurança

Facilite o acesso dos seus usuários para relatar confidencialmente vulnerabilidades de segurança que encontraram no seu repositório. Para obter mais informações, consulte "[Adicionar uma política de segurança ao seu repositório](/code-security/getting-started/adding-a-security-policy-to-your-repository)".
{% endif %}

{% ifversion fpt %}
### Consultorias de segurança

Discute em particular e corrige vulnerabilidades de segurança no código do seu repositório. Em seguida, você pode publicar uma consultoria de segurança para alertar a sua comunidade sobre a vulnerabilidade e incentivar os integrantes da comunidade a atualizá-la. Para obter mais informações, consulte "[Sobre {% data variables.product.prodname_security_advisories %}](/github/managing-security-vulnerabilities/about-github-security-advisories)".

### {% data variables.product.prodname_dependabot_alerts %} e atualizações de segurança

Ver alertas sobre dependências conhecidas por conter vulnerabilidades de segurança e escolher se deseja gerar pull requests para atualizar essas dependências automaticamente. Para obter mais informações, consulte "[Sobre alertas de dependências vulneráveis](/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies) e "[Sobre {% data variables.product.prodname_dependabot_security_updates %}](/github/managing-security-vulnerabilities/about-dependabot-security-updates)".
{% endif %}

{% ifversion ghes > 2.22 %}
### {% data variables.product.prodname_dependabot_alerts %}

Exibir alertas sobre dependências conhecidas por conter vulnerabilidades de segurança e gerenciar esses alertas. Para obter mais informações, consulte "[Sobre alertas para dependências vulneráveis](/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)"
{% endif %}

{% ifversion fpt %}
### atualizações de versão de {% data variables.product.prodname_dependabot %}

Use {% data variables.product.prodname_dependabot %} para levantar automaticamente os pull requests a fim de manter suas dependências atualizadas. Isso ajuda a reduzir a exposição a versões mais antigas de dependências. Usar versões mais recentes facilita a aplicação de patches, caso as vulnerabilidades de segurança sejam descobertas e também torna mais fácil para {% data variables.product.prodname_dependabot_security_updates %} levantar, com sucesso, os pull requests para atualizar as dependências vulneráveis. Para obter mais informações, consulte "[Sobre o {% data variables.product.prodname_dependabot_version_updates %}](/github/administering-a-repository/about-dependabot-version-updates)".
{% endif %}

### Gráfico de dependências
O gráfico de dependências permite explorar os ecossistemas e pacotes dos quais o repositório depende e os repositórios e pacotes que dependem do seu repositório.

Você pode encontrar o gráfico de dependências na aba **Ideias** para o seu repositório. Para obter mais informações, consulte "[Sobre o gráfico de dependência](/github/visualizing-repository-data-with-graphs/about-the-dependency-graph)".
{% endif %}

{% ifversion fpt or ghes > 2.22 or ghae %}

## Disponível {% ifversion fpt %}para repositórios públicos e para repositórios {% endif %}com {% data variables.product.prodname_advanced_security %}

{% ifversion fpt or ghes > 2.22 %}
Essas funcionalidades estão disponíveis {% ifversion fpt %}para todos os repositórios públicos e para repositórios privados pertencentes a organizações com {% else %}se você tiver {% endif %}uma licença de {% data variables.product.prodname_advanced_security %}. {% data reusables.advanced-security.more-info-ghas %}
{% endif %}

### Alertas de {% data variables.product.prodname_code_scanning_capc %}

Detectar automaticamente vulnerabilidades de segurança e erros de codificação em códigos novos ou modificados. São destacados os problemas potenciais, com informações detalhadas, o que permite que você corrija o código antes que seja mesclado no seu branch-padrão. Para obter mais informações, consulte "[Sobre a varredura de código](/github/finding-security-vulnerabilities-and-errors-in-your-code/about-code-scanning)".

### Alertas de {% data variables.product.prodname_secret_scanning_caps %}

{% ifversion fpt %}Para repositórios privados, veja {% else %}Visualizar {% endif %}qualquer segredo que {% data variables.product.prodname_dotcom %} encontrou no seu código. Você deve tratar os tokens ou credenciais verificados no repositório como comprometidos. Para obter mais informações, consulte "[Sobre a varredura de segredos](/github/administering-a-repository/about-secret-scanning)."

{% endif %}

{% ifversion fpt or ghes > 3.1 %}
### Revisão de dependência

Mostre o impacto completo das alterações nas dependências e veja detalhes de qualquer versão vulnerável antes de fazer merge de um pull request. Para obter mais informações, consulte "[Sobre a revisão de dependências](/code-security/supply-chain-security/about-dependency-review)".
{% endif %}

## Leia mais
- "[Produtos do {% data variables.product.prodname_dotcom %}](/github/getting-started-with-github/githubs-products)"
- "[Suporte à linguagem de {% data variables.product.prodname_dotcom %}](/github/getting-started-with-github/github-language-support)"
