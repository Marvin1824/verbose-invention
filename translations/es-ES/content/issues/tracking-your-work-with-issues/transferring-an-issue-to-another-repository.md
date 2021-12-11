---
title: Transferir una propuesta a otro repositorio
intro: 'Para mover una propuesta a un repositorio al que mejor se ajuste, puedes transferir propuestas abiertas a otros repositorios.'
redirect_from:
  - /github/managing-your-work-on-github/managing-your-work-with-issues-and-pull-requests/transferring-an-issue-to-another-repository
  - /articles/transferring-an-issue-to-another-repository
  - /github/managing-your-work-on-github/transferring-an-issue-to-another-repository
  - /issues/tracking-your-work-with-issues/managing-issues/transferring-an-issue-to-another-repository
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
topics:
  - Pull requests
shortTitle: Transferir una propuesta
---

Para transferir una propuesta abierta a otro repositorio, debes tener permisos de escritura sobre el repositorio en el que está la propuesta y sobre el repositorio al que le estás transfiriendo la propuesta. Para obtener más información, consulta "[Niveles de permiso del repositorio para una organización](/articles/permission-levels-for-an-organization)".

Solo puedes transferir propuestas entre repositorios que son propiedad del mismo usuario o de la misma cuenta de la organización. {% ifversion fpt or ghes %}No puedes transferir una propuesta desde un repositorio privado hacia un repositorio público.{% endif %}

Cuando transfieres un informe de problemas, se retendrá tanto los comentarios como las personas asignadas. No se retendrán los hitos y etiquetas de la propuesta. Esta propuesta se mantendrá en cualquier tablero de proyecto que pertenezca al usuario o que se encuentre en la organización y se eliminará de cualquier tablero de proyecto de los repositorios. Para obtener más información, consulta "[Acerca de los tableros de proyectos](/articles/about-project-boards)."

Las personas o equipos que se mencionan en la propuesta recibirán una notificación que les haga saber que la propuesta se transfirió a un repositorio nuevo. La URL original se redirige a la URL nueva de la propuesta. Las personas que no tengan permisos de lectura en el repositorio nuevo verán un anuncio que les hará saber que la propuesta se transfirió a un repositorio nuevo al que no pueden acceder.

## Transferir una propuesta abierta a otro repositorio

{% include tool-switcher %}

{% webui %}

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.sidebar-issues %}
3. En la lista de propuestas, haz clic en la propuesta que quieres transferir.
4. En la barra lateral derecha, haz clic en **Transfer issue** (Transferir propuesta). ![Botón para transferir propuesta](/assets/images/help/repository/transfer-issue.png)
5. Utiliza el menú desplegable **Choose a repository** (Elegir un repositorio) y selecciona el repositorio al que quieres transferir la propuesta. ![Elige una selección de repositorio](/assets/images/help/repository/choose-a-repository.png)
6. Haz clic en **Transfer issue** (Transferir propuesta). ![Botón Transfer issue (Transferir propuesta)](/assets/images/help/repository/transfer-issue-button.png)

{% endwebui %}

{% cli %}

{% data reusables.cli.cli-learn-more %}

To transfer an issue, use the `gh issue transfer` subcommand. Replace the `issue` parameter with the number or URL of the issue. Replace the `{% ifversion ghes %}hostname/{% endif %}owner/repo` parameter with the {% ifversion ghes %}URL{% else %}name{% endif %} of the repository that you want to transfer the issue to, such as `{% ifversion ghes %}https://ghe.io/{% endif %}octocat/octo-repo`.

```shell
gh issue transfer <em>issue</em> <em>{% ifversion ghes %}hostname/{% endif %}owner/repo</em>
```

{% endcli %}

## Leer más

- "[Acerca de las propuestas](/articles/about-issues)"
- "[Revisar tu registro de seguridad](/articles/reviewing-your-security-log)"
- "[Revisar el registro de auditoría para tu organización](/articles/reviewing-the-audit-log-for-your-organization)"
