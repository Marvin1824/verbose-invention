---
title: Sobre READMEs
intro: 'Você pode adicionar um arquivo README ao seu repositório para informar outras pessoas por que seu projeto é útil, o que elas podem fazer com o projeto e como elas podem usá-lo.'
redirect_from:
  - /articles/section-links-on-readmes-and-blob-pages/
  - /articles/relative-links-in-readmes/
  - /articles/about-readmes
  - /github/creating-cloning-and-archiving-repositories/about-readmes
  - /github/creating-cloning-and-archiving-repositories/creating-a-repository-on-github/about-readmes
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
topics:
  - Repositories
---

## Sobre READMEs

É possível adicionar um arquivo README a um repositório para comunicar informações importantes sobre o seu projeto. A README, along with a repository license{% ifversion fpt or ghes > 3.2 or ghae-issue-4651 %}, citation file{% endif %}{% ifversion fpt %}, contribution guidelines, and a code of conduct{% elsif ghes %} and contribution guidelines{% endif %}, communicates expectations for your project and helps you manage contributions.

Para obter mais informações sobre como fornecer diretrizes para o seu projeto, consulte {% ifversion fpt %}"[Adicionar um código de conduta ao seu projeto](/communities/setting-up-your-project-for-healthy-contributions/adding-a-code-of-conduct-to-your-project)e {% endif %}"[Configurar o seu projeto para contribuições saudáveis](/communities/setting-up-your-project-for-healthy-contributions)".

Um README, muitas vezes, é o primeiro item que um visitante verá ao visitar seu repositório. Os arquivos README geralmente incluem informações sobre:
- O que o projeto faz
- Por que o projeto é útil
- Como os usuários podem começar a usar o projeto
- Onde os usuários podem obter ajuda com seu projeto
- Quem mantém e contribui com o projeto

Se você colocar o arquivo README na raiz do repositório, `docs`, ou no diretório `.github` oculto, o {% data variables.product.product_name %} reconhecerá e apresentará automaticamente o README aos visitantes do repositório.

![Página principal do repositório github/scientist e seu arquivo README](/assets/images/help/repository/repo-with-readme.png)

{% ifversion fpt or ghes %}

{% data reusables.profile.profile-readme %}

{% endif %}

![Arquivo README no nome de usuário/repositório do nome de usuário](/assets/images/help/repository/username-repo-with-readme.png)

{% ifversion fpt or ghae-next or ghes > 3.1 %}

## Índice gerado automaticamente para arquivos README

Para a visualização interpretada de qualquer arquivo Markdown em um repositório, incluindo arquivos README {% data variables.product.product_name %} irá gerar automaticamente um índice com base nos títulos da seção. Você pode visualizar o índice para um arquivo LEIAME, clicando no ícone de menu {% octicon "list-unordered" aria-label="The unordered list icon" %} no canto superior esquerdo da página interpretada.

![README com TOC gerado automaticamente](/assets/images/help/repository/readme-automatic-toc.png)

O índice gerado automaticamente é habilitado por padrão para todos os arquivos Markdown em um repositório, mas você pode desabilitar esta funcionalidade para o repositório.

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.sidebar-settings %}
1. Em "Funcionalidades", desmarque **Índice**. ![Configuração automática de TOC para repositórios](/assets/images/help/repository/readme-automatic-toc-setting.png)

{% endif %}

## Links de seção nos arquivos README e páginas blob

{% data reusables.repositories.section-links %}

## Links relativos e caminhos de imagem em arquivos README

{% data reusables.repositories.relative-links %}

## Leia mais

- "[Adicionar um arquivo a um repositório](/articles/adding-a-file-to-a-repository)"
- "[Tornar READMEs legíveis](https://github.com/18F/open-source-guide/blob/18f-pages/pages/making-readmes-readable.md)" da 18F
