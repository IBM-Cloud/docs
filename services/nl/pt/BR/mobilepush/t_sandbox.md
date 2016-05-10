---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Modos de ambiente de simulação e de produção

{: #push-sandboxandproduction-modes}

É possível usar o Push Notifications em um dos modos a seguir: ambiente de simulação ou de produção. Ambiente de simulação é um ambiente de teste autocontido para desenvolver e testar a integração de API push com o serviço de push do aplicativo do servidor. Você primeiro configura os modos de ambiente de simulação e produção usando o painel Push. Você alterna o modo de operação de serviço de push entre o ambiente de simulação e produção usando a [API REST de Push](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}. Por padrão, o modo de ambiente de simulação fica ativado. No entanto, ao alternar entre os modos, as tags, os dispositivos e as assinaturas não são compartilhados entre esses modos.


Quando estiver pronto para implementar o aplicativo em um ambiente de produção, selecione o modo de PRODUÇÃO, usando a API REST de Push. Para obter informações sobre a API REST, consulte a API REST.

Para alternar o modo de operação do serviço de push de ambiente de simulação para produção:

1. Use a chamada de API REST PUT ApplicationID Settings
2. No corpo de JSON, confirme se o modo foi alternado usando a chamada de API [GET ApplicationID Settings REST](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}. A resposta esperada é "mode": "PRODUCTION
 
 ```
 { 
 "mode": "PRODUCTION"
 }
 ```
1. Depois de ter alternado seu modo de ambiente, execute o código do cliente novamente para registrar seu dispositivo no modo de PRODUÇÃO.

Para obter informações sobre a API REST, consulte a API REST.
