---
title: Entender las conexiones entre repositorios
intro: You can better understand the connections that exist between repositories by viewing a repository's network and forks and the projects that depend on the repository.
redirect_from:
  - /articles/viewing-a-repository-s-network
  - /articles/viewing-a-repositorys-network
  - /github/visualizing-repository-data-with-graphs/viewing-a-repositorys-network
  - /articles/understanding-connections-between-repositories
  - /articles/listing-the-forks-of-a-repository
  - /github/visualizing-repository-data-with-graphs/listing-the-forks-of-a-repository
  - /github/visualizing-repository-data-with-graphs/viewing-the-dependencies-of-a-repository
  - /github/visualizing-repository-data-with-graphs/understanding-connections-between-repositories
  - /github/visualizing-repository-data-with-graphs/understanding-connections-between-repositories/viewing-a-repositorys-network
  - /github/visualizing-repository-data-with-graphs/understanding-connections-between-repositories/listing-the-forks-of-a-repository
  - /github/visualizing-repository-data-with-graphs/understanding-connections-between-repositories/viewing-the-dependencies-of-a-repository
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
topics:
  - Repositories
shortTitle: Connections between repositories
---

## Ver la red de un repositorio

'The network graph displays the branch history of the entire repository network, including branches of the root repository and branches of forks that contain commits unique to the network.' product: '{% data reusables.gated-features.repository-insights %}'

![Gráfico de red del repositorio](/assets/images/help/graphs/repo_network_graph.png)

{% tip %}

**Sugerencia:** para ver ramas antiguas, haz clic y arrastra dentro del gráfico.

{% endtip %}

## Acceder al gráfico de la red

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.accessing-repository-graphs %}
3. En la barra lateral izquierda, haz clic en **Network (Red)**. ![Pestaña de red](/assets/images/help/graphs/network_tab.png)

## Detallar las bifurcaciones de un repositorio

El Gráfico de miembros muestra todas las bifurcaciones de un repositorio.

Las bifurcaciones se detallan alfabéticamente por el nombre de usuario de la persona que bifurcó el repositorio. Puedes hacer clic en el nombre de usuario para ser redirigido a la página de perfil del usuario {% data variables.product.product_name %} o hacer clic en el nombre de la bifurcación para ser redirigido a la bifurcación específica del repositorio.

{% ifversion fpt %}

![Gráfico de miembros del repositorio](/assets/images/help/graphs/repo_forks_graph_dotcom.png)

{% else %}

![Gráfico de miembros del repositorio](/assets/images/help/graphs/repo_members_graph.png)

{% endif %}

### Acceder al Gráfico de miembros

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.accessing-repository-graphs %}
3. En la barra lateral izquierda, haz clic en **Forks** (Bifurcaciones). ![Pestaña Forks (Bifurcaciones)](/assets/images/help/graphs/graphs-sidebar-forks-tab.png)

{% ifversion fpt or ghes > 2.22 %}
## Visualizar las dependencias de un repositorio

Puedes utilizar la gráfica de dependencias para explorar el código del cual depende tu repositorio.

Casi todo el software depende de el código que otros desarrolladores mantienen y desarrollan, a menudo conocido como una cadena de suministro. Por ejemplo, las utilidades, bibliotecas y marcos de trabajo. Estas dependencias son una parte integral de tu código y cualquier error o vulnerabilidad en ellos podría afectar tu código. Es importante revisar y mantener estas dependencias.

La gráfica de dependencias proporciona una forma genial de visualizar y explorar las depdendencias para un repositorio. Para obtener más información, consulta las secciones "[Acerca de la gráfica de dependencias](/code-security/supply-chain-security/about-the-dependency-graph)" y "[Explorar las dependencias de un repositorio](/code-security/supply-chain-security/exploring-the-dependencies-of-a-repository)".

También puedes configurar tu repositorio para que {% data variables.product.company_short %} te alerte automáticamente en cualquier momento en el que se encuentre una vulnerabilidad de seguridad en alguna de tus dependencias. Para obtener más información, consulta la sección "[Acerca de las alertas para las dependencias vulnerables](/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)".
{% endif %}
