---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Protegendo arquivos {: #understanding-authentication}


## Entendendo credenciais de serviço {: #understanding-credentials}

As credenciais de serviço são usadas para fornecer autenticação e segurança para o
serviço. Um conjunto de credenciais é gerado automaticamente quando uma instância é
provisionada. O cliente Swift obtém as informações de autenticação das variáveis de
ambiente na tabela a seguir.

<table>
  <tr>
    <th> Variável de ambiente </th>
    <th> Descrição </th>
  </tr>
  <tr>
    <td> <code>OS_USER_ID</code> </td>
    <td> Seu ID do usuário do {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> <code>OS_PASSWORD</code> </td>
    <td> A senha para a instância do {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> <code>OS_PROJECT_ID</code> </td>
    <td> Seu ID do projeto. </td>
  </tr>
  <tr>
    <td> <code>OS_REGION_NAME</code> </td>
    <td> A região na qual seus objetos são armazenados. O
{{site.data.keyword.objectstorageshort}} está disponível nas regiões Dallas e
Londres. </td>
  </tr>
  <tr>
    <td> <code>OS_AUTH_URL</code> </td>
    <td> A URL do terminal. Certifique-se de que `/v3` esteja incluído no final da URL. </td>
  </tr>
</table>

Tabela 1: Variáveis e descrições de autenticação

####  Incluindo credenciais de serviço na UI
1. Na guia **Credenciais de serviço** no painel da instância de serviço, clique em **Nova credencial** e dê um nome a ela.
2. (*Opcional*) No campo de texto **Incluir parâmetros de
configuração sequenciais**, insira as informações de credenciais para a função
que você deseja criar. As informações devem ser
formatadas como uma carga útil de JSON. Para obter mais informações sobre funções de
usuário do {{site.data.keyword.objectstorageshort}}, consulte
[Tipos de acesso](../os_security.html#access-types).
    - Para criar um usuário administrativo: `{"role":"admin"}`
    - Para criar um usuário não administrativo: `{"role":"member"}`
3. Clique em ** Adicionar**.


## Tipos de acesso {: #access-types}

O acesso ao serviço é controlado por funções de usuário e listas de controle de acesso de contêiner. Usuários do {{site.data.keyword.objectstorageshort}} podem ser administrativos ou não
administrativos. Listas de controle de acesso são ativadas por usuários administrativos no nível de contêiner e não estão disponíveis para a instância de serviço, conta de armazenamento ou no nível de projeto.

<table>
  <tr>
    <th> Usuários administrativos (administradores) </th>
    <th> Usuários não administrativos (membros) </th>
  </tr>
  <tr>
    <td> Gerenciar controle de acesso </td>
    <td> Por padrão, sem acesso ao serviço ou aos seus contêineres </td>
  </tr>
  <tr>
    <td> Podem criar e excluir contêineres </td>
    <td> Podem executar ações com base nas ACLs de leitura/gravação de contêineres </td>
  </tr>
  <tr>
    <td> Podem ler e gravar em contêineres </td>
    <td> Podem executar ações conforme determinado pelo administrador </td>
  </tr>
</table>

Tabela 2: Funções definidas pelo usuário

É possível gerenciar usuários do {{site.data.keyword.objectstorageshort}} por meio da interface com o usuário do {{site.data.keyword.Bluemix_notm}}, da API do Cloud Foundry ou da CLI do
Cloud Foundry.




## Concedendo acesso de leitura {: #read-access}

Um usuário {{site.data.keyword.objectstorageshort}} com uma função
administrativa pode conceder acesso de leitura a um contêiner para outro usuário e
manipular combinações de ACL de leitura.

<table>
  <tr>
    <th> Permissão </th>
    <th> Opções de ACL de leitura </th>
  </tr>
  <tr>
    <td> Ler para todas as referências, independentemente da conta de filiação </td>
    <td> <code> .r,*` </code> </td>
  </tr>
  <tr>
    <td> Ler e listar para todas as referências e listagens </td>
    <td> <code>.r:*,.rlistings</code> </td>
  </tr>
  <tr>
    <td> Ler e listar para um usuário especificado em um projeto específico </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Ler e listar para um usuário especificado em cada projeto </td>
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> Ler e listar para cada usuário em um projeto específico </td>
    <td> <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> Ler e listar para cada usuário em cada projeto  </td>
    <td> <code> *:* </code> </td>
  </tr>
</table>

Tabela 3: Permissões de acesso de leitura por opção



1. Autentique suas credenciais. É possível usar as credenciais que são localizadas
na guia de credenciais de serviço da interface com o usuário ou gerar novas credenciais. Para obter mais
informações sobre como gerar novas credenciais, consulte
[Gerando credenciais de serviço](insert link here). Você recebe a URL do
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

    É possível ver na saída de exemplo a seguir que o acesso de leitura foi concedido:

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



## Concedendo acesso de gravação {: #write-access}

Um usuário {{site.data.keyword.objectstorageshort}} com uma função
administrativa pode conceder acesso de gravação a um contêiner para outro usuário e
manipular combinações de ACL de gravação.

<table>
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
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> Gravar para cada usuário em um projeto específico </td>
    <td>  <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> Gravar para cada usuário em cada projeto </td>
    <td>  <code> *:* </code> </td>
  </tr>
</table>

Tabela 4: Permissões de acesso de gravação por opção



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

2. Conceda acesso de gravação executando o comando a seguir:
    comando Swift:

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



## Removendo o acesso {: #removing-access}

Para remover ACLs de leitura de um contêiner:
* Comando Swift:

    ```
    swift post <container_name> --read-acl “”
    ```
    {: pre}

*  Comando cURL:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

Para remover ACLs de gravação de um contêiner:

* Comando Swift:

    ```
    swift post <container_name> --write-acl “”
    ```
    {: pre}

*  Comando cURL:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

Para verificar se você removeu uma ACL:

* Comando Swift:

    ```
    swift stat <container_name>
    ```
    {: pre}

  O exemplo de saída a seguir mostra a ACL de leitura e de gravação como em branco,
o que significa que o acesso foi removido.

  ```
           Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8
  ```
  {: screen}

* Comando cURL:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
  {: pre}
