---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Modos de ambiente de simulação e de produção
{: #push-sandboxandproduction-modes}
Última atualização: 11 de janeiro de 2017
{: .last-updated}

É possível usar o {{site.data.keyword.mobilepushshort}} em um dos modos a seguir: ambiente de
simulação ou produção. Ambiente de simulação é um ambiente de teste autocontido para desenvolver e testar a integração de API push com o serviço de push do aplicativo do servidor. 

Configure os modos de ambiente de simulação e produção usando o painel Push. É possível alternar entre o modo de operações de serviço de push, entre o ambiente de simulação e produção usando a [API de REST de Push](https://mobile.{DomainName}/imfpush/){: new_window}. Por padrão, o
modo de ambiente de simulação é ativado. No entanto, ao alternar entre os modos, as tags, os dispositivos e as assinaturas não são compartilhados entre esses modos.

Quando você estiver pronto para implementar o aplicativo em um ambiente de produção, selecione o modo PRODUÇÃO usando a [API de REST de Push](https://mobile.{DomainName}/imfpush/){: new_window}. 

Para alternar o modo de operação do serviço de push de ambiente de simulação para produção:

1. Use a chamada de API REST PUT ApplicationID Settings
2. No corpo de JSON, confirme se o modo foi alternado usando a chamada de API [GET ApplicationID Settings REST](https://mobile.{DomainName}/imfpush/){: new_window}. A resposta esperada é "mode": "PRODUCTION
```{ 
    "mode": "PRODUCTION"
    }
```
	{: codeblock}
1. Depois de ter alternado seu modo de ambiente, execute o código do cliente novamente para registrar seu dispositivo no modo de PRODUÇÃO.

Para obter informações sobre a API REST, consulte [Usando APIs REST](t_restapi.html).
