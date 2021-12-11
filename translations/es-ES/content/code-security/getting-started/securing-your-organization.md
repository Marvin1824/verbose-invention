---
title: Asegurar tu organización
intro: 'Puedes utilizar varias características de {% data variables.product.prodname_dotcom %} para ayudar a mantener tu organización segura.'
permissions: Organization owners can configure organization security settings.
versions:
  fpt: '*'
  ghes: '>=3.0'
  ghae: '*'
type: how_to
topics:
  - Organizations
  - Dependencies
  - Vulnerabilities
  - Advanced Security
shortTitle: Asegurar tu organización
---

## Introducción
Esta guía te muestra cómo configurar las características de seguridad para una organización. Las necesidades de seguridad de tu organización son únicas y puede que no necesites habilitar cada una de las características de seguridad. Para obtener más información, consulta la sección "[Características de seguridad de {% data variables.product.prodname_dotcom %}](/code-security/getting-started/github-security-features)".

Algunas características de seguridad solo se encuentran disponibles {% ifversion fpt %}para repositorios públicos y para repositorios privados que pertenezcan a organizaciones con {% else %}si tienes {% endif %}una licencia de {% data variables.product.prodname_advanced_security %}. {% data reusables.advanced-security.more-info-ghas %}

## Administrar el acceso a tu organización

Puedes utilizar niveles de permisos para controlar las acciones que las personas pueden tomar en tu organización. Para obtener más información, consulta ´la sección "[Niveles de permisos para una organización](/organizations/managing-peoples-access-to-your-organization-with-roles/permission-levels-for-an-organization)".

{% ifversion fpt or ghes > 3.0 or ghae-next %}

## Crear una política de seguridad predeterminada

Puedes crear una política de seguridad predeterminada que se mostrará en cualquier repositorio público de tu organización que no tenga su propia política de seguridad. Para obtener más información, consulta "[Crear un archivo de salud predeterminado para la comunidad](/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)."

{% endif %}

{% ifversion fpt or ghes > 2.22 %}
## Administrar las {% data variables.product.prodname_dependabot_alerts %} y la gráfica de dependencias

Predeterminadamente, {% data variables.product.prodname_dotcom %} detecta vulnerabilidades en repositorios públicos y genera {% data variables.product.prodname_dependabot_alerts %} y una gráfica de dependencias. Puedes habilitar o inhabilitar las {% data variables.product.prodname_dependabot_alerts %} y la gráfica de dependencias para todos los repositorios que pertenezcan a tu organización.

1. Haz clic en tu foto de perfil y luego en **Organizaciones**.
2. Haz clic en **Configuración** junto a tu organización.
3. Haz clic en **Análisis & seguridad**.
4. Haz clic en **Habilitar todo** o en **Inhabilitar todo** junto a la característica que quieras administrar.
5. Opcionalmente, selecciona **Habilitar automáticamente para los repositorios nuevos**.

Para obtener más información, consulta las secciones "[Acerca de las alertas para las dependencias vulnerables](/code-security/supply-chain-security/about-alerts-for-vulnerable-dependencies)," "[Explorar las dependencias de un repositorio](/code-security/supply-chain-security/exploring-the-dependencies-of-a-repository#enabling-and-disabling-the-dependency-graph-for-a-private-repository)," y "[Administrar la configuración de seguridad y análisis para tu organización](/organizations/keeping-your-organization-secure/managing-security-and-analysis-settings-for-your-organization)".

{% endif %}

{% ifversion fpt or ghes > 3.1 %}

## Administrar la revisión de dependencias

La revisión de dependencias te permite visualizar los cambios a las dependencias en las solicitudes de cambios antes de que se fusionen con tus repositorios. La revisión de dependencias se encuentra disponible en todos los repositorios públicos y en aquellos que pertenecen a organizaciones con una licencia de {% data variables.product.prodname_advanced_security %} y que tengan habilitada la gráfica de dependencias. Para obtener más información, consulta la sección "[Acerca de la revisión de dependencias](/code-security/supply-chain-security/understanding-your-software-supply-chain/about-dependency-review)".

{% endif %}

{% ifversion fpt %}
## Administrar las {% data variables.product.prodname_dependabot_security_updates %}

En el caso de cualquier repositorio que utilice las {% data variables.product.prodname_dependabot_alerts %}, puedes habilitar las {% data variables.product.prodname_dependabot_security_updates %} para levantar solicitudes de cambio con actualizaciones de seguridad cuando se detectan las vulnerabilidades. También puedes habilitar o inhabilitar las {% data variables.product.prodname_dependabot_security_updates %} para todos los repositorios a lo largo de tu organización.

1. Haz clic en tu foto de perfil y luego en **Organizaciones**.
2. Haz clic en **Configuración** junto a tu organización.
3. Haz clic en **Análisis & seguridad**.
4. Haz clic en **Habilitar todas** or en **Inhabilitar todas** junto a {% data variables.product.prodname_dependabot_security_updates %}.
5. Opcionalmente, selecciona **Habilitar automáticamente para los repositorios nuevos**.

Para obtener más información, consulta las secciones "[Acerca de {% data variables.product.prodname_dependabot_security_updates %}](/code-security/supply-chain-security/about-dependabot-security-updates)" y "[Administrar la configuración de análisis y seguridad para tu organización](/organizations/keeping-your-organization-secure/managing-security-and-analysis-settings-for-your-organization)".

## Administrar las {% data variables.product.prodname_dependabot_version_updates %}

Puedes habilitar el {% data variables.product.prodname_dependabot %} para levantar automáticamente las solicitudes de cambios para mantener tus dependencias actualizadas. Para obtener más información, consulta la sección "[Acerca de las {% data variables.product.prodname_dependabot_version_updates %}](/code-security/supply-chain-security/about-dependabot-version-updates)".

Para habilitar las {% data variables.product.prodname_dependabot_version_updates %}, debes crear un archivo de configuración *dependabot.yml*. Para obtener más información, consulta la sección "[Habilitar e inhabilitar las actualizaciones de versión](/code-security/supply-chain-security/enabling-and-disabling-version-updates)".

{% endif %}

{% ifversion fpt or ghes > 2.22 or ghae %}
## Admnistrar la {% data variables.product.prodname_GH_advanced_security %}

Si tu organización cuenta con una licencia de {% data variables.product.prodname_advanced_security %}, puedes habilitar o inhabilitar las características de la {% data variables.product.prodname_advanced_security %}.

1. Haz clic en tu foto de perfil y luego en **Organizaciones**.
2. Haz clic en **Configuración** junto a tu organización.
3. Haz clic en **Análisis & seguridad**.
4. Haz clic en **Habilitar todas** or en **Inhabilitar todas** junto a {% data variables.product.prodname_GH_advanced_security %}.
5. Opcionalmente, selecciona **Habilitar automáticamente para los repositorios privados nuevos**.

Para obtener más información, consulta la sección "[Acerca de {% data variables.product.prodname_GH_advanced_security %}](/github/getting-started-with-github/about-github-advanced-security)" y "[Administrar la configuración de análisis y seguridad para tu organización](/organizations/keeping-your-organization-secure/managing-security-and-analysis-settings-for-your-organization)".

## Configurar el {% data variables.product.prodname_secret_scanning %}
{% data variables.product.prodname_secret_scanning_caps %} se encuentra disponible {% ifversion fpt %}para todos los repositorios públicos, y en los repositorios privados que pertenezcan a las organizaciónes con {% else %}si tienes {% endif %}una licencia de {% data variables.product.prodname_advanced_security %}.

Puedes habilitar o inhabilitar el {% data variables.product.prodname_secret_scanning %} para todos los repositorios a lo largo de tu organización que tengan habilitada la {% data variables.product.prodname_advanced_security %}.

1. Haz clic en tu foto de perfil y luego en **Organizaciones**.
2. Haz clic en **Configuración** junto a tu organización.
3. Haz clic en **Análisis & seguridad**.
4. Haz clic en **Habilitar todo** o en **Inhabilitar todo** junto a {% data variables.product.prodname_secret_scanning_caps %} (solo para repositorios de la {% data variables.product.prodname_GH_advanced_security %}).
5. Opcionalmente, selecciona **Habilitar automáticamente para los repositorios privados que se agregan a la {% data variables.product.prodname_advanced_security %}**.

Para obtener más información, consulta la sección "[Administrar la configuración de seguridad y análisis para tu organización](/organizations/keeping-your-organization-secure/managing-security-and-analysis-settings-for-your-organization)".

{% endif %}

## Pasos siguientes
{% ifversion fpt or ghes > 3.1 or ghae-next %}You can view, filter, and sort security alerts for repositories owned by your organization in the security overview. For more information, see "[About the security overview](/code-security/security-overview/about-the-security-overview)."{% endif %}

Puedes ver y administrar las alertas de las características de seguridad para abordar dependencias y vulnerabilidades en tu código. Para obtener más información, consulta las secciones {% ifversion fpt or ghes > 2.22 %} "[Visualizar y actualizar las dependencias vulnerables en tu repositorio](/code-security/supply-chain-security/viewing-and-updating-vulnerable-dependencies-in-your-repository),"{% endif %} {% ifversion fpt %}"[Administrar las solicitudes de cambio para las actualizaciones de dependencias](/code-security/supply-chain-security/managing-pull-requests-for-dependency-updates)," {% endif %}"[Administrar el {% data variables.product.prodname_code_scanning %} para tu repositorio](/code-security/secure-coding/managing-code-scanning-alerts-for-your-repository)," y "[Administrar las alertas desde el {% data variables.product.prodname_secret_scanning %}](/code-security/secret-security/managing-alerts-from-secret-scanning)".

{% ifversion fpt %}Si tienes una vulnerabilidad de seguridad, puedes crear una asesoría de seguridad para debatir y resolver dicha vulnerabilidad en privado. Para obtener más información, consulta las secciones "[Acerca de {% data variables.product.prodname_security_advisories %}](/code-security/security-advisories/about-github-security-advisories)" y "[Crear una asesoría de seguridad](/code-security/security-advisories/creating-a-security-advisory)".
{% endif %}
