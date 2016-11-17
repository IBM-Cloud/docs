---

copyright:
  years: 2016
lastupdated: "2016-10-27"

---
<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}

# Resolução de problemas do {{site.data.keyword.iotinsurance_short}}
{: #ts}

Aqui estão as respostas para questões comuns sobre resolução de problemas quanto ao uso de {{site.data.keyword.iotinsurance_full}} no {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problemas na implementação de apps
{: #deployingapps}
Talvez não seja possível implementar os apps para o {{site.data.keyword.iotinsurance_short}} se não houver memória livre suficiente em sua organização do {{site.data.keyword.Bluemix_notm}}. É
possível reduzir a memória que seus apps usam ou aumentar a cota de memória para sua conta.
{:shortdesc}

Ao abrir o serviço do {{site.data.keyword.iotinsurance_short}}, a função Implementar não está ativada e não é possível implementar apps.
{: tsSymptoms}

Pelo menos 2 GB de memória livre devem estar disponíveis em sua organização para ativar a função Implementar. Contas para teste têm uma cota máxima de memória de 2 GB. Se você tiver criado serviços ou apps diferentes do {{site.data.keyword.iotinsurance_short}}, sua organização não terá memória suficiente para implementar os aplicativos do {{site.data.keyword.iotinsurance_short}}.
{: tsCauses}

É possível aumentar a cota de memória de sua conta ou reduzir a memória que seus serviços e apps usam.
- Para aumentar a cota de memória de sua conta, é possível [converter sua conta para teste para uma conta paga](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).
- Para reduzir a memória em uso rapidamente, remova todos os serviços e apps diferentes de {{site.data.keyword.iotinsurance_short}}. Reinicie o serviço do {{site.data.keyword.iotinsurance_short}} para que as mudanças entrem em vigor.
- Para contas pagas que têm mais de 2 GB de memória total, talvez você possa evitar a remoção de outros apps ou serviços ajustando a quantia de memória que eles usam. Para obter
informações, consulte [O limite de memória da organização foi excedido](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory).
{: tsResolve}

## Problemas de desempenho
{: #performance_issues}

Durante períodos de atividade de pico, você pode ter desempenho lento.
{:shortdesc}

Sistemas ocupados que fazem chamadas frequentes de API podem ter atrasos nos tempos de resposta.
{: tsSymptoms}

Por padrão, o {{site.data.keyword.iotinsurance_short}} implementa uma versão de avaliação do {{site.data.keyword.cloudantfull}}. Essa versão limita o número de chamadas de API que podem ser feitas por segundo.
{: tsCauses}

Faça upgrade para a versão padrão do {{site.data.keyword.cloudant}}.
{: tsResolve}

## Obtendo ajuda e suporte para o {{site.data.keyword.iotinsurance_short}}
{: #gettinghelp}

Se você tiver problemas ou perguntas ao usar o
{{site.data.keyword.iotinsurance_full}}, será possível verificar o
{{site.data.keyword.Bluemix_notm}} ou obter ajuda procurando informações ou
perguntando em um fórum. Também
é possível abrir um chamado de suporte.

* É possível verificar se o {{site.data.keyword.Bluemix_notm}} está disponível acessando a
[página de status do
Bluemix](https://developer.ibm.com/bluemix/support/#status){:new_window}.

* Você pode revisar os fóruns para ver se outros usuários tiveram o mesmo problema. Ao usar os fóruns para fazer uma pergunta, marque a sua pergunta para que ela possa ser vista pelas equipes de desenvolvimento do {{site.data.keyword.Bluemix_notm}}.
  <!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->
* Se você tiver questões técnicas sobre como desenvolver ou implementar um app
com o {{site.data.keyword.iotinsurance_short}}, poste sua pergunta em
[Stack
Overflow](http://stackoverflow.com/search?q=iot-insurance+ibm-bluemix){:new_window} e identifique-a com "ibm-bluemix" e "iot-for-insurance".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* Para perguntas sobre o serviço e instruções de introdução, use o fórum do
[IBM
developerWorks dW Answers](https://developer.ibm.com/answers/topics/iot-insurance/?smartspace=bluemix){:new_window}. Inclua as tags "iot-for-insurance" e "bluemix".

Consulte [Obtendo ajuda](https://www.{DomainName}/docs/support/index.html#getting-help) para obter mais detalhes sobre o
uso dos fóruns.

* Se você ainda não puder resolver o problema, será possível abrir um chamado de suporte IBM. Para obter informações sobre como abrir um chamado de suporte IBM ou sobre níveis de suporte e severidades de chamado, consulte [Entrando em contato com o suporte](https://www.{DomainName}/docs/support/index.html#contacting-support).


# Links Relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}
* [Código de app móvel de amostra no GitHub](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## Referência de API
{: #api}
* [API do {{site.data.keyword.iotinsurance_short}}](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [Exemplos de API do {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## Links Relacionados
{: #general}
* [Documentação do {{site.data.keyword.iot_full}}](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Fórum de suporte do desenvolvedor](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
  * [Fórum de suporte do Stack overflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
