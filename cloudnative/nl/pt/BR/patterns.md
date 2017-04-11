
---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Tipos de Padrões
{: #patterns}

Padrões nativos da nuvem são designs comprovados que ajudam a assegurar uma topologia consistente, escalável e confiável para seus aplicativos. Ao criar um projeto, serão apresentados diferentes tipos padrão dos quais é possível escolher. Basta selecionar o tipo padrão e os recursos que você deseja incorporar ao projeto. Depois de definir as preferências do projeto, um projeto iniciador é gerado para você editar, executar ou depurar e implementar localmente ou no {{site.data.keyword.Bluemix}}.

## Aplicativo Web
{: #web}

Os projetos da web incluem a capacidade de entregar conteúdo da web, como HTML, JavaScript e folhas de estilo para o servidor da web.

Os iniciadores da web a seguir estão disponíveis:

* Basic Web: entrega um arquivo `index.html` estático, folha de estilo padrão e vazia, além do arquivo JavaScript.
* Webpack: cria um projeto em que os arquivos de origem ECMAScript 6 (ES6) estão em `src/client` e são compilados com o WebPack para torná-los reduzidos e convertidos para uso no navegador.
* Webpack + React: uma estrutura avançada para construir interfaces com o usuário. Os arquivos de origem estão em `src/client/app` e serão compilados com o WebPack e entregues no diretório público.


## Aplicativo Remoto
{: #mobile}

Os padrões de app móvel ajudam a construir apps móveis que se conectam diretamente aos serviços de backend, como {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}},
{{site.data.keyword.appid_short}} e muito mais. Os projetos também podem ser incluídos por meio de sdkGen, como BFFs e Microsserviços.

É possível escolher em uma lista de iniciadores, como {{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}}, {{site.data.keyword.openwhisk_short}} e muito mais.

É possível gerar os apps móveis em Swift, Android ou Cordova.


## Backend for Frontend (BFF)
{: #bff}

Os padrões de Backend for Frontend, comumente conhecidos como BFFs, ajudam a focar na exposição de dados de negócios e serviços em um formato que corresponde aos requisitos de interação com o usuário. Para otimizar uma jornada do usuário para sua solução de nuvem, pode ser necessária uma jornada de usuário diferente para o aplicativo móvel e uma jornada mais detalhada e mais rica para o aplicativo da web. Com a introdução de dispositivos controlados por voz, como o serviço [{{site.data.keyword.conversationfull}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/conversation.html), a interação com um usuário poderia ser controlada por voz. Esse canal digital requererá um BFF muito diferente para gerenciar essas interações baseadas em intenção de voz.

Com o {{site.data.keyword.Bluemix_notm}}, é possível construir um BFF usando abordagem de programação poliglota para definir o BFF. A IBM recomenda usar Node.js, Swift ou Java e executá-los em um padrão nativo de nuvem com o Cloud Foundry, serviços de Contêiner ou sem servidor.

O BFF gerenciará a integração com serviços para persistência de dados, armazenamento em cache e integração com serviços de alto valor, como o {{site.data.keyword.ibmwatson}}, o {{site.data.keyword.iot_short_notm}}, o {{site.data.keyword.weather_short}} e de análise de dados, como o {{site.data.keyword.sparks}}.

O BFF exporá uma API mais comumente usando um padrão de REST, mas será possível projetar o BFF para trabalhar de uma arquitetura de sistema de mensagens usando o {{site.data.keyword.messagehub}}.

Um iniciador BFF Basic está disponível usando Node.js ou Swift.


## Microsserviço
{: #microservice}

Os projetos de microsserviço fornecem a base para construir microsserviços de backend, incluindo um terminal básico de funcionamento, uma API de REST. Os projetos gerados conterão todas as dependências necessárias tanto para o próprio microsserviço quanto para qualquer serviço de nuvem anexado.

Um iniciador Microservice Basic está disponível usando Java.

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


## Linguagens
{: #languages notoc}

As linguagens suportadas são:

   * [Java ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](../runtimes/swift/getting-started.html){: new_window}


### Compilador Java
{: #java notoc}

O Java possui recursos comprovados para construir aplicativos de nível corporativo. Mas os novos recursos em Java 8, combinados com os tempos de execução mais leves, como o Liberty e estruturas, como o Spring Boot, tornam o Java perfeitamente adequado para a construção de microsserviços também.


### Node.js
{: #node notoc}

O Node.js é um tempo de execução JavaScript que usa um modelo de E/S não bloqueador orientado a eventos, tornando-o leve e eficiente, destacando-se no rendimento e na escalabilidade para aplicativos da web, padrões backend-for-front-end e microsserviços. O ecossistema de pacote do Node.js, npm, fornece acesso a uma grande coleção de módulos de software livre, fornecendo uma ampla gama de recursos para acelerar o desenvolvimento de seu aplicativo.


### Swift
{: #swift notoc}

Swift é uma linguagem de programação moderna criada pela Apple em 2014, que foi projetada para substituir o uso de Objective C e tornou-se software livre em dezembro de 2015. Hoje, ela é usada para construir iOS, macOS, serviços da web e software de sistemas nos sistemas operacionais Linux e macOS usando a arquitetura x86, ARM ou Z. É escrita como uma linguagem de script, mas é compilada para obter alto desempenho como C, com baixa sobrecarga, tornando-a ideal para tempos de execução de nuvem. Usa um sistema de tipo forte e estático visto em Java, mas o estilo funcional e as rotinas assíncronas vistos em JavaScript. Tem um excelente aproveitamento e a origem é compilada em código nativo usando a cadeia de ferramentas do compilador LLVM e pode usar as bibliotecas de sistema estrangeiras escritas em C facilmente.
