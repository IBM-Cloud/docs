---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introdução às cadeias de ferramentas (Experimental)
{: #toolchains_getting_started}

*Última atualização: 8 de junho de 2016*
{: .last-updated}  

Uma cadeia de ferramentas é um conjunto de integrações de ferramenta que suporta as tarefas de desenvolvimento, implementação e operações. O
poder coletivo de uma cadeia de ferramentas é maior que a soma de suas integrações de ferramentas individuais.
{: shortdesc}

É possível criar uma cadeia de ferramentas de duas formas: usar um modelo para criar uma cadeia de ferramentas ou criar uma cadeia de
ferramentas a partir de um app. Dependendo do modelo ou cadeia de
ferramentas que usar, a cadeia de ferramentas poderá incluir um
repositório
(repo) GitHub que é preenchido com o código de início do app e um pipeline de entrega pré-configurado. Ao
enviar por push as mudanças no repo GitHub da cadeia de
ferramentas, o pipeline de entrega automaticamente constrói e implementa o app no {{site.data.keyword.Bluemix}}.

Como um ponto de início, é possível usar um modelo de cadeia de ferramentas para criar uma cadeia de ferramentas que tenha um conjunto específico de integrações de ferramenta ou uma cadeia de ferramentas vazia em que é possível incluir integrações de ferramentas.

**Importante**: este recurso é experimental. As cadeias de ferramentas podem não ser estáveis e podem mudar de formas que
não sejam compatíveis com versões anteriores. Elas não são recomendadas para uso em ambientes de produção. Para usar cadeias de ferramentas,
deve-se fazer uma
[solicitação
para acesso](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window} única. As cadeias de ferramentas estão disponíveis na região sul dos EUA somente.


##Criando uma cadeia de ferramentas com base em um modelo   
{: #creating_a_toolchain_from_a_template}

Após sua solicitação de acesso a cadeias de ferramentas ser aprovada, será possível usar um modelo como um ponto de início para criar uma
cadeia de ferramentas que inclua um conjunto específico de integrações de ferramenta.

1. No painel DevOps, na guia **Cadeias de ferramentas**, clique em **Criar uma cadeia de ferramentas** para
criar sua primeira cadeia de ferramentas. Se você já tiver uma cadeia de ferramentas, clique no botão (+) para criar outra cadeia de ferramentas.
1. Clique em um modelo da cadeia de ferramentas. Por exemplo, para usar uma amostra de armazenamento on-line para criar a cadeia de
ferramentas, clique em **Cadeia de ferramentas de microsserviços**. 
1. Na página de criação da cadeia de ferramentas, revise o diagrama da cadeia de ferramentas que estiver prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas. O diagrama na imagem a seguir é um exemplo. Ao criar
uma cadeia de ferramentas, o diagrama mostrará cada integração de ferramenta que é parte da cadeia de ferramentas.
![Diagrama da cadeia de ferramentas](images/toolchain_diagram.png)

1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em
{{site.data.keyword.Bluemix}}. Se você já tiver uma cadeia de ferramentas com esse nome ou se desejar usar um nome diferente, mude o nome
da cadeia de ferramentas.  
1. Na seção Integrações configuráveis, selecione cada integração de ferramenta que deseja configurar para sua cadeia de ferramentas. Para
obter informações sobre configurar integrações de ferramentas, consulte [Configurando integrações de ferramenta](../toolchains/toolchains_integrations.html){: new_window}.
1. Clique em **Criar**.  Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas:

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


##Criando uma cadeia de ferramentas com base em um aplicativo
{: #creating_a_toolchain_from_an_app}

Após sua solicitação de acesso a cadeias de ferramentas ser aprovada, será possível criar uma cadeia de ferramentas do seu app. A cadeia de
ferramentas pode suportar desenvolvimento, implementação e monitoramento contínuos e mais, e é associada ao seu app. Cada app pode ser
associado a uma cadeia de ferramentas. Ao enviar por push mudanças no
repo GitHub da cadeia de ferramentas, o pipeline automaticamente
constrói e implementa o app.  

1. Em sua página Visão geral, no ladrilho Entrega contínua, clique em **Incluir cadeia de ferramentas**. Como
alternativa, no Bluemix Classic Experience, clique em **INCLUIR GIT**. Seu app é configurado para entrega contínua a partir
de um novo repo GitHub que é preenchido com o código de início do
iniciador.
1. Na página de criação da cadeia de ferramentas, revise o diagrama da cadeia de ferramentas que estiver prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas. 
1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em
{{site.data.keyword.Bluemix}}. Se você já tiver uma cadeia de ferramentas com esse nome ou se desejar usar um nome diferente, mude o nome
da cadeia de ferramentas.
1. Na seção Integrações configuráveis, selecione cada integração de ferramenta que deseja configurar para sua cadeia de ferramentas. Para
obter informações sobre configurar integrações de ferramentas, consulte [Configurando
integrações de ferramenta](../toolchains/toolchains_integrations.html){: new_window}.
1. Clique em **Criar**.  Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas:

 * A cadeia de ferramentas é criada.
 * Se você tiver configurado a integração de ferramenta Pipeline de entrega, os pipelines serão acionados.
 * Se você tiver configurado a integração de ferramenta Sauce Labs, a integração Sauce Labs será configurada para incluir tarefas nos
pipelines e executar testes.
 * Se você tiver configurado a integração de ferramenta PagerDuty, a integração PagerDuty será configurada para enviar notificações ao canal
configurado no Slack. Essas notificações indicam quando ocorre um problema.
 * Se você tiver configurado a integração de ferramenta Slack, a integração Slack será configurada para enviar notificações ao canal
configurado no Slack. Essas notificações indicam o progresso da implementação; por exemplo, `Conectado com projeto XYZ`,
`Pipeline configurado` e `Estágio 'construção' iniciado`.
 * Se você tiver configurado a integração de ferramenta
GitHub, o repo GitHub de amostra é clonado na conta do GitHub.

 
##Visualizando uma cadeia de ferramentas
{: #viewing_a_toolchain}

Após a cadeia de ferramentas e todas as integrações de ferramentas serem configuradas, será possível visualizar uma representação visual da
cadeia de ferramentas na página Integrações de ferramenta.

1. No Painel DevOps, na guia **Cadeias de ferramentas**, clique em uma cadeia de ferramentas para abrir sua página
Integrações de ferramentas. Como alternativa, na página Visão geral do app, no ladrilho Entrega contínua, clique em **Visualizar cadeia de
ferramentas** e, em seguida, clique em **Integrações de ferramenta**.
1. Revise a página para ver uma representação visual da cadeia de ferramentas.
1. Para acessar uma integração de ferramenta que esteja em sua cadeia de ferramentas, clique no ladrilho da ferramenta. 
 
 **Dica**: se você tiver mais de um
repo
GitHub, poderá ter diversos ladrilhos para a mesma integração de ferramenta
porque cada repo precisa de seu próprio pipeline.


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# Links relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}

* [Criar um aplicativo com três microsserviços](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}

## Links relacionados
{: #general}

* [Cadeia de ferramentas de microsserviços (Experimental)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Cadeia de ferramentas simples (Experimental)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM&reg; Bluemix&reg; Garage Method](https://www.ibm.com/devops/method){:new_window}
