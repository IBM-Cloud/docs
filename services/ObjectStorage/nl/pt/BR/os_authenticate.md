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


# Autenticando sua instância do {{site.data.keyword.objectstorageshort}} com o Keystone

Para interagir com o serviço, deve-se autenticar a instância do {{site.data.keyword.objectstorageshort}} com o Keystone para obter sua URL e o token de acesso.
{: shortdesc}


O provisionamento de uma nova instância do {{site.data.keyword.objectstorageshort}} cria um projeto Keystone isolado no IBM Public Cloud. A estrutura de credenciais do Keystone contém um conjunto completo de atributos para que seja possível escolher o método de solicitação de token do OpenStack ou do SDK do OpenStack que melhor se ajuste ao seu aplicativo. Ao ligar um novo app à instância, um novo usuário Keystone com acesso ao projeto será criado. Quando você desprovisiona a instância, o projeto e o usuário são excluídos.

Para obter mais informações sobre como usar o OpenStack Swift e o Keystone, visualize o <a href="http://docs.openstack.org" target="_blank">site de documentação do OpenStack. <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>



1. Faça uma solicitação de POST em `https://identity.open.softlayer.com/v3/auth/tokens` conforme mostrado no comando cURL a seguir.
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

2. Selecione um terminal `object-store` na resposta do catálogo e tome nota. Ele será necessário para construir a URL completa. O exemplo de resposta a seguir foi cortado para mostrar somente informações relevantes para o {{site.data.keyword.objectstorageshort}}.

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
  	            "url" : "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "admin"
  	          },
  	          {
  	            "id" : "38b8c081b11a452bb951698c334a406d",
  	            "region" : "london",
  	            "region_id" : "london",
  	            "url" : "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "internal"
  	          },
  	          {
  	            "id" : "4207049680fa4effbecd044c7448a8cb",
                "region" : "dallas",
                "region_id" : "dallas",
                "url" : "https://dal.objectstorage.open.softlayer.com/v1/AUTH_4abf7d7bac2c4eda89c03dd3afa7a0a3",
                "interface" : "public"
  	          },
  	          {
  	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
  	            "region" : "london",
  	            "region_id" : "london",
  	            "url" : "https://lon.objectstorage.open.softlayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "public"
  	          },
  	          {
  	            "id" : "a60cf32be624491d89170ef8264de5e8",
  	            "region" : "dallas",
  	            "region_id" : "dallas",
  	            "url" : "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "admin"
  	          },
  	          {
  	            "id" : "c769862200124a308d6748e418c971ba",
  	            "region" : "dallas",
  	            "region_id" : "dallas",
  	            "url" : "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
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

  <table>
  <caption> Tabela 1. Resposta de solicitação de post explicada </caption>
    <tr>
      <th> Terminal de resposta </th>
      <th> Explicação </th>
    </tr>
    <tr>
      <td> <code> X-Subject-Token </code> </td>
      <td> Seu token de autenticação. </td>
    </tr>
    <tr>
      <td> <code> id </code> </td>
      <td> Seu ID da instância do {{site.data.keyword.objectstorageshort}}. </td>
    </tr>
    <tr>
      <td> <code> region </code> </td>
      <td> Sua região de armazenamento. Certifique-se de selecionar a região que corresponda ao campo que é listado em suas credenciais. </td>
    </tr>
    <tr>
      <td> <code> url </code> </td>
      <td> Sua URL do {{site.data.keyword.objectstorageshort}}. </td>
    </tr>
    <tr>
      <td> <code> interface </code> </td>
      <td> A interface interna não pode ser acessada por meio do {{site.data.keyword.Bluemix_notm}}. Use a interface pública (<code>publicURL</code>). </td>
    </tr>
  </table>
