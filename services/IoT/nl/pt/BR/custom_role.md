---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-10"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sobre funções customizadas
{: #custom_roles}

Além das funções predefinidas que são detalhadas na [documentação do usuário, do aplicativo e da função do gateway](roles_index.html), os usuários podem criar funções customizadas que têm combinações exclusivas de permissões. Funções representam acesso a operações específicas e, ao criar uma função customizada, é possível combinar qualquer uma das permissões que estão disponíveis para as funções predefinidas.
{:shortdesc}

Para obter mais informações sobre as operações de API que estão disponíveis para as funções de usuário, consulte a [documentação do usuário, do aplicativo e da função do gateway](roles_index.html).

## Criando uma função customizada
{: #custom-role-create}

Para criar uma função customizada:

1. No painel {{site.data.keyword.iot_short_notm}}, abra a área de janela **Membros** da barra de navegação.
2. Selecione a guia **Funções** e clique em **Nova função**.
3. Insira um nome para sua função customizada.
4. Opcional: Insira uma descrição para sua função customizada.
5. Opcional: Funções customizadas podem usar uma função existente como um modelo. Para basear a função customizada em uma função de usuário existente, selecione a função na lista.
6. Clique em **Avançar**.
7. Na lista de permissões, expanda as categorias de permissão e selecione as operações que a função customizada deve incluir.
8. Clique em **Incluir função**.

A função customizada é incluída na lista de funções disponíveis.

## Editando ou excluindo uma função customizada
{: #custom-role-edit}

Para editar ou excluir uma função customizada:

1. No painel {{site.data.keyword.iot_short_notm}}, abra a área de janela **Membros** da barra de navegação.
2. Selecione a guia **Funções**.
3. Localize a coluna que corresponde à função customizada que você deseja editar.
3. Clique no ícone de edição para o nome da função customizada.
4. Faça todas as mudanças necessárias para a descrição da função e para as permissões.
5. Para excluir a função, role para a parte inferior da lista de categorias de permissão e clique em **Excluir função**.
5. Se tiver feito quaisquer mudanças, clique em **Salvar** para atualizar a função.

A função é atualizada.
