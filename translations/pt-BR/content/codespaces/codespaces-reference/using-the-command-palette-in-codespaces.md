---
title: Usando a paleta de comando em codespaces
intro: 'Você pode usar o recurso de Paleta de Comando de {% data variables.product.prodname_vscode %} para acessar muitos comandos em codespaces.'
versions:
  fpt: '*'
type: reference
topics:
  - Codespaces
  - Visual Studio Code
product: '{% data reusables.gated-features.codespaces %}'
shortTitle: Paleta de comandos
---

## Sobre a Paleta de Comando

A Paleta de Comando é uma das funcionalidades principais de {% data variables.product.prodname_vscode %} e está disponível para uso em codespaces. A Paleta de Comando permite que você acesse muitos comandos para {% data variables.product.prodname_codespaces %} e {% data variables.product.prodname_vscode %}. Para obter mais informações sobre o uso da Paleta de Comando, consulte "[Interface do Usuário](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette)" na documentação do Visual Studio Code.

## Acessando a Paleta de Comando

Você pode acessar a Paleta de Comando de várias maneiras.

- `Shift + Command + P` (Mac) / `Ctrl + Shift + P` (Windows).

  Observe que este comando é um atalho de teclado reservado no Firefox.
- `F1`
- No Menu de Aplicativos, clique em **Ver > Paleta de Comando…**.

  ![Menu do aplicativo](/assets/images/help/codespaces/codespaces-view-menu.png)

## Comandos para {% data variables.product.prodname_github_codespaces %}

Para ver todos os comandos relacionados a {% data variables.product.prodname_github_codespaces %}, acesse a Paleta de Comando e, em seguida, comece a digitar "Códigos".

![Uma lista de todos os comandos que se referem a codespaces](/assets/images/help/codespaces/codespaces-command-palette.png)

### Suspender ou interromper um codespace

If you add a new secret or change the machine type, you'll have to stop and restart the codespace for it to apply your changes.

Para suspender ou parar o contêiner do seu codespace, acesse a Paleta de Comando e, em seguida, comece a digitar "parar". Selecione **Codespaces: Parar o codespace atual**.

![Comando para parar um codespace](/assets/images/help/codespaces/codespaces-stop.png)

### Adicionando um contêiner de desenvolvimento a partir de um modelo

Para adicionar um contêiner de desenvolvimento a partir de um modelo, acesse a Paleta de Comando e, em seguida, comece a digitar "dev container". Selecione **Codespaces: Adicionar arquivos de configuração de Contêiner do Desenvolvimento...**

![Comando para adicionar um contêiner de desenvolvimento](/assets/images/help/codespaces/add-prebuilt-container-command.png)

### Reconstruindo um codespace

Se você adicionar um contêiner de desenvolvimento ou editar qualquer um dos arquivos de configuração (`devcontainer.json` e `arquivo Docker`), você terá que reconstruir seu codespace para aplicar suas alterações.

Para reconstruir seu contêiner, acesse a Paleta de Comando e comece a digitar "reconstruir". Selecione **Codespaces: Reconstruir Contêiner**.

![Comando para reconstruir um codespace](/assets/images/help/codespaces/codespaces-rebuild.png)

### Registros de codespaces

Você pode usar a Paleta de Comando para acessar os registros de criação dos codespaces ou você pode usá-lo para exportar todos os registros.

Para recuperar os logs para os codespaces, acesse a Paleta de Comando e, em seguida, comece a digitar "registro". Selecione **Codespaces: Exportar registros** para exportar todos os registros relacionados aos codespaces ou selecione **Codespaces: Visualizar o registro de criação** para visualizar os registros relacionados à configuração.

![Comando para acessar os registros](/assets/images/help/codespaces/codespaces-logs.png)
