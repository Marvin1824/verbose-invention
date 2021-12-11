---
title: About large files on GitHub
intro: '{% data variables.product.product_name %} limits the size of files you can track in regular Git repositories. Learn how to track or remove files that are beyond the limit.'
redirect_from:
  - /articles/distributing-large-binaries
  - /github/managing-large-files/distributing-large-binaries
  - /github/managing-large-files/working-with-large-files/distributing-large-binaries
  - /articles/removing-files-from-a-repository-s-history
  - /articles/removing-files-from-a-repositorys-history
  - /github/managing-large-files/removing-files-from-a-repositorys-history
  - /github/managing-large-files/working-with-large-files/removing-files-from-a-repositorys-history
  - /articles/conditions-for-large-files
  - /github/managing-large-files/conditions-for-large-files
  - /github/managing-large-files/working-with-large-files/conditions-for-large-files
  - /articles/what-is-the-size-limit-for-a-repository/
  - /articles/what-is-my-disk-quota
  - /github/managing-large-files/what-is-my-disk-quota
  - /github/managing-large-files/working-with-large-files/what-is-my-disk-quota
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
shortTitle: Large files
---

## About size limits on {% data variables.product.product_name %}

{% ifversion fpt %}
{% data variables.product.product_name %} intenta proporcionar almacenamiento abundante para todos los repositorios de Git, aunque existen límites físicos para los tamaños de los archivos y repositorios. Para garantizar el rendimiento y la legibilidad para nuestros usuarios, monitoreamos activamente las señales de la salud general de los repositorios. La salud de los repositorios es una función de varios factores de interacción, incluyendo el tamaño, frecuencia de confirmaciones y estructura.

### File size limits
{% endif %}

{% data variables.product.product_name %} limits the size of files allowed in repositories. Recibirás una advertencia de Git si intentas añadir o actualizar un archivo mayor a {% data variables.large_files.warning_size %}. Los cambios aún se subirán a tu repositorio, pero puedes considerar eliminar la confirmación para minimizar el impacto en el rendimiento. Para obtener información, consulta [Eliminar archivos del historial de un repositorio](#removing-files-from-a-repositorys-history)"

{% note %}

**Nota:** si agregas un archivo a un repositorio por medio de un navegador, el archivo no puede ser mayor de {% data variables.large_files.max_github_browser_size %}. Para obtener más información, consulta la sección "[Agregar un archivo a un repositorio](/repositories/working-with-files/managing-files/adding-a-file-to-a-repository)."

{% endnote %}

{% ifversion ghes %}Predeterminadamente, {% endif %}{% data variables.product.product_name %} bloquea las subidas que excedan {% data variables.large_files.max_github_size %}. {% ifversion ghes %}Sin embargo, un administrador de sitio puede configurar un límite diferente para {% data variables.product.product_location %}.  For more information, see "[Setting Git push limits](/enterprise/{{ currentVersion }}/admin/guides/installation/setting-git-push-limits)."{% endif %}

To track files beyond this limit, you must use {% data variables.large_files.product_name_long %} ({% data variables.large_files.product_name_short %}). Para obtener más información, consulta la sección "[Acerca de {% data variables.large_files.product_name_long %}](/repositories/working-with-files/managing-large-files/about-git-large-file-storage)".

If you need to distribute large files within your repository, you can create releases on {% data variables.product.product_location %} instead of tracking the files. Para obtener más información, consulta la sección "[Distribuir archivos binarios grandes](#distributing-large-binaries)".

Git is not designed to handle large SQL files. Para compartir bases de datos grandes con otros desarrolladores, te recomendamos utilizar [Dropbox](https://www.dropbox.com/).

{% ifversion fpt %}
### Repository size limits

Te recomendamos que los repositorios sean siempre pequeños, idealmente, de menos de 1 GB, y se recomienda ampliamente que sean de menos de 5GB. Los repositorios más pequeños se clonan más rápido y se puede mantenerlos mejor y trabajar en ellos más fácilmente. Si tu repositorio impacta excesivamente nuestra infraestructura, puede que recibas un mensaje de correo electrónico de {% data variables.contact.github_support %}, el cual te solicitará que tomes acciones correctivas. Intentamos ser flexibles, especialmente con proyectos grandes que tienen muchos colaboradores, y trabajaremos junto contigo para encontrar una resolución cada que sea posible. Puedes prevenir que tu repositorio impacte nuestra infraestructura si administras el tamaño de tu repositorio y su salud general con eficacia. Puedes encontrar consejos y una herramienta para análisis de repositorios en el repositorio [`github/git-sizer`](https://github.com/github/git-sizer).

Las dependencias externas pueden causar que los repositorios de Git se hagan muy grandes. Para evitar llenar un repositorio con dependencias externas, te recomendamos utilizar un administrador de paquetes. Los administradores de paquetes populares para lenguajes (de programación) comunes incluyen a [Bundler](http://bundler.io/), [Node's Package Manager](http://npmjs.org/), y [Maven](http://maven.apache.org/). Estos administradores de paquetes soportan la utilización directa de repositorios de Git para que no dependas de fuentes pre-empacadas.

Git no está diseñado para fungir como una herramienta de respaldo. Sin embargo, existen muchas soluciones diseñadas específicamente para realizar respaldos, tales como [Arq](https://www.arqbackup.com/), [Carbonite](http://www.carbonite.com/), y [CrashPlan](https://www.crashplan.com/en-us/).
{% endif %}

## Eliminar archivos del historial de un repositorio

{% warning %}

**Advertencia**: Estos procedimientos eliminarán archivos de manera permanente del repositorio de tu computadora y de {% data variables.product.product_location %}. Si el archivo es importante, haz una copia de seguridad local en un directorio por fuera del repositorio.

{% endwarning %}

### Eliminar un archivo agregado en la confirmación más reciente no subida

Si el archivo se agregó con tu confirmación más reciente, y no lo subiste a {% data variables.product.product_location %}, puedes eliminar el archivo y modificar la confirmación:

{% data reusables.command_line.open_the_multi_os_terminal %}
{% data reusables.command_line.switching_directories_procedural %}
3. Para eliminar el archivo, ingresa a `git rm --cached`:
  ```shell
  $ git rm --cached <em>giant_file</em>
  # Stage our giant file for removal, but leave it on disk
  ```
4. Confirma este cambio usando `--amend -CHEAD`:
  ```shell
  $ git commit --amend -CHEAD
  # Amend the previous commit with your change
  # Simply making a new commit won't work, as you need
  # to remove the file from the unpushed history as well
  ```
5. Sube tus confirmaciones a {% data variables.product.product_location %}:
  ```shell
  $ git push
  # Push our rewritten, smaller commit
  ```

### Eliminar un archivo que se añadió en una confirmación de cambios previa

Si añadiste un archivo en una confirmación previa, necesitas eliminarlo del historial del repositorio. Para eliminar archivos de la historia del repositorio, puedes utilizar BFG Repo-Cleaner o el comando `git filter-branch`. Para obtener más información, consulta la sección "[Eliminar datos sensibles de un repositorio](/github/authenticating-to-github/removing-sensitive-data-from-a-repository)".

## Distribuir binarios grandes

Si necesitas distribuir archivos grandes dentro de tu repositorio, puedes crear lanzamientos en {% data variables.product.product_location %}. Los lanzamientos te permiten empaquetar el software, notas de lanzamiento y enlaces a los archivos binarios para que otras personas puedan utilizarlos. Para obtener más información, consulta la sección "[Acerca de los lanzamientos](/github/administering-a-repository/about-releases)".

{% ifversion fpt %}

No limitamos el tamaño total de los archivos binarios en los lanzamientos o anchos de banda que se utilizan para entregarlos. Sin embargo, cada archivo individual debe ser menor a {% data variables.large_files.max_lfs_size %}.

{% endif %}

