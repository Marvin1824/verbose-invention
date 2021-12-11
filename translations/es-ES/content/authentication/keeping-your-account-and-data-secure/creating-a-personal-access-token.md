---
title: Crear un token de acceso personal
intro: Debes crear un token de acceso personal para utilizar como contraseña con la línea de comandos o con la API.
redirect_from:
  - /articles/creating-an-oauth-token-for-command-line-use/
  - /articles/creating-an-access-token-for-command-line-use/
  - /articles/creating-a-personal-access-token-for-the-command-line
  - /github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line
  - /github/authenticating-to-github/creating-a-personal-access-token
  - /github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
topics:
  - Identity
  - Access management
shortTitle: Crear un PAT
---

{% note %}

**Note:** If you use {% data variables.product.prodname_cli %} to authenticate to {% data variables.product.product_name %} on the command line, you can skip generating a personal access token and authenticate via the web browser instead. For more information about authenticating with {% data variables.product.prodname_cli %}, see [`gh auth login`](https://cli.github.com/manual/gh_auth_login).

{% endnote %}

Los tokens de acceso personal (PAT) son una alternativa al uso de contraseñas para la autenticación en {% data variables.product.product_name %} cuando utilizas la [API de GitHub](/rest/overview/other-authentication-methods#via-oauth-and-personal-access-tokens) o la [línea de comandos](#using-a-token-on-the-command-line).

{% ifversion fpt %}Si quieres utilizar un PAT para acceder a los recursos que pertenecen a una organización que utiliza el SSO de SAML, debes autorizarlo. Para obtener más información, consulta las secciónes "[Acerca de la autenticación, con el inicio de sesión único de SAML](/github/authenticating-to-github/about-authentication-with-saml-single-sign-on)" y "[Autorizar un token de acceso personal para su uso con el inicio de sesión único de SAML](/github/authenticating-to-github/authorizing-a-personal-access-token-for-use-with-saml-single-sign-on)".{% endif %}

{% ifversion fpt %}{% data reusables.user_settings.removes-personal-access-tokens %}{% endif %}

A token with no assigned scopes can only access public information. Para usar tu token para acceder a repositorios desde la línea de comando, selecciona `repo`. For more information, see “[Available scopes](/apps/building-oauth-apps/scopes-for-oauth-apps#available-scopes)”.

## Crear un token

{% ifversion fpt %}1. [Verifica tu dirección de correo electrónico](/github/getting-started-with-github/verifying-your-email-address), si aún no ha sido verificada.{% endif %}
{% data reusables.user_settings.access_settings %}
{% data reusables.user_settings.developer_settings %}
{% data reusables.user_settings.personal_access_tokens %}
4. Haz clic en **Generar un nuevo token**. ![Generar el botón para el nuevo token](/assets/images/help/settings/generate_new_token.png)
5. Asígnale a tu token un nombre descriptivo. ![Token description field](/assets/images/help/settings/token_description.png){% ifversion fpt or ghes > 3.2 or ghae-issue-4374 %}
6. To give your token an expiration, select the **Expiration** drop-down menu, then click a default or use the calendar picker. ![Token expiration field](/assets/images/help/settings/token_expiration.png){% endif %}
7. Selecciona los alcances o permisos que deseas otorgarle a este token. Para usar tu token para acceder a repositorios desde la línea de comando, selecciona **repo**.
   {% ifversion fpt or ghes %}
   ![Seleccionar los alcances del token](/assets/images/help/settings/token_scopes.gif)
   {% elsif ghae %}
   ![Seleccionar los alcances del token](/assets/images/enterprise/github-ae/settings/access-token-scopes-for-ghae.png)
   {% endif %}
8. Haz clic en **Generar token**. ![Generar un botón para el token](/assets/images/help/settings/generate_token.png)
   {% ifversion fpt %}
   ![Token recién creado](/assets/images/help/settings/personal_access_tokens.png)
   {% elsif ghes > 3.1 or ghae-next %}
   ![Token recién creado](/assets/images/help/settings/personal_access_tokens_ghe.png)
   {% else %}
   ![Token recién creado](/assets/images/help/settings/personal_access_tokens_ghe_legacy.png)
   {% endif %}
   {% warning %}

   **Advertencia:**Preserva tus tokens de la misma manera que tus contraseñas y no se las reveles a nadie. Cuando trabajes con la API, usa tokens como variables del entorno en lugar de codificarlos de forma rígida en tus programas.

   {% endwarning %}

{% ifversion fpt %}9. Para usar tu token para autenticar a una organización que usa SAML SSO, [autoriza el token para el uso con una organización con inicio de sesión único SAML.](/github/authenticating-to-github/authorizing-a-personal-access-token-for-use-with-saml-single-sign-on){% endif %}

## Usar un token en la línea de comando

{% data reusables.command_line.providing-token-as-password %}

Los tokens de acceso personal solo se pueden usar para operaciones HTTPS Git. Si tu repositorio usa una URL SSH remota, necesitarás [pasar de la URL SSH remota a HTTPS](/github/getting-started-with-github/managing-remote-repositories/#switching-remote-urls-from-ssh-to-https).

Si no se te solicita tu nombre de usuario y contraseña, tus credenciales pueden estar almacenadas en la caché de tu computadora. Puedes [actualizar tus credenciales en la keychain](/github/getting-started-with-github/updating-credentials-from-the-macos-keychain) para reemplazar tu contraseña anterior con el token.

En vez de ingresar tu PAT manualmente para cada operación de HTTPS de Git, puedes almacenarlo en caché con un cliente de Git. Git almacenará tus credenciales temporalmente en la memoria hasta que haya pasado un intervalo de vencimiento. También puedes almacenar el token en un archivo de texto simple que pueda leer Git antes de cada solicitud. Para obtener más información, consulta la sección "[ Almacenar tus credencialesde {% data variables.product.prodname_dotcom %} en el caché dentro de Git](/github/getting-started-with-github/caching-your-github-credentials-in-git)".

## Leer más

- "[About authentication to GitHub](/github/authenticating-to-github/about-authentication-to-github)"{% ifversion fpt or ghae-issue-4374 or ghes > 3.2 %}
- "[Token expiration and revocation](/github/authenticating-to-github/keeping-your-account-and-data-secure/token-expiration-and-revocation)"{% endif %}
