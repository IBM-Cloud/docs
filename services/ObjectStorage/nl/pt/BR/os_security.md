---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Protegendo arquivos {: #understanding-authentication}
*Última atualização: 19 de outubro de 2016*
{: .last-updated}

## OpenStack Identity (Keystone) v3 {: #keystone-authentication}

O provisionamento de uma nova instância do {{site.data.keyword.objectstorageshort}} cria um projeto Keystone isolado no IBM Public Cloud.
{: shortdesc}

A estrutura de credenciais contém um conjunto completo de atributos para permitir a
escolha do método de solicitação de token do OpenStack ou o OpenStack SDK que melhor se
ajusta ao seu app. Ao ligar um novo aplicativo à instância, é criado um novo usuário do
Keystone com acesso ao projeto. Quando você desprovisiona a instância, o projeto e o usuário são excluídos.

Para obter mais informações sobre como usar o OpenStack Swift e o Keystone, visualize o [site de documentação do OpenStack](http://docs.openstack.org).

A solicitação de token v3 recomendada é uma solicitação de POST para https://identity.open.softlayer.com/v3/auth/tokens conforme mostrado no comando curl a seguir:

```
	curl -i \
	  -H "Content-Type: application/json" \
	  -d '
	{
		"auth": {
			"identity": {
				"methods": [
					"password"
				],
				"password": {
					"user": {
						"id": "ad78b2a3f843466988afd077731c61fc",
						"password": "XXXXXXXXXX"
					}
				}
			},
			"scope": {
				"project": {
					"id": "0f47b41b06d047f9aae3b33f1db061ed"
				}
			}
		}
	}' \
	  https://identity.open.softlayer.com/v3/auth/tokens ; echo
```
{: codeblock}

Use o valor do campo `X-Subject-Token` a partir do cabeçalho de resposta como o campo `X-Auth-Token` quando fizer solicitações para o serviço {{site.data.keyword.objectstorageshort}}.

A seguir está uma resposta de exemplo. A resposta foi cortada para mostrar somente as informações relevantes do {{site.data.keyword.objectstorageshort}}.

```
	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json

	{
	  "token" : {
	    "roles" : [
	      {
	        "id" : "f61f06a84f6443e880210fa986bd8691",
	        "name" : "ObjectStorageOperator"
	      }
	    ],
	    "catalog" : [
	      {
	        "endpoints": [
			{
	            "id" : "20cbfa6ff22b4a67a1484d30235bfc80",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "38b8c081b11a452bb951698c334a406d",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          },
	          {
	            "id" : "4207049680fa4effbecd044c7448a8cb",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "a60cf32be624491d89170ef8264de5e8",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "c769862200124a308d6748e418c971ba",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          }
	        ],
	        "id" : "896e4064cbe742afbf9a543c15f27ac0",
	        "type" : "object-store",
	        "name" : "swift"
	      },
	    ],
	    "extras" : {

	    },
	    "user" : {
	      "id" : "0b8aebd924ef4cc7aa9232f07e47e874",
	      "name" : "user_87c094ce47a9feae3a137ffcbbfa098a888c12a8",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "expires_at" : "2016-02-29T22:03:42.061343Z",
	    "audit_ids" : [
	      "cbA-iL2dSheyB72PHd7q8Q"
	    ],
	    "issued_at" : "2016-02-29T21:03:42.000000Z",
	    "project" : {
	      "id" : "3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	      "name" : "object_storage_c1d8b3a1",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "methods" : [
	      "password"
	    ]
	  }
	}
```
{: screen}

A URL do {{site.data.keyword.objectstorageshort}} está localizada no
catálogo de serviços. O catálogo de serviços está contido no corpo de resposta da
solicitação de token. A resposta é um catálogo completo de serviços do OpenStack que estão disponíveis. Selecione
o terminal a partir do catálogo de serviços com o tipo `object-store` e a região
que corresponde ao campo de região nas credenciais.

**Nota:** use a interface pública (`publicURL`). A interface interna (`internalURL`) não é acessível a partir do {{site.data.keyword.Bluemix_notm}}.


## Entendendo credenciais de serviço{: #understanding-credentials}

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
    <td> `OS_USER_ID` </td>
    <td> Seu ID do usuário do {{site.data.keyword.objectstorageshort}}.</td>
  </tr>
  <tr>
    <td> `OS_PASSWORD` </td>
    <td> A senha para a instância do {{site.data.keyword.objectstorageshort}}.</td>
  </tr>
  <tr>
    <td> `OS_PROJECT_ID` </td>
    <td> Seu ID do projeto.</td>
  </tr>
  <tr>
    <td> `OS_REGION_NAME` </td>
    <td> A região na qual seus objetos são armazenados. O
{{site.data.keyword.objectstorageshort}} está disponível nas regiões Dallas e
Londres. </td>
  </tr>
  <tr>
    <td> `OS_AUTH_URL` </td>
    <td> A URL do terminal. Certifique-se de que `/v3` esteja incluído no final da URL.</td>
  </tr>
</table>

*Tabela 1: Variáveis de autenticação e descrições*

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

*Tabela 2: Funções de usuário definidas*

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
    <td> `.r,*` </td>
  </tr>
  <tr>
    <td> Ler e listar para todas as referências e listagens </td>
    <td> `.r:*,.rlistings` </td>
  </tr>
  <tr>
    <td> Ler e listar para um usuário especificado em um projeto específico </td>
    <td> `< project_id>:< user_id>` </td>
  </tr>
  <tr>
    <td> Ler e listar para um usuário especificado em cada projeto </td>
    <td> `<*>:< user_id>` </td>
  </tr>
  <tr>
    <td> Ler e listar para cada usuário em um projeto específico </td>
    <td> `< project_id>:<*>` </td>
  </tr>
  <tr>
    <td> Ler e listar para cada usuário em cada projeto  </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*Tabela 3: Permissões de acesso de leitura por opção*



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
    <td> `< project_id>:< user_id>` </td>
  </tr>
  <tr>
    <td> Gravar para um usuário especificado em cada projeto </td>
    <td> `*:<user_id>` </td>
  </tr>
  <tr>
    <td> Gravar para cada usuário em um projeto específico </td>
    <td> `< project_id>:<*>` </td>
  </tr>
  <tr>
    <td> Gravar para cada usuário em cada projeto </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*Tabela 4: Permissões de acesso de gravação por opção*




1. Autentique as suas credenciais usando as informações nas credenciais de serviço que você criou.  Você
recebe a URL do {{site.data.keyword.objectstorageshort}} e o token de
autenticação como saída.
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
