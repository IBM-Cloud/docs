---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Criando um serviço {{site.data.keyword.mobilepushshort}} desvinculado para Android
{: #create_android_unbound}
Última atualização: 11 de janeiro de 2017
{: .last-updated}

Crie uma instância de serviço do {{site.data.keyword.mobilepushshort}}. É possível usar a instância de serviço do {{site.data.keyword.mobilepushshort}} sem ligar a nenhum aplicativo backend.

1. Ligue a instância de serviço do {{site.data.keyword.mobilepushshort}} a um aplicativo Bluemix. Ao ligar, você será capaz de ver que todos os detalhes relacionados ao serviço são armazenados no formato JSON na variável de ambiente VCAP_SERVICES. 

![Ligando um serviço Push Notification](images/unbound_1.jpg)
 2. Clique em **Ligar** e escolha a instância de serviço do {{site.data.keyword.mobilepushshort}} a ser ligada. Quando o aplicativo é ligado ao serviço {{site.data.keyword.mobilepushshort}}, as informações sobre o serviço são armazenadas no formato JSON na variável de ambiente VCAP_SERVICES do app. Por exemplo: 
```
 	{
    "imfpush_Dev": [
   {
         "name": "myname_sampleUnbound",
         "label": "imfpush_Dev",
         "plan": "Basic",
         "credentials": null
      }
    ]
    }
```
	{: codeblock}
