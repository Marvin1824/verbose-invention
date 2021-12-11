---
title: 仓库
intro: '仓库 API 允许创建、管理以及控制公共和私有 {% data variables.product.product_name %} 仓库的工作流程。'
allowTitleToDifferFromFilename: true
redirect_from:
  - /v3/repos
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
topics:
  - API
miniTocMaxHeadingLevel: 3
---

{% for operation in currentRestOperations %}
  {% unless operation.subcategory %}{% include rest_operation %}{% endunless %}
{% endfor %}

{% ifversion fpt %}
## Autolinks

{% tip %}

**Note:** The Autolinks API is in beta and may change.

{% endtip %}

To help streamline your workflow, you can use the API to add autolinks to external resources like JIRA issues and Zendesk tickets. For more information, see "[Configuring autolinks to reference external resources](/github/administering-a-repository/configuring-autolinks-to-reference-external-resources)."

{% data variables.product.prodname_github_apps %} require repository administration permissions with read or write access to use the Autolinks API.

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'autolinks' %}{% include rest_operation %}{% endif %}
{% endfor %}
{% endif %}

## 分支

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'branches' %}{% include rest_operation %}{% endif %}
{% endfor %}

## 协作者

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'collaborators' %}{% include rest_operation %}{% endif %}
{% endfor %}

## 评论

### 提交评论的自定义媒体类型

以下是提交评论支持的媒体类型。 You can read more about the use of media types in the API [here](/rest/overview/media-types).

    application/vnd.github-commitcomment.raw+json
    application/vnd.github-commitcomment.text+json
    application/vnd.github-commitcomment.html+json
    application/vnd.github-commitcomment.full+json

更多信息请参阅“[自定义媒体类型](/rest/overview/media-types)”。

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'comments' %}{% include rest_operation %}{% endif %}
{% endfor %}

## 提交

仓库提交 API 支持列出、查看和比较仓库中的提交。

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'commits' %}{% include rest_operation %}{% endif %}
{% endfor %}

{% ifversion fpt %}
## 社区

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'community' %}{% include rest_operation %}{% endif %}
{% endfor %}

{% endif %}

## 内容

此 API 端点允许您在仓库中创建、修改和删除 Base64 编码的内容。 要请求原始格式或渲染的 HTML（如果支持），请对仓库内容使用自定义媒体类型。

### 仓库内容的自定义媒体类型

[READMEs](/rest/reference/repos#get-a-repository-readme), [files](/rest/reference/repos#get-repository-content), and [symlinks](/rest/reference/repos#get-repository-content) support the following custom media types:

    application/vnd.github.VERSION.raw
    application/vnd.github.VERSION.html

使用 `.raw` 媒体类型检索文件内容。

对于 Markdown 或 AsciiDoc 等标记文件，您可以使用 `.html` 媒体类型检索渲染的 HTML。 使用我们的开源[标记库](https://github.com/github/markup)将标记语言渲染为 HTML。

[All objects](/rest/reference/repos#get-repository-content) support the following custom media type:

    application/vnd.github.VERSION.object

使用 `object` 媒体类型参数以一致的对象格式检索内容，而不考虑内容类型。 例如，响应将是包含对象数组的 `entries` 属性的对象，而不是目录的对象数组。

您可以在[此处](/rest/overview/media-types)阅读有关 API 中媒体类型使用情况的更多信息。

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'contents' %}{% include rest_operation %}{% endif %}
{% endfor %}

## 部署密钥

{% data reusables.repositories.deploy-keys %}

部署密钥可以使用以下 API 端点进行设置，也可以使用 GitHub 进行设置。 要了解如何在 GitHub 中设置部署密钥，请参阅“[管理部署密钥](/developers/overview/managing-deploy-keys)”。

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'keys' %}{% include rest_operation %}{% endif %}
{% endfor %}

## 部署

部署是部署特定引用（分支、SHA、标记）的请求。 GitHub 分发一个 [`deployment` 事件](/developers/webhooks-and-events/webhook-events-and-payloads#deployment)，使外部服务可以在创建新部署时侦听并采取行动。 部署使开发者和组织能够围绕部署构建松散耦合的工具，而不必担心交付不同类型的应用程序（例如 Web 和本地应用程序）的实现细节。

部署状态允许外部服务将部署标记为 `error`、`failure`、`pending`、`in_progress`、`queued` 或 `success` 状态，以供侦听 [`deployment_status` 事件](/developers/webhooks-and-events/webhook-events-and-payloads#deployment_status)的系统使用。

部署状态还可以包含可选的 `description` 和 `log_url`，强烈建议使用它们，因为它们使部署状态更有用。 `log_url` 是部署输出的完整 URL，`description` 是关于部署过程中所发生情况的高级摘要。

在创建新的部署和部署状态时，GitHub 将分发 `deployment` 和 `deployment_status` 事件。 这些事件允许第三方集成接收对部署请求的响应，并在取得进展时更新部署的状态。

下面是一个说明这些交互的工作方式的简单序列图。

```
+---------+             +--------+            +-----------+        +-------------+
| Tooling |             | GitHub |            | 3rd Party |        | Your Server |
+---------+             +--------+            +-----------+        +-------------+
     |                      |                       |                     |
     |  Create Deployment   |                       |                     |
     |--------------------->|                       |                     |
     |                      |                       |                     |
     |  Deployment Created  |                       |                     |
     |<---------------------|                       |                     |
     |                      |                       |                     |
     |                      |   Deployment Event    |                     |
     |                      |---------------------->|                     |
     |                      |                       |     SSH+Deploys     |
     |                      |                       |-------------------->|
     |                      |                       |                     |
     |                      |   Deployment Status   |                     |
     |                      |<----------------------|                     |
     |                      |                       |                     |
     |                      |                       |   Deploy Completed  |
     |                      |                       |<--------------------|
     |                      |                       |                     |
     |                      |   Deployment Status   |                     |
     |                      |<----------------------|                     |
     |                      |                       |                     |
```

请记住，GitHub 从未真正访问过您的服务器。 与部署事件的交互取决于第三方集成。 多个系统可以侦听部署事件，由其中每个系统来决定它们是否负责将代码推送到服务器、构建本地代码等。

请注意，`repo_deployment` [OAuth 作用域](/developers/apps/scopes-for-oauth-apps)授予对部署和部署状态的定向访问权限，但**不**授予对仓库代码的访问权限，而 {% ifversion not ghae %}`public_repo` 和{% endif %}`repo` 作用域还授予对代码的权限。


### 非活动部署

When you set the state of a deployment to `success`, then all prior non-transient, non-production environment deployments in the same repository with the same environment name will become `inactive`. 为避免这种情况，您可以在创建部署状态时将 `auto_inactive` 设置为 `false`。

您可以通过将 `state` 设为 `inactive` 来表示某个瞬态环境不再存在。  将 `state` 设为 `inactive`，表示部署在 {% data variables.product.prodname_dotcom %} 中 `destroyed` 并删除对它的访问权限。

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'deployments' %}{% include rest_operation %}{% endif %}
{% endfor %}

{% ifversion fpt or ghes > 3.1 or ghae-next %}
## 环境

环境 API 允许您创建、配置和删除环境。 有关环境的更多信息，请参阅“[环境](/actions/reference/environments)”。 要管理环境密码，请参阅“[密码](/rest/reference/actions#secrets)”。

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'environments' %}{% include rest_operation %}{% endif %}
{% endfor %}
{% endif %}

## 复刻

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'forks' %}{% include rest_operation %}{% endif %}
{% endfor %}

## 邀请

仓库邀请 API 允许用户或外部服务邀请其他用户参与仓库协作。 受邀用户（或代表受邀用户的外部服务）可以选择接受或拒绝邀请。

请注意，`repo:invite` [OAuth 作用域](/developers/apps/scopes-for-oauth-apps)授予对邀请的定向访问权限，但**不**授予对仓库代码的访问权限，而 `repo` 作用域同时授予对代码和邀请的权限。

### 邀请用户参与仓库

使用 API 端点来添加协作者。 更多信息请参阅“[添加仓库协作者](/rest/reference/repos#add-a-repository-collaborator)”。

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'invitations' %}{% include rest_operation %}{% endif %}
{% endfor %}

{% ifversion fpt or ghae or ghes > 3.2 %}

## Git LFS

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'lfs' %}{% include rest_operation %}{% endif %}
{% endfor %}

{% endif %}

## 合并

仓库合并 API 支持合并仓库中的分支。 其过程基本上等同于在本地仓库中合并分支然后将其推送到 {% data variables.product.product_name %}。 其好处是合并是在服务器端完成的，不需要使用本地仓库。 这使它更适用于自动化，以及使用其他工具维护本地仓库比较繁琐且低效的情况。

经过身份验证的用户将是通过此端点完成的任何合并的作者。

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'merging' %}{% include rest_operation %}{% endif %}
{% endfor %}

## 页面

{% data variables.product.prodname_pages %} API 可检索关于您的 {% data variables.product.prodname_pages %} 配置以及构建状态的信息。 只有经过验证的所有者才能访问有关网站和构建的信息{% ifversion not ghae %}，即使网站是公开的也一样{% endif %}。 For more information, see "[About {% data variables.product.prodname_pages %}](/pages/getting-started-with-github-pages/about-github-pages)."

在其响应中包含 `status` 键的 {% data variables.product.prodname_pages %} API 端点中，其值可能是以下值之一：
* `null`：站点尚未构建。
* `queued`：已请求构建，但尚未开始。
* `building`：正在构建中。
* `built`：站点已构建。
* `errored`：表示构建过程中发生错误。

在返回 GitHub Pages 站点信息的 {% data variables.product.prodname_pages %} API 端点中，JSON 响应包括以下字段：
* `html_url`：所渲染的 Pages 站点的绝对 URL（包括模式）。 例如，`https://username.github.io`。
* `source`：包含所渲染 Pages 站点的源分支和目录的对象。 这包括：
   - `branch`：用于发布[站点源文件](/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)的仓库分支。 例如，_main_ 或 _gh-pages_。
   - `path`：提供站点发布内容的仓库目录。 可能是 `/` 或 `/docs`。

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'pages' %}{% include rest_operation %}{% endif %}
{% endfor %}

## 版本发布

{% note %}

**注：**发布 API 取代了下载 API。 您可以从返回发行版和发行版资产的 API 端点检索下载次数和浏览器下载 URL。

{% endnote %}

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'releases' %}{% include rest_operation %}{% endif %}
{% endfor %}

## 统计

仓库统计 API 允许您获取 {% data variables.product.product_name %} 用于可视化不同类型仓库活动的数据。

### 谈一谈缓存

计算仓库统计信息是一项昂贵的操作，所以我们尽可能返回缓存的数据。  如果您查询仓库的统计信息时，数据尚未缓存，您将会收到 `202` 响应；同时触发后台作业以开始编译这些统计信息。 稍等片刻，待作业完成，然后再次提交请求。 如果作业已完成，该请求将返回 `200` 响应，响应正文中包含统计信息。

仓库统计信息由仓库默认分支的 SHA 缓存；推送到默认分支将重置统计信息缓存。

### 统计排除某些类型的提交

API 公开的统计信息与[各种仓库图](/github/visualizing-repository-data-with-graphs/about-repository-graphs)显示的统计信息相匹配。

总结：
- 所有统计信息都排除合并提交。
- 参与者统计信息还排除空提交。

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'statistics' %}{% include rest_operation %}{% endif %}
{% endfor %}

## 状态

状态 API 允许外部服务将提交标记为 `error`、`failure`、`pending` 或 `success` 状态，然后将其反映在涉及这些提交的拉取请求中。

状态还可以包含可选的 `description` 和 `target_url`，强烈建议使用它们，因为它们使状态在 GitHub UI 中更有用。

一种常见用例是持续集成服务使用状态将提交标记为构建成功或失败。  `target_url` 是构建输出的完整 URL，`description` 是关于构建过程中所发生情况的高级摘要。

状态可以包括 `context` 以指示提供该状态的服务是什么。 例如，您可以让持续集成服务推送上下文为 `ci` 的状态，让安全审核工具推送上下文为 `security` 的状态。  然后，您可以使用[获取特定引用的组合状态](/rest/reference/repos#get-the-combined-status-for-a-specific-reference)来检索提交的整个状态。

请注意，`repo:status` [OAuth 作用域](/developers/apps/scopes-for-oauth-apps)授予对状态的定向访问权限，但**不**授予对仓库代码的访问权限，而 `repo` 作用域同时授予对代码和状态的权限。

如果您正在开发 GitHub 应用程序，希望提供有关外部服务的更多信息，则可能需要使用[检查 API](/rest/reference/checks)。

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'statuses' %}{% include rest_operation %}{% endif %}
{% endfor %}

{% ifversion fpt %}
## 流量

对于您具有推送权限的仓库，流量 API 提供对仓库图中所示信息的访问权限。 For more information, see "<a href="/repositories/viewing-activity-and-data-for-your-repository/viewing-traffic-to-a-repository" class="dotcom-only">Viewing traffic to a repository</a>."

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'traffic' %}{% include rest_operation %}{% endif %}
{% endfor %}
{% endif %}

## Web 挂钩

Repository webhooks allow you to receive HTTP `POST` payloads whenever certain events happen in a repository. {% data reusables.webhooks.webhooks-rest-api-links %}

如果您要设置一个 web 挂钩来接收来自组织所有仓库的事件，请参阅关于[组织 web 挂钩](/rest/reference/orgs#webhooks)的 API 文档。

In addition to the REST API, {% data variables.product.prodname_dotcom %} can also serve as a [PubSubHubbub](#pubsubhubbub) hub for repositories.

{% for operation in currentRestOperations %}
  {% if operation.subcategory == 'webhooks' %}{% include rest_operation %}{% endif %}
{% endfor %}

### 接收 web 挂钩

为了让 {% data variables.product.product_name %} 发送 web 挂钩有效负载，您的服务器需要能够从 Internet 访问。 我们还强烈建议使用 SSL，以便我们可以通过 HTTPS 发送加密的有效负载。

#### Web 挂钩标头

{% data variables.product.product_name %} 发送时将附带几个 HTTP 标头，以区分事件类型和有效负载标识符。 更多信息请参阅 [web 挂钩标头](/developers/webhooks-and-events/webhook-events-and-payloads#delivery-headers)。

### PubSubHubbub

GitHub 还可以作为所有仓库的 [PubSubHubbabub](https://github.com/pubsubhubbub/PubSubHubbub) 枢纽。 PSHB 是一个简单的发布/订阅协议，允许服务器注册在主题更新时接收更新。 这些更新随 HTTP POST 请求一起发送到回调 URL。 GitHub 仓库推送的主题 URL 采用以下格式：

`https://github.com/{owner}/{repo}/events/{event}`

事件可以是任何可用的 web 挂钩事件。 更多信息请参阅“[web 挂钩事件和有效负载](/developers/webhooks-and-events/webhook-events-and-payloads)”。

#### 响应格式

The default format is what [existing post-receive hooks should expect](/post-receive-hooks/): A JSON body sent as the `payload` parameter in a POST.  您还可以指定接收带有 `Accept` 标头或 `.json` 扩展名的原始 JSON 正文。

    Accept: application/json
    https://github.com/{owner}/{repo}/events/push.json

#### 回调 URL

回调 URL 可以使用 `http://` 协议。

    # Send updates to postbin.org
    http://postbin.org/123

#### 订阅

GitHub PubSubHubbub 端点为：`{% data variables.product.api_url_code %}/hub`。 使用 cURL 的成功请求如下所示：

``` shell
curl -u "user" -i \
  {% data variables.product.api_url_pre %}/hub \
  -F "hub.mode=subscribe" \
  -F "hub.topic=https://github.com/{owner}/{repo}/events/push" \
  -F "hub.callback=http://postbin.org/123"
```

PubSubHubbub 请求可以多次发送。 如果挂钩已经存在，它将根据请求进行修改。

##### 参数

| 名称             | 类型    | 描述                                                                                                                                                                                                                                                                                                                                                       |
| -------------- | ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `hub.mode`     | `字符串` | **必填**。 值为 `subscribe` 或 `unsubscribe`。                                                                                                                                                                                                                                                                                                                  |
| `hub.topic`    | `字符串` | **必填**。  要订阅的 GitHub 仓库的 URI。  路径格式必须为 `/{owner}/{repo}/events/{event}`。                                                                                                                                                                                                                                                                                 |
| `hub.callback` | `字符串` | 要接收主题更新的 URI。                                                                                                                                                                                                                                                                                                                                            |
| `hub.secret`   | `字符串` | 用于生成传出正文内容的哈希签名的共享密钥。  您可以通过比较原始请求正文与 {% ifversion fpt or ghes > 2.22 %}`X-Hub-Signature` 或 `X-Hub-Signature-256` 标头{% elsif ghes < 3.0 %}`X-Hub-Signature` 标头{% elsif ghae %}`X-Hub-Signature-256` 标头{% endif %} 的内容来验证来自 GitHub 的推送。 您可以查看 [PubSubHubbub 文档](https://pubsubhubbub.github.io/PubSubHubbub/pubsubhubbub-core-0.4.html#authednotify)了解详情。 |
