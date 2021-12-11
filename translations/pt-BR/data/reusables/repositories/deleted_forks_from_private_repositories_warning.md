{% warning %}

**Aviso:**

- Se você remover o acesso de uma pessoa a um repositório privado, todas as suas bifurcações desse repositório privado serão excluídas. Os clones locais do repositório privado são mantidos. Se o acesso de uma equipe a um repositório privado for revogado ou uma equipe com acesso a um repositório privado for excluída, e os integrantes da equipe não tiverem acesso ao repositório por meio de outra equipe, as bifurcações privadas do repositório serão excluídas.{% ifversion ghes %}
- When [LDAP Sync is enabled](/enterprise/{{ page.version }}/admin/guides/user-management/using-ldap/#enabling-ldap-sync), if you remove a person from a repository, they will lose access but their forks will not be deleted. Se a pessoa for adicionada a uma equipe com acesso ao repositório original da organização dentro de três meses, seu acesso às bifurcações será automaticamente restaurado na próxima sincronização.{% endif %}
- Você é responsável por garantir que as pessoas que perderam o acesso a um repositório excluam qualquer informação confidencial ou de propriedade intelectual.

- Pessoas com permissões de administrador a um repositório privado{% ifversion fpt or ghes or ghae %} ou interno{% endif %} não podem permitir a bifurcação desse repositório, e os proprietários da organização podem impedir a bifurcação de qualquer repositório privado{% ifversion fpt or ghes or ghae %} ou interno{% endif %} em uma organização. Para mais informações, consulte "[Gerenciar a política de bifurcação da sua organização](/organizations/managing-organization-settings/managing-the-forking-policy-for-your-organization)" e "[Gerenciar a política de bifurcação do seu repositório](/github/administering-a-repository/managing-the-forking-policy-for-your-repository)".

{% endwarning %}
