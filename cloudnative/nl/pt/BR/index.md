---

copyright:
  years: 2016, 2017
lastupdated: "2016-04-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Construindo projetos nativos de nuvem
{: #web-mobile}

É possível gerenciar apps nativos de nuvem por meio do conceito de [Projetos](projects.html) do {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}. É possível criar um projeto usando o [{{site.data.keyword.dev_console}}](devex.html) ou a [{{site.data.keyword.dev_cli_notm}}](dev_cli.html) para o {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}} CLI. O {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} traz as competências de serviços mais comuns que são necessárias a um desenvolvedor de aplicativo nativo de nuvem para uma experiência única e conectada que foi otimizada para o desenvolvedor.

O {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} permite que um desenvolvedor de aplicativo nativo de nuvem crie um projeto usando uma variedade de [tipos padrão](patterns.html) e [Iniciadores](starters.html), crie e conecte os principais serviços otimizados pelo {{site.data.keyword.Bluemix_notm}} ao projeto e faça download rapidamente do código de trabalho com SDKs. Os SDKs estão totalmente integrados a credenciais ou dependências de recurso que permitem tê-los em execução em minutos. Quando seu aplicativo está em execução e você instalou e configurou recursos, é possível retornar ao projeto para monitorar e gerenciar engajamento com os usuários do aplicativo. Também é possível configurar e gerenciar os serviços por meio do {{site.data.keyword.dev_console}}.

<!--
While the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} provides an integrated development experience, some developers might still want to have finer-grained control and wire services together manually. If this is your preferred approach, you might want to consider using the [{{site.data.keyword.mobilefirstbp}} Starter boilerplate](try_mobile.html).
-->

<!--With {{site.data.keyword.Bluemix}} Mobile services, you can incorporate pre-built, managed, and scalable cloud services into your mobile applications. You can focus on building your mobile apps, instead of the complexities of managing the back-end infrastructure.

The Mobile dashboard provides an integrated experience on {{site.data.keyword.Bluemix_notm}} where you can create mobile projects easily from within the dashboard.
-->


## Projects
{: #projects}

O {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} combina a interface com o usuário do app, dados e serviços em um *projeto* completo. Ao criar um
projeto, todas as partes necessárias de seu app e os recursos incluídos são mantidos no
servidor {{site.data.keyword.Bluemix_notm}}. Será possível fazer download do código de app e das credenciais e inicializadores necessários, se os serviços estiverem configurados em seu projeto. É possível visualizar todos os seus projetos selecionando **Projetos**.  

É possível visualizar informações adicionais sobre um único projeto, selecionando-o na página **Projetos**. Isso exibe a página **Visão geral do projeto**, que inclui os serviços que estão configurados e disponíveis para o projeto. Serviços são recursos
separados que estendem seu app incluindo uma função. Como são incluídos individualmente, é possível incluir os serviços necessários, como serviços de push, autenticação, dados e armazenamento ou outros serviços. Ao
incluir um serviço em seu projeto na página **Visão geral do projeto** e seguir as instruções para configurá-la, ela será
automaticamente associada ao seu app. Para obter mais informações sobre a página Visão geral do projeto, consulte [página Visão geral do projeto](project_overview_page.html).

Para criar seu projeto, deve-se selecionar um [padrão](patterns.html), seguido por um [iniciador](starters.html).


### Página Visão geral do projeto
{: #project_overview}

É possível visualizar e trabalhar com um único projeto do {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}, selecionando o projeto na página **Projetos**, que abre a página Visão geral do projeto. 
{: shortdesc}

A página **Visão geral do projeto** exibe um quadro para cada recurso que está configurado ou disponível para configuração com o projeto selecionado. O quadro exibe o tipo do recurso e um botão *ações* com três pontos alinhados verticalmente. Exemplos de recursos que podem estar disponíveis ou configurados incluem {{site.data.keyword.mobilepushshort}}, Analítica ou Dados e armazenamento. Os recursos compatíveis dependem do tipo de projeto e dos recursos que estão disponíveis nessa região, portanto, nem todos eles estarão disponíveis para serem associados a todos os projetos. 

Quando um tipo de recurso ainda não está associado ao projeto, um botão **Criar** é exibido no quadro. As opções do botão de ações são para criar uma instância do serviço ou para incluir uma instância de serviço existente quando o recurso ainda não estiver associado. Selecionar **Incluir existente** fornece uma lista das instâncias de serviço desse tipo em seu espaço.

Se o recurso já estiver associado a esse projeto, o nome da instância de serviço associada será exibido no quadro depois do tipo de recurso. Isso facilita localizar qual instância de serviço está relacionada a esse projeto no {{site.data.keyword.dev_console}}. As ações que estão disponíveis no botão de ações são **Visualizar** e **Remover** quando o recurso já está associado ao projeto. A remoção de uma instância de serviço remove apenas a associação a esse projeto e não exclui a instância de serviço do {{site.data.keyword.dev_console}}. Para excluir uma instância de serviço, clique na página **Web e Dispositivo móvel > Serviços** para visualizar e excluir as instâncias de serviço.

Selecione **Obter o código** no quadro **Código** para fazer download do código para seu projeto. Para obter mais informações sobre como fazer download do código, veja [Obter código](get_code.html).


### Atualizando seu projeto para usar um novo Iniciador
{: #update-starter}

1. Na página **Projetos** ou **Visão geral do projeto**, clique no ícone do **Menu overflow** e selecione **Atualizar Iniciador**.

2. Escolha um novo Iniciador e clique em **Atualizar**.

3. Clique em **Obter o código** na página **Visão geral do projeto** para selecionar sua linguagem.

   Como alternativa, é possível clicar na página **Código**.


### Atualizando seu projeto para gerar uma nova linguagem
{: #update-language}

1. Nas páginas **Projetos** ou **Visão geral do projeto**, clique no ícone do **Menu overflow** e selecione **Atualizar Iniciador**.

2. Selecione uma nova linguagem e clique em **Atualizar**.

3. Clique em **Obter o código** na página **Visão geral do projeto** para selecionar sua linguagem.


## Tipos de Padrões
{: #patterns}

Padrões nativos da nuvem são designs comprovados que ajudam a assegurar uma topologia consistente, escalável e confiável para seus aplicativos. Ao criar um projeto, serão apresentados diferentes tipos padrão dos quais é possível escolher. Basta selecionar o tipo padrão e os recursos que você deseja incorporar ao projeto. Depois de definir as preferências do projeto, um projeto iniciador é gerado para você editar, executar ou depurar e implementar localmente ou no {{site.data.keyword.Bluemix}}.


### Aplicativo Web
{: #web}

Os projetos da web incluem a capacidade de entregar conteúdo da web, como HTML, JavaScript e folhas de estilo para o servidor da web.

Os iniciadores da web a seguir estão disponíveis:

* Basic Web: entrega um arquivo `index.html` estático, folha de estilo padrão e vazia, além do arquivo JavaScript.
* Webpack: cria um projeto em que os arquivos de origem ECMAScript 6 (ES6) estão em `src/client` e são compilados com o WebPack para torná-los reduzidos e convertidos para uso no navegador.
* Webpack + React: uma estrutura avançada para construir interfaces com o usuário. Os arquivos de origem estão em `src/client/app` e serão compilados com o WebPack e entregues no diretório público.


### Aplicativo Remoto
{: #mobile}

Os padrões de app móvel ajudam a construir apps móveis que se conectam diretamente aos serviços de backend, como {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}},
{{site.data.keyword.appid_short}} e muito mais. Os projetos também podem ser incluídos por meio de sdkGen, como BFFs e Microsserviços.

É possível escolher em uma lista de iniciadores, como {{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}}, {{site.data.keyword.openwhisk_short}} e muito mais.

É possível gerar os apps móveis em Swift, Android ou Cordova.


### Backend for Frontend (BFF)
{: #bff}

Os padrões de Backend for Frontend, comumente conhecidos como BFFs, ajudam a focar na exposição de dados de negócios e serviços em um formato que corresponde aos requisitos de interação com o usuário. Para otimizar uma jornada do usuário para sua solução de nuvem, pode ser necessária uma jornada de usuário diferente para o aplicativo móvel e uma jornada mais detalhada e mais rica para o aplicativo da web. Com a introdução de dispositivos controlados por voz, como o serviço [{{site.data.keyword.conversationfull}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/conversation.html), a interação com um usuário poderia ser controlada por voz. Esse canal digital requererá um BFF muito diferente para gerenciar essas interações baseadas em intenção de voz.

Com o {{site.data.keyword.Bluemix_notm}}, é possível construir um BFF usando abordagem de programação poliglota para definir o BFF. A IBM recomenda usar Node.js, Swift ou Java e executá-los em um padrão nativo de nuvem com o Cloud Foundry, serviços de Contêiner ou sem servidor.

O BFF gerenciará a integração com serviços para persistência de dados, armazenamento em cache e integração com serviços de alto valor, como o {{site.data.keyword.ibmwatson}}, o {{site.data.keyword.iot_short_notm}}, o {{site.data.keyword.weather_short}} e de análise de dados, como o {{site.data.keyword.sparks}}.

O BFF exporá uma API mais comumente usando um padrão de REST, mas será possível projetar o BFF para trabalhar de uma arquitetura de sistema de mensagens usando o {{site.data.keyword.messagehub}}.

Um iniciador BFF Basic está disponível usando Node.js ou Swift.


### Microsserviço
{: #microservice}

Os projetos de microsserviço fornecem a base para construir microsserviços de backend, incluindo um terminal básico de funcionamento, uma API de REST. Os projetos gerados conterão todas as dependências necessárias tanto para o próprio microsserviço quanto para qualquer serviço de nuvem anexado.

Um iniciador Microservice Basic está disponível usando Java.

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


### Linguagens
{: #languages notoc}

As linguagens suportadas são:

   * [Java ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](../runtimes/swift/getting-started.html){: new_window}


#### Compilador Java
{: #java notoc}

O Java possui recursos comprovados para construir aplicativos de nível corporativo. Mas os novos recursos em Java 8, combinados com os tempos de execução mais leves, como o Liberty e estruturas, como o Spring Boot, tornam o Java perfeitamente adequado para a construção de microsserviços também.


#### Node.js
{: #node notoc}

O Node.js é um tempo de execução JavaScript que usa um modelo de E/S não bloqueador orientado a eventos, tornando-o leve e eficiente, destacando-se no rendimento e na escalabilidade para aplicativos da web, padrões backend-for-front-end e microsserviços. O ecossistema de pacote do Node.js, npm, fornece acesso a uma grande coleção de módulos de software livre, fornecendo uma ampla gama de recursos para acelerar o desenvolvimento de seu aplicativo.


#### Swift
{: #swift notoc}

Swift é uma linguagem de programação moderna criada pela Apple em 2014, que foi projetada para substituir o uso de Objective C e tornou-se software livre em dezembro de 2015. Hoje, ela é usada para construir iOS, macOS, serviços da web e software de sistemas nos sistemas operacionais Linux e macOS usando a arquitetura x86, ARM ou Z. É escrita como uma linguagem de script, mas é compilada para obter alto desempenho como C, com baixa sobrecarga, tornando-a ideal para tempos de execução de nuvem. Usa um sistema de tipo forte e estático visto em Java, mas o estilo funcional e as rotinas assíncronas vistos em JavaScript. Tem um excelente aproveitamento e a origem é compilada em código nativo usando a cadeia de ferramentas do compilador LLVM e pode usar as bibliotecas de sistema estrangeiras escritas em C facilmente.


## Dispositivos de Arranque
{: #starters}

Com o {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}, é possível escolher entre uma variedade de iniciadores para cada tipo padrão.

Os iniciadores são otimizados para ser o código iniciador pronto para produção que foca na demonstração de uma integração principal do {{site.data.keyword.Bluemix_notm}} a um serviço de alto valor. Cada iniciador
foca em um serviço e mostra a integração dos SDKs de serviço no código. Em alguns casos, os iniciadores oferecem uma experiência de usuário simples para destacar a integração dos dados de serviço ou as interações com o usuário. Cada iniciador será configurado para ser ativado com Autenticação, Dados e, possivelmente, outros recursos, se você decidir configurá-los para seu projeto.
