---
title: Mejores prácticas para administrar proyectos (beta)
intro: 'Consejos para administrar tus proyectos en {% data variables.product.company_short %}.'
allowTitleToDifferFromFilename: true
miniTocMaxHeadingLevel: 3
versions:
  fpt: '*'
type: overview
topics:
  - Projects
  - Issues
  - Project management
---

{% data reusables.projects.projects-beta %}

Puedes utilizar proyectos para administrar tu trabajo en {% data variables.product.company_short %}, donde viven tus propuestas y solicitudes de cambios. Lee los tips para administrar tus proyectos de forma eficaz y eficiente. Para obtener más información sobre los proyectos, consulta la sección "[Acerca de los proyectos](/issues/trying-out-the-new-projects-experience/about-projects)".

## Desglosa las propuestas grandes en unas más pequeñas

El desglosar una propuesta grande en propuestas más pequeñas hace el trabajo más administrable y habilita a los miembros del equipo para que trabajen en paralelo. Esto también conlleva a tener solicitudes de cambios más pequeñas, las cuales se pueden revisar con mayor facilidad.

Para rastrear cómo las propuestas más pequeñas encajan en una meta más grande, utiliza listas de tareas, hitos o etiquetas. Para obtener más información, consulta las secciones "[Acerca de las listas de tareas](/issues/tracking-your-work-with-issues/creating-issues/about-task-lists)", "[Acerca de los hitos](/issues/using-labels-and-milestones-to-track-work/about-milestones)", y "[Administrar etiquetas](/issues/using-labels-and-milestones-to-track-work/managing-labels)".

## Comunica

Las propuestas y solicitudes de cambio incluyen características integradas que te permiten comunicarte fácilmente con tus colaboradores. Utiliza las @menciones para alertar a una persona o a todo el equipo sobre un comentario. Asigna colaboradores a las propuestas para comunicar las responsabilidades. Enlaza las propuestas o solicitudes de cambio relacionadas para comunicar cómo están conectadas.

## Utiliza las vistas

Utiliza las vistas de proyecto para mirarlo desde diferentes ángulos.

Por ejemplo:

- Filtra por estado para ver los elementos que no se marcaron como favoritos
- Group by a custom priority field to monitor the volume of high priority items
- Ordena por un campo personalizado de fecha para ver los elementos con la fecha de envío destino más cercana

Para obtener más información, consulta la sección "[Personalizar las vistas de tu proyecto](/issues/trying-out-the-new-projects-experience/customizing-your-project-views)".

## Ten una fuente única de la verdad

Para prevenir que la información se desincronice, manten una fuente única de verdad. Por ejemplo, rastrea una fecha de envío destino en una sola ubicación en vez de que se propague a través de campos múltiples. Posteriormente, si la fecha de envío destino cambia, solo necesitas actualizar la fecha en una ubicación.

Los proyectos de {% data variables.product.company_short %} se actualizan automáticamente con los datos de {% data variables.product.company_short %}, tales como los asignados, hitos y etiquetas. Cuando uno de estos campos cambia en una propuesta o solicitud de cambios, este cambio se refleja automáticamente en tu proyecto.

## Utiliza la automatización

Las tareas de auotmatización te permiten pasar menos tiempo trabajando y más en el proyecto mismo. Entre menos tengas que recordar para hacer manualmente, será más probable que tu proyecto se mantenga actualizado. {% data variables.product.prodname_actions %} y la API de GraphQL te permiten automatizar las tareas de administración rutinarias de un proyecto. Por ejemplo, para hacer un seguimiento de las solicitudes de cambios que están esperando una revisión, puedes crear un flujo de trabajo que agregue una solicitud de cambios a un proyecto y configure el estado en "necesita revisión"; este proceso se puede activar automátiamente cuando una solicitud de cambios se marque como "lista para revisión".

- Para encontrar un flujo de trabajo de ejemplo, consulta la sección "[Automatizar proyectos](/issues/trying-out-the-new-projects-experience/automating-projects)".
- Para obtener más información sobre la API, consulta la sección "[Utilizar la API para administrar los proyectos](/issues/trying-out-the-new-projects-experience/using-the-api-to-manage-projects)".
- Para obtener más información acerca de {% data variables.product.prodname_actions %}, consulta la sección "[{% data variables.product.prodname_actions %}](/actions)".
