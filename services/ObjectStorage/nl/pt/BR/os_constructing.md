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


# Construindo sua URL do {{site.data.keyword.objectstorageshort}} para usar a API de REST do Swift

É possível usar a API de REST do Swift com uma interface do cliente da linha de comando, como cURL, ou chamar a API por meio do seu aplicativo.
{: shortdesc}


Para uma lista abrangente das opções e exemplos da API de REST do {{site.data.keyword.objectstorageshort}}, veja a [Referência completa da API do OpenStack Swift](http://developer.openstack.org/api-ref-objectstorage-v1.html).

Antes de editar a URL, deve-se [autenticar](/docs/services/ObjectStorage/os_authenticate.html) a instância de serviço com o Keystone. Certifique-se de observar o seu catálogo de resposta. Ele será semelhante ao exemplo a seguir.

```
{
  "id" : "4207049680fa4effbecd044c7448a8cb",
  "region" : "dallas",
  "region_id" : "dallas",
  "url" : "https://dal.objectstorage.open.softlayer.com/v1/AUTH_4abf7d7bac2c4eda89c03dd3afa7a0a3",
  "interface" : "public"
},
```
{: codeblock}


Inclua o namespace de seu contêiner e do objeto no final da URL do {{site.data.keyword.objectstorageshort}} conforme mostrado na imagem a seguir.

Partes da URL do ![{{site.data.keyword.objectstorageshort}} mostradas em uma imagem de exemplo](images/Swift_URL.png)

Figura 1. {{site.data.keyword.objectstorageshort}} Exemplo de URL
