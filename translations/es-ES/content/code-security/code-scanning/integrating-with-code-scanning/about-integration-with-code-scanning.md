---
title: Acerca de la integración con el escaneo de código
shortTitle: Acerca de la integración
intro: 'Puedes llevar a cabo un {% data variables.product.prodname_code_scanning %} externamente y luego mostrar los resultados en {% data variables.product.prodname_dotcom %}, o configurar webhooks que escuchen a la actividad de {% data variables.product.prodname_code_scanning %} en tu repositorio.'
product: '{% data reusables.gated-features.code-scanning %}'
redirect_from:
  - /github/finding-security-vulnerabilities-and-errors-in-your-code/about-integration-with-code-scanning
  - /code-security/secure-coding/about-integration-with-code-scanning
  - /code-security/secure-coding/integrating-with-code-scanning/about-integration-with-code-scanning
versions:
  fpt: '*'
  ghes: '>=3.0'
  ghae: '*'
type: overview
topics:
  - Advanced Security
  - Code scanning
  - Webhooks
  - Integration
---

<!--For this article in earlier GHES versions, see /content/github/finding-security-vulnerabilities-and-errors-in-your-code-->

{% data reusables.code-scanning.beta %}
{% data reusables.code-scanning.enterprise-enable-code-scanning %}

Como alternativa a ejecutar un {% data variables.product.prodname_code_scanning %} dentro de {% data variables.product.prodname_dotcom %}, puedes realizar el análisis en cualquier otra parte y luego cargar los resultados. Las alertas para {% data variables.product.prodname_code_scanning %} que puedes ejecutar externamente se muestran de la misma forma que aquellas para el {% data variables.product.prodname_code_scanning %} que ejecutas con {% data variables.product.prodname_dotcom %}. Para obtener más información, consulta la sección "[Administrar las alertas de {% data variables.product.prodname_code_scanning %} para tu repositorio](/code-security/secure-coding/managing-code-scanning-alerts-for-your-repository)".

Si utilizas una herramienta de análisis estático de terceros que pueda producir resultados como datos del Formato de Intercambio de Resultados para Análisis Estático (SARIF) 2.1.0, puedes cargarlos a {% data variables.product.prodname_dotcom %}. Para obtener más información, consulta la sección "[Cargar un archivo SARIF a GitHub](/code-security/secure-coding/uploading-a-sarif-file-to-github)".

## Integraciones con webhooks

You can use {% data variables.product.prodname_code_scanning %} webhooks to build or set up integrations, such as [{% data variables.product.prodname_github_apps %}](/apps/building-github-apps/) or [{% data variables.product.prodname_oauth_apps %}](/apps/building-oauth-apps/), that subscribe to {% data variables.product.prodname_code_scanning %} events in your repository. Por ejemplo, puedes crear una integración que cree una propuesta en {% data variables.product.product_name %} o que te envíe una notificación de Slack cuando se agregue una alerta de {% data variables.product.prodname_code_scanning %} en tu repositorio. Para obtener más información, consulta las secciones "[Crear webhooks](/developers/webhooks-and-events/creating-webhooks)" y "[Eventos de webhook y cargas útiles](/developers/webhooks-and-events/webhook-events-and-payloads#code_scanning_alert)".

## Leer más

* "[Acerca del {% data variables.product.prodname_code_scanning %}](/code-security/secure-coding/about-code-scanning)"
* "[Utilizar el {% data variables.product.prodname_code_scanning %} de {% data variables.product.prodname_codeql %} con tu sistema de IC existente](/code-security/secure-coding/using-codeql-code-scanning-with-your-existing-ci-system)"
* "[Soporte de SARIF para {% data variables.product.prodname_code_scanning %}](/code-security/secure-coding/sarif-support-for-code-scanning)"
