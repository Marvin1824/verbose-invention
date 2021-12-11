---
title: Desenvolver em um codespace
intro: 'Você pode abrir um codespace em {% data variables.product.product_name %} e, em seguida, desenvolver usando os recursos do {% data variables.product.prodname_vscode %}.'
product: '{% data reusables.gated-features.codespaces %}'
permissions: 'You can develop in codespaces you''ve created for repositories owned by organizations using {% data variables.product.prodname_team %} and {% data variables.product.prodname_ghe_cloud %}.'
redirect_from:
  - /github/developing-online-with-github-codespaces/developing-in-a-codespace
  - /github/developing-online-with-codespaces/developing-in-a-codespace
versions:
  fpt: '*'
type: how_to
topics:
  - Codespaces
  - Fundamentals
  - Developer
---

 

## Sobre o desenvolvimento com {% data variables.product.prodname_codespaces %}

{% data variables.product.prodname_codespaces %} fornece a você a experiência completa de desenvolvimento de {% data variables.product.prodname_vscode %}. {% data reusables.codespaces.use-visual-studio-features %}

![Visão geral do codespace com anotações](/assets/images/help/codespaces/codespace-overview-annotated.png)

1. Barra lateral - Por padrão, esta área mostra os arquivos do seu projeto no Explorador.
2. Barra de Atividades - Exibe a visualização e fornece uma maneira de alternar entre elas. Você pode reordenar as Visualizações arrastando e soltando-as.
3. Editor - É aqui que você edita seus arquivos. Você pode usar a aba para cada editor para posicioná-lo exatamente onde você precisa.
4. Painéis - É aqui que você pode visualizar as informações de saída e depuração, bem como o local padrão para o Terminal integrado.
5. Barra de Status - Esta área fornece informações úteis sobre seu codespace e projeto. Por exemplo, o nome da agência, portas configuradas e muito mais.

Para obter mais informações sobre como usar {% data variables.product.prodname_vscode %}, consulte o [Guia da Interface do Usuário](https://code.visualstudio.com/docs/getstarted/userinterface) na documentação de {% data variables.product.prodname_vscode %}

{% data reusables.codespaces.connect-to-codespace-from-vscode %}

{% data reusables.codespaces.use-chrome %} For more information, see "[Troubleshooting Codespaces clients](/codespaces/troubleshooting/troubleshooting-codespaces-clients)."

### Personalizando seu codespace

{% data reusables.codespaces.about-personalization %} Para obter mais informações, consulte "[Personalizar {% data variables.product.prodname_codespaces %} para sua conta](/codespaces/setting-up-your-codespace/personalizing-codespaces-for-your-account)".

{% data reusables.codespaces.apply-devcontainer-changes %} Para obter mais informações, consulte "[Configurar o {% data variables.product.prodname_codespaces %} para o seu projeto](/github/developing-online-with-codespaces/configuring-codespaces-for-your-project#apply-changes-to-your-configuration)".

### Executando seu aplicativo a partir de um codespace
{% data reusables.codespaces.about-port-forwarding %} Para obter mais informações, consulte "[Encaminhar portas no seu codespace](/github/developing-online-with-codespaces/forwarding-ports-in-your-codespace)".

### Fazendo commit das suas alterações

{% data reusables.codespaces.committing-link-to-procedure %}

### Usando a Paleta de Comando

A Paleta de Comando permite acessar e gerenciar muitas funcionalidades para {% data variables.product.prodname_codespaces %} e {% data variables.product.prodname_vscode %}. Para obter mais informações, consulte "[Usando a Paleta de Comando em {% data variables.product.prodname_codespaces %}](/codespaces/codespaces-reference/using-the-command-palette-in-codespaces)".

## Acessar um codespace existente

1. {% data reusables.codespaces.you-can-see-all-your-codespaces %}
2. Clique no nome do codespace em que você deseja desenvolver. ![Nome do codespace](/assets/images/help/codespaces/click-name-codespace.png)

Alternatively, you can see any active codespaces for a repository by navigating to that repository and selecting **{% octicon "code" aria-label="The code icon" %} Code**. The drop-down menu will display all active codespaces for a repository.
