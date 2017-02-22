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


# Gerando credenciais de serviço {: #credentials}

As credenciais de serviço são usadas para fornecer autenticação e segurança para o
serviço. É possível gerar novas credenciais usando a CLI ou a UI do {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}


## Para incluir credenciais na UI:

1. Na guia **Credenciais de serviço** no painel da instância de serviço, clique em **Nova credencial** e dê um nome a ela.
2. Opcional: no campo de texto **Incluir parâmetros de configuração sequenciais**, insira as informações de credenciais para a função com o [tipo de acesso](/docs/services/ObjectStorage/os_access_types.html) que você deseja fornecer. As informações devem ser
formatadas como uma carga útil de JSON.
    - Para criar um usuário administrativo: `{"role":"admin"}`
    - Para criar um usuário não administrativo: `{"role":"member"}`
3. Clique em ** Adicionar**.


## Para incluir credenciais usando comandos Cloud Foundry na CLI:

1. Se você não tiver efetuado login no {{site.data.keyword.Bluemix_notm}}, efetue login como um usuário com uma função do desenvolvedor. Deve-se estar localizado dentro do espaço da instância de serviço que você deseja gerenciar.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Gere credenciais de serviço. Forneça um nome para a sua credencial substituindo a variável
`service-key-name`. Opcionalmente, também é possível designar uma [função de usuário](/docs/services/ObjectStorage/os_access_types.html).

  ```
  cf create-service-key "<service_instance_name>" <service-key-name> -c '{"role":"<user_role>"}'
  ```
  {: pre}

  Exemplo:
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
  ```
  {: screen}

3. Valide as credenciais para a chave criada.

  ```
  cf service-keys <service_instance_name>
  ```
  {: pre}

  Chave de exemplo para uma instância nomeada Object-Storage-Acl-Test para um usuário com uma função de membro:

  ```
  {
    "auth_url": "https://identity.open.softlayer.com",
    "domainId": "8753ff40ac1a4f4a9f162ad8026b6ce0",
    "domainName": "757955",
    "password": "xxxxxxxx",
    "project": "object_storage_6046b6e2_ee53_4884_916f_89c65e4d408e",
    "projectId": "c727d7e248b448f6b268f31a1bd8691e",
    "region": "dallas",
    "role": "member",
    "userId": "3c5b516655e4479881d3d216895faedb",
    "username": "member_2afbeea1d58b1867f46c699553d1e4513e7df83a"
  }
  ```
  {: screen}



#### Para incluir credenciais usando comandos cURL na CLI:

1. Se você não tiver efetuado login no {{site.data.keyword.Bluemix_notm}}, efetue login como um usuário com uma função do desenvolvedor. Deve-se estar localizado dentro do espaço da instância de serviço que você deseja gerenciar.

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Execute o comando a seguir para gerar credenciais de serviço.

  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name: <service_instance_name>", "role: <user_role>"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: <content_type" -H "Cookie: <cookie>"
  ```
  {: pre}

  <table>
  <caption> Tabela 1. Variáveis de credenciais de serviço cURL explicadas</caption>
    <tr>
      <th> Variável  </th>
      <th> Explicação </th>
    </tr>
    <tr>
      <td> <code>https://api.ng.bluemix.net/v2/service_keys</code> </td>
      <td> O terminal de chave de serviço.  </td>
    </tr>
    <tr>
      <td><i> service_instance_guid </i></td>
      <td> Pode ser localizada em sua URL.  </td>
    </tr>
    <tr>
      <td><i>name</i></td>
      <td> O nome de sua instância de serviço. </td>
    </tr>
    <tr>
      <td><i>role</i></td>
      <td> Especifique a <a href= /docs/services/ObjectStorage/os_constructing.html>função do membro</a> como administrador ou membro. </td>
    </tr>
    <tr>
      <td><i> bearer_token </i></td>
      <td> O token que você recebeu quando autenticou sua instância com o Keystone.</td>
    </tr>
  </table>



3. Valide suas credenciais executando o comando a seguir.

  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```
  {: screen}
