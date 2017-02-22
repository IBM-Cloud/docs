---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Concedendo acesso de gravação

Um usuário do {{site.data.keyword.objectstorageshort}} com uma [função administrativa](/docs/services/ObjectStorage/os_access_types.html) pode conceder acesso de gravação para outro usuário e manipular combinações de ACL de gravação.
{: shortdesc}

<table>
<caption> Tabela 1. Permissões de acesso de gravação por opção</caption>
  <tr>
    <th> Permissão </th>
    <th> Opções de ACL de gravação </th>
  </tr>
  <tr>
    <td> Gravar para um usuário especificado em um projeto específico </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Gravar para um usuário especificado em cada projeto </td>
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> Gravar para cada usuário em um projeto específico </td>
    <td>  <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> Gravar para cada usuário em cada projeto </td>
    <td>  <code> &#42;:&#42; </code> </td>
  </tr>
</table>



1. Autentique as suas credenciais usando as informações nas credenciais de serviço que você criou.  Você recebe a URL do
{{site.data.keyword.objectstorageshort}} e o token de autenticação como saída.

    Comando Swift:

    ```
    export OS_USER_ID="<user_id>"
    export OS_PASSWORD="<password>"
    export OS_TENANT_ID=<project_id>
    export OS_AUTH_URL=https://identity.open.softlayer.com/v3
    export OS_REGION_NAME=<region>
    export OS_IDENTITY_API_VERSION=3
    export OS_AUTH_VERSION=3

    swift auth
    ```
    {: codeblock}

    Comando cURL:

    ```
    curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
    ```
    {: pre}

2. Conceda acesso de gravação executando o comando a seguir.

    Comando Swift:

    ```
    swift post <container_name> --write-acl "<user_id>:<project_id>"
    ```
    {: pre}

    Comando cURL:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}

    **Nota**: use vírgula (,) para separar listas de controle
de acesso.

3. Verifique o valor de ACL de gravação.

    Comando Swift:

    ```
    swift stat <container_name>
    ```
    {: pre}

    Comando cURL:

    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}
