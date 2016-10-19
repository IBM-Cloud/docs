---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Resolução de problemas do {{site.data.keyword.iot_short_notm}}
{: #ts}
Última atualização: 1 de agosto de 2016
{: .last-updated}

Aqui estão as respostas às perguntas comuns de resolução de problemas sobre o
uso do {{site.data.keyword.iot_full}} no
{{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problema ao se conectar ao {{site.data.keyword.iot_short_notm}}
{: #connection_problem}

Sua conexão com o {{site.data.keyword.iot_short_notm}} cai ou desconecta inesperadamente.
{:shortdesc}

Ao tentar se conectar ao {{site.data.keyword.iot_short_notm}}, seu dispositivo ou aplicativo recebe um erro.
{: tsSymptoms}

Você pode ter dois dispositivos tentando se conectar com o mesmo clientID e credenciais. Apenas uma conexão exclusiva é permitida por clientID. Não é possível ter duas conexões simultâneas usando o mesmo ID. Os aplicativos podem compartilhar a mesma chave API (interface de programação de aplicativos), mas MQTT requer que o ID do cliente sempre seja exclusivo.
{: tsCauses}

É possível resolver esse problema confirmando que você não tem dois dispositivos tentando se conectar usando as mesmas credenciais.
{: tsResolve}

## O dispositivo desconecta-se de forma intermitente do {{site.data.keyword.iot_short_notm}}
{: #disconnection_problem}

Sua conexão de dispositivo com o {{site.data.keyword.iot_short_notm}} cai de forma intermitente inesperadamente.
{:shortdesc}

Um dispositivo que está conectado ao serviço do {{site.data.keyword.iot_short_notm}} é desconectado de forma intermitente. O dispositivo reconecta-se, mas é desconectado inesperadamente mais uma vez após algum tempo.
{: tsSymptoms}

Pode ser que ao conectar-se você esteja usando um valor para uma opção de ping MQTT que é muito baixa, o que faz parecer que a conexão atingiu o tempo limite. Por exemplo, se o cliente MQTT estiver configurado incorretamente, os pings não serão recebidos em tempo hábil e a conexão é fechada.
{: tsCauses}

É possível corrigir este problema, confirmando se você configurou corretamente o ping e os parâmetros de KeepAlive para sua conexão.   
{: tsResolve}


## Obtendo ajuda e suporte para o {{site.data.keyword.iot_short_notm}}
{: #gettinghelp}

Se você tiver problemas ou perguntas ao usar o
{{site.data.keyword.iot_short_notm}},
será possível obter ajuda procurando informações ou fazendo perguntas
por meio de um fórum. Também é possível abrir um chamado de suporte.

Ao usar os fóruns para fazer uma pergunta, marque a sua pergunta para que ela possa ser vista pelas equipes de desenvolvimento do {{site.data.keyword.Bluemix_notm}}.

* Se você tiver perguntas técnicas sobre como desenvolver ou implementar um aplicativo com o {{site.data.keyword.iot_short_notm}}, poste sua pergunta em [Estouro da capacidade](http://stackoverflow.com/search?q=watson-iot+ibm-bluemix){:new_window} e identifique sua pergunta com "ibm-bluemix" e "watson-iot".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* Para perguntas sobre o serviço e as instruções de introdução, use o fórum do [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/watson-iot/?smartspace=bluemix){:new_window}. Inclua as identificações "watson-iot" e "bluemix".

Consulte
[Obtendo
ajuda](https://www.{DomainName}/docs/support/index.html#getting-help) para obter mais detalhes sobre o uso dos fóruns.

Para obter informações sobre como abrir um chamado de suporte
IBM ou sobre os níveis de suporte e severidades de chamado, consulte
[Entrando
em contato com o suporte](https://www.{DomainName}/docs/support/index.html#contacting-support).
