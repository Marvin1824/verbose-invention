---
title: Trabalhando com o registro do Gradle
intro: 'Você pode configurar o Gradle para publicar pacotes no registro do Gradle de {% data variables.product.prodname_registry %} e usar pacotes armazenados em {% data variables.product.prodname_registry %} como dependências de um projeto Java.'
product: '{% data reusables.gated-features.packages %}'
redirect_from:
  - /articles/configuring-gradle-for-use-with-github-package-registry
  - /github/managing-packages-with-github-package-registry/configuring-gradle-for-use-with-github-package-registry
  - /github/managing-packages-with-github-packages/configuring-gradle-for-use-with-github-packages
  - /packages/using-github-packages-with-your-projects-ecosystem/configuring-gradle-for-use-with-github-packages
  - /packages/guides/configuring-gradle-for-use-with-github-packages
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
shortTitle: Registro do Gradle
---

{% data reusables.package_registry.packages-ghes-release-stage %}
{% data reusables.package_registry.packages-ghae-release-stage %}

**Note:** When installing or publishing a docker image, {% data variables.product.prodname_registry %} does not currently support foreign layers, such as Windows images.

## Autenticar-se no {% data variables.product.prodname_registry %}

{% data reusables.package_registry.authenticate-packages %}

{% data reusables.package_registry.authenticate-packages-github-token %} Para obter mais informações sobre como usar `GITHUB_TOKEN` com Gradle, consulte "[Publicar pacotes Java com o Gradle](/actions/guides/publishing-java-packages-with-gradle#publishing-packages-to-github-packages)".

### Efetuando a autenticação com um token de acesso pessoal

{% data reusables.package_registry.required-scopes %}

Você pode efetuar a autenticação no {% data variables.product.prodname_registry %} com Gradle usando Gradle Groovy ou Kotlin DSL e editando o seu arquivo *build.gradle* (Gradle Groovy) ou o arquivo *build.gradle.kts* (Kotlin DSL) para incluir seu token de acesso pessoal. Também é possível configurar o Gradle Groovy e o Kotlin DSL para reconhecer um único pacote ou vários pacotes em um repositório.

{% ifversion ghes %}
Substitua *REGISTRY-URL* pela URL do registro do Maven para a sua instância. Se sua instância tiver o isolamento de subdomínio habilitado, use `maven.HOSTNAME`. Se sua instância estiver com o isolamento de subdomínio desabilitado, use `HOSTNAME/registry/maven`. Em ambos os casos, substitua *HOSTNAME* pelo nome de host da sua instância do {% data variables.product.prodname_ghe_server %}.
{% elsif ghae %}
Substitua *URL REGISTRA-* pela URL para o registro Maven da sua empresa, `maven.HOSTNAME`. Substitua *HOSTNAME* pelo nome do host de {% data variables.product.product_location %}.
{% endif %}

Substitua *NOME DE USUÁRIO* pelo seu nome de usuário do {% data variables.product.prodname_dotcom %} *TOKEN* pelo seu token de acesso pessoal, *REPOSITÓRIO* pelo nome do repositório que contém o pacote que você deseja publicar, e *PROPRIETÁRIO* pelo nome do usuário ou conta de organização no {% data variables.product.prodname_dotcom %} que é proprietário do repositório. Como não é permitido usar letras maiúsculas, é preciso usar letras minúsculas no nome do proprietário do repositório, mesmo que o nome do usuário ou da organização no {% data variables.product.prodname_dotcom %} contenha letras maiúsculas.

{% note %}

**Observação:** {% data reusables.package_registry.apache-maven-snapshot-versions-supported %} Por exemplo, consulte "[Configuraro Apache Maven para uso com {% data variables.product.prodname_registry %}](/packages/using-github-packages-with-your-projects-ecosystem/configuring-apache-maven-for-use-with-github-packages)".

{% endnote %}

#### Exemplo de uso do Gradle Groovy para um único pacote em um repositório

```shell
plugins {
    id("maven-publish")
}
publishing {
    repositories {
        maven {
            name = "GitHubPackages"
            url = uri("https://{% ifversion fpt %}maven.pkg.github.com{% else %}<em>REGISTRY-URL</em>{% endif %}/<em>OWNER</em>/<em>REPOSITORY</em>")
            credentials {
                username = project.findProperty("gpr.user") ?: System.getenv("<em>USERNAME</em>")
                password = project.findProperty("gpr.key") ?: System.getenv("<em>TOKEN</em>")
            }
        }
    }
    publications {
        gpr(MavenPublication) {
            from(components.java)
        }
    }
}
```

#### Exemplo de uso do Gradle Groovy para vários pacotes no mesmo repositório

```shell
plugins {
    id("maven-publish") apply false
}
subprojects {
    apply plugin: "maven-publish"
    publishing {
        repositories {
            maven {
                name = "GitHubPackages"
                url = uri("https://{% ifversion fpt %}maven.pkg.github.com{% else %}<em>REGISTRY-URL</em>{% endif %}/<em>OWNER</em>/<em>REPOSITORY</em>")
                credentials {
                    username = project.findProperty("gpr.user") ?: System.getenv("<em>USERNAME</em>")
                    password = project.findProperty("gpr.key") ?: System.getenv("<em>TOKEN</em>")
                }
            }
        }
        publications {
            gpr(MavenPublication) {
                from(components.java)
            }
        }
    }
}
```

#### Exemplo de uso do Kotlin DSL para um único pacote no mesmo repositório

```shell
plugins {
    `maven-publish`
}
publishing {
    repositories {
        maven {
            name = "GitHubPackages"
            url = uri("https://{% ifversion fpt %}maven.pkg.github.com{% else %}<em>REGISTRY-URL</em>{% endif %}/<em>OWNER</em>/<em>REPOSITORY</em>")
            credentials {
                username = project.findProperty("gpr.user") as String? ?: System.getenv("<em>USERNAME</em>")
                password = project.findProperty("gpr.key") as String? ?: System.getenv("<em>TOKEN</em>")
            }
        }
    }
    publications {
        register&lt;MavenPublication>("gpr") {
            from(components["java"])
        }
    }
}
```

#### Exemplo de uso do Kotlin DSL para vários pacotes no mesmo repositório

```shell
plugins {
    `maven-publish` apply false
}
subprojects {
    apply(plugin = "maven-publish")
    configure&lt;PublishingExtension> {
        repositories {
            maven {
                name = "GitHubPackages"
                url = uri("https://{% ifversion fpt %}maven.pkg.github.com{% else %}<em>REGISTRY-URL</em>{% endif %}/<em>OWNER</em>/<em>REPOSITORY</em>")
                credentials {
                    username = project.findProperty("gpr.user") as String? ?: System.getenv("<em>USERNAME</em>")
                    password = project.findProperty("gpr.key") as String? ?: System.getenv("<em>TOKEN</em>")
                }
            }
        }
        publications {
            register&lt;MavenPublication>("gpr") {
                from(components["java"])
            }
        }
    }
}
```

## Publicar um pacote

{% data reusables.package_registry.default-name %} Por exemplo, {% data variables.product.prodname_dotcom %} publicará um pacote denominado `com.example.test` no repositório `OWNER/test` {% data variables.product.prodname_registry %}.

{% data reusables.package_registry.viewing-packages %}

{% data reusables.package_registry.authenticate-step %}
2. Depois de criar seu pacote, você poderá publicá-lo.

  ```shell
   $ gradle publish
  ```

## Using a published package

To use a published package from {% data variables.product.prodname_registry %}, add the package as a dependency and add the repository to your project. Para obter mais informações, consulte "[Declarar dependências](https://docs.gradle.org/current/userguide/declaring_dependencies.html)" na documentação do Gradle.

{% data reusables.package_registry.authenticate-step %}
2. Adicione as dependências do pacote ao seu arquivo *build.gradle* (Gradle Groovy) ou ao arquivo *build.gradle.kts* (arquivo de Kotlin DSL).

  Exemplo do uso do Gradle Groovy:
  ```shell
  dependencies {
      implementation 'com.example:package'
  }
  ```
  Exemplo de uso do Kotlin DSL:
  ```shell
  dependencies {
      implementation("com.example:package")
  }
  ```

3. Add the repository to your *build.gradle* file (Gradle Groovy) or *build.gradle.kts* file (Kotlin DSL) file.

  Exemplo do uso do Gradle Groovy:
  ```shell
  repositories {
      maven {
          url = uri("https://{% ifversion fpt %}maven.pkg.github.com{% else %}<em>REGISTRY-URL</em>{% endif %}/<em>OWNER</em>/<em>REPOSITORY</em>")
          credentials {
              username = project.findProperty("gpr.user") ?: System.getenv("<em>USERNAME</em>")
              password = project.findProperty("gpr.key") ?: System.getenv("<em>TOKEN</em>")
          }
      }
  }
  ```
  Exemplo de uso do Kotlin DSL:
  ```shell
  repositories {
      maven {
          url = uri("https://{% ifversion fpt %}maven.pkg.github.com{% else %}<em>REGISTRY-URL</em>{% endif %}/<em>OWNER</em>/<em>REPOSITORY</em>")
          credentials {
              username = project.findProperty("gpr.user") as String? ?: System.getenv("<em>USERNAME</em>")
              password = project.findProperty("gpr.key") as String? ?: System.getenv("<em>TOKEN</em>")
          }
      }
  }
  ```

## Leia mais

- "[Trabalhando com o registro Apache Maven](/packages/working-with-a-github-packages-registry/working-with-the-apache-maven-registry)"
- "{% ifversion fpt or ghes > 3.0 %}[Excluir e restaurar um pacote](/packages/learn-github-packages/deleting-and-restoring-a-package){% elsif ghes < 3.1 or ghae %}[Excluir um pacote](/packages/learn-github-packages/deleting-a-package){% endif %}"
