---
title: Administrar la verificación de GPG para los Codespaces
intro: 'Puedes permitir que {% data variables.product.company_short %} utilice automáticamente GPG para firmar las confirmaciones que haces en tus codespaces para que otras personas puedan tener la confianza de que los cambios vienen de una fuente confiable.'
product: '{% data reusables.gated-features.codespaces %}'
versions:
  fpt: '*'
type: how_to
topics:
  - Codespaces
  - Developer
  - Security
redirect_from:
  - /github/developing-online-with-codespaces/managing-gpg-verification-for-codespaces
  - /codespaces/working-with-your-codespace/managing-gpg-verification-for-codespaces
shortTitle: Verificación GPG
---

 

Después de que habilitas la verificación de GPG, {% data variables.product.company_short %} firmará automáticamente las confirmaciones que hagas en los {% data variables.product.prodname_codespaces %} y éstas tendrán un estado de verificado en {% data variables.product.product_name %}. Predeterminadamente, la verificación GPG se encuentra inhabilitada para los codespaces que creas. Puedes elegir permitir la verificación de GPG para todos los repositorios o para repositorios específicos. Habilita la verificación GPG únicamente para los repositorios en los cuales confías. Para obtener más información acerca de las confirmaciones firmadas por {% data variables.product.product_name %}, consulta la sección "[Acerca de la verificación de firmas de las confirmaciones](/github/authenticating-to-github/about-commit-signature-verification)".

Once you enable GPG verification, it will immediately take effect for all your codespaces.

{% data reusables.user_settings.access_settings %}
{% data reusables.user_settings.codespaces-tab %}
1. Debajo de "verificación GPG", selecciona la configuración que quieras para la verificación de GPG. ![Botones radiales para administrar la verificación GPG](/assets/images/help/settings/codespaces-gpg-verification-radio-buttons.png)
1. Si eliges "Repositorios seleccionados"; selecciona el menú desplegable y luego da clic en el repositorio para el cual quieras habilitar la verificación de GPG. Repite esto para todos los repositorios en los cuales quieras habilitar la verificación GPG. ![Menú desplegable de "Repositorios seleccionados"](/assets/images/help/settings/codespaces-gpg-verification-repository-drop-down.png)


{% note %}

**Note:** Once you have enabled GPG verification for {% data variables.product.prodname_codespaces %}, you also must append `-s` to each commit in order for it to be signed. To do this in {% data variables.product.prodname_vscode %}, ensure the "Git: Enable Commit Signing" option is enabled from the Settings.

{% endnote %}
