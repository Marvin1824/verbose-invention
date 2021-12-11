---
title: 使用 Docker 注册表
intro: '{% ifversion fpt %}Docker 注册表现已被 {% data variables.product.prodname_container_registry %} 取代。{% else %}您可以使用 {% data variables.product.prodname_registry %} Docker 注册表推送和拉取您的 Docker 映像，该注册表使用软件包命名空间 `https://docker.pkg.github.com`。{% endif %}'
product: '{% data reusables.gated-features.packages %}'
redirect_from:
  - /articles/configuring-docker-for-use-with-github-package-registry
  - /github/managing-packages-with-github-package-registry/configuring-docker-for-use-with-github-package-registry
  - /github/managing-packages-with-github-packages/configuring-docker-for-use-with-github-packages
  - /packages/using-github-packages-with-your-projects-ecosystem/configuring-docker-for-use-with-github-packages
  - /packages/guides/container-guides-for-github-packages/configuring-docker-for-use-with-github-packages
  - /packages/guides/configuring-docker-for-use-with-github-packages
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
shortTitle: Docker 注册表
---

<!-- Main versioning block. Short page for dotcom -->
{% ifversion fpt %}

{% data variables.product.prodname_dotcom %} 的 Docker 注册表（使用命名空间 `docker.pkg.github.com`）已被 {% data variables.product.prodname_container_registry %} 取代（使用命名空间 `https://ghcr.io`）。 {% data variables.product.prodname_container_registry %} 为 Docker 映像提供粒度权限和存储优化等优点。

先前存储在 Docker 注册表中的 Docker 映像将自动迁移到 {% data variables.product.prodname_container_registry %}。 更多信息请参阅“[从 Docker 注册表迁移到 {% data variables.product.prodname_container_registry %}](/packages/working-with-a-github-packages-registry/migrating-to-the-container-registry-from-the-docker-registry)”和“[使用 {% data variables.product.prodname_container_registry %}](/packages/working-with-a-github-packages-registry/working-with-the-container-registry)”。

{% else %}
<!-- The remainder of this article is displayed for releases that don't support the Container registry -->

{% data reusables.package_registry.packages-ghes-release-stage %}
{% data reusables.package_registry.packages-ghae-release-stage %}

**注：**安装或发布 Docker 映像时，{% data variables.product.prodname_registry %} 当前不支持外部图层，如 Windows 映像。

## 关于 Docker 支持

安装或发布 Docker 映像时，Docker 注册表目前不支持外部层，例如 Windows 映像。

{% ifversion ghes = 2.22 %}

必须在 {% data variables.product.product_location %} 的网站管理员为您的实例启用 Docker 支持和子域隔离后，您才可在 {% data variables.product.prodname_registry %} 上使用 Docker 注册表。 更多信息请参阅“[为企业管理 GitHub Packages](/enterprise/admin/packages)”。

{% endif %}

## 向 {% data variables.product.prodname_registry %} 验证

{% data reusables.package_registry.authenticate-packages %}

{% data reusables.package_registry.authenticate-packages-github-token %}

### 使用个人访问令牌进行身份验证

{% data reusables.package_registry.required-scopes %}

您可以使用 `docker` 登录命令，通过 Docker 向 {% data variables.product.prodname_registry %} 验证。

为确保凭据安全，我们建议您将个人访问令牌保存在您计算机上的本地文件中，然后使用 Docker 的 `--password-stdin` 标志从本地文件读取您的令牌。

{% ifversion fpt %}
{% raw %}
  ```shell
  $ cat <em>~/TOKEN.txt</em> | docker login https://docker.pkg.github.com -u <em>USERNAME</em> --password-stdin
  ```
{% endraw %}
{% endif %}

{% ifversion ghes or ghae %}
{% ifversion ghes > 2.22 %}
有关创建包的更多信息，请参阅 [maven.apache.org 文档](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)。
{% endif %}
{% raw %}
 ```shell
 $ cat <em>~/TOKEN.txt</em> | docker login docker.HOSTNAME -u <em>USERNAME</em> --password-stdin
```
{% endraw %}
{% ifversion ghes > 2.22 %}
例如，*OctodogApp* 和 *OctocatApp* 项目将发布到同一个仓库：

{% raw %}
 ```shell
 $ cat <em>~/TOKEN.txt</em> | docker login <em>HOSTNAME</em> -u <em>USERNAME</em> --password-stdin
```
{% endraw %}
{% endif %}

{% endif %}

要使用此示例登录命令，请将 `USERNAME` 替换为您的 {% data variables.product.product_name %} 用户名{% ifversion ghes or ghae %}，将 `HOSTNAME` 替换为 {% data variables.product.product_location %},{% endif %} 的 URL，并将 `~/TOKEN.txt` 替换为您用于 {% data variables.product.product_name %} 的个人访问令牌的文件路径。

更多信息请参阅“[Docker 登录](https://docs.docker.com/engine/reference/commandline/login/#provide-a-password-using-stdin)”。

## 发布映像

{% data reusables.package_registry.docker_registry_deprecation_status %}

{% note %}

**注：**映像名称只能使用小写字母。

{% endnote %}

{% data variables.product.prodname_registry %} 支持每个仓库的多个顶层 Docker 镜像。 仓库可以拥有任意数量的映像标记。 在发布或安装大于 10GB 的 Docker 映像（每个图层上限为 5GB）时，可能会遇到服务降级的情况。 更多信息请参阅 Docker 文档中的“[Docker 标记](https://docs.docker.com/engine/reference/commandline/tag/)”。

{% data reusables.package_registry.viewing-packages %}

1. 使用 `docker images` 确定 docker 映像的名称和 ID。
  ```shell
  $ docker images
  > <&nbsp>
  > REPOSITORY        TAG        IMAGE ID       CREATED      SIZE
  > <em>IMAGE_NAME</em>        <em>VERSION</em>    <em>IMAGE_ID</em>       4 weeks ago  1.11MB
  ```
2. 使用 Docker 映像 ID、标记和 Docker 映像，将 *OWNER* 替换为拥有仓库的用户或组织帐户的名称，将 *REPOSITORY* 替换为包含项目的仓库的名称，将 *IMAGE_NAME* 替换为包或映像的名称，{% ifversion ghes or ghae %}将 *HOSTNAME* 替换为 {% data variables.product.product_location %} 的主机名，{% endif %}并将 *VERSION* 替换为构建时的包版本。
  {% ifversion fpt %}
  ```shell
  $ docker tag <em>IMAGE_ID</em> docker.pkg.github.com/<em>OWNER/REPOSITORY/IMAGE_NAME:VERSION</em>
  ```
  {% else %}
  {% ifversion ghes > 2.22 %}
  有关创建包的更多信息，请参阅 [maven.apache.org 文档](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)。
  {% endif %}
  ```shell
  如果尚未为包构建 docker 映像，请构建映像，将 <em x-id="3">OWNER</em> 替换为拥有仓库的用户或组织帐户的名称，将 <em x-id="3">REPOSITORY</em> 替换为包含项目的仓库的名称，将 <em x-id="3">IMAGE_NAME</em> 替换为包或映像的名称，将 <em x-id="3">VERSION</em> 替换为构建时的包版本，将 <em x-id="3">PATH</em> 替换为映像路径（如果映像未在当前工作目录中）。
  ```
  {% ifversion ghes > 2.22 %}
  例如，*OctodogApp* 和 *OctocatApp* 项目将发布到同一个仓库：
  ```shell
  $ docker tag <em>IMAGE_ID</em> <em>HOSTNAME/OWNER/REPOSITORY/IMAGE_NAME:VERSION</em>
  ```
  {% endif %}
  {% endif %}
3. 如果尚未为包构建 docker 映像，请构建映像，将 *OWNER* 替换为拥有仓库的用户或组织帐户的名称，将 *REPOSITORY* 替换为包含项目的仓库的名称，将 *IMAGE_NAME* 替换为包或映像的名称，将 *VERSION* 替换为构建时的包版本，{% ifversion ghes or ghae %}将 *HOSTNAME* 替换为 {% data variables.product.product_location %} 的主机名，{% endif %}将 *PATH* 替换为映像路径（如果映像未在当前工作目录中）。
  {% ifversion fpt %}
  ```shell
  $ docker build -t docker.pkg.github.com/<em>OWNER/REPOSITORY/IMAGE_NAME:VERSION</em> <em>PATH</em>
  ```
  {% else %}
  {% ifversion ghes > 2.22 %}
  有关创建包的更多信息，请参阅 [maven.apache.org 文档](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)。
  {% endif %}
  ```shell
  $ docker build -t docker.<em>HOSTNAME/OWNER/REPOSITORY/IMAGE_NAME:VERSION</em> <em>PATH</em>
  ```
  {% ifversion ghes > 2.22 %}
  例如，*OctodogApp* 和 *OctocatApp* 项目将发布到同一个仓库：
  ```shell
  $ docker build -t <em>HOSTNAME/OWNER/REPOSITORY/IMAGE_NAME:VERSION</em> <em>PATH</em>
  ```
  {% endif %}
  {% endif %}
4. 将映像发布到 {% data variables.product.prodname_registry %}。
  {% ifversion fpt %}
  ```shell
  $ docker push docker.pkg.github.com/<em>OWNER/REPOSITORY/IMAGE_NAME:VERSION</em>
  ```
  {% else %}
  {% ifversion ghes > 2.22 %}
  有关创建包的更多信息，请参阅 [maven.apache.org 文档](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)。
  {% endif %}
  ```shell
  $ docker push docker.<em>HOSTNAME/OWNER/REPOSITORY/IMAGE_NAME:VERSION</em>
  ```
  {% ifversion ghes > 2.22 %}
  例如，*OctodogApp* 和 *OctocatApp* 项目将发布到同一个仓库：
  ```shell
  $ docker push <em>HOSTNAME/OWNER/REPOSITORY/IMAGE_NAME:VERSION</em>
  ```
  {% endif %}
  {% endif %}
  {% note %}

  **注：**必须使用 `IMAGE_NAME:VERSION` 推送映像，而不能使用 `IMAGE_NAME:SHA`。

  {% endnote %}

### 发布 Docker 映像的示例

{% ifversion ghes > 2.22 %}
这些示例假设您的实例已启用子域隔离。
{% endif %}

您可以使用映像 ID 将 `monalisa` 映像的 1.0 版本发布到 `octocat/octo-app` 仓库。

{% ifversion fpt %}
```shell
$ docker images

> REPOSITORY           TAG      IMAGE ID      CREATED      SIZE
> monalisa             1.0      c75bebcdd211  4 weeks ago  1.11MB

# Tag the image with <em>OWNER/REPO/IMAGE_NAME</em>
$ docker tag c75bebcdd211 docker.pkg.github.com/octocat/octo-app/monalisa:1.0

# Push the image to {% data variables.product.prodname_registry %}
$ docker push docker.pkg.github.com/octocat/octo-app/monalisa:1.0
```

{% else %}

```shell
$ docker images

> REPOSITORY           TAG      IMAGE ID      CREATED      SIZE
> monalisa             1.0      c75bebcdd211  4 weeks ago  1.11MB

# Tag the image with <em>OWNER/REPO/IMAGE_NAME</em>
$ docker tag c75bebcdd211 docker.<em>HOSTNAME</em>/octocat/octo-app/monalisa:1.0

# Push the image to {% data variables.product.prodname_registry %}
$ docker push docker.<em>HOSTNAME</em>/octocat/octo-app/monalisa:1.0
```

{% endif %}

您可能首次发布新的 Docker 映像并将其命名为 `monalisa`。

{% ifversion fpt %}
```shell
# Build the image with docker.pkg.github.com/<em>OWNER/REPOSITORY/IMAGE_NAME:VERSION</em>
# Assumes Dockerfile resides in the current working directory (.)
$ docker build -t docker.pkg.github.com/octocat/octo-app/monalisa:1.0 .

# Push the image to {% data variables.product.prodname_registry %}
$ docker push docker.pkg.github.com/octocat/octo-app/monalisa:1.0
```

{% else %}
```shell
# Build the image with docker.<em>HOSTNAME/OWNER/REPOSITORY/IMAGE_NAME:VERSION</em>
# Assumes Dockerfile resides in the current working directory (.)
$ docker build -t docker.<em>HOSTNAME</em>/octocat/octo-app/monalisa:1.0 .

# Push the image to {% data variables.product.prodname_registry %}
$ docker push docker.<em>HOSTNAME</em>/octocat/octo-app/monalisa:1.0
```
{% endif %}

## 下载映像

{% data reusables.package_registry.docker_registry_deprecation_status %}

您可以使用 `docker pull` 命令从 {% data variables.product.prodname_registry %} 安装 Docker 映像，将 *OWNER* 替换为拥有仓库的用户或组织帐户的名称，将 *REPOSITORY* 替换为包含项目的仓库的名称，将 *IMAGE_NAME* 替换为包或映像的名称，{% ifversion ghes or ghae %}将*HOSTNAME* 替换为 {% data variables.product.product_location %} 的名称，{% endif %}将 *TAG_NAME* 替换为要安装的映像的标记。

{% ifversion fpt %}
```shell
$ docker pull docker.pkg.github.com/<em>OWNER/REPOSITORY/IMAGE_NAME:TAG_NAME</em>
```
{% else %}
<!--Versioning out this "subdomain isolation enabled" line because it's the only option for GHES 2.22 so it can be misleading.-->
{% ifversion ghes > 2.22 %}
有关创建包的更多信息，请参阅 [maven.apache.org 文档](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)。
{% endif %}
```shell
$ docker pull docker.<em>HOSTNAME/OWNER/REPOSITORY/IMAGE_NAME:TAG_NAME</em>
```
{% ifversion ghes > 2.22 %}
例如，*OctodogApp* 和 *OctocatApp* 项目将发布到同一个仓库：
```shell
$ docker pull <em>HOSTNAME/OWNER/REPOSITORY/IMAGE_NAME:TAG_NAME</em>
```
{% endif %}
{% endif %}

{% note %}

**注：**必须使用 `IMAGE_NAME:VERSION` 推送映像，而不能使用 `IMAGE_NAME:SHA`。

{% endnote %}

## 延伸阅读

- "{% ifversion fpt or ghes > 3.0 %}[删除和恢复包](/packages/learn-github-packages/deleting-and-restoring-a-package){% elsif ghes < 3.1 or ghae %}[删除包](/packages/learn-github-packages/deleting-a-package){% endif %}"

{% endif %}  <!-- End of main versioning block -->
