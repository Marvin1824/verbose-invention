---
title: リポジトリのデフォルトブランチ名を管理する
intro: 'You can set the default branch name for new repositories that you create on {% data variables.product.product_location %}.'
versions:
  fpt: '*'
  ghes: '>=3.0'
  ghae: '*'
topics:
  - Accounts
redirect_from:
  - /github/setting-up-and-managing-your-github-user-account/managing-the-default-branch-name-for-your-repositories
  - /github/setting-up-and-managing-your-github-user-account/managing-user-account-settings/managing-the-default-branch-name-for-your-repositories
shortTitle: デフォルトブランチ名の管理
---

## デフォルトブランチ名について

{% data variables.product.product_location %} に新しいリポジトリを作成すると、リポジトリにはデフォルトブランチである 1 つのブランチが含まれます。 作成する新しいリポジトリのデフォルトブランチに {% data variables.product.product_name %} が使用する名前を変更できます。 デフォルトブランチの詳細については、「[ブランチについて](/github/collaborating-with-issues-and-pull-requests/about-branches#about-the-default-branch)」を参照してください。

{% data reusables.branches.set-default-branch %}

## デフォルトブランチ 名を設定する

{% data reusables.user_settings.access_settings %}
{% data reusables.user_settings.repo-tab %}
3. [Repository default branch] で、[**Change default branch name now**] をクリックします。 ![[Override] ボタン](/assets/images/help/settings/repo-default-name-button.png)
4. 新しいブランチに使用したいデフォルト名を入力します。 ![デフォルト名を入力するテキストフィールド](/assets/images/help/settings/repo-default-name-text.png)
5. [**Update**] をクリックします。 ![[Update] ボタン](/assets/images/help/settings/repo-default-name-update.png)

## 参考リンク

- 「[Organization のリポジトリのデフォルブランチ名を管理する](/organizations/managing-organization-settings/managing-the-default-branch-name-for-repositories-in-your-organization)」
