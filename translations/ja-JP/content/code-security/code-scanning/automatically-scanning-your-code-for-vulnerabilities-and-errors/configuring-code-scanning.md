---
title: コードスキャンを設定する
intro: '{% data variables.product.prodname_dotcom %} がプロジェクトのコードをスキャンして脆弱性やエラーを検出する方法を設定できます。'
product: '{% data reusables.gated-features.code-scanning %}'
permissions: 'People with write permissions to a repository can configure {% data variables.product.prodname_code_scanning %} for the repository.'
miniTocMaxHeadingLevel: 3
redirect_from:
  - /github/finding-security-vulnerabilities-and-errors-in-your-code/configuring-code-scanning
  - /code-security/secure-coding/configuring-code-scanning
  - /code-security/secure-coding/automatically-scanning-your-code-for-vulnerabilities-and-errors/configuring-code-scanning
versions:
  fpt: '*'
  ghes: '>=3.0'
  ghae: '*'
type: how_to
topics:
  - Advanced Security
  - Code scanning
  - Actions
  - Repositories
  - Pull requests
  - JavaScript
  - Python
shortTitle: Code scanningの設定
---

<!--For this article in earlier GHES versions, see /content/github/finding-security-vulnerabilities-and-errors-in-your-code-->

{% data reusables.code-scanning.beta %}
{% data reusables.code-scanning.enterprise-enable-code-scanning-actions %}

## {% data variables.product.prodname_code_scanning %} の設定について

{% data variables.product.prodname_actions %}を使って、あるいは継続的インテグレーション（CI）システムから、{% data variables.product.product_name %}上で{% data variables.product.prodname_code_scanning %}を実行できます。 詳しい情報については「[{% data variables.product.prodname_actions %}について](/actions/getting-started-with-github-actions/about-github-actions)」あるいは
{%- ifversion fpt or ghes > 3.0 or ghae-next %}
「[CIシステムでの{% data variables.product.prodname_codeql %} {% data variables.product.prodname_code_scanning %}について](/code-security/secure-coding/about-codeql-code-scanning-in-your-ci-system)」を参照してください。
{%- else %}
「[CIシステムでの{% data variables.product.prodname_codeql_runner %}の実行](/code-security/secure-coding/running-codeql-runner-in-your-ci-system)」を参照してください。
{% endif %}

この記事は、Actionsを使って{% data variables.product.product_name %} 上で {% data variables.product.prodname_code_scanning %} を実行することについて説明しています。

リポジトリに {% data variables.product.prodname_code_scanning %} を設定する前に、リポジトリに {% data variables.product.prodname_actions %} ワークフローを追加して {% data variables.product.prodname_code_scanning %} をセットアップする必要があります。 詳しい情報については、「[リポジトリに対する {% data variables.product.prodname_code_scanning %} をセットアップする](/code-security/secure-coding/setting-up-code-scanning-for-a-repository)」を参照してください。

{% data reusables.code-scanning.edit-workflow %}

{% data variables.product.prodname_codeql %} 解析は、{% data variables.product.prodname_dotcom %} で実行できる {% data variables.product.prodname_code_scanning %} のほんの一例に過ぎません。 {% ifversion ghes %}{% data variables.product.prodname_dotcom_the_website %}上の{% endif %}{% data variables.product.prodname_marketplace %}は、使用可能な他の{% data variables.product.prodname_code_scanning %}ワークフローを含みます。 {% ifversion fpt %}**{% octicon "shield" aria-label="The shield symbol" %} セキュリティ**タブからアクセスできる"Get started with {% data variables.product.prodname_code_scanning %}"ページ上には、それらの選択肢があります。{% endif %}この記事で示されている例は、{% data variables.product.prodname_codeql_workflow %}ファイルに関連しています。

## Editing a code scanning workflow

{% data variables.product.prodname_dotcom %} は、リポジトリの _.github/workflows_ ディレクトリにワークフローファイルを保存します。 ファイル名を検索して、追加済みのワークフローを見つけることができます。 For example, the default workflow file for CodeQL code scanning is called `codeql-analysis.yml`.

1. リポジトリで、編集したいワークフローファイルにアクセスします。
1. ファイルビューの右上隅の {% octicon "pencil" aria-label="The edit icon" %}をクリックしてワークフローエディタを開きます。 ![ワークフローファイルの編集ボタン](/assets/images/help/repository/code-scanning-edit-workflow-button.png)
1. ファイルを編集したら、[**Start commit**] をクリックして、[Commit changes] フォームに入力します。 現在のブランチに直接コミットするか、新しいブランチを作成してプルリクエストを開始するかを選択できます。 ![codeql.yml ワークフローの更新をコミットする](/assets/images/help/repository/code-scanning-workflow-update.png)

ワークフローファイルの編集に関する詳しい情報については、「[{% data variables.product.prodname_actions %} を学ぶ](/actions/learn-github-actions)」を参照してください。

## 頻度を設定する

スケジュール設定されているときや、リポジトリで特定のイベントが発生したときに、コードをスキャンできます。

リポジトリへのプッシュごと、およびプルリクエストが作成されるたびにコードをスキャンすることで、開発者がコードに新しい脆弱性やエラーをもたらすことを防ぎます。 スケジュールに従ってコードをスキャンすると、開発者がリポジトリを積極的に維持していない場合でも、{% data variables.product.company_short %}、セキュリティ研究者、コミュニティが発見した最新の脆弱性とエラーが通知されます。

### プッシュ時にスキャンする

デフォルトのワークフローを使用する場合、{% data variables.product.prodname_code_scanning %} は、イベントによってトリガーされるスキャンに加えて、リポジトリ内のコードを週に1回スキャンします。 このスケジュールを調整するには、ワークフローで `cron` 値を編集します。 詳細については、「[{% data variables.product.prodname_actions %}のワークフロー構文](/actions/reference/workflow-syntax-for-github-actions#on)」を参照してください。

プッシュ時にスキャンするなら、結果はリポジトリの** Security（セキュリティ）**タブに表示されます。 詳しい情報については、「[リポジトリの コードスキャンアラートを管理する](/code-security/secure-coding/managing-code-scanning-alerts-for-your-repository#viewing-the-alerts-for-a-repository)」を参照してください。

{% note %}

**ノート**: {% data variables.product.prodname_code_scanning %}アラートをPull Requestのチェックとして表示させたいなら、以下に述べる`pull_request`イベントを使わなければなりません。

{% endnote %}

### プルリクエストをスキャンする

デフォルトの {% data variables.product.prodname_codeql_workflow %} は、`pull_request` イベントを使用して、デフォルトブランチに対するプルリクエストのコードスキャンをトリガーします。 {% ifversion ghes %}`pull_request`イベントは、Pull Requestがプライベートフォークからオープンされたときにはトリガーされません。{% else %}Pull Requestがプライベートフォークからのものであれば、リポジトリの設定で"Run workflows from fork pull requests（フォークのPull Requestからワークフローを実行）"オプションを選択している場合にのみ`pull_request`イベントはトリガーされます。 For more information, see "[Managing {% data variables.product.prodname_actions %} settings for a repository](/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#enabling-workflows-for-private-repository-forks)."{% endif %}

`pull_request` イベントに関する詳しい情報については、「"[{% data variables.product.prodname_actions %}のためのワークフローの構文](/actions/reference/workflow-syntax-for-github-actions#onpushpull_requestbranchestags)」を参照してください。

Pull Requestをスキャンすると、その結果はPull Requestチェック内のアラートとして表示されます。 詳しい情報については、「[プルリクエストでコードスキャンアラートをトリアージする](/code-security/secure-coding/triaging-code-scanning-alerts-in-pull-requests)」を参照してください。

{% ifversion fpt or ghes > 3.1 or ghae-next %}
### Defining the severities causing pull request check failure

By default, only alerts with the severity level of `Error`{% ifversion fpt or ghes > 3.1  or ghae-issue-4697 %} or security severity level of `Critical` or `High`{% endif %} will cause a pull request check failure, and a check will still succeed with alerts of lower severities. You can change the levels of alert severities{% ifversion fpt or ghes > 3.1  or ghae-issue-4697 %} and of security severities{% endif %} that will cause a pull request check failure in your repository settings. For more information about severity levels, see "[Managing code scanning alerts for your repository](/code-security/secure-coding/automatically-scanning-your-code-for-vulnerabilities-and-errors/managing-code-scanning-alerts-for-your-repository#about-alerts-details)."

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.sidebar-settings %}
{% data reusables.repositories.navigate-to-security-and-analysis %}
1. Under "Code scanning", to the right of "Check Failure", use the drop-down menu to select the level of severity you would like to cause a pull request check failure.
{% ifversion fpt or ghes > 3.1  or ghae-issue-4697 %}
![チェック失敗の設定](/assets/images/help/repository/code-scanning-check-failure-setting.png)
{% else %}
![チェック失敗の設定](/assets/images/help/repository/code-scanning-check-failure-setting-ghae.png)
{% endif %}
{% endif %}

### プルリクエストの不要なスキャンを回避する

どのファイルが変更されたかに関わらず、デフォルトブランチに対する特定のプルリクエストにコードスキャンがトリガーされることを避けたい場合もあるでしょう。 これを設定するには、{% data variables.product.prodname_code_scanning %} ワークフローで `on:pull_request:paths-ignore` または `on:pull_request:paths` を指定します。 たとえば、プルリクエストにおける変更が、`.md` または `.txt` のファイル拡張子を持つファイルである場合、次の `paths-ignore` 配列を使用できます。

``` yaml
on:
  push:
    branches: [main, protected]
  pull_request:
    branches: [main]
    paths-ignore:
      - '**/*.md'
      - '**/*.txt'
```

{% note %}

**注釈**

* `on:pull_request:paths-ignore` と `on:pull_request:paths` は、ワークフローのアクションがプルリクエストで実行されるかどうかを決定する条件を設定します。 アクションが実行されたときにどのファイルが解析__されるかは決定しません。 プルリクエストに、`on:pull_request:paths-ignore` または `on:pull_request:paths` にマッチしないファイルが含まれている場合、ワークフローはそのアクションを実行し、`on:pull_request:paths-ignore` または `on:pull_request:paths` にマッチするものを含む、プルリクエストにおいて変更されたすべてのファイルをスキャンします。ただし、除外されているファイルは除きます。 ファイルを解析から除外する方法については、「[スキャンするディレクトリを指定する](#specifying-directories-to-scan)」を参照してください。
* For {% data variables.product.prodname_codeql %} {% data variables.product.prodname_code_scanning %} ワークフローファイルに対しては、`on:push` イベントで `paths-ignore` や `paths` といったキーワードは使用しないでください。解析に漏れが生じる恐れがあります。 正確な結果を得るには、{% data variables.product.prodname_codeql %} {% data variables.product.prodname_code_scanning %} が新しい変更を前回のコミットの解析と比較できる必要があります。

{% endnote %}

`on:pull_request:paths-ignore` と `on:pull_request:paths` を使用して、プルリクエストに対していつワークフローを実行するかを決定することに関する詳しい情報については、「[{% data variables.product.prodname_actions %} のワークフロー構文](/actions/reference/workflow-syntax-for-github-actions#onpushpull_requestpaths)」を参照してください。

### スケジュールに従ってスキャンする

デフォルトの {% data variables.product.prodname_code_scanning %} ワークフローは、`pull_request` イベントを使用して、プルリクエストの `HEAD` コミットでコードスキャンをトリガーします。 このスケジュールを調整するには、ワークフローで `cron` 値を編集します。 詳しい情報については、「[{% data variables.product.prodname_actions %} のワークフロー構文](/actions/reference/workflow-syntax-for-github-actions#onschedule)」を参照してください。

{% note %}

**注釈**: {% data variables.product.prodname_dotcom %} は、デフォルトのブランチのワークフローにあるスケジュール設定されたジョブのみを実行します。 他のブランチのワークフローでスケジュールを変更しても、ブランチをデフォルトブランチにマージするまで影響はありません。

{% endnote %}

### サンプル

以下の例は、デフォルトブランチの名前が `main` で、`protected` という保護されたブランチがある特定のリポジトリに対する {% data variables.product.prodname_codeql_workflow %} を示しています。

``` yaml
on:
  push:
    branches: [main, protected]
  pull_request:
    branches: [main]
  schedule:
    - cron: '20 14 * * 1'
```

このワークフローは、次をスキャンします。
* デフォルトブランチと保護されたブランチに対する全てのプッシュ
* デフォルトブランチに対する全てのプルリクエスト
* 毎週月曜の14:20 UTCにデフォルトブランチ

## オペレーティングシステムを指定する

コードのコンパイルに特定のオペレーティングシステムが必要な場合は、そのオペレーティングシステムを {% data variables.product.prodname_codeql_workflow %} で設定できます。 `jobs.analyze.runs-on` の値を編集して、{% data variables.product.prodname_code_scanning %} のアクションを実行するマシンのオペレーティングシステムを指定します。 {% ifversion ghes %}オペレーティングシステムの指定には、`self-hosted` の後に、2 つの要素がある配列の 2 番目の要素として、適切なラベルを使用します。{% else %}

Code Scanningにセルフホストランナーを使うことにしたなら、`self-hosted` の後に、2 つの要素がある配列の 2 番目の要素として適切なラベルを使用し、オペレーティングシステムを指定できます。{% endif %}

``` yaml
jobs:
  analyze:
    name: Analyze
    runs-on: [self-hosted, ubuntu-latest]
```

{% ifversion fpt %}詳しい情報については、「[セルフホストランナーについて](/actions/hosting-your-own-runners/about-self-hosted-runners)」および「[セルフホストランナーを追加する](/actions/hosting-your-own-runners/adding-self-hosted-runners)」を参照してください。{% endif %}

{% data variables.product.prodname_code_scanning_capc %} は、macOS、Ubuntu、Windows の最新バージョンをサポートしています。 Typical values for this setting are therefore: `ubuntu-latest`, `windows-latest`, and `macos-latest`. 詳しい情報については、{% ifversion ghes %}「[GitHub Actions のワークフロー構文](/actions/reference/workflow-syntax-for-github-actions#self-hosted-runners)」および「[セルフホストランナーでラベルを使用する](/actions/hosting-your-own-runners/using-labels-with-self-hosted-runners)」{% else %}「[GitHub Actionsのワークフロー構文](/actions/reference/workflow-syntax-for-github-actions#jobsjob_idruns-on)」{% endif %}を参照してください。

{% ifversion ghes %}GitがセルフホストランナーのPATH変数内にあるようにしなければなりません。{% else %}セルフホストランナーを使っているなら、GitがPATH変数内にあるようにしなければなりません。{% endif %}

{% ifversion fpt or ghes > 3.1 or ghae-next %}
## {% data variables.product.prodname_codeql %}データベースの場所の指定

一般に、{% data variables.product.prodname_codeql_workflow %}が{% data variables.product.prodname_codeql %}データベースを置く場所について気にする必要はありません。これは、以前のステップで作成されたデータベースを後のステップは自動的に見つけるからです。 ただし、たとえばこのデータベースをワークフローの成果物としてアップロードするといったような、{% data variables.product.prodname_codeql %}データベースが特定のディスク上の場所にあることを必要とするカスタムのワークフローステップを書いているなら、`init`アクションの下で`db-location`を使って場所を指定することもできます。

{% raw %}
``` yaml
- uses: github/codeql-action/init@v1
  with:
    db-location: '${{ github.workspace }}/codeql_dbs'
```
{% endraw %}

{% data variables.product.prodname_codeql_workflow %}は、`db-location`で提供されたパスが書き込み可能であり、存在しないか空のディレクトリであることを期待します。 セルフホストランナー上で動作するか、Dockerコンテナを使うジョブでこのパラメータを使う場合、選択されたディレクトリが実行間でクリアされること、あるいは不要になったらデータベースが削除されることを保証するのはユーザの責任です。 これは、実行のたびに新しいインスタンスとクリーンなファイルシステムになる{% data variables.product.prodname_dotcom %}ホストランナー上で動作するジョブには必要ありません。 詳しい情報については「[{% data variables.product.prodname_dotcom %}ホストランナーについて](/actions/using-github-hosted-runners/about-github-hosted-runners)」を参照してください。

このパラメータが使われなければ、{% data variables.product.prodname_codeql_workflow %}はデータベースを自分が選択した一時的な場所に作成します。
{% endif %}

## 解析される言語を変更する

{% data variables.product.prodname_codeql %} {% data variables.product.prodname_code_scanning %} automatically detects code written in the supported languages.

{% data reusables.code-scanning.codeql-languages-bullets %}

The default {% data variables.product.prodname_codeql_workflow %} file contains a build matrix called `language` which lists the languages in your repository that are analyzed. {% data variables.product.prodname_codeql %} automatically populates this matrix when you add {% data variables.product.prodname_code_scanning %} to a repository. Using the `language` matrix optimizes {% data variables.product.prodname_codeql %} to run each analysis in parallel. We recommend that all workflows adopt this configuration due to the performance benefits of parallelizing builds. For more information about build matrices, see "[Managing complex workflows](/actions/learn-github-actions/managing-complex-workflows#using-a-build-matrix)."

{% data reusables.code-scanning.specify-language-to-analyze %}

If your workflow uses the `language` matrix then {% data variables.product.prodname_codeql %} is hardcoded to analyze only the languages in the matrix. To change the languages you want to analyze, edit the value of the matrix variable. You can remove a language to prevent it being analyzed or you can add a language that was not present in the repository when {% data variables.product.prodname_code_scanning %} was set up. For example, if the repository initially only contained JavaScript when {% data variables.product.prodname_code_scanning %} was set up, and you later added Python code, you will need to add `python` to the matrix.

```yaml
jobs:
  analyze:
    name: Analyze
    ...
    strategy:
      fail-fast: false
      matrix:
        language: ['javascript', 'python']
```

If your workflow does not contain a matrix called `language`, then {% data variables.product.prodname_codeql %} is configured to run analysis sequentially. If you don't specify languages in the workflow, {% data variables.product.prodname_codeql %} automatically detects, and attempts to analyze, any supported languages in the repository. If you want to choose which languages to analyze, without using a matrix, you can use the `languages` parameter under the `init` action.

```yaml
- uses: github/codeql-action/init@v1
  with:
    languages: cpp, csharp, python
```
{% ifversion fpt %}
## 追加のクエリを実行する

For GitHub-hosted runners that use Linux only, the {% data variables.product.prodname_codeql_workflow %} will try to auto-install Python dependencies to give more results for the CodeQL analysis. You can control this behavior by specifying the `setup-python-dependencies` parameter for the action called by the "Initialize CodeQL" step. By default, this parameter is set to `true`:

-  リポジトリがPythonで書かれたコードを含むなら、"Initialize CodeQL"ステップは必要な依存関係をGitHubがホストするランナーにインストールします。 自動インストールが成功したら、このアクションは環境変数の`CODEQL_PYTHON`を依存関係を含むPythonの実行可能ファイルに設定することもします。

- リポジトリがPythonの依存関係を持たない場合、あるいは依存関係が予想外の方法で指定されている場合、警告が示されてアクションは残りのジョブを継続します。 依存関係の解釈に問題があってもアクションの実行は成功することがありますが、結果は不完全かも知れません。

Alternatively, you can install Python dependencies manually on any operating system. You will need to add `setup-python-dependencies` and set it to `false`, as well as set `CODEQL_PYTHON` to the Python executable that includes the dependencies, as shown in this workflow extract:

```yaml
jobs:
  CodeQL-Build:

    runs-on: ubuntu-latest{% ifversion fpt or ghes > 3.1 or ghae-next %}
    permissions:
      security-events: write
      actions: read{% endif %}

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.x'
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          if [ -f requirements.txt ];
          then pip install -r requirements.txt;
          fi
          # 環境変数`CODEQL-PYTHON`を
          # 依存関係を含むPythonの実行可能ファイルに設定
          echo "CODEQL_PYTHON=$(which python)" >> $GITHUB_ENV
      - name: Initialize CodeQL
        uses: github/codeql-action/init@v1
        with:
          languages: python
          # デフォルトの動作をオーバーライドして、アクションが
          # Pythonの依存関係を自動インストールしないようにする
          setup-python-dependencies: false
```
{% endif %}

{% ifversion fpt or ghes > 3.1 %}
## 分析のカテゴリの設定

`category`を使って、同じツールやコミットに対して行われる、ただし様々な言語やコードの様々な部分に対して行われる複数の分析を区別してください。 ワークフロー中で指定したカテゴリは、SARIF結果ファイルに含まれます。

このパラメータは、特に単一リポジトリで作業をしていて、単一リポジトリの様々なコンポーネントに対して複数のSARIFファイルがある場合に有益です。

{% raw %}
``` yaml
    - name: Perform CodeQL Analysis
      uses: github/codeql-action/analyze
      with:
        # Optional. Specify a category to distinguish between multiple analyses
        # for the same tool and ref. If you don't use `category` in your workflow, 
        # GitHub will generate a default category name for you
        category: "my_category"
```
{% endraw %}

ワークフローで`category`を指定しない場合、{% data variables.product.product_name %}はアクションをトリガーしたワークフロー名、アクション名、任意のマトリクス変数に基づいてカテゴリ名を生成します。 例:
- `.github/workflows/codeql-analysis.yml`ワークフローと`analyze`アクションは、`.github/workflows/codeql.yml:analyze`というカテゴリを生成します。
- `.github/workflows/codeql-analysis.yml`ワークフロー、`analyze`アクション、マトリクス変数`{language: javascript, os: linux}`は、`.github/workflows/codeql-analysis.yml:analyze/language:javascript/os:linux`というカテゴリを生成します。

`category`の値は、SARIF v2.1.0で&lt;run&gt;.automationDetails.id</code>プロパティに現れます。 詳しい情報については「[{% data variables.product.prodname_code_scanning %}の SARIF サポート](/code-security/secure-coding/sarif-support-for-code-scanning#runautomationdetails-object)」を参照してください。

指定したカテゴリは、SARIFファイルファイルに`runAutomationDetails`が含まれている場合、その詳細を上書きしません。

{% endif %}

## 追加のクエリを実行する

{% data reusables.code-scanning.run-additional-queries %}

{% if codeql-packs %}
### Using {% data variables.product.prodname_codeql %} query packs

{% data reusables.code-scanning.beta-codeql-packs-cli %}

To add one or more {% data variables.product.prodname_codeql %} query packs (beta), add a `with: packs:` entry within the `uses: github/codeql-action/init@v1` section of the workflow. Within `packs` you specify one or more packages to use and, optionally, which version to download. Where you don't specify a version, the latest version is downloaded. If you want to use packages that are not publicly available, you need to set the `GITHUB_TOKEN` environment variable to a secret that has access to the packages. For more information, see "[Authentication in a workflow](/actions/reference/authentication-in-a-workflow)" and "[Encrypted secrets](/actions/reference/encrypted-secrets)."

{% note %}

**Note:** For workflows that generate {% data variables.product.prodname_codeql %} databases for multiple languages, you must instead specify the {% data variables.product.prodname_codeql %} query packs in a configuration file. For more information, see "[Specifying {% data variables.product.prodname_codeql %} query packs](#specifying-codeql-query-packs)" below.

{% endnote %}

In the example below, `scope` is the organization or personal account that published the package. When the workflow runs, the three {% data variables.product.prodname_codeql %} query packs are downloaded from {% data variables.product.product_name %} and the default queries or query suite for each pack run. The latest version of `pack1` is downloaded as no version is specified. Version 1.2.3 of `pack2` is downloaded, as well as the latest version of `pack3` that is compatible with version 1.2.3.

{% raw %}
``` yaml
- uses: github/codeql-action/init@v1
  with:
    # Comma-separated list of packs to download
    packs: scope/pack1,scope/pack2@1.2.3,scope/pack3@~1.2.3
```
{% endraw %}

### Using queries in QL packs
{% endif %}
1つ以上のクエリスイートを追加するには、設定ファイルに `queries` セクションを追加します。 If the queries are in a private repository, use the `external-repository-token` parameter to specify a token that has access to checkout the private repository.

{% raw %}
``` yaml
- uses: github/codeql-action/init@v1
  with:
    queries: COMMA-SEPARATED LIST OF PATHS
    # Optional. Provide a token to access queries stored in private repositories.
    external-repository-token: ${{ secrets.ACCESS_TOKEN }}
```
{% endraw %}

設定ファイルでこれらを指定して、追加のクエリスイートを実行することもできます。 クエリスイートはクエリのコレクションであり、通常は目的または言語ごとにグループ化されています。

{% data reusables.code-scanning.codeql-query-suites %}

{% if codeql-packs %}
### Working with custom configuration files
{% endif %}

If you also use a configuration file for custom settings, any additional {% if codeql-packs %}packs or {% endif %}queries specified in your workflow are used instead of those specified in the configuration file. If you want to run the combined set of additional {% if codeql-packs %}packs or {% endif %}queries, prefix the value of {% if codeql-packs %}`packs` or {% endif %}`queries` in the workflow with the `+` symbol. 設定ファイルの例については、「[Example configuration files](#example-configuration-files)」を参照してください。

In the following example, the `+` symbol ensures that the specified additional {% if codeql-packs %}packs and {% endif %}queries are used together with any specified in the referenced configuration file.

``` yaml
- uses: github/codeql-action/init@v1
  with:
    config-file: ./.github/codeql/codeql-config.yml
    queries: +security-and-quality,octo-org/python-qlpack/show_ifs.ql@main
    {%- if codeql-packs %}
    packs: +scope/pack1,scope/pack2@v1.2.3
    {% endif %}
```

## サードパーティのコードスキャンツールを使用する

A custom configuration file is an alternative way to specify additional {% if codeql-packs %}packs and {% endif %}queries to run. You can also use the file to disable the default queries and to specify which directories to scan during analysis.

In the workflow file, use the `config-file` parameter of the `init` action to specify the path to the configuration file you want to use. この例では、設定ファイル _./.github/codeql/codeql-config.yml_ を読み込みます。

``` yaml
- uses: github/codeql-action/init@v1
  with:
    config-file: ./.github/codeql/codeql-config.yml
```

{% data reusables.code-scanning.custom-configuration-file %}

If the configuration file is located in an external private repository, use the `external-repository-token` parameter of the `init` action to specify a token that has access to the private repository.

{% raw %}
```yaml
- uses: github/codeql-action/init@v1
  with:
    external-repository-token: ${{ secrets.ACCESS_TOKEN }}
```
{% endraw %}

The settings in the configuration file are written in YAML format.

{% if codeql-packs %}
### Specifying {% data variables.product.prodname_codeql %} query packs

{% data reusables.code-scanning.beta-codeql-packs-cli %}

You specify {% data variables.product.prodname_codeql %} query packs in an array. Note that the format is different from the format used by the workflow file.

{% raw %}
``` yaml
packs: 
  # Use the latest version of 'pack1' published by 'scope'
  - scope/pack1 
  # Use version 1.23 of 'pack2' 
  - scope/pack2@v1.2.3
  # Use the latest version of 'pack3' compatible with 1.23
  - scope/pack3@~1.2.3
```
{% endraw %}

If you have a workflow that generates more than one {% data variables.product.prodname_codeql %} database, you can specify any {% data variables.product.prodname_codeql %} query packs to run in a custom configuration file using a nested map of packs.

{% raw %}
``` yaml
packs:
  # Use these packs for JavaScript analysis
  javascript:
    - scope/js-pack1
    - scope/js-pack2
  # Use these packs for Java analysis
  java:
    - scope/java-pack1
    - scope/java-pack2@v1.0.0
```
{% endraw %}
{% endif %}

### 追加のクエリを指定する

You specify additional queries in a `queries` array. Each element of the array contains a `uses` parameter with a value that identifies a single query file, a directory containing query files, or a query suite definition file.

``` yaml
queries:
  - uses: ./my-basic-queries/example-query.ql
  - uses: ./my-advanced-queries
  - uses: ./query-suites/my-security-queries.qls
```

Optionally, you can give each array element a name, as shown in the example configuration files below. For more information about additional queries, see "[Running additional queries](#running-additional-queries)" above.

### デフォルトのクエリを無効にする

カスタムクエリのみを実行する場合は、構成ファイルに `disable-default-queries: true` を追加して、デフォルトのセキュリティクエリを無効にすることができます。

### スキャンするディレクトリを指定する

For the interpreted languages that {% data variables.product.prodname_codeql %} supports (Python and JavaScript/TypeScript), you can restrict {% data variables.product.prodname_code_scanning %} to files in specific directories by adding a `paths` array to the configuration file. You can exclude the files in specific directories from analysis by adding a `paths-ignore` array.

``` yaml
paths:
  - src
paths-ignore:
  - src/node_modules
  - '**/*.test.js'
```

{% note %}

**ノート**:

* The `paths` and `paths-ignore` keywords, used in the context of the {% data variables.product.prodname_code_scanning %} configuration file, should not be confused with the same keywords when used for `on.<push|pull_request>.paths` in a workflow. When they are used to modify `on.<push|pull_request>` in a workflow, they determine whether the actions will be run when someone modifies code in the specified directories. 詳細については、「[{% data variables.product.prodname_actions %}のワークフロー構文](/actions/reference/workflow-syntax-for-github-actions#onpushpull_requestpaths)」を参照してください。
* The filter pattern characters `?`, `+`, `[`, `]`, and `!` are not supported and will be matched literally.
* `**` **Note**: `**` characters can only be at the start or end of a line, or surrounded by slashes, and you can't mix `**` and other characters. たとえば、`foo/**`、`**/foo`、および `foo/**/bar` はすべて使用できる構文ですが、`**foo` は使用できません。 ただし、例に示すように、単一の * を他の文字と一緒に使用できます。 You'll need to quote anything that contains a `*` character.

{% endnote %}

For compiled languages, if you want to limit {% data variables.product.prodname_code_scanning %} to specific directories in your project, you must specify appropriate build steps in the workflow. ビルドからディレクトリを除外するために使用するコマンドは、ビルドシステムによって異なります。 詳しい情報については、「[コンパイル型言語の {% data variables.product.prodname_codeql %} ワークフローを設定する](/code-security/secure-coding/configuring-the-codeql-workflow-for-compiled-languages#adding-build-steps-for-a-compiled-language)」を参照してください。

特定のディレクトリのコードを変更すると、monorepo の一部をすばやく分析できます。 ビルドステップでディレクトリを除外し、ワークフローファイルで [`on.<push|pull_request>`](https://help.github.com/actions/reference/workflow-syntax-for-github-actions#onpushpull_requestpaths) の`paths-ignore` および `paths` キーワードを使用する必要があります。

### 設定ファイルの例

{% data reusables.code-scanning.example-configuration-files %}

## コンパイルされた言語の {% data variables.product.prodname_code_scanning %} を設定する

{% data reusables.code-scanning.autobuild-compiled-languages %} {% data reusables.code-scanning.analyze-go %}

{% data reusables.code-scanning.autobuild-add-build-steps %}コンパイルされた言語で {% data variables.product.prodname_codeql %} {% data variables.product.prodname_code_scanning %} を設定する方法に関する詳しい情報については、「[コンパイルされた言語の {% data variables.product.prodname_codeql %} を設定する](/code-security/secure-coding/configuring-the-codeql-workflow-for-compiled-languages)」を参照してください。

## {% data variables.product.prodname_code_scanning %} 用の設定ファイルを作成できます。

{% data variables.product.prodname_dotcom %} can display code analysis data generated externally by a third-party tool. ワークフローに `upload-sarif` アクションを追加することで、{% data variables.product.prodname_dotcom %} のサードパーティツールからのコード分析を表示できます。 詳しい情報については、「[SARIF ファイルを GitHub にアップロードする](/code-security/secure-coding/uploading-a-sarif-file-to-github)」を参照してください。
