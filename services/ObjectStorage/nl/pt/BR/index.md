---

copyright:
  years: 2014, 2016
---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Introdução ao {{site.data.keyword.objectstorageshort}} {: #getting-started-with-object-storage}

*Última atualização: 19 de outubro de 2016*
{: .last-updated}

O {{site.data.keyword.objectstoragefull}} fornece armazenamento de dados em nuvem não estruturado. É possível armazenar e acessar seu conteúdo, assim como interativamente compor e conectar-se a apps e serviços.
{: shortdesc}

Alguns casos de uso comuns para o serviço {{site.data.keyword.objectstorageshort}} são:

* Fazendo backup dos dados de volume de suas instâncias
* Usando como um local intermediário ao transferir grandes quantias de dados
* Transferindo dados entre os ambientes que não estão diretamente conectados
* Agindo como um armazenador central



O {{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}} fornece a você acesso a uma conta do Swift {{site.data.keyword.objectstorageshort}} totalmente provisionada para gerenciar seus dados. A criptografia no lado do provedor não é fornecida.


1.	Provisione sua instância de serviço a partir do catálogo do
{{site.data.keyword.Bluemix_notm}}. Configure sua instância e clique em
**Criar**. Se você inicialmente escolher a opção **Deixar
desvinculado** para o campo **App**, ainda será possível
ligar a instância de serviço ao seu app {{site.data.keyword.Bluemix_notm}}
posteriormente.
2. No painel da instância de serviço, crie um contêiner para começar a armazenar objetos.
3. Inclua um arquivo em seu contêiner ou depósito no menu suspenso **Ações**.
4. Para testar o acesso aos seus objetos, clique em **Fazer download** e revise o arquivo.
5. Quando estiver pronto para conectar sua instância a um aplicativo, configure as credenciais de serviço e [ligue o serviço](https://new-console.stage1.ng.bluemix.net/docs/services/reqnsi.html#add_service).



# Links relacionados
{: #rellinks}

## Referência da API
{: #api}
* [API OpenStack {{site.data.keyword.objectstorageshort}} (Swift) v1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
* [API do OpenStack Identity (Keystone) v3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}

## SDK
{: #sdk}
* [Kits de desenvolvimento de software (SDK) do OpenStack ](https://wiki.openstack.org/wiki/SDKs){: new_window}

## Tutoriais e amostras
{: #samples}
* [Conectando-se ao IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} com Java](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
* [Use o Python para acessar o {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
* [Use o PHP para alavancar o {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-php-to-leverage-object-storage-for-bluemix/){: new_window}

## Tempos de execução compatíveis
{: #buildpacks}
* [Liberty for Java](https://www.ng.bluemix.net/docs/runtimes/liberty/index.html){: new_window}
* [SDK for Node.js](https://www.ng.bluemix.net/docs/runtimes/nodejs/index.html){: new_window}
* [Go](https://www.ng.bluemix.net/docs/runtimes/go/index.html){: new_window}
* [PHP](https://www.ng.bluemix.net/docs/runtimes/php/index.html){: new_window}
* [Python](https://www.ng.bluemix.net/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://www.ng.bluemix.net/docs/runtimes/ruby/index.html){: new_window}
* [Buildpacks
de comunidade](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}


## Links relacionados
{: #general}
* [Folha de precificação do IBM {{site.data.keyword.Bluemix_notm}}](https://www.ng.bluemix.net/#/pricing){: new_window}
* [Pré-requisitos do IBM {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
