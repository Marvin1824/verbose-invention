---
title: GitHub アカウントへの新しい SSH キーの追加
intro: '{% data variables.product.product_name %} アカウントが新しい (あるいは既存の) SSH キーを使うように設定するには、そのキーを {% data variables.product.product_name %} アカウントに追加する必要もあります。'
redirect_from:
  - /articles/adding-a-new-ssh-key-to-your-github-account
  - /github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account
  - /github/authenticating-to-github/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
topics:
  - SSH
shortTitle: Add a new SSH key
---

新しい SSH キーを {% data variables.product.product_name %} アカウントに追加する前に、以下のことを済ませておかなければなりません:
* [既存の SSH キーの確認](/articles/checking-for-existing-ssh-keys)
* [新しい SSH キーを生成して ssh-agent に追加する](/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

新しい SSH キーを {% data variables.product.product_name %}アカウントに追加したら、任意のローカルリポジトリで SSH を使うように再設定できます。 詳しい情報については[リモート URL の HTTPS から SSH への切り替え](/github/getting-started-with-github/managing-remote-repositories/#switching-remote-urls-from-https-to-ssh)を参照してください。

{% data reusables.ssh.key-type-support %}

{% mac %}

{% include tool-switcher %}
{% webui %}

1. SSH 公開鍵をクリップボードにコピーします。

  SSH 公開鍵のファイル名がサンプルコードと異なる場合は、現在の設定に一致するようにファイル名を変更してください。 キーをコピーする際には、改行や空白を追加しないでください。

  ```shell
  $ pbcopy &lt; ~/.ssh/id_ed25519.pub
  # id_ed25519.pub ファイルの内容をクリップボードにコピーする
  ```

  {% tip %}

  **ヒント:** `pbcopy` がうまく動作しない場合は、隠れフォルダ `.ssh` にアクセスし、使い慣れたテキストエディタでこのファイルを開き、クリップボードにコピーしてください。

  {% endtip %}

{% data reusables.user_settings.access_settings %}
{% data reusables.user_settings.ssh %}
4. [**New SSH key**] または [**Add SSH key**] をクリックします。 ![SSH キーボタン](/assets/images/help/settings/ssh-add-ssh-key.png)
5. [Title] フィールドで、新しいキーを説明するラベルを追加します。 たとえば個人の Mac を使っている場合、このキーを "Personal MacBook Air" などと呼ぶことが考えられます。
6. キーを [Key] フィールドに貼り付けます。 ![キーフィールド](/assets/images/help/settings/ssh-key-paste.png)
7. **[Add SSH key]** をクリックしてください。 ![キーの追加ボタン](/assets/images/help/settings/ssh-add-key.png)
{% data reusables.user_settings.sudo-mode-popup %}

{% endwebui %}

{% endmac %}

{% windows %}

{% include tool-switcher %}

{% webui %}

1. SSH 公開鍵をクリップボードにコピーします。

  SSH 公開鍵のファイル名がサンプルコードと異なる場合は、現在の設定に一致するようにファイル名を変更してください。 キーをコピーする際には、改行や空白を追加しないでください。

  ```shell
  $ clip &lt; ~/.ssh/id_ed25519.pub
  # id_ed25519.pub ファイルの内容をクリップボードにコピーする
  ```

  {% tip %}

  **ヒント:** `clip` がうまく動作しない場合は、隠しフォルダ `.ssh` にアクセスし、使い慣れたテキストエディタでこのファイルを開き、クリップボードにコピーしてください。

  {% endtip %}

{% data reusables.user_settings.access_settings %}
{% data reusables.user_settings.ssh %}
4. [**New SSH key**] または [**Add SSH key**] をクリックします。 ![SSH キーボタン](/assets/images/help/settings/ssh-add-ssh-key.png)
5. [Title] フィールドで、新しいキーを説明するラベルを追加します。 たとえば個人の Mac を使っている場合、このキーを "Personal MacBook Air" などと呼ぶことが考えられます。
6. キーを [Key] フィールドに貼り付けます。 ![キーフィールド](/assets/images/help/settings/ssh-key-paste.png)
7. **[Add SSH key]** をクリックしてください。 ![キーの追加ボタン](/assets/images/help/settings/ssh-add-key.png)
8. {% data variables.product.product_name %} パスワードの確認を促された場合は、確認します。 ![sudo モードダイアログ](/assets/images/help/settings/sudo_mode_popup.png)

{% endwebui %}

{% endwindows %}

{% linux %}

{% include tool-switcher %}
{% webui %}

1. SSH 公開鍵をクリップボードにコピーします。

  SSH 公開鍵のファイル名がサンプルコードと異なる場合は、現在の設定に一致するようにファイル名を変更してください。 キーをコピーする際には、改行や空白を追加しないでください。

  ```shell
  $ cat ~/.ssh/id_ed25519.pub
  # Then select and copy the contents of the id_ed25519.pub file
  # displayed in the terminal to your clipboard
  ```

  {% tip %}

  **Tip:** Alternatively, you can locate the hidden `.ssh` folder, open the file in your favorite text editor, and copy it to your clipboard.

  {% endtip %}

{% data reusables.user_settings.access_settings %}
{% data reusables.user_settings.ssh %}
4. [**New SSH key**] または [**Add SSH key**] をクリックします。 ![SSH キーボタン](/assets/images/help/settings/ssh-add-ssh-key.png)
5. [Title] フィールドで、新しいキーを説明するラベルを追加します。 たとえば個人の Mac を使っている場合、このキーを "Personal MacBook Air" などと呼ぶことが考えられます。
6. キーを [Key] フィールドに貼り付けます。 ![キーフィールド](/assets/images/help/settings/ssh-key-paste.png)
7. **[Add SSH key]** をクリックしてください。 ![キーの追加ボタン](/assets/images/help/settings/ssh-add-key.png)
8. {% data variables.product.product_name %} パスワードの確認を促された場合は、確認します。 ![sudo モードダイアログ](/assets/images/help/settings/sudo_mode_popup.png)

{% endwebui %}

{% endlinux %}

{% cli %}

{% data reusables.cli.cli-learn-more %}

To add an SSH key to your GitHub account, use the `ssh-key add` subcommand, specifying your public key.

```shell
gh ssh-key add <em>key-file</em>
```

To include a title for the new key, use the `-t` or `--title` flag.

```shell
gh ssh-key add <em>key-file</em> --title "personal laptop"
```

{% endcli %}

{% ifversion fpt %}
## 参考リンク

- [SAML シングルサインオンで使うためにSSHキーを認可する](/articles/authorizing-an-ssh-key-for-use-with-saml-single-sign-on)
{% endif %}
