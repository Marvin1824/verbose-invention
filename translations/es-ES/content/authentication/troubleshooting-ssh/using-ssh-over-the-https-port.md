---
title: Uso de SSH a través del puerto HTTPS
intro: 'Algunas veces, los firewalls se niegan a permitir conexiones SSH por completo.  Si el utilizar el [clonado de HTTPS con almacenamiento de credenciales en el caché](/github/getting-started-with-github/caching-your-github-credentials-in-git) no es una opción, puedes intentar clonar utilizando una conexión SSH que hayas hecho a través del puerto HTTPS.  La mayoría de las reglas del firewall deberían permitir esto, pero los servidores proxy pueden interferir.'
redirect_from:
  - /articles/using-ssh-over-the-https-port
  - /github/authenticating-to-github/using-ssh-over-the-https-port
  - /github/authenticating-to-github/troubleshooting-ssh/using-ssh-over-the-https-port
versions:
  fpt: '*'
topics:
  - SSH
shortTitle: Utilizar SSH por un puerto HTTPS
---

{% tip %}

**Usuarios de {% data variables.product.prodname_ghe_server %}**: Actualmente no hay compatibilidad para acceder a {% data variables.product.prodname_ghe_server %} por SSH mediante el puerto HTTPS.

{% endtip %}

Para probar si es posible el SSH a través del puerto HTTPS, ejecuta este comando SSH:

```shell
$ ssh -T -p 443 git@ssh.github.com
> Hi <em>username</em>! You've successfully authenticated, but GitHub does not
> provide shell access.
```

Si eso funcionó, ¡fantástico! De lo contrario, puede que debas [seguir nuestra guía de solución de problemas](/articles/error-permission-denied-publickey).

## Habilitar conexiones SSH a través de HTTPS

If you are able to SSH into `git@ssh.{% data variables.command_line.backticks %}` over port 443, you can override your SSH settings to force any connection to {% data variables.product.product_location %} to run through that server and port.

Para establecer esto en tus parámetros ssh, edita el archivo en `~/.ssh/config` y agrega esta sección:

```
Host {% data variables.command_line.codeblock %}
Hostname ssh.{% data variables.command_line.codeblock %}
Port 443
User git
```

Puedes probar que esto funcione volviéndote a conectar a {% data variables.product.product_location %}:

```shell
$ ssh -T git@{% data variables.command_line.codeblock %}
> Hi <em>username</em>! You've successfully authenticated, but GitHub does not
> provide shell access.
```
