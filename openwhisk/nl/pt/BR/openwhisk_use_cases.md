---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
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

Outro argumento importante em favor do {{site.data.keyword.openwhisk_short}} é o custo de um sistema em uma configuração de recuperação de desastre. Vamos comparar microsserviços com PaaS ou CaaS versus o uso do {{site.data.keyword.openwhisk_short}}. Supondo-se que tenhamos 10 microsserviços usando contêineres ou tempos de execução do CloudFoundry, são 10 processos em execução contínua e faturáveis em uma única zona de disponibilidade, 20 quando executados em 2 AZs e 40 quando executados em 2 regiões com duas zonas cada um. Ao fazer o mesmo executando os microsserviços no {{site.data.keyword.openwhisk_short}}, será possível executar os microsserviços em tantos AZs e regiões quantos você quiser, sem ter que pagar um centavo por custos incrementais.

O [Logistics Wizard](https://www.ibm.com/blogs/bluemix/2017/02/microservices-multi-compute-approach-using-cloud-foundry-openwhisk/) é um aplicativo de amostra de classificação corporativa que alavanca o {{site.data.keyword.openwhisk_short}} e o CloudFoundry para construir aplicativos no estilo de 12 fatores. É uma solução inteligente de gerenciamento da cadeia de suprimento que visa simular um ambiente que executa um sistema ERP. Ele aumenta esse sistema ERP com aplicativos para melhorar a visibilidade e a agilidade de gerenciadores da cadeia de suprimento.

## Apps da web
{: #openwhisk_common_use_cases_webapps}

Dada a natureza orientada a eventos do {{site.data.keyword.openwhisk_short}}, ele oferece vários benefícios para aplicativos voltados para o usuário, enquanto as solicitações de HTTP provenientes do navegador do usuário servem como os eventos. Os aplicativos {{site.data.keyword.openwhisk_short}} usam a capacidade de cálculo e são faturados apenas quando estão entregando solicitações do usuário. Não existe espera inativa ou modo de espera. Isso torna o {{site.data.keyword.openwhisk_short}} consideravelmente menos caro em comparação com contêineres tradicionais ou aplicativos CloudFoundry que podem passar a maior parte do tempo simplesmente esperando pela solicitação recebida do usuário e sendo cobrados por todo esse tempo "inativo". 

É possível construir e executar um aplicativo da web completo com o {{site.data.keyword.openwhisk_short}}. A combinação de APIs serverless com o hosting de arquivo estático para recursos do site, por exemplo, HTML, JavaScript e CSS, significa que podemos construir aplicativos da web serverless inteiros. A simplicidade de operação de um ambiente hospedado do {{site.data.keyword.openwhisk_short}} (ou melhor, não ter que operar nada porque ele está hospedado no Bluemix) é um grande benefício comparado ao suporte e operação de um Node.js Express ou a outro tempo de execução tradicional do servidor.

Aqui estão alguns exemplos sobre como usar o {{site.data.keyword.openwhisk_short}} para construir um app da web:
- [Ações da web: apps da web Serverless com o {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba).
- [Construir um aplicativo {{site.data.keyword.openwhisk_short}} voltado ao usuário com o Bluemix e o Node.js](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Manipuladores de HTTP Serverless com o {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

Os cenários de Internet of Things são frequentemente orientados por sensores de forma inerente. Por
exemplo, uma ação no {{site.data.keyword.openwhisk_short}} poderá ser
acionada se houver necessidade de reagir a um sensor que está excedendo uma determinada
temperatura. As interações IoT são geralmente stateless com potencial para um nível muito alto de carga no caso de eventos principais (desastres naturais, eventos climáticos significativos, engarrafamentos, etc.). Isso cria uma necessidade de um sistema elástico em que a carga de trabalho normal pode ser pequena, mas precisa escalar muito rapidamente com tempo de resposta previsível e capacidade para manipular um grande número de eventos sem aviso prévio no sistema. É muito difícil construir um sistema para atender a esses requisitos usando arquiteturas de servidor tradicionais, pois elas tendem a ser menos potentes e incapazes de manipular o pico no tráfego ou ser superprovisionadas e extremamente caras.

É certamente possível implementar aplicativos IoT usando arquiteturas de servidor tradicional, porém, em muitos casos, a combinação de diferentes serviços e pontes de dados requer pipelines flexíveis e de alto desempenho, abrangendo de dispositivos IoT a armazenamento em nuvem e uma plataforma de análise. As pontes geralmente pré-configuradas são desprovidas da programabilidade necessária para implementar e ajustar adequadamente a arquitetura de solução específica. Dada a grande variedade de possíveis pipelines e a falta de padronização em torno da fusão de dados em geral e no IoT em particular, há muitos casos em que o pipeline requer transformação de dados customizados (para conversão de formato, filtragem, aumento, etc). O {{site.data.keyword.openwhisk_short}} é uma ferramenta excelente para implementar tal transformação, de uma maneira ‘serverless’, em que a lógica customizada é hospedada em uma plataforma de nuvem totalmente gerenciada e elástica.

Aqui está um aplicativo IoT de amostra que usa o {{site.data.keyword.openwhisk_short}}, o NodeRed, o Cognitive e outros serviços: [Transformação de Serverless de dados em movimento do IoT com o {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt).

![Exemplo de arquitetura de solução IoT](images/IoT_solution_architecture_example.png)

## Backend da
API
{: #openwhisk_common_use_cases_iot}

As plataformas computacionais Serverless fornecem aos desenvolvedores uma maneira rápida de construir APIs sem servidores. O {{site.data.keyword.openwhisk_short}} suporta a geração automática de API de REST para ações. O [recurso experimental](./apigateway.md) do {{site.data.keyword.openwhisk_short}} permite que você chame uma ação com métodos de HTTP, além do POST e sem a chave API de autorização da ação por meio do API Gateway do {{site.data.keyword.openwhisk_short}}. Esse recurso é útil não apenas para expor APIs a consumidores externos, mas também para construir aplicativos de microsserviços.

Além disso, as ações do {{site.data.keyword.openwhisk_short}} podem ser conectadas a uma ferramenta API Management de sua preferência (como [IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) ou outra). Semelhante a outros casos de uso, todas as considerações para escalabilidade e outras Qualidades de Serviços (QoS) se aplicam. 

[Emoting](https://github.com/l2fprod/openwhisk-emoting) é um app de amostra que usa ações do {{site.data.keyword.openwhisk_short}} via API de REST.

Aqui está um exemplo e uma discussão de [como usar Serverless como um backend de API](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples).

## Backend móvel
{: #openwhisk_common_use_cases_mobile}

Muitos aplicativos móveis requerem lógica do lado do servidor. Considerando que os
desenvolvedores de dispositivos móveis geralmente não têm experiência no gerenciamento
de lógica do lado do servidor e prefeririam focar no app em execução no dispositivo, usar
o {{site.data.keyword.openwhisk_short}} como backend do lado do servidor é uma
boa solução. Além disso, o suporte integrado para o Swift do lado do servidor permite que os desenvolvedores reutilizem suas qualificações existentes de programação do iOS. Os aplicativos móveis geralmente têm padrões de carregamento imprevisíveis e uma solução {{site.data.keyword.openwhisk_short}} hospedada, de modo que o IBM Bluemix pode escalar para atender praticamente a qualquer demanda de carga de trabalho sem a necessidade de provisionar recursos antecipadamente.

[Skylink](https://github.com/IBM-Bluemix/skylink) é um aplicativo de amostra que permite conectar uma aeronave drone via iPad ao IBM Cloud com análise de imagem quase em tempo real alavancando o {{site.data.keyword.openwhisk_short}}, o IBM Cloudant, o IBM Watson e o Alchemy Vision.

[BluePic](https://github.com/IBM-Swift/BluePic) é um aplicativo de compartilhamento de fotos e imagens que permite tirar fotos e compartilhá-las com outros usuários do BluePic. Esse aplicativo demonstra como alavancar, em um aplicativo móvel iOS 10, um aplicativo do servidor baseado no Kitura escrito em Swift; usa o {{site.data.keyword.openwhisk_short}}, o Cloudant, o Object Storage para dados de imagem. O AlchemyAPI também é usado na sequência do {{site.data.keyword.openwhisk_short}} para analisar a imagem e extrair tags de texto com base no conteúdo da imagem e, em seguida, para enviar uma notificação push para o usuário.

## Processamento de Dados
{: #openwhisk_common_use_cases_data}

Com a quantia de dados agora disponível, o desenvolvimento de aplicativo requer a capacidade de processar novos dados e, potencialmente reagir a eles. Esse requisito inclui o processamento tanto de registros do banco de dados estruturado quanto de documentos, imagens ou vídeos não estruturados. O {{site.data.keyword.openwhisk_short}} pode ser configurado por meio do sistema fornecido ou feeds customizados para reagir a mudanças nos dados e executar ações automaticamente nos feeds de dados recebidos. As ações podem ser programadas para processar mudanças, transformar formatos de dados, enviar e receber mensagens, chamar outras ações, atualizar vários armazenamentos de dados, incluindo bancos de dados relacionais baseados em SQL, grades de dados na memória, banco de dados NoSQL, arquivos, brokers de sistema de mensagens e vários outros sistemas. As regras e sequências do {{site.data.keyword.openwhisk_short}} fornecem flexibilidade para fazer mudanças no processamento de pipeline sem programação, simplesmente por meio de mudanças na configuração. Isso torna o sistema baseado no {{site.data.keyword.openwhisk_short}} altamente ágil e facilmente adaptável à mudança de requisitos.

O projeto [OpenChecks](https://github.com/krook/openchecks) é uma prova de conceito que mostra como o {{site.data.keyword.openwhisk_short}} pode ser usado para processar o depósito de verificações em uma conta bancária usando reconhecimento de caractere ótico. Ele é construído atualmente no serviço público Bluemix {{site.data.keyword.openwhisk_short}} e baseia-se no Cloudant e no SoftLayer Object Storage. No local, ele poderia usar o CouchDB e o OpenStack Swift. Outros serviços de armazenamento poderiam incluir o FileNet ou o Cleversafe. O Tesseract fornece a biblioteca OCR.
## Cognitivo
{: #openwhisk_common_use_cases_cognitive}

As tecnologias cognitivas podem ser efetivamente combinadas com o {{site.data.keyword.openwhisk_short}} para criar aplicativos poderosos. Por exemplo, o IBM Alchemy API e o Watson Visual Recognition podem ser usados com o {{site.data.keyword.openwhisk_short}} para extrair automaticamente informações úteis dos vídeos sem precisar realmente assisti-los. Isso pode ser simplesmente uma extensão "cognitiva" do caso de uso [Processamento de dados](#data-processing) discutido anteriormente. Outro bom uso para o {{site.data.keyword.openwhisk_short}} é implementar a função Bot combinada com serviços cognitivos. 

Aqui está um aplicativo de amostra [Dark vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp) que faz exatamente isso. Neste aplicativo, o usuário faz upload de um vídeo ou imagem usando o aplicativo da web Dark Vision, que o armazena em um BD Cloudant. Após o vídeo ser transferido por upload, o {{site.data.keyword.openwhisk_short}} detecta o novo vídeo recebendo as mudanças do Cloudant (acionador). Em seguida, o {{site.data.keyword.openwhisk_short}} aciona a ação do extrator de vídeo. Durante sua execução, o extrator produz quadros (imagens) e os armazena no Cloudant. Os quadros são então processados usando o Watson Visual Recognition e os resultados são armazenados no mesmo BD Cloudant. Os resultados podem ser visualizados usando o aplicativo da web Dark Vision OU um aplicativo iOS. Além do Cloudant, o Armazenamento de objetos pode ser usado. Ao fazer isso, os metadados de vídeo e imagem são armazenados no Cloudant e os arquivos de mídia são armazenados no Object Storage.

Aqui está um [aplicativo iOS Swift de exemplo](https://github.com/gconan/BluemixMobileServicesDemoApp) que mostra o {{site.data.keyword.openwhisk_short}}, o IBM Mobile Analytics e o Watson para analisar o sinal e postar em um canal do Slack.

## Processamento de eventos com o Kafka ou o Message Hub 

O {{site.data.keyword.openwhisk_short}} é muito adequado para ser usado em combinação com Kafka, serviço IBM Message Hub (baseado em Kafka) e outros sistemas de mensagens. A natureza orientada a eventos desses sistemas requer que o tempo de execução orientado a eventos processe mensagens e aplique lógica de negócios a essas mensagens, que é exatamente o que o {{site.data.keyword.openwhisk_short}} fornece com seus feeds, acionadores, ações, etc. O Kafka e o Message Hub são frequentemente usados para volumes de carga de trabalho muito altos e imprevisíveis e requerem que os consumidores dessas mensagens precisem ser escaláveis em um aviso do momento, que é novamente um ponto favorável para o {{site.data.keyword.openwhisk_short}}. O {{site.data.keyword.openwhisk_short}} possui capacidade integrada para consumir mensagens, bem como mensagens de publicação fornecidas no pacote [openwhisk-package-kafka](https://github.com/openwhisk/openwhisk-package-kafka).

Aqui está um [aplicativo de exemplo que implementa o cenário de processamento de eventos](https://github.com/IBM/openwhisk-data-processing-message-hub) com o {{site.data.keyword.openwhisk_short}}, o Message Hub e o Kafka.
