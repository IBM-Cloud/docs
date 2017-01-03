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

# Usando a API REST do Swift para acessar o {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}


É possível usar a API REST do Swift com uma interface do cliente da linha de comandos, como cURL, ou chamar a API a partir do aplicativo.
{: shortdesc}



## OpenStack Identity (Keystone) v3 {: #keystone-authentication}

O provisionamento de uma nova instância do {{site.data.keyword.objectstorageshort}} cria um projeto Keystone isolado no IBM Public Cloud.

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






## Construindo sua URL do {{site.data.keyword.objectstorageshort}} {: #access-points}

Para interagir com a API do {{site.data.keyword.objectstorageshort}}, construa a URL do {{site.data.keyword.objectstorageshort}} como a seguir:
  ```
  https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>
  ```
  {: pre}

<table>
  <tr>
    <th> Partes da URL  </th>
    <th> Definição </th>
  </tr>
  <tr>
    <td> Versão da API  </td>
    <td> Versão 1: v1 </td>
  </tr>
  <tr>
    <td> Dados da conta  </td>
    <td> Este é o ID do projeto e o prefixo combinado. Ele pode ser localizado na interface com o usuário. </td>
  </tr>
  <tr>
    <td> Namespace do contêiner  </td>
    <td> O nome do contêiner. Ele pode ser localizado na interface com o usuário. </td>
  </tr>
  <tr>
    <td> Namespace de Objeto  </td>
    <td> O nome do seu arquivo ou objeto. Ele pode ser localizado na interface com o usuário. </td>
  </tr>
  <tr>
    <td> Ponto de acesso</td>
    <td> Londres: https://lon.objectstorage.open.softlayer.com/
    <br> Dallas: https://dal.objectstorage.open.softlayer.com/ </br> </td>
  </tr>
</table>

Tabela 1. Partes da URL do {{site.data.keyword.objectstorageshort}} explicadas

Exemplo:

Partes da URL do ![{{site.data.keyword.objectstorageshort}} mostradas em uma imagem de exemplo](images/Swift_URL.png)





## API do {{site.data.keyword.objectstorageshort}} {: #openstack-reference}

Consulte a
[Referência
completa da API Swift OpenStack](http://developer.openstack.org/api-ref-objectstorage-v1.html) para obter uma lista abrangente das opções e dos
exemplos da API REST {{site.data.keyword.objectstorageshort}}.
