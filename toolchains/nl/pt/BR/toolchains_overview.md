---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introdução às cadeias de ferramentas (Experimental)
{: #toolchains_getting_started}

Última atualização: 17 de agosto de 2016
{: .last-updated}  

As cadeias de ferramentas estão disponíveis nos ambientes Public e Dedicated no {{site.data.keyword.Bluemix}}. É possível criar uma cadeia de ferramentas de duas formas: usar um modelo para criar uma cadeia de ferramentas ou criar uma cadeia de
ferramentas a partir de um app.
{: shortdesc}

**Importante**: este recurso é experimental. As cadeias de ferramentas podem não ser estáveis e podem mudar de maneiras incompatíveis com as versões anteriores. Elas não são recomendadas para uso em ambientes de produção. 
No {{site.data.keyword.Bluemix_notm}} Public, cadeias de ferramentas estão disponíveis somente na região sul dos EUA.


##Introdução às cadeias de ferramentas: Public
{: #getting_started_public}

Cada cadeia de ferramentas é associada a uma organização específica (org) e qualquer usuário que for um membro dessa organização poderá acessar as suas cadeias de ferramentas associadas. Antes de criar uma cadeia, certifique-se de estar trabalhando na organização em que você deseja criar a cadeia de ferramentas. Para alternar para outra
organização, clique no ícone **{{site.data.keyword.avatar}}** ![ícone Avatar](../icons/i-avatar-icon.svg) na barra de menus para abrir o widget de Conta e suporte.

###Criando uma cadeia de ferramentas com base em um modelo   
{: #creating_a_toolchain_from_a_template}

É possível usar um modelo como um ponto de início para criar uma cadeia de ferramentas que inclui um conjunto específico de integrações de ferramenta.

1. Se você estiver criando a sua primeira cadeia de ferramentas, certifique-se de que as cadeias de ferramentas estejam ativadas em sua organização:
   1. Abra o painel do DevOps e clique na guia **Cadeias de ferramentas**.
   2. Se o botão **Ativar cadeias de ferramentas** for mostrado, clique nele e siga os avisos para criar a sua cadeia de ferramentas.
   3. Se o botão **Ativar cadeias de ferramentas** não for mostrado, as cadeias de ferramentas já estarão ativadas. Continue
na etapa 2.
1. No painel do DevOps, na guia **Cadeias de ferramentas**, clique no botão de inclusão (+) para criar uma cadeia de ferramentas.
1. Clique em um modelo da cadeia de ferramentas. Por exemplo, para usar uma amostra de armazenamento on-line para criar a cadeia de ferramentas, clique em **Cadeia de ferramentas de
microsserviços**. 
1. Na página de criação da cadeia de ferramentas, revise o diagrama da cadeia de ferramentas que estiver prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas. O diagrama na imagem a seguir é um exemplo. Ao criar
uma cadeia de ferramentas, o diagrama mostrará cada integração de ferramenta que é parte da cadeia de ferramentas.
![Diagrama da cadeia de ferramentas](images/toolchain_diagram.png)

1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em {{site.data.keyword.Bluemix_notm}}. Se você já tiver uma cadeia de ferramentas com esse nome ou se desejar usar um nome diferente, mude o nome
da cadeia de ferramentas.  
1. Na seção Integrações configuráveis, selecione cada integração de ferramenta que deseja configurar para sua cadeia de ferramentas. Algumas integrações de ferramenta não requerem nenhuma configuração. Para
obter informações sobre configurar integrações de ferramentas, consulte [Configurando
integrações de ferramenta](../toolchains/toolchains_integrations.html){: new_window}.
1. Clique **Criar**.  Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas:

 * A cadeia de ferramentas é criada.
 * Se você tiver configurado a integração de ferramenta Pipeline de entrega, os pipelines serão acionados.
 * Se você tiver configurado a integração de ferramenta Sauce Labs, a integração Sauce Labs será configurada para incluir tarefas nos
pipelines e executar testes.
 * Se você tiver configurado a integração de ferramenta PagerDuty, a integração PagerDuty será configurada para enviar notificações
ao canal configurado no Slack. Essas notificações indicam quando ocorre um problema.
 * Se você tiver configurado a integração de ferramenta Slack, a integração Slack será configurada para enviar notificações ao canal
configurado no Slack. Essas notificações indicam o progresso da implementação; por exemplo, `Conectado com projeto XYZ`,
`Pipeline configurado` e `Estágio 'construção' iniciado`.
 * Se você tiver configurado a integração de ferramenta
GitHub, o repo GitHub de amostra é clonado na conta do GitHub.


###Criando uma cadeia de ferramentas com base em um aplicativo
{: #creating_a_toolchain_from_an_app}

É possível criar uma cadeia de ferramentas a partir de seu aplicativo. A cadeia de
ferramentas pode suportar desenvolvimento, implementação e monitoramento contínuos e mais, e é associada ao seu app. Cada app pode ser
associado a uma cadeia de ferramentas. Ao enviar por push mudanças no
repo GitHub da cadeia de ferramentas, o pipeline automaticamente
constrói e implementa o app.  

1. Se você estiver criando a sua primeira cadeia de ferramentas, certifique-se de que as cadeias de ferramentas estejam ativadas em sua organização:
   1. Abra o painel do DevOps e clique na guia **Cadeias de ferramentas**.
   2. Se o botão **Ativar cadeias de ferramentas** for mostrado, clique nele e siga os avisos para criar a sua cadeia de ferramentas.
   3. Se o botão **Ativar cadeias de ferramentas** não for mostrado, as cadeias de ferramentas já estarão ativadas. Continue
na etapa 2.
1. Em sua página Visão geral, no ladrilho Entrega contínua, clique em **Incluir cadeia de ferramentas**. Como alternativa, no {{site.data.keyword.Bluemix_notm}} Classic
Experience, no canto superior direito da página Visão geral do aplicativo, clique em **Incluir cadeia de ferramentas**. Seu app é configurado para entrega contínua a partir
de um novo repo GitHub que é preenchido com o código de início do
aplicativo.
1. Na página de criação da cadeia de ferramentas, revise o diagrama da cadeia de ferramentas que estiver prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas.
1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em {{site.data.keyword.Bluemix_notm}}. Se você já tiver uma cadeia de ferramentas com esse nome ou se desejar usar um nome diferente, mude o nome
da cadeia de ferramentas.
1. Na seção Integrações configuráveis, selecione cada integração de ferramenta que deseja configurar para sua cadeia de ferramentas. Algumas integrações de ferramenta não requerem nenhuma configuração. Para
obter informações sobre configurar integrações de ferramentas, consulte [Configurando
integrações de ferramenta](../toolchains/toolchains_integrations.html){: new_window}.
1. Clique **Criar**.  Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas:

 * A cadeia de ferramentas é criada.
 * Se você tiver configurado a integração de ferramenta Pipeline de entrega, os pipelines serão acionados.
 * Se você tiver configurado a integração de ferramenta Sauce Labs, a integração Sauce Labs será configurada para incluir tarefas nos
pipelines e executar testes.
 * Se você tiver configurado a integração de ferramenta PagerDuty, a integração PagerDuty será configurada para enviar notificações
ao canal configurado no Slack. Essas notificações indicam quando ocorre um problema.
 * Se você tiver configurado a integração de ferramenta Slack, a integração Slack será configurada para enviar notificações ao canal
configurado no Slack. Essas notificações indicam o progresso da implementação; por exemplo, `Conectado com projeto XYZ`,
`Pipeline configurado` e `Estágio 'construção' iniciado`.
 * Se você tiver configurado a integração de ferramenta
GitHub, o repo GitHub de amostra é clonado na conta do GitHub.


##Introdução às cadeias de ferramentas: Dedicated
{: #getting_started_dedicated}

Cada cadeia de ferramentas é associada a uma organização específica (org) e qualquer usuário que for um membro dessa organização poderá acessar as suas cadeias de ferramentas associadas. Antes de
criar uma cadeia de ferramentas, clique no ícone **{{site.data.keyword.avatar}}** ![ícone Avatar](../icons/i-avatar-icon.svg) na barra de menus para
abrir o widget de Conta e suporte e visualizar a organização na qual você está trabalhando. Se essa organização não for a organização na qual você deseja criar a cadeia de ferramentas, alterne para outra organização.

###Criando uma cadeia de ferramentas com base em um modelo   
{: #creating_a_toolchain_from_a_template_dedicated}

É possível usar um modelo como um ponto de início para criar uma cadeia de ferramentas que inclui um conjunto específico de integrações de ferramenta.

1. Se você estiver criando a sua primeira cadeia de ferramentas, certifique-se de que as cadeias de ferramentas estejam ativadas em sua organização:
   1. Abra o painel do DevOps e clique na guia **Cadeias de ferramentas**.
   2. Se o botão **Ativar cadeias de ferramentas** for mostrado, clique nele e siga os avisos para criar a sua cadeia de ferramentas.
   3. Se o botão **Ativar cadeias de ferramentas** não for mostrado, as cadeias de ferramentas já estarão ativadas. Continue
na etapa 2.
1. No {{site.data.keyword.Bluemix_notm}} Dashboard, na guia **DEVOPS**, clique no botão de inclusão (+) para criar uma cadeia de ferramentas.
1. Clique em um modelo da cadeia de ferramentas. Por exemplo, para criar uma cadeia de ferramentas simples para implementar um novo aplicativo Cloud Foundry, clique em
**Cadeia de ferramentas simples do Cloud Foundry**. 
1. Na página de criação da cadeia de ferramentas, revise o diagrama da cadeia de ferramentas que estiver prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas. O diagrama na imagem a seguir é um exemplo. Ao criar
uma cadeia de ferramentas, o diagrama mostrará cada integração de ferramenta que é parte da cadeia de ferramentas.
![Diagrama de cadeia de ferramentas dedicada](images/toolchain_dedicated_diagram.png)

1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em {{site.data.keyword.Bluemix_notm}}. Se você já tiver uma cadeia de ferramentas com esse nome ou se desejar usar um nome diferente, mude o nome
da cadeia de ferramentas.  
1. Na seção Integrações configuráveis, selecione cada integração de ferramenta que deseja configurar para sua cadeia de ferramentas. Algumas integrações de ferramenta não requerem nenhuma configuração. Para
obter informações sobre configurar integrações de ferramentas, consulte [Configurando
integrações de ferramenta](../toolchains/toolchains_integrations.html){: new_window}.
1. Clique **Criar**.  Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas:

 * A cadeia de ferramentas é criada.
 * Se você tiver configurado a integração de ferramenta Pipeline de entrega, os pipelines serão acionados.
 * Se você configurou a integração de ferramenta GitHub Enterprise, o repositório de amostra GitHub Enterprise será clonado em sua conta do GitHub Enterprise.


###Criando uma cadeia de ferramentas com base em um aplicativo
{: #creating_a_toolchain_from_an_app_dedicated}

É possível criar uma cadeia de ferramentas a partir de seu aplicativo. A cadeia de
ferramentas pode suportar desenvolvimento, implementação e monitoramento contínuos e mais, e é associada ao seu app. Cada app pode ser
associado a uma cadeia de ferramentas. Quando você enviar mudanças por push para o repositório GitHub Enterprise da cadeia de ferramentas, o pipeline automaticamente construirá e implementará o aplicativo.  

1. Se você estiver criando a sua primeira cadeia de ferramentas, certifique-se de que as cadeias de ferramentas estejam ativadas em sua organização:
   1. Abra o painel do DevOps e clique na guia **Cadeias de ferramentas**.
   2. Se o botão **Ativar cadeias de ferramentas** for mostrado, clique nele e siga os avisos para criar a sua cadeia de ferramentas.
   3. Se o botão **Ativar cadeias de ferramentas** não for mostrado, as cadeias de ferramentas já estarão ativadas. Continue
na etapa 2.
1. No canto superior direito da página Visão geral do aplicativo, clique em **Incluir cadeia de ferramentas**. O seu aplicativo é configurado para entrega contínua a partir
de um novo repositório GitHub Enterprise que é preenchido com o código de início do aplicativo.
1. Na página de criação da cadeia de ferramentas, revise o diagrama da cadeia de ferramentas que estiver prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas.
1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em {{site.data.keyword.Bluemix_notm}}. Se você já tiver uma cadeia de ferramentas com esse nome ou se desejar usar um nome diferente, mude o nome
da cadeia de ferramentas.
1. Na seção Integrações configuráveis, selecione cada integração de ferramenta que deseja configurar para sua cadeia de ferramentas. Algumas integrações de ferramenta não requerem nenhuma configuração. Para
obter informações sobre configurar integrações de ferramentas, consulte [Configurando
integrações de ferramenta](../toolchains/toolchains_integrations.html){: new_window}.
1. Clique **Criar**.  Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas:

 * A cadeia de ferramentas é criada.
 * Se você tiver configurado a integração de ferramenta Pipeline de entrega, os pipelines serão acionados.
 * Se você configurou a integração de ferramenta GitHub Enterprise, o repositório de amostra GitHub Enterprise será clonado em sua conta do GitHub Enterprise.


##Visualizando uma cadeia de ferramentas
{: #viewing_a_toolchain}

Após configurar a cadeia de ferramentas e as suas integrações de ferramenta, será possível visualizar uma representação visual da cadeia de ferramentas na página Integrações de ferramenta.

* Se você usar o {{site.data.keyword.Bluemix_notm}} Public, no painel do DevOps, na guia **Cadeias de ferramentas**, clique em uma cadeia de ferramentas para abrir a sua
página Integrações de ferramenta. Como
alternativa, na página Visão geral do app, no ladrilho Entrega contínua, clique em **Visualizar cadeia de ferramentas**. Em
seguida, clique em **Integrações de ferramenta**. 
   
* Se você usar o {{site.data.keyword.Bluemix_notm}} Dedicated, no painel, na guia **DEVOPS**, clique na cadeia de ferramentas para abrir a sua página Integrações de
ferramenta. Como alternativa, no canto superior direito da página Visão geral do aplicativo, clique em **Visualizar cadeia de ferramentas**.

* Para acessar uma integração de ferramenta que está em sua cadeia de ferramentas, clique no ladrilho da ferramenta. 
 
 **Dica**: se você tiver mais de um repositório GitHub ou GitHub Enterprise, poderá ter múltiplos ladrilhos para a mesma integração de ferramenta porque cada repositório é
representado pelo seu próprio ladrilho.


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# Links Relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}

* [Criar um aplicativo com três microsserviços](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}
* [Criar uma cadeia de ferramentas a partir de um modelo no {{site.data.keyword.Bluemix_notm}} Dedicated
(Experimental)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Criar uma cadeia de ferramentas a partir de um aplicativo no {{site.data.keyword.Bluemix_notm}}
Dedicated (Experimental)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Links Relacionados
{: #general}

* [Cadeia de ferramentas de microsserviços (Experimental)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Cadeia de ferramentas simples (Experimental)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method](https://www.ibm.com/devops/method){:new_window}
