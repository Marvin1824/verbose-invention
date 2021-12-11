---
title: Acerca del resumen de seguridad
intro: 'You can view, filter, and sort security alerts for repositories owned by your organization or team in one place: the Security Overview page.'
product: '{% data reusables.gated-features.security-center %}'
redirect_from:
  - /code-security/security-overview/exploring-security-alerts
versions:
  fpt: '*'
  ghes: '>3.1'
  ghae: next
type: how_to
topics:
  - Security overview
  - Advanced Security
  - Alerts
  - Organizations
  - Teams
shortTitle: About security overview
---

{% data reusables.security-center.beta %}

## Acerca del resumen de seguridad

Puedes utilizar el resumen de seguirdad para tener una vista de nivel alto del estado de seguridad de tu organización o para identificar repositorios problemáticos que requieren intervención. A nivel organizacional, el resumen de seguridad muestra seguridad agregada y específica del repositorio para aquellos que pertenezcan a tu organización. A nivel de equipo, el resumen de seguridad muestra la información de seguridad específica del repositorio para aquellos en los que el equipo tenga privilegios de administración. Para obtener más información, consulta la sección "[Administrar el acceso de un equipo a un repositorio organizacional](/organizations/managing-access-to-your-organizations-repositories/managing-team-access-to-an-organization-repository)".

El resumen de seguridad indica si las características de {% ifversion fpt or ghes > 3.1 %}seguridad{% endif %}{% ifversion ghae-next %}{% data variables.product.prodname_GH_advanced_security %}{% endif %}están habilitadas para los repositorios que pertenecen a tu organización y consolidan las alertas para cada característica.{% ifversion fpt or ghes > 3.1 %} Las características de seguridad incluyen aquellas de {% data variables.product.prodname_GH_advanced_security %}, tales como el {% data variables.product.prodname_code_scanning %} y el {% data variables.product.prodname_secret_scanning %}, así como las {% data variables.product.prodname_dependabot_alerts %}.{% endif %} Para obtener más información sobre las características de {% data variables.product.prodname_GH_advanced_security %}, consulta la sección "[Acerca de la {% data variables.product.prodname_GH_advanced_security %}](/get-started/learning-about-github/about-github-advanced-security)".{% ifversion fpt or ghes > 3.1 %} para obtener más información sobre las {% data variables.product.prodname_dependabot_alerts %}, consulta la sección "[Acerca de las alertas para las dependencias vulnerables](/code-security/supply-chain-security/managing-vulnerabilities-in-your-projects-dependencies/about-alerts-for-vulnerable-dependencies#dependabot-alerts-for-vulnerable-dependencies)".{% endif %}

For more information about securing your code at the repository and organization levels, see "[Securing your repository](/code-security/getting-started/securing-your-repository)" and "[Securing your organization](/code-security/getting-started/securing-your-organization)."

En el resumen de seguridad, puedes ver, clasificar y filtrar las alertas para entender los riesgos de seguridad en tu organización y en los repositorios específicos. Puedes aplicar varios filtros para enfocarte en áreas de interés. Por ejemplo, puedes identificar repositorios privados que tengan una gran cantidad de {% data variables.product.prodname_dependabot_alerts %} o repositorios que no tengan alertas del {% data variables.product.prodname_code_scanning %}.

![El resumen de seguridad para una organziación](/assets/images/help/organizations/security-overview.png)

For each repository in the security overview, you will see icons for each type of security feature and how many alerts there are of each type. If a security feature is not enabled for a repository, the icon for that feature will be grayed out.

![Los iconos en el resumen de seguridad](/assets/images/help/organizations/security-overview-icons.png)

| Icono                                                         | Significado                                                                                                                                                                                                                                               |
| ------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| {% octicon "code-square" aria-label="Code scanning alerts" %} | Alertas de {% data variables.product.prodname_code_scanning_capc %}. Para obtener más información, consulta la sección "[Acerca del {% data variables.product.prodname_code_scanning %}](/code-security/secure-coding/about-code-scanning)".          |
| {% octicon "key" aria-label="Secret scanning alerts" %}       | alertas del {% data variables.product.prodname_secret_scanning_caps %}. Para obtener más información, consulta la sección "[Acerca del {% data variables.product.prodname_secret_scanning %}](/code-security/secret-security/about-secret-scanning)". |
| {% octicon "hubot" aria-label="Dependabot alerts" %}          | {% data variables.product.prodname_dependabot_alerts %}. Para obtener más información, consulta la sección "[Acerca de las alertas para las dependencias vulnerables](/code-security/supply-chain-security/about-alerts-for-vulnerable-dependencies)".  |
| {% octicon "check" aria-label="Check" %}                      | The security feature is enabled, but does not raise alerts in this repository.                                                                                                                                                                            |
| {% octicon "x" aria-label="x" %}                              | The security feature is not supported in this repository.                                                                                                                                                                                                 |

Predeterminadamente, los repositorios archivados se excluyen del resumen de seguridad de una organización. Puedes aplicar filtros para ver los repositorios archivados en el resumen de seguridad. Para obtener más información, consulta la sección "[Filtrar la lista de alertas](#filtering-the-list-of-alerts)".

The security overview displays active alerts raised by security features. Si no hay alertas en el resumen de seguridad de un repositorio, las vulnerabilidades de seguridad no detectadas o los errores de código podrían aún existir.

## Visualizar el resumen de seguridad de una organización

Los propietarios de las organizaciones pueden ver el resumen de seguridad de estas.

{% data reusables.organizations.navigate-to-org %}
{% data reusables.organizations.security-overview %}
1. Para ver la información agregada sobre los tipos de alerta, haz clic en **Mostrar más**. ![Botón de mostrar más](/assets/images/help/organizations/security-overview-show-more-button.png)
{% data reusables.organizations.filter-security-overview %}

## Visualizar el resumen de seguridad de un equipo

Los miembros de un equipo pueden ver el resumen de seguridad de los repositorios para los cuales dicho equipo tiene privilegios administrativos.

{% data reusables.profile.access_org %}
{% data reusables.user_settings.access_org %}
{% data reusables.organizations.specific_team %}
{% data reusables.organizations.team-security-overview %}
{% data reusables.organizations.filter-security-overview %}

## Filtrar la lista de alertas

### Filtrar por nivel de riesgo para los repositorios

The level of risk for a repository is determined by the number and severity of alerts from security features. If one or more security features are not enabled for a repository, the repository will have an unknown level of risk. If a repository has no risks that are detected by security features, the repository will have a clear level of risk.

| Qualifier      | Descripción                                                          |
| -------------- | -------------------------------------------------------------------- |
| `risk:high`    | Muestra los repositorios que tienen un riesgo alto.                  |
| `risk:medium`  | Muestra los repositorios que tienen un riesgo medio.                 |
| `risk:low`     | Muestra los repositorios que tienen un nivel de riesgo bajo.         |
| `risk:unknown` | Muestra los repositorios que tienen un nivel de riesgo desconocido.  |
| `risk:clear`   | Muestra los repositorios que no tienen un nivel de riesgo detectado. |

### Filtra por cantidad de alertas

| Qualifier                 | Descripción                                                                                                                                                                           |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <code>code-scanning-alerts:<em>n</em></code> | Muestra los repositorios que tienen *n* alertas del {% data variables.product.prodname_code_scanning %}. Este calificador puede utilizar los operadores de comparación &gt y &lt.   |
| <code>secret-scanning-alerts:<em>n</em></code> | Muestra los repositorios que tienen *n* alertas del {% data variables.product.prodname_secret_scanning %}. Este calificador puede utilizar los operadores de comparación &gt y &lt. |
| <code>dependabot-alerts:<em>n</em></code> | Muestra los repositorios que tienen *n* {% data variables.product.prodname_dependabot_alerts %}. Este calificador puede utilizar los operadores de comparación &gt y &lt.           |

### Filter by whether security features are enabled

| Qualifier                       | Descripción                                                                                                       |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `enabled:code-scanning`         | Muestra los repositorios que tienen habilitado el {% data variables.product.prodname_code_scanning %}.          |
| `not-enabled:code-scanning`     | Muestra los repositorios que no tienen habilitado el {% data variables.product.prodname_code_scanning %}.       |
| `enabled:secret-scanning`       | Muestra los repositorios que tienen habilitado el {% data variables.product.prodname_secret_scanning %}.        |
| `not-enabled:secret-scanning`   | Muestra los repositorios que tienen habilitado el {% data variables.product.prodname_secret_scanning %}.        |
| `enabled:dependabot-alerts`     | Muestra los repositorios que tienen habilitadas las {% data variables.product.prodname_dependabot_alerts %}.    |
| `not-enabled:dependabot-alerts` | Muestra los repositorios que no tienen habilitadas las {% data variables.product.prodname_dependabot_alerts %}. |

### Filtrar por tipo de repositorio

| Qualifier | Description | | -------- | -------- |{% ifversion fpt or ghes > 3.1 %} | `is:public` | Display public repositories. |{% endif %} | `is:internal` | Display internal repositories. | | `is:private` | Display private repositories. | | `archived:true` | Display archived repositories. |

### Filtrar por equipo

| Qualifier                 | Descripción                                                                        |
| ------------------------- | ---------------------------------------------------------------------------------- |
| <code>team:<em>TEAM-NAME</em></code> | Muestra los repositorios en los que *TEAM-NAME* tiene privilegios administrativos. |

### Filtrar por tema

| Qualifier                 | Descripción                                                  |
| ------------------------- | ------------------------------------------------------------ |
| <code>topic:<em>TOPIC-NAME</em></code> | Muestra los repositorios que se clasifican con *TOPIC-NAME*. |

### Clasifica la lista de alertas

| Qualifier                     | Descripción                                                                                                                                   |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `sort:risk`                   | Clasifica los repositorios por riesgo en tu resumen de seguridad.                                                                             |
| `sort:repos`                  | Clasifica los repositorios en tu resumen de seguridad por órden alfabético de nombre.                                                         |
| `sort:code-scanning-alerts`   | Clasifica los repositorios en tu resumen de seguridad por la cantidad de alertas del {% data variables.product.prodname_code_scanning %}.   |
| `sort:secret-scanning-alerts` | Clasifica los repositorios en tu resumen de seguridad por la cantidad de alertas del {% data variables.product.prodname_secret_scanning %}. |
| `sort:dependabot-alerts`      | Clasifica los repositorios en tu resumen de seguridad por cantidad de {% data variables.product.prodname_dependabot_alerts %}.              |
