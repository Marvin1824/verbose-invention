---
title: リポジトリを保護する
intro: 'リポジトリをセキュアに保つために、いくつもの{% data variables.product.prodname_dotcom %}の機能が利用できます。'
permissions: Repository administrators and organization owners can configure repository security settings.
redirect_from:
  - /github/administering-a-repository/about-securing-your-repository
  - /github/code-security/getting-started/about-securing-your-repository
versions:
  fpt: '*'
  ghes: '>=3.0'
  ghae: '*'
type: how_to
topics:
  - Repositories
  - Dependencies
  - Vulnerabilities
  - Advanced Security
shortTitle: リポジトリの保護
---

## はじめに
このガイドは、リポジトリでのセキュリティ機能の設定方法を紹介します。 リポジトリのセキュリティ設定を構成するには、リポジトリ管理者かOrganizationのオーナーでなければなりません。

セキュリティの要件はリポジトリに固有のものなので、リポジトリですべての機能を有効化する必要はないかもしれません。 詳しい情報については「[{% data variables.product.prodname_dotcom %}のセキュリティ機能](/code-security/getting-started/github-security-features)」を参照してください。

セキュリティの機能の中には、{% data variables.product.prodname_advanced_security %}ライセンスを持っている{% ifversion fpt %}Organizationが所有するプライベートリポジトリとパブリックリポジトリでのみ{% else %}場合にのみ{% endif %}利用できるものがあります。 {% data reusables.advanced-security.more-info-ghas %}

## リポジトリへのアクセスの管理

リポジトリを保護するための最初の手順は、コードを表示および変更できるユーザを設定することです。 詳しい情報については、「[リポジトリ設定を管理する](/github/administering-a-repository/managing-repository-settings)」を参照してください。

リポジトリのメインページから、**{% octicon "gear" aria-label="The Settings gear" %}Settings（設定）**をクリックし、続いて"Danger Zone（危険区域）"まで下へスクロールしてください。

- リポジトリを見ることができる人を変更するには**Change visibility（可視性を変更）**をクリックしてください。 詳しい情報については「[リポジトリの可視性の設定](/github/administering-a-repository/setting-repository-visibility)」を参照してください。{% ifversion fpt %}
- リポジトリにアクセスできる人を変更し、権限を調整するには**Manage access（アクセスの管理）**をクリックしてください。 詳しい情報については「[リポジトリにアクセスできるTeamと人の管理](/github/administering-a-repository/managing-teams-and-people-with-access-to-your-repository)」を参照してください。{% endif %}

{% ifversion fpt or ghes > 3.0 or ghae-next %}
## セキュリティポリシーの設定

1. リポジトリのメインページから**{% octicon "shield" aria-label="The shield symbol" %} Security（セキュリティ）**をクリックしてください。
2. **Security policy（セキュリティポリシー）**をクリックしてください。
3. **Start setup（セットアップの開始）**をクリックします。
4. プロジェクトのサポートされているバージョンに関する情報と、脆弱性の報告方法に関する情報を追加してください。

詳しい情報については「[リポジトリにセキュリティポリシーを追加する](/code-security/getting-started/adding-a-security-policy-to-your-repository)」を参照してください。

{% endif %}

{% ifversion fpt or ghes > 2.22 %}
## 依存関係グラフの管理

Once you have [enabled the dependency graph](/code-security/supply-chain-security/understanding-your-software-supply-chain/about-the-dependency-graph#enabling-the-dependency-graph), it is automatically generated for {% ifversion fpt or ghes > 2.22 %} all public repositories, and you can choose to enable it for private repositories.{% else %} all repositories.{% endif %}

1. リポジトリのメインページから、**{% octicon "gear" aria-label="The Settings gear" %} Settings（設定）**をクリックしてください。
2. **Security & analysis（セキュリティと分析）**をクリックしてください。
3. 依存関係グラフの隣で**Enable（有効化）**もしくは**Disable（無効化）**をクリックしてください。

詳しい情報については、「[リポジトリの依存関係を調べる](/code-security/supply-chain-security/exploring-the-dependencies-of-a-repository#enabling-and-disabling-the-dependency-graph-for-a-private-repository)」を参照してください。

{% endif %}

{% ifversion fpt or ghes > 2.22 %}
## {% data variables.product.prodname_dependabot_alerts %}の管理

デフォルトで、{% data variables.product.prodname_dotcom %}はパブリックリポジトリ内の脆弱性を検出し、{% data variables.product.prodname_dependabot_alerts %}を生成します。 {% data variables.product.prodname_dependabot_alerts %}は、プライベートリポジトリでも有効化できます。

1. 自分のプロフィール写真をクリックし、続いて** Settings（設定）**をクリックしてください。
2. **Security & analysis（セキュリティと分析）**をクリックしてください。
3. {% data variables.product.prodname_dependabot_alerts %}の隣の**Enable all（すべて有効化）**をクリックしてください。

詳しい情報については「[脆弱な依存関係に対するアラートについて](/code-security/supply-chain-security/about-alerts-for-vulnerable-dependencies)」{% ifversion fpt %}及び「[ユーザアカウントのセキュリティ及び分析設定の管理](/github/setting-up-and-managing-your-github-user-account/managing-security-and-analysis-settings-for-your-user-account)」{% endif %}を参照してください。

{% endif %}

{% ifversion fpt or ghes > 3.1 %}
## 依存関係レビューの管理

依存関係レビューを使うと、Pull Requestがリポジトリにマージされる前に、Pull Request内での依存関係の変化を可視化できます。 依存関係レビューは、すべてのパブリックリポジトリと、依存関係グラフが有効化された{% data variables.product.prodname_advanced_security %}ライセンスを持つOrganizationが所有するリポジトリで利用できます。 詳しい情報については「[依存関係レビューについて](/code-security/supply-chain-security/understanding-your-software-supply-chain/about-dependency-review)」を参照してください。

{% endif %}

{% ifversion fpt %}

## {% data variables.product.prodname_dependabot_security_updates %}の管理

{% data variables.product.prodname_dependabot_alerts %}を使用するリポジトリでは、{% data variables.product.prodname_dependabot_security_updates %}を有効化して脆弱性が検出された際にセキュリティ更新でPull Requestを発行させることができます。

1. リポジトリのメインページから、**{% octicon "gear" aria-label="The Settings gear" %} Settings（設定）**をクリックしてください。
2. **Security & analysis（セキュリティと分析）**をクリックしてください。
3. {% data variables.product.prodname_dependabot_security_updates %}の隣で**Enable（有効化）**をクリックしてください。

詳しい情報については、「[{% data variables.product.prodname_dependabot_security_updates %} について](/code-security/supply-chain-security/about-dependabot-security-updates)」および「[{% data variables.product.prodname_dependabot_security_updates %} の設定](/code-security/supply-chain-security/configuring-dependabot-security-updates)」を参照してください。

## {% data variables.product.prodname_dependabot_version_updates %}の管理

{% data variables.product.prodname_dependabot %}を有効化して、依存関係を最新の状態に保つためのPull Requestを自動的に発行するようにできます。 詳しい情報については「[{% data variables.product.prodname_dependabot_version_updates %}について](/code-security/supply-chain-security/about-dependabot-version-updates)」を参照してください。

{% data variables.product.prodname_dependabot_version_updates %}を有効化するには、設定ファイルの*dependabot.yml*を作成しなければなりません。 詳しい情報については「[バージョンアップデートの有効化と無効化](/code-security/supply-chain-security/enabling-and-disabling-version-updates)」を参照してください。

{% endif %}

{% ifversion fpt or ghes > 2.22 or ghae %}
## {% data variables.product.prodname_code_scanning %} を設定する

{% data variables.product.prodname_code_scanning_capc %}は、{% data variables.product.prodname_advanced_security %}ライセンスを持つ{% ifversion fpt %}Organizationが所有するプライベートリポジトリと、すべてのパブリックリポジトリで{% else %}Organizationが所有するリポジトリで{% endif %}利用できます。

{% data variables.product.prodname_codeql_workflow %}もしくはサードパーティのツールを使い、リポジトリ中に保存されたコードの脆弱性やエラーを自動的に特定するよう、{% data variables.product.prodname_code_scanning %}をセットアップできます。 詳しい情報については、「[リポジトリに対する {% data variables.product.prodname_code_scanning %} をセットアップする](/code-security/secure-coding/setting-up-code-scanning-for-a-repository)」を参照してください。

## {% data variables.product.prodname_secret_scanning %}の設定
{% data variables.product.prodname_secret_scanning_caps %}は、{% data variables.product.prodname_advanced_security %}ライセンスを持つ{% ifversion fpt %}Organizationが所有するプライベートリポジトリと、すべてのパブリックリポジトリで{% else %}Organizationが所有するリポジトリで{% endif %}利用できます。

{% data variables.product.prodname_secret_scanning_caps %}はOrganizationの設定によって、デフォルトでリポジトリに対して有効にできます。

1. リポジトリのメインページから、**{% octicon "gear" aria-label="The Settings gear" %} Settings（設定）**をクリックしてください。
2. **Security & analysis（セキュリティと分析）**をクリックしてください。
3. まだ{% data variables.product.prodname_GH_advanced_security %}が有効化されていなければ、**Enable（有効化）**をクリックしてください。
4. {% data variables.product.prodname_secret_scanning_caps %}の隣で**Enable（有効化）**をクリックしてください。

{% endif %}

## 次のステップ
セキュリティの機能からのアラートを表示及び管理して、コード中の依存関係と脆弱性に対処できます。 詳しい情報については{% ifversion fpt or ghes > 2.22 %}「[リポジトリ中の脆弱な依存関係の表示と更新](/code-security/supply-chain-security/viewing-and-updating-vulnerable-dependencies-in-your-repository)」、{% endif %}{% ifversion fpt %}「[依存関係の更新のためのPull Requestの管理](/code-security/supply-chain-security/managing-pull-requests-for-dependency-updates)」、{% endif %}「[リポジトリの{% data variables.product.prodname_code_scanning %}の管理](/code-security/secure-coding/managing-code-scanning-alerts-for-your-repository)」、「[{% data variables.product.prodname_secret_scanning %}からのアラートの管理](/code-security/secret-security/managing-alerts-from-secret-scanning)」を参照してください。

{% ifversion fpt %}セキュリティの脆弱性があるなら、セキュリティアドバイザリを作成して非公開で議論し、脆弱性を修正できます。 詳しい情報については「[{% data variables.product.prodname_security_advisories %}について](/code-security/security-advisories/about-github-security-advisories)」及び「[セキュリティアドバイザリの作成](/code-security/security-advisories/creating-a-security-advisory)」を参照してください。
{% endif %}
