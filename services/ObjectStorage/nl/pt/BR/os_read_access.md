---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Concedendo acesso de leitura

Um usuário do {{site.data.keyword.objectstorageshort}} com uma [função administrativa](/docs/services/ObjectStorage/os_access_types.html) pode conceder acesso de leitura a um contêiner para outro usuário e manipular combinações de ACL de leitura.
{: shortdesc}

<table>
<caption> Tabela 1. Permissões de acesso de leitura por opção </caption>
  <tr>
    <th> Permissão </th>
    <th> Opções de ACL de leitura </th>
  </tr>
  <tr>
    <td> Ler para todas as referências, independentemente da conta de filiação </td>
    <td> <code> .r,&#42;  </code> </td>
  </tr>
  <tr>
    <td> Ler e listar para todas as referências e listagens </td>
    <td> <code> .r:&#42;,.rlistings </code> </td>
  </tr>
  <tr>
    <td> Ler e listar para um usuário especificado em um projeto específico </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Ler e listar para um usuário especificado em cada projeto </td>
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> Ler e listar para cada usuário em um projeto específico </td>
    <td> <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> Ler e listar para cada usuário em cada projeto  </td>
    <td> <code> &#42;:&#42; </code> </td>
  </tr>
</table>


1. Autentique suas credenciais. É possível usar as credenciais que são localizadas
na guia de credenciais de serviço da interface com o usuário ou gerar novas credenciais. Para obter mais informações sobre como gerar novas credenciais, consulte [Gerando credenciais de serviço](/docs/services/ObjectStorage/os_credentials.html). Você recebe a URL do
{{site.data.keyword.objectstorageshort}} e o token de autenticação como saída.

    Comando Swift:

    ```
    export OS_USER_ID=<user_id>
  export OS_PASSWORD=<password>
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
    curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
    ```
    {: pre}

2. Conceda acesso de leitura executando o comando a seguir:
    comando Swift:

    ```
    swift post <container_name> --read-acl "<user_id>:<project_id>"
    ```
    {: pre}

    Comando cURL:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}
    **Nota**: use vírgula (,) para separar listas de controle de acesso.

3. Verifique o valor de ACL de leitura.

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

    Exemplo: o valor `X-Container-Read` mostra qual é o contêiner e para quem é concedido o acesso de leitura.

    ```
    HTTP/1.1 204 No Content
  Content-Length: 0
  X-Container-Object-Count: 1
  Accept-Ranges: bytes
  X-Storage-Policy: standard
  X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
  X-Container-Bytes-Used: 31512
  X-Timestamp: 1462818314.11220
  Content-Type: text/plain; charset=utf-8
  X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
  Date: Tue, 28 Jun 2016 20:57:58 GMT
    ```
    {: screen}
