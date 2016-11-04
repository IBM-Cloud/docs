---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Gerenciando {{site.data.keyword.objectstorageshort}} em regiões{: #multi-regions}
*Última atualização: 19 de outubro de 2016*
{: .last-updated}

O serviço {{site.data.keyword.objectstorageshort}} suporta as regiões de
armazenamento Dallas e Londres. Essas regiões de armazenamento são independentes da região do {{site.data.keyword.Bluemix_notm}}, como sul do EUA e Reino Unido, na qual a instância de serviço {{site.data.keyword.objectstorageshort}} foi criada. Se
você criar uma instância na região Sul dos EUA do {{site.data.keyword.Bluemix_notm}}, será possível ler e gravar dados na região de armazenamento Dallas ou Londres.
{: shortdesc}

Para a região sul dos EUA do {{site.data.keyword.Bluemix_notm}}, a região de armazenamento Dallas é a padrão. Para a região Reino Unido do {{site.data.keyword.Bluemix_notm}}, a região de armazenamento Londres é a padrão.  A interface com o usuário do {{site.data.keyword.objectstorageshort}} sempre ativa a região de armazenamento padrão da região do {{site.data.keyword.Bluemix_notm}}. Para alternar regiões, clique na lista suspensa da Região do {{site.data.keyword.objectstorageshort}} e escolha outra região.

**Nota:** o serviço {{site.data.keyword.objectstorageshort}} NÃO suporta replicação de região de armazenamento cruzada.

### Acesso multiregion

Para usar o serviço {{site.data.keyword.objectstorageshort}}, deve-se [autenticar no OpenStack Keystone](../ObjectStorage/os_security.html#keystone-authentication){: new_window}. Depois
de ter autenticado com êxito, um `X-Subject-Token` e os terminais
{{site.data.keyword.objectstorageshort}} estarão disponíveis na resposta. Cada região de armazenamento tem um
[ponto de acesso](../ObjectStorage/os_api.html#access-points) diferente.


Por exemplo, para criar um contêiner denominado `my_container` na
região de armazenamento Dallas, especifique um ponto de acesso Dallas no comando curl
conforme a seguir:

  ```
  curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
Você receberia o seguinte como saída:

  ```
  HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

Para criar um contêiner denominado `my_container` na região de armazenamento de Londres, especifique um ponto de acesso de Londres no comando curl, como segue:

  ```
  curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
Você receberia o seguinte como saída:

  ```
  HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

**Nota:** o `X-Subject-Token` adquirido do
Keystone, rotulado como `X-Trans-ID` no exemplo, funciona entre as
regiões de armazenamento.
