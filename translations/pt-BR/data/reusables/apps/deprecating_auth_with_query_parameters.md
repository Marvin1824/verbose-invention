{% ifversion fpt or ghes or ghae or ghec %}
{% warning %}

**Aviso de método obsoleto:** {% data variables.product.prodname_dotcom %} irá descontinuar a autenticação para a API usando parâmetros de consulta. A autenticação na API deve ser feita com [HTTP basic authentication](/rest/overview/other-authentication-methods#via-oauth-and-personal-access-tokens).{% ifversion fpt or ghec %} Usar parâmetros de consulta para autenticar na API não funcionará mais em 5 de maio de 2021. {% endif %}  Para mais informações, incluindo brownouts agendadas, veja [blog post](https://developer.github.com/changes/2020-02-10-deprecating-auth-through-query-param/).

{% ifversion ghes or ghae %} Autenticação à API usando parâmetros de consulta, enquanto disponível não é mais suportada devido a questões de segurança. Em vez disso, recomendamos que integradores movam seu token de acesso, `client_id`, or `client_secret` no cabeçalho. {% data variables.product.prodname_dotcom %} anunciará a remoção da autenticação por parâmetros de consulta com aviso prévio. {% endif %}

{% endwarning %}
{% endif %}
