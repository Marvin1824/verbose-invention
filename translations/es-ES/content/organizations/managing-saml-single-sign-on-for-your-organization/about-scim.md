---
title: Acerca de SCIM
intro: 'Con Sistema para la administración de identidades entre dominios (SCIM), los administradores pueden automatizar el intercambio de información de identidad del usuario entre los sistemas.'
product: '{% data reusables.gated-features.saml-sso %}'
redirect_from:
  - /articles/about-scim
  - /github/setting-up-and-managing-organizations-and-teams/about-scim
versions:
  fpt: '*'
  ghec: '*'
topics:
  - Organizations
  - Teams
---

{% data reusables.enterprise-accounts.emu-scim-note %}

Si usas [SAML SSO](/articles/about-identity-and-access-management-with-saml-single-sign-on) en tu organización, puedes implementar SCIM para agregar, administrar y eliminar el acceso de los miembros de la organización a {% data variables.product.product_name %}. Por ejemplo, un administrador puede desaprovisionar a un miembro de la organización usando el SCIM y eliminar automáticamente el miembro de la organización.

Si usas SAML SSO sin implementar SCIM, no tendrás un desaprovisionamiento automático. Cuando las sesiones de los miembros de la organización expiran una vez que su acceso ha sido eliminado del IdP, no se eliminan automáticamente de la organización. Los tokens autorizados otorgan acceso a la organización incluso una vez que las sesiones han expirado. Para eliminar el acceso, los administradores de la organización pueden eliminar de forma manual el token autorizado de la organización o automatizar su eliminación con SCIM.

Estos proveedores de identidad son compatibles con la API de SCIM de {% data variables.product.product_name %} para organizaciones. For more information, see [SCIM](/rest/reference/scim) in the {% ifversion fpt or ghec %}{% data variables.product.prodname_dotcom %}{% else %}{% data variables.product.product_name %}{% endif %} API documentation.
- Azure AD
- Okta
- OneLogin

{% data reusables.scim.enterprise-account-scim %}

## Leer más

- "[Acerca de la administración de identidad y el acceso con el inicio de sesión único de SAML](/articles/about-identity-and-access-management-with-saml-single-sign-on)"
- "[Conectar tu proveedor de identidad a tu organización](/articles/connecting-your-identity-provider-to-your-organization)"
- "[Activar y probar el inicio de sesión único de SAML para tu organización](/articles/enabling-and-testing-saml-single-sign-on-for-your-organization)"
- "[Visualizar y administrar un acceso de SAML de un miembro a tu organización](/github/setting-up-and-managing-organizations-and-teams//viewing-and-managing-a-members-saml-access-to-your-organization)"
