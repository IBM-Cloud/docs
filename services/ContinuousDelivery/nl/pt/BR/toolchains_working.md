---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Trabalhando com cadeias de ferramentas
{: #toolchains_getting_started}

Última atualização: 17 de novembro de 2016
{: .last-updated}  

Uma *cadeia de ferramentas* é um conjunto de integrações de ferramentas que suporta tarefas de desenvolvimento, de implementação e de operações. O
poder coletivo de uma cadeia de ferramentas é maior que a soma de suas integrações de ferramentas individuais.
{: shortdesc}

Cadeias de ferramentas estão disponíveis nos ambientes Public e Dedicated no {{site.data.keyword.Bluemix}}. É possível criar uma cadeia de ferramentas de duas formas: usar um modelo para criar uma cadeia de ferramentas ou criar uma cadeia de
ferramentas a partir de um app. No {{site.data.keyword.Bluemix_notm}} Public, cadeias de ferramentas estão disponíveis somente na região sul dos EUA.

## Introdução às cadeias de ferramentas: Público
{: #getting_started_public}

Cada cadeia de ferramentas é associada com uma organização específica (org) e qualquer usuário que for um membro dessa organização poderá acessar as suas cadeias de ferramentas associadas. Antes de
você criar uma cadeia de ferramentas, certifique-se de estar trabalhando na organização na qual deseja criar a cadeia de ferramentas. A organização na qual você está trabalhando atualmente está exibida na barra de menus. Para alternar para outra organização, clique na organização na barra de menus e, em seguida, selecione a organização para a qual você deseja alternar.

### Criando uma cadeia de ferramentas com base em um modelo   
{: #creating_a_toolchain_from_a_template}

É possível usar um modelo como um ponto de início para [criar uma cadeia de ferramentas (o link é aberto em uma nova janela)](https://console.ng.bluemix.net/devops/create){: new_window} que inclui um conjunto específico de integrações de ferramenta. Saiba mais sobre como usar os modelos no [IBM Bluemix Garage Method (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/category/tools){:new_window}.

1. Efetue login no [{{site.data.keyword.Bluemix_notm}} (o link é aberto em uma nova janela)](http://console.ng.bluemix.net){:new_window}. O Painel do {{site.data.keyword.Bluemix_notm}} é aberto e mostra uma visão geral do espaço ativo do {{site.data.keyword.Bluemix_notm}} para sua organização.
1. No menu de hamburger, clique em **Serviços** e, em seguida, clique em **DevOps**.
1. No painel DevOps, na página **Cadeias de ferramentas**, clique em **Criar uma cadeia de ferramentas**. 
1. Na página **Criar uma cadeia de ferramentas**, clique em um modelo de cadeia de ferramentas.
1. Revise o diagrama da cadeia de ferramentas que você está prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas. O diagrama na imagem a seguir é um exemplo. Ao criar
uma cadeia de ferramentas, o diagrama mostrará cada integração de ferramenta que é parte da cadeia de ferramentas.
![Diagrama da cadeia de ferramentas](images/toolchain_diagram.png)

1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em
{{site.data.keyword.Bluemix_notm}}. Se você desejar usar um nome diferente, mude o nome da cadeia de ferramentas.  
1. Na seção Integrações configuráveis, selecione cada integração de ferramenta que deseja configurar para sua cadeia de ferramentas. Algumas integrações de ferramentas não requerem configuração. Para obter informações sobre como configurar as integrações de ferramentas, consulte [Configurando integrações de ferramentas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Clique em **Criar**.  Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas:

 * A cadeia de ferramentas é criada.
 * Se você tiver configurado a integração de ferramenta Pipeline de entrega, os pipelines serão criados e acionados.
 * Se você tiver configurado a integração de ferramenta Sauce Labs, o Sauce Labs estará configurado para incluir tarefas nos pipelines e executar testes.
 * Se você tiver configurado a integração de ferramenta PagerDuty, o PagerDuty estará configurado para enviar notificações de alerta para o serviço especificado.
 * Se você tiver configurado a integração de ferramenta Slack, o Slack estará configurado para enviar notificações de alerta sobre status de implementação para o canal especificado.
 * Se você tiver configurado a integração de ferramenta
GitHub, o repo GitHub de amostra é clonado na conta do GitHub.


### Criando uma cadeia de ferramentas com base em um aplicativo
{: #creating_a_toolchain_from_an_app}

É possível criar uma cadeia de ferramentas a partir de seu aplicativo. A cadeia de
ferramentas pode suportar desenvolvimento, implementação e monitoramento contínuos e mais, e é associada ao seu app. Cada app pode ser
associado a uma cadeia de ferramentas. Ao enviar por push mudanças no
repo GitHub da cadeia de ferramentas, o pipeline automaticamente
constrói e implementa o app.  

1. Na Página de visão geral de seu app, no quadro Entrega Contínua, clique em **Ativar**. Seu app é configurado para entrega contínua a partir
de um novo repo GitHub que é preenchido com o código de início do
iniciador.
1. Na página de criação da cadeia de ferramentas, revise o diagrama da cadeia de ferramentas que estiver prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas.
1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em
{{site.data.keyword.Bluemix_notm}}. Se você desejar usar um nome diferente, mude
o nome da cadeia de ferramentas.
1. Na seção Integrações configuráveis, selecione cada integração de ferramenta que deseja configurar para sua cadeia de ferramentas. Algumas integrações de ferramentas não requerem configuração. 
Para obter informações sobre como configurar as integrações de ferramentas, consulte
[Configurando
integrações de ferramentas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Clique em **Criar**.  Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas:

 * A cadeia de ferramentas é criada.
 * Se você tiver configurado a integração de ferramenta Pipeline de entrega, os pipelines serão criados e acionados.
 * Se você tiver configurado a integração de ferramenta Sauce Labs, o Sauce Labs estará configurado para incluir tarefas nos pipelines e executar testes.
 * Se você tiver configurado a integração de ferramenta PagerDuty, o PagerDuty estará configurado para enviar notificações de alerta para o serviço especificado.
 * Se você tiver configurado a integração de ferramenta Slack, o Slack estará configurado para enviar notificações de alerta sobre status de implementação para o canal especificado.
 * Se você tiver configurado a integração de ferramenta
GitHub, o repo GitHub de amostra é clonado na conta do GitHub.


## Introdução às cadeias de ferramentas: Dedicado
{: #getting_started_dedicated}

Cada cadeia de ferramentas é associada a uma organização específica e qualquer
usuário que for membro dessa organização poderá acessar suas cadeias de ferramentas
associadas. Antes de criar uma cadeia de ferramentas, clique no ícone
**{{site.data.keyword.avatar}}** na barra de menus para
abrir o widget de Conta e Suporte e visualizar a organização na qual você está
trabalhando. Se essa organização não for a organização na qual você deseja criar a cadeia de ferramentas, alterne para outra
organização.

### Criando uma cadeia de ferramentas com base em um modelo   
{: #creating_a_toolchain_from_a_template_dedicated}

É possível usar um modelo como um ponto de início para criar uma cadeia de ferramentas que inclua um conjunto específico de integrações de ferramentas.

1. No painel do {{site.data.keyword.Bluemix_notm}}, na guia **DEVOPS**, clique no botão incluir (+) para criar uma cadeia de ferramentas.
1. Na página **Criar uma cadeia de ferramentas**, clique em um
modelo de cadeia de ferramentas. 
1. Revise o diagrama da cadeia de ferramentas que você está prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas. O diagrama na imagem a seguir é um exemplo. Ao criar
uma cadeia de ferramentas, o diagrama mostrará cada integração de ferramenta que é parte da cadeia de ferramentas.
![Diagrama de cadeia de ferramentas dedicada](images/toolchain_dedicated_diagram.png)

1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em
{{site.data.keyword.Bluemix_notm}}. Se você já tiver uma cadeia de ferramentas com esse nome ou se desejar usar um nome diferente, mude o nome
da cadeia de ferramentas.  
1. Na seção Integrações configuráveis, selecione cada integração de ferramenta que deseja configurar para sua cadeia de ferramentas. Algumas integrações de ferramentas não requerem configuração. 
Para obter informações sobre como configurar as integrações de ferramentas, consulte
[Configurando
integrações de ferramentas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Clique em **Criar**.  Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas:

 * A cadeia de ferramentas é criada.
 * Se você tiver configurado a integração de ferramenta Pipeline de entrega, os pipelines serão criados e acionados.
 * Se você tiver configurado a integração de ferramenta PagerDuty, o PagerDuty estará configurado para enviar notificações de alerta para o serviço especificado.
 * Se você tiver configurado a integração de ferramenta Slack, o Slack estará configurado para enviar notificações de alerta sobre status de implementação para o canal especificado.
 * Se você tiver configurado a integração de ferramenta do GitHub Enterprise, o repositório GitHub Enterprise será clonado na sua conta do GitHub Enterprise.


### Criando uma cadeia de ferramentas com base em um aplicativo
{: #creating_a_toolchain_from_an_app_dedicated}

É possível criar uma cadeia de ferramentas a partir de seu aplicativo. A cadeia de
ferramentas pode suportar desenvolvimento, implementação e monitoramento contínuos e mais, e é associada ao seu app. Cada app pode ser
associado a uma cadeia de ferramentas. Quando você envia por push as mudanças no repositório GitHub Enterprise da cadeia de ferramentas, a pipeline automaticamente constrói e implementa o aplicativo.  

1. No canto superior direito de sua página Visão geral do aplicativo, clique em **Incluir cadeia de ferramentas**. O seu aplicativo é configurado para entrega contínua a partir
de um novo repositório GitHub Enterprise que é preenchido com o código de início do aplicativo.
1. Na página de criação da cadeia de ferramentas, revise o diagrama da cadeia de ferramentas que estiver prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas.
1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em
{{site.data.keyword.Bluemix_notm}}. Se você já tiver uma cadeia de ferramentas com esse nome ou se desejar usar um nome diferente, mude o nome
da cadeia de ferramentas.
1. Na seção Integrações configuráveis, selecione cada integração de ferramenta que deseja configurar para sua cadeia de ferramentas. Algumas integrações de ferramentas não requerem configuração. 
Para obter informações sobre como configurar as integrações de ferramentas, consulte
[Configurando
integrações de ferramentas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Clique em **Criar**.  Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas:

 * A cadeia de ferramentas é criada.
 * Se você tiver configurado a integração de ferramenta Pipeline de entrega, os pipelines serão criados e acionados.
 * Se você tiver configurado a integração de ferramenta PagerDuty, o PagerDuty estará configurado para enviar notificações de alerta para o serviço especificado.
 * Se você tiver configurado a integração de ferramenta Slack, o Slack estará configurado para enviar notificações de alerta sobre status de implementação para o canal especificado.
 * Se você tiver configurado a integração de ferramenta do GitHub Enterprise, o repositório GitHub Enterprise será clonado na sua conta do GitHub Enterprise.


## Visualizando uma cadeia de ferramentas
{: #viewing_a_toolchain}

Após configurar a cadeia de ferramentas e as suas integrações de ferramenta, é possível visualizar uma representação visual da cadeia de ferramentas.

* Se você usar o {{site.data.keyword.Bluemix_notm}} Public, no painel do DevOps, na página **Cadeias de ferramentas**, clique em uma cadeia de ferramentas para abrir sua página Visão geral. Como alternativa,
na página Visão geral do app, no ladrilho Entrega contínua, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique em **Visão geral**. 
   
* Se você usar o {{site.data.keyword.Bluemix_notm}} Dedicated, no Painel, na guia **DEVOPS**, clique na cadeia de ferramentas para abrir a sua página Integrações de ferramentas. Como alternativa, no canto superior direito da página Visão geral do aplicativo, clique em **Visualizar cadeia de ferramentas**.

* Para acessar uma integração de ferramenta que estiver em sua cadeia de ferramentas, clique no ladrilho da ferramenta. 
 
 **Dica**: se você tiver mais de um repositório GitHub ou GitHub Enterprise, poderá ter múltiplos ladrilhos para a mesma integração de ferramenta porque cada repositório é
representado por seu próprio ladrilho.


# Links relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}

* [Crie e use sua primeira cadeia de ferramentas (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Crie uma cadeia de ferramentas customizada (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Crie um aplicativo com três microsserviços (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [Crie uma cadeia de ferramentas a partir de um modelo em {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Crie uma cadeia de ferramentas a partir de um app em {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Links relacionados
{: #general}

* [Cadeia de ferramentas de microsserviços (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Cadeia de ferramentas simples (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (O link é aberto em uma nova janela)](https://www.ibm.com/devops/method){:new_window}
