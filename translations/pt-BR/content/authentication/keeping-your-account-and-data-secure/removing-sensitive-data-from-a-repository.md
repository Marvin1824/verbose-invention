---
title: Remover dados confidenciais do repositório
intro: 'Se você fizer commit de dados confidenciais, como uma senha ou chave SSH em um repositório Git, poderá removê-los do histórico. To entirely remove unwanted files from a repository''s history you can use either the `git filter-repo` tool or the BFG Repo-Cleaner open source tool.'
redirect_from:
  - /remove-sensitive-data/
  - /removing-sensitive-data/
  - /articles/remove-sensitive-data/
  - /articles/removing-sensitive-data-from-a-repository
  - /github/authenticating-to-github/removing-sensitive-data-from-a-repository
  - /github/authenticating-to-github/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
topics:
  - Identity
  - Access management
shortTitle: Remover dados confidenciais
---

The `git filter-repo` tool and the BFG Repo-Cleaner rewrite your repository's history, which changes the SHAs for existing commits that you alter and any dependent commits. Os SHAs do commit alterados podem afetar as pull requests abertas no repositório. Recomendamos que você faça merge ou feche todas todas as pull requests abertas antes de remover os arquivos do repositório.

Você pode remover o arquivo com o commit mais recente com `git rm`. For information on removing a file that was added with the latest commit, see "[About large files on {% data variables.product.prodname_dotcom %}](/repositories/working-with-files/managing-large-files/about-large-files-on-github#removing-files-from-a-repositorys-history)."

{% warning %}

Este artigo explica como fazer commits com dados confidenciais que não podem ser acessados de nenhum branch ou tag no repositório do {% data variables.product.product_name %}. No entanto, é importante destacar que esses commits talvez ainda possam ser acessados em clones ou bifurcações do repositório diretamente por meio de hashes SHA-1 em visualizações em cache no {% data variables.product.product_name %} e por meio de qualquer pull request que faça referência a eles. You cannot remove sensitive data from other users' clones or forks of your repository, but you can permanently remove cached views and references to the sensitive data in pull requests on {% data variables.product.product_name %} by contacting {% data variables.contact.contact_support %}.

**Warning: Once you have pushed a commit to {% data variables.product.product_name %}, you should consider any sensitive data in the commit compromised.** If you committed a password, change it! Se tiver feito commit de uma chave, crie outra. Removing the compromised data doesn't resolve its initial exposure, especially in existing clones or forks of your repository. Consider these limitations in your decision to rewrite your repository's history.

{% endwarning %}

## Remover um arquivo do histórico do repositório

You can purge a file from your repository's history using either the `git filter-repo` tool or the BFG Repo-Cleaner open source tool.

### Usar o BFG

O [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/) é uma ferramenta desenvolvida e mantida pela comunidade de código aberto. Ele fornece uma alternativa mais rápida e simples ao `git filter-branch` para remover dados não desejados.

Por exemplo: para remover o arquivo com dados confidenciais sem alterar o commit mais recente, execute:

```shell
$ bfg --delete-files <em>YOUR-FILE-WITH-SENSITIVE-DATA</em>
```

Para substituir todo o texto relacionado no `passwords.txt` sempre que ele for encontrado no histórico do repositório, execute:

```shell
$ bfg --replace-text passwords.txt
```

Depois que os dados confidenciais são removidos, você deve fazer push forçado das suas alterações para {% data variables.product.product_name %}.

```shell
$ git push --force
```

Consulte as instruções completas de download e uso na documentação do [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/).

### Using git filter-repo

{% warning %}

**Warning:** If you run `git filter-repo` after stashing changes, you won't be able to retrieve your changes with other stash commands. Before running `git filter-repo`, we recommend unstashing any changes you've made. Para desfazer o stash do último conjunto de alterações no qual você fez stash, execute `git stash show -p | git apply -R`. For more information, see [Git Tools - Stashing and Cleaning](https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning).

{% endwarning %}

To illustrate how `git filter-repo` works, we'll show you how to remove your file with sensitive data from the history of your repository and add it to `.gitignore` to ensure that it is not accidentally re-committed.

1. Install the latest release of the [git filter-repo](https://github.com/newren/git-filter-repo) tool. You can install `git-filter-repo` manually or by using a package manager. For example, to install the tool with HomeBrew, use the `brew install` command.
  ```
  brew install git-filter-repo
  ```
  For more information, see [*INSTALL.md*](https://github.com/newren/git-filter-repo/blob/main/INSTALL.md) in the `newren/git-filter-repo` repository.

2. Se você ainda não tiver uma cópia local do repositório com dados confidenciais no histórico, [faça um clone do repositório](/articles/cloning-a-repository/) no computador local.
  ```shell
  $ git clone https://{% data variables.command_line.codeblock %}/<em>YOUR-USERNAME</em>/<em>YOUR-REPOSITORY</em>
  > Initialized empty Git repository in /Users/<em>YOUR-FILE-PATH</em>/<em>YOUR-REPOSITORY</em>/.git/
  > remote: Counting objects: 1301, done.
  > remote: Compressing objects: 100% (769/769), done.
  > remote: Total 1301 (delta 724), reused 910 (delta 522)
  > Receiving objects: 100% (1301/1301), 164.39 KiB, done.
  > Resolving deltas: 100% (724/724), done.
  ```
3. Acesse o diretório de trabalho do repositório.
  ```shell
  $ cd <em>YOUR-REPOSITORY</em>
  ```
4. Execute o seguinte comando substituindo `PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA` pelo **caminho do arquivo que deseja remover, não apenas o nome do arquivo**. Esses argumentos vão:
    - Forçar o Git a processar, mas não fazer checkout, do histórico completo de cada branch e tag
    - Remover o arquivo especificado, bem como qualquer commit vazio gerado como resultado
    - Remove some configurations, such as the remote URL, stored in the *.git/config* file. You may want to back up this file in advance for restoration later.
    - **Sobrescrever as tags existentes**
        ```shell
        $ git filter-repo --invert-paths --path PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA
        Parsed 197 commits
        New history written in 0.11 seconds; now repacking/cleaning...
        Repacking your repo and cleaning out old unneeded objects
        Enumerating objects: 210, done.
        Counting objects: 100% (210/210), done.
        Delta compression using up to 12 threads
        Compressing objects: 100% (127/127), done.
        Writing objects: 100% (210/210), done.
        Building bitmaps: 100% (48/48), done.
        Total 210 (delta 98), reused 144 (delta 75), pack-reused 0
        Completely finished after 0.64 seconds.
        ```

  {% note %}

  **Observação:** se o arquivo com dados confidenciais existir em qualquer outro caminho (porque foi movido ou renomeado), execute esse comando nesses caminhos também.

  {% endnote %}

5. Adicione o arquivo com dados confidenciais ao `.gitignore` para impedir a repetição acidental do commit.

  ```shell
  $ echo "<em>YOUR-FILE-WITH-SENSITIVE-DATA</em>" >> .gitignore
  $ git add .gitignore
  $ git commit -m "Add <em>YOUR-FILE-WITH-SENSITIVE-DATA</em> to .gitignore"
  > [main 051452f] Add <em>YOUR-FILE-WITH-SENSITIVE-DATA</em> to .gitignore
  >  1 files changed, 1 insertions(+), 0 deletions(-)
  ```
6. Verifique se você removeu todo o conteúdo desejado do histórico do repositório e fez checkout de todos os branches.
7. Quando estiver satisfeito com o estado do repositório, force o push das alterações locais para sobrescrever o repositório do {% data variables.product.product_name %} e todos os branches presentes no push:
  ```shell
  $ git push origin --force --all
  > Counting objects: 1074, done.
  > Delta compression using 2 threads.
  > Compressing objects: 100% (677/677), done.
  > Writing objects: 100% (1058/1058), 148.85 KiB, done.
  > Total 1058 (delta 590), reused 602 (delta 378)
  > To https://{% data variables.command_line.codeblock %}/<em>YOUR-USERNAME</em>/<em>YOUR-REPOSITORY</em>.git
  >  + 48dc599...051452f main -> main (forced update)
  ```
8. Para remover o arquivo com dados confidenciais das [versões com tag](/articles/about-releases), você também precisará forçar o push das tags do Git:
  ```shell
  $ git push origin --force --tags
  > Counting objects: 321, done.
  > Delta compression using up to 8 threads.
  > Compressing objects: 100% (166/166), done.
  > Writing objects: 100% (321/321), 331.74 KiB | 0 bytes/s, done.
  > Total 321 (delta 124), reused 269 (delta 108)
  > To https://{% data variables.command_line.codeblock %}/<em>YOUR-USERNAME</em>/<em>YOUR-REPOSITORY</em>.git
  >  + 48dc599...051452f main -> main (forced update)
  ```

## Fully removing the data from {% data variables.product.prodname_dotcom %}

After using either the BFG tool or `git filter-repo` to remove the sensitive data and pushing your changes to {% data variables.product.product_name %}, you must take a few more steps to fully remove the data from {% data variables.product.product_name %}.

1. Entre em contato com o {% data variables.contact.contact_support %} e solicite a remoção das visualizações em cache e das referências aos dados confidenciais em pull requests no {% data variables.product.product_name %}. Please provide the name of the repository and/or a link to the commit you need removed.

2. Peça para os colaboradores [fazerem rebase](https://git-scm.com/book/en/Git-Branching-Rebasing), *e não* merge, nos branches criados a partir do histórico antigo do repositório. Um commit de merge poderia reintroduzir o histórico antigo completo (ou parte dele) que você acabou de se dar ao trabalho de corrigir.

3. After some time has passed and you're confident that the BFG tool / `git filter-repo` had no unintended side effects, you can force all objects in your local repository to be dereferenced and garbage collected with the following commands (using Git 1.8.5 or newer):
  ```shell
  $ git for-each-ref --format="delete %(refname)" refs/original | git update-ref --stdin
  $ git reflog expire --expire=now --all
  $ git gc --prune=now
  > Counting objects: 2437, done.
  > Delta compression using up to 4 threads.
  > Compressing objects: 100% (1378/1378), done.
  > Writing objects: 100% (2437/2437), done.
  > Total 2437 (delta 1461), reused 1802 (delta 1048)
  ```
  {% note %}

   **Observação:** você também pode conseguir isso fazendo push do histórico filtrado em um repositório novo ou vazio e, em seguida, criando um clone usando o {% data variables.product.product_name %}.

  {% endnote %}

## Evitar commits acidentais no futuro

Há alguns truques simples para evitar fazer commit de coisas não desejadas:

- Use um programa visual, como o [{% data variables.product.prodname_desktop %}](https://desktop.github.com/) e o [gitk](https://git-scm.com/docs/gitk), para fazer commit das alterações. Nos programas visuais, geralmente é mais fácil ver exatamente quais arquivos serão adicionados, excluídos e modificados em cada commit.
- Evite os comandos catch-all `git add .` e `git commit -a` na linha de comando— use `git add filename` e `git rm filename` para fazer stage de arquivos individuais.
- Use o `git add --interactive` para revisar e fazer stage das alterações em cada arquivo de forma individual.
- Use o `git diff --cached` para revisar as alterações que você incluiu no stage para commit. Esse é o diff exato que o `git commit` produzirá, contanto que você não use o sinalizador `-a`.

## Leia mais

- [`git filter-repo` man page](https://htmlpreview.github.io/?https://github.com/newren/git-filter-repo/blob/docs/html/git-filter-repo.html)
- [Pro Git: Git Tools - Rewriting History](https://git-scm.com/book/en/Git-Tools-Rewriting-History){% ifversion fpt or ghae or ghes > 2.22 %}
- "[About Secret scanning](/code-security/secret-security/about-secret-scanning)"{% endif %}
