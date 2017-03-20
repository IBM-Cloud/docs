---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Casos de uso comuns do {{site.data.keyword.openwhisk_short}}
{: #openwhisk_common_use_cases}

O modelo de execução oferecido pelo {{site.data.keyword.openwhisk_short}}
suporta diversos casos de uso. As seções a seguir incluem exemplos típicos. Para uma discussão mais detalhada da arquitetura Serverless, casos de usos de exemplo, discussão de prós e contras e melhores práticas de implementação, leia o excelente [artigo de Mike Roberts no blog do Martin Fowler](https://martinfowler.com/articles/serverless.html).
{: shortdesc}

## Microsserviços
{: #openwhisk_common_use_cases_microservices}

Apesar de seu benefício, as soluções baseadas em microsserviço continuam difíceis de serem construídas usando tecnologias de nuvem tradicionais, geralmente requerendo o controle de uma cadeia de ferramentas complexa e pipelines de construção e operações separados. As equipes pequenas e ágeis, gastando muito tempo lidando com complexidades infraestruturais e operacionais (tolerância a falhas, balanceamento de carga, ajuste automático de escala e criação de log), desejam especialmente uma forma de desenvolver código aperfeiçoado e de valor agregado com linguagens de programação que eles já conhecem e gostam e que são mais adequadas para resolver problemas específicos. 

A natureza modular e inerentemente escalável do {{site.data.keyword.openwhisk_short}} o torna ideal para implementar partes granulares de lógica em ações. As ações do {{site.data.keyword.openwhisk_short}} são independentes umas das outras e podem ser implementadas usando vários idiomas diferentes suportados pelo {{site.data.keyword.openwhisk_short}} e acessar vários sistemas backend. Cada ação pode ser implementada e gerenciada independentemente, além de ser escalada independentemente de outras ações. A interconectividade entre as ações é fornecida pelo {{site.data.keyword.openwhisk_short}} na forma de regras, sequências e convenções de nomenclatura. Isso é bom para aplicativos baseados em microsserviços.

## Apps da web
{: #openwhisk_common_use_cases_webapps}

Mesmo que o {{site.data.keyword.openwhisk_short}} tenha sido originalmente projetado para programação baseada em evento, ele oferece vários benefícios para aplicativos voltados ao usuário. Por exemplo, quando você combina isso com um pequeno stub Node.js, é possível usá-lo para entregar aplicativos que são relativamente fácil de depurar. E como os aplicativos {{site.data.keyword.openwhisk_short}} são muito menos computacionalmente intensivos do que executar um processo do servidor em uma plataforma PaaS, eles são consideravelmente mais baratos também. 

Um aplicativo da web integral pode ser construído e executado com o OpenWhisk. A combinação de APIs serverless com o hosting de arquivo estático para recursos do site, por exemplo, HTML, JavaScript e CSS, significa que podemos construir aplicativos da web serverless inteiros. A simplicidade de operar um ambiente {{site.data.keyword.openwhisk_short}} hospedado (ou melhor, não ter que operar nada porque ele está hospedado no Bluemix) é um grande benefício comparado a levantar e operar um Node.js Express ou outro tempo de execução do servidor tradicional.

Uma das coisas que ajuda é a opção da ferramenta da CLI do {{site.data.keyword.openwhisk_short}} *wsk* chamada "--annotation web-export true", que torna o código acessível em um navegador da web.

Aqui estão alguns exemplos sobre como usar o {{site.data.keyword.openwhisk_short}} para construir um app da web:
- [Ações da web: apps da web Serverless com o OpenWhisk](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba).
- [Construir um aplicativo {{site.data.keyword.openwhisk_short}} voltado ao usuário com o Bluemix e o Node.js](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Manipuladores de HTTP Serverless com o OpenWhisk](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

É certamente possível implementar aplicativos IoT usando arquiteturas de servidor tradicional, porém, em muitos casos, a combinação de diferentes serviços e pontes de dados requer pipelines flexíveis e de alto desempenho, abrangendo de dispositivos IoT a armazenamento em nuvem e uma plataforma de análise. As pontes geralmente pré-configuradas são desprovidas da programabilidade necessária para implementar e ajustar adequadamente a arquitetura de solução específica. Dada a grande variedade de possíveis pipelines e a falta de padronização em torno da fusão de dados em geral e no IoT em particular, há muitos casos em que o pipeline requer transformação de dados customizados (para conversão de formato, filtragem, aumento, etc). O {{site.data.keyword.openwhisk_short}} é uma ferramenta excelente para implementar tal transformação, de uma maneira ‘serverless’, em que a lógica customizada é hospedada em uma plataforma de nuvem totalmente gerenciada e elástica.

Os cenários de Internet of Things são frequentemente orientados por sensores de forma inerente. Por
exemplo, uma ação no {{site.data.keyword.openwhisk_short}} poderá ser
acionada se houver necessidade de reagir a um sensor que está excedendo uma determinada
temperatura. As interações IoT são geralmente stateless com potencial para um nível muito alto de carga no caso de eventos principais (desastres naturais, eventos climáticos significativos, engarrafamentos, etc.). Isso cria uma necessidade de um sistema elástico em que a carga de trabalho normal pode ser pequena, mas precisa escalar muito rapidamente com tempo de resposta previsível e capacidade para manipular um grande número de eventos sem aviso prévio no sistema. É muito difícil construir um sistema para atender esses requisitos usando arquiteturas de servidor tradicional, pois elas tendem a ser menos potentes e incapazes de manipular o pico no tráfego ou ser superprovisionadas e extremamente caras.

Há um aplicativo IoT de amostra que usa o OpenWhisk, NodeRed, Cognitive e outros serviços: [Transformação de Serverless de dados em movimento do IoT com o OpenWhisk](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt).

![Exemplo de arquitetura de solução IoT](images/IoT_solution_architecture_example.png)

## Backend da
API
{: #openwhisk_common_use_cases_iot}

As plataformas computacionais Serverless fornecem aos desenvolvedores uma maneira rápida de construir APIs sem servidores. O {{site.data.keyword.openwhisk_short}} suporta a geração automática de API de REST para ações e é muito fácil conectar a ferramenta API Management de sua escolha (como [IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) ou outra) a essas APIs de REST fornecidas pelo OpenWhisk. Semelhante a outros casos de uso, todas as considerações para escalabilidade e outras Qualidades de Serviços (QoS) se aplicam. 

Aqui está um exemplo e uma discussão de [como usar Serverless como um backend de API](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples).

## Backend móvel
{: #openwhisk_common_use_cases_mobile}

Muitos aplicativos móveis requerem lógica do lado do servidor. Para desenvolvedores de dispositivos móveis que não desejam gerenciar a lógica do lado do servidor e prefeririam manter o foco no app em execução no dispositivo ou navegador, usar o {{site.data.keyword.openwhisk_short}} como backend do lado do servidor é uma boa solução. Além disso, o suporte integrado para o Swift permite que desenvolvedores reutilizem suas qualificações existentes de programação do iOS. Os aplicativos móveis geralmente têm padrões de carregamento imprevisíveis e uma solução {{site.data.keyword.openwhisk_short}} hospedada, de modo que o IBM Bluemix pode escalar para atender praticamente a qualquer demanda de carga de trabalho sem a necessidade de provisionar recursos antecipadamente.

## Processamento de Dados
{: #openwhisk_common_use_cases_data}

Com a quantia de dados agora disponível, o desenvolvimento de aplicativo requer a capacidade de processar novos dados e, potencialmente reagir a eles. Esse requisito inclui o processamento tanto de registros do banco de dados estruturado quanto de documentos, imagens ou vídeos não estruturados. O {{site.data.keyword.openwhisk_short}} pode ser configurado por meio do sistema fornecido ou feeds customizados para reagir a mudanças nos dados e executar ações automaticamente nos feeds de dados recebidos. As ações podem ser programadas para processar mudanças, transformar formatos de dados, enviar e receber mensagens, chamar outras ações, atualizar vários armazenamentos de dados, incluindo bancos de dados relacionais baseados em SQL, grades de dados na memória, banco de dados NoSQL, arquivos, brokers de sistema de mensagens e vários outros sistemas. As regras e sequências do {{site.data.keyword.openwhisk_short}} fornecem flexibilidade para fazer mudanças no processamento de pipeline sem programação, simplesmente por meio de mudanças na configuração. Isso torna o sistema baseado no {{site.data.keyword.openwhisk_short}} altamente ágil e facilmente adaptável à mudança de requisitos.

## Cognitivo
{: #openwhisk_common_use_cases_cognitive}

As tecnologias cognitivas podem ser efetivamente combinadas com o {{site.data.keyword.openwhisk_short}} para criar aplicativos poderosos. Por exemplo, o IBM Alchemy API e o Watson Visual Recognition podem ser usados com o {{site.data.keyword.openwhisk_short}} para extrair automaticamente informações úteis dos vídeos sem precisar realmente assisti-los. 

Aqui está um aplicativo de amostra [Dark vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp) que faz exatamente isso. Neste aplicativo, o usuário faz upload de um vídeo ou imagem usando o aplicativo da web Dark Vision, que o armazena em um BD Cloudant. Após o vídeo ser transferido por upload, o {{site.data.keyword.openwhisk_short}} detecta o novo vídeo recebendo as mudanças do Cloudant (acionador). Em seguida, o {{site.data.keyword.openwhisk_short}} aciona a ação do extrator de vídeo. Durante sua execução, o extrator produz quadros (imagens) e os armazena no Cloudant. Os quadros são então processados usando o Watson Visual Recognition e os resultados são armazenados no mesmo BD Cloudant. Os resultados podem ser visualizados usando o aplicativo da web Dark Vision OU um aplicativo iOS. Além do Cloudant, o Armazenamento de objetos pode ser usado. Ao fazer isso, os metadados de vídeo e imagem são armazenados no Cloudant e os arquivos de mídia são armazenados no Armazenamento de objetos.
