---
title: Personalizar las vistas de tu proyecto (beta)
intro: 'Muestra la información que necesitas cambiando el diseño, agrupamiento, forma de ordenar y los filtros de tu proyecto.'
allowTitleToDifferFromFilename: true
versions:
  fpt: '*'
type: reference
topics:
  - Projects
---

{% data reusables.projects.projects-beta %}

## Paleta de comandos

Utiliza la paleta de comandos para cambiar rápidamente la configuración y ejecutar comandos en tu proyecto.

1. {% data reusables.projects.open-command-palette %}
2. Comienza a teclear cualquier parte de un comando o navega a través de la ventana de la paleta de comandos para encontrarlo. Consulta las siguientes secciones para encontrar más ejemplos de comandos.

## Cambiar el diseño

Puedes ver tu proyecto como una tabla o como un tablero.

1. {% data reusables.projects.open-command-palette %}
2. Comienza a teclear "Switch layout".
3. Selecciona el comando deseado (por ejemplo: "Switch layout: Table").
3. Como alternativa, selecciona el menú desplegable junto a un nombre de vista y haz clic en**Tabla** o en **Tablero**.

## Mostrar u ocultar los campos

En el diseño de la tabla, puedes mostrar u ocultar un campo específico.

1. {% data reusables.projects.open-command-palette %}
2. Comienza a teclear la acción que quieres tomar ("show" o "hide") o el nombre del campo.
3. Selecciona el comando deseado (por ejemplo: "Show: Milestone").
4. Como alternativa, haz clic en {% octicon "plus" aria-label="the plus icon" %} a la derecha de la tabla. En el menú desplegable que se muestra, indica qué campos mostrar u ocultar. Un {% octicon "check" aria-label="check icon" %} indica qué campos se muestran.
5. Como alternativa, selecciona el menú desplegable junto al nombre del campo y haz clic en **Esconder campo**.

## Reordenar campos

Puedes cambiar el orden de los campos.

1. Haz clic en el encabezado del campo.
2. A la par que haces clic, arrastra el campo a la ubicación deseada.

## Reordenar filas

En el diseño de tabla, puedes cambiar el orden de las filas.

1. Haz clic en el número al inicio de la fila.
2. A la par que haces clic, arrastra la fila a la ubicación deseada.

## Clasificar

En el diseño de tabla, puedes organizar los elementos por valor de campo.

1. {% data reusables.projects.open-command-palette %}
2. Comienza a teclear "Sort by" o el nombre del campo por el cual quieras ordenar.
3. Selecciona el comando deseado (por ejemplo: "Ordenar por: Asignados, asc").
4. Como alternativa, selecciona el menú desplegable junto al nombre del campo que quieres ordenar y haz clic en **Ordenar ascendentemente** u **Ordenar descendientemente**.

{% note %}

**Nota:** Cuando se ordena una tabla, no puedes reordenar las filas manualmente.

{% endnote %}

Sigue pasos similares para eliminar una clasificación.

1. {% data reusables.projects.open-command-palette %}
2. Comienza a teclear "Remove sort-by".
3. Selecciona el comando "Remove sort-by".
4. Como alternativa, selecciona el menú desplegable junto al nombre de la vista y haz clic en el elemento de menú que indique a clasificación actual.

## Grupo

In the table layout, you can group items by a custom field value. Cuando los elementos se agrupan, si arrastras un elemento a un grupo nuevo, se aplica el valor de este grupo. Por ejemplo, si agrupas por `Status` y luego arrastras un elemento con un estado a `In progress` hacia el grupo `Done`, el estado del elemento cambiará a `Done`.

{% note %}

**Note:** Currently, you cannot group by title, assignees, repository or labels.

{% endnote %}

1. {% data reusables.projects.open-command-palette %}
2. Comienza a teclear "Group by" o el nombre del campo por el cual quieres agrupar.
3. Selecciona el comando deseado (por ejemplo "Group by: Status").
4. Como alternativa, selecciona el menú desplegable junto al nombre de campo por el cual quieras agrupar y haz clic en **Agrupar por valores**.

Sigue pasos similares para eliminar un agrupamiento.

1. {% data reusables.projects.open-command-palette %}
2. Comienza a teclear "Remove group-by".
3. Selecciona el comando "Remove group-by".
4. Como alternativa, selecciona un menú descendente para ver el nombre y haz clic en el elemento del menú que indica el agrupamiento actual.

## Filtrar

En el diseño de tabla, puedes filtrar por valores de campo.

1. {% data reusables.projects.open-command-palette %}
2. Comienza a teclear "Filter by" o el nombre del campo por el cual quieres filtrar.
3. Selecciona el comando deseado (por ejemplo "filter by Status").
4. Ingresa el valor por el cual quieras filtrar (por ejemplo: "In progress"). You can also filter for the absence of specific values (for example: "Exclude status") or the absence of all values (for example: "No status").
5. Como alternativa, haz clic en {% octicon "search" aria-label="the search icon" %} en la parte superior de la tabla para mostrar la barra de "Filtrar por palabra clave o campo". Ingresa el nombre de campo y el valor por el cual quieras filtrar. Conforme teclees, se mostrarán los posibles valores.

   To filter for multiple values, separate the values with a comma. For example `label:"good first issue",bug` will list all issues with a label `good first issue` or `bug`.

   To filter for the absence of a specific value, place `-` before your filter. For example, `-label:"bug"` will only show items that do not have the label `bug`.

   To filter for the absence of all values, enter `no:` followed by the field name. For example, `no:assignee` will only show items that do not have an assignee.

   Separa los filtros múltiples con un espacio. For example, `status:"In progress" -label:"bug" no:assignee` will show only items that have a status of `In progress`, do not have the label `bug`, and do not have an assignee.
6. Alternatively, select the drop-down menu next to the view name and click the menu item that indicates the desired filter.

## Guardar vistas

Las vistas guardadas te permiten ver rápidamente los aspectos específicos de tu proyecto. Por ejemplo, puedes tener lo siguiente:
- una vista que muestre todos los elementos sin comenzar (filtrar por "Status").
- una vista que muestre la carga de trabajo para cada miembro del equipo (agrupar por "Asignee" y filtrar por "Status").
- una vista que muestre los elementos con la fecha de envío destino más cercana (agrupar por el campo de fecha).

Los siguientes pasos demuestran cómo agregar una vista nueva:

1. {% data reusables.projects.open-command-palette %}
2. Comienza a teclear "New view" (para crear una vista nueva) o "Duplicate view" (para duplicar la vista actual).
3. Selecciona el comando deseado.
4. Como alternativa, haz clic en {% octicon "plus" aria-label="the plus icon" %} **Vista nueva** junto a la vista que está más hacia la derecha.
5. Como alternativa, selecciona el menú desplegable junto a un nombre de vista y haz clic en **Duplicar vista**.

Cuando hagas cambios a una vista, se mostrará un punto junto al nombre de vista para indicar que dicha vista se modificó. Si no quieres guardar los cambios, puedes ignorar este indicador. Para guardar la vista de todos los miembros del proyecto:

1. {% data reusables.projects.open-command-palette %}
1. Comienza a teclear "Save view" o "Save changes to new view".
1. Selecciona el comando deseado.
1. Como alternativa, selecciona el menú desplegable junto a un nombre de vista y haz clic en **Guardar vista** o en **Guardar los cambios a la vista nueva**.

Para renombrar una vista, haz doble clic en el nombre de vista y teclea el nombre deseado.

Para borrar una vista:

1. {% data reusables.projects.open-command-palette %}
2. Comienza a teclear "Delete view".
3. Selecciona el comando deseado.
4. Como alternativa, selecciona el menú desplegable junto a un nombre de vista y haz clic en **Borrar vista**.

## Leer más

- "[Acerca de los proyectos (beta)](/issues/trying-out-the-new-projects-experience/about-projects)
- "[Crear un proyecto (beta)](/issues/trying-out-the-new-projects-experience/creating-a-project)
