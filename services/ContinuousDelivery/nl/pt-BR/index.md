---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introdução ao {{site.data.keyword.contdelivery_short}}
{: #cd_getting_started}

Última atualização: 18 de novembro de 2016
{: .last-updated}  

Adote uma abordagem DevOps usando {{site.data.keyword.contdelivery_full}}, que inclui cadeias de ferramentas que automatizam a construção e implementação de aplicativos. É possível começar criando uma cadeia de ferramentas de implementação simples que suporte as tarefas de desenvolvimento, implementação e operações.
{: shortdesc}

Depois de criar uma instância de {{site.data.keyword.contdelivery_short}}
selecionando seu quadro de serviço no catálogo do
{{site.data.keyword.Bluemix_notm}}, será possível escolher como você deseja
começar a usar o serviço.
 ![Página de boas-vindas da Entrega contínua](images/cd_landing_page.png)

 * Para iniciar rapidamente e implementar seu aplicativo usando um pipeline
automatizado, na seção "Iniciando com um pipeline", clique em
**[Iniciar aqui](#starting_with_a_pipeline)**. Posteriormente,
será possível incluir mais ferramentas. 
 * Para criar e configurar uma cadeia de ferramentas de entrega contínua a partir
de um modelo, na seção "Iniciando a partir de um modelo de cadeia de ferramentas", clique
em **[Iniciar aqui](#starting_from_a_toolchain_template)**. A
cadeia de ferramentas integra ferramentas para planejar, desenvolver, implementar
pipelines e gerenciar aplicativos. Sempre é possível incluir ou remover ferramentas de
suas cadeias de ferramentas.
 * Se você já tiver cadeias de ferramentas, na seção "Iniciando a partir de
um modelo de cadeia de ferramentas", clique em **Visualizar suas cadeias de
ferramentas**. Para obter mais informações sobre como trabalhar com cadeias de ferramentas, consulte
[Usando cadeias de
ferramentas no Bluemix público](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}.

##Iniciando com um pipeline
{: #starting_with_a_pipeline}

Os pipelines automatizam construções, implementações e muito mais. Para iniciar com um pipeline automatizado, selecione um modelo e forneça o local de seu repositório GitHub (repo).

Para
[criar um
pipeline (o link é aberto em uma nova janela)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} que esteja
configurado para implementar um aplicativo Cloud Foundry, siga estas etapas:

1. Clique em **Cloud Foundry**.
1. Se você desejar usar um nome diferente para o pipeline, mude o nome padrão. O
nome do pipeline o identifica no {{site.data.keyword.Bluemix_notm}}. 
1. Se você desejar usar um nome diferente para o aplicativo, mude o nome padrão. O
nome do aplicativo o identifica no {{site.data.keyword.Bluemix_notm}}. Esse nome é o aplicativo no qual o pipeline é implementado. 
1. Se você não tiver uma cadeia de ferramentas, será criada uma com um nome padrão. Se você desejar usar um nome diferente para a cadeia de ferramentas, mude o nome. Os
pipelines são gerenciados pelas cadeias de ferramentas. Com a cadeia de ferramentas, é possível ampliar os recursos de seu pipeline por meio da integração com outras ferramentas e serviços.  

 **Dica**: os pipelines e as cadeias de ferramentas pertencem às
organizações (orgs). Se você pertencer a uma organização que tenha cadeias de ferramentas,
será possível usar essas cadeias de ferramentas mesmo que você não as tenha criado.
 
1. Selecione a cadeia de ferramentas que deseja usar ou digite um nome para a nova cadeia de ferramentas que deseja criar.
1. Forneça o local de seu repositório GitHub.

 **Dica**: se você não estiver autorizado o {{site.data.keyword.Bluemix_notm}} a acessar o GitHub, será solicitado a clicar em **Autorizar** para acessar o website do GitHub. Se você não
tiver uma sessão GitHub ativa, será solicitado que efetue login. Clique em **Autorizar aplicativo** para permitir que o {{site.data.keyword.Bluemix_notm}} acesse sua conta GitHub. Se
você tiver uma sessão GitHub ativa, mas não tiver inserido sua senha recentemente, poderá ser solicitado que insira sua senha GitHub para
confirmar.

   * Se você tiver um repositório GitHub e desejar usá-lo, para o tipo de repositório, selecione **Link**. Procure o local do repositório e
selecione-o na lista de repositórios disponíveis.
   
   * Se você desejar criar um repositório GitHub vazio, para o tipo de repositório, selecione **Novo**. Digite um nome para o repositório.
   
   * Se você desejar criar um clone de um repositório GitHub, para o tipo de
repositório, selecione **Copiar**. Procure o local do repositório e
selecione-o na lista de repositórios disponíveis.
   
   * Se desejar bifurcar um repositório GitHub para que possa contribuir com as mudanças por meio de solicitações pull, selecione **Bifurcar**. Procure o local do repositório e
selecione-o na lista de repositórios disponíveis.
 
1. Clique em **Criar**. O pipeline é criado, configurado e exibido na página Visão geral da cadeia de ferramentas.
 ![Título do pipeline](images/cd_pipeline.png)
 
Para criar um
[pipeline
vazio (o link é aberto em uma nova janela)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} sem qualquer estágio
pré-configurado:

1. Clique em **Customizado**.
1. Se você desejar usar um nome diferente para o pipeline, mude o nome padrão. O
nome do pipeline o identifica no {{site.data.keyword.Bluemix_notm}}. 
1. Se você não tiver uma cadeia de ferramentas, será criada uma com um nome padrão. Se você desejar usar um nome diferente para a cadeia de ferramentas, mude o nome. Os pipelines são gerenciados pelas cadeias de ferramentas. Com a cadeia de ferramentas, é possível ampliar os recursos de seu pipeline por meio da integração com outras ferramentas e serviços. 
1. Selecione a cadeia de ferramentas que deseja usar ou digite um nome para a nova cadeia de ferramentas que deseja criar.
1. Clique em **Criar**. Um pipeline vazio é criado e
representado como um quadro na página Visão geral da cadeia de ferramentas.

##Iniciando a partir de um modelo de cadeia de ferramentas
{: #starting_from_a_toolchain_template}

Para criar e configurar uma cadeia de ferramentas de entrega contínua a partir de um
[modelo (o link é aberto em uma
nova janela)](https://console.ng.bluemix.net/devops/create){: new_window}:

1. Na página **Criar uma cadeia de ferramentas**, clique em um
modelo de cadeia de ferramentas.  
1. Revise o diagrama da cadeia de ferramentas que você está prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas. O diagrama na imagem a seguir é um exemplo. Ao criar
uma cadeia de ferramentas, o diagrama mostrará cada integração de ferramenta que é parte da cadeia de ferramentas.
 ![Toolchain_diagram](images/toolchain_diagram.png)
1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em
{{site.data.keyword.Bluemix_notm}}. Se você desejar usar um nome diferente, mude
o nome da cadeia de ferramentas.
1. Na seção Integrações configuráveis, selecione cada integração de ferramenta que deseja configurar para sua cadeia de ferramentas. Algumas integrações de ferramentas não requerem configuração. 
Para obter informações sobre como configurar as integrações de ferramentas, consulte
[Configurando
integrações de ferramentas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Clique em **Criar**. Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas:

 * A cadeia de ferramentas é criada.
 * Se você tiver configurado a integração de ferramenta Pipeline de entrega, os pipelines serão criados e acionados.
 * Se você tiver configurado a integração de ferramenta Sauce Labs, o Sauce Labs estará configurado para incluir tarefas nos pipelines e executar testes.
 * Se você tiver configurado a integração de ferramenta PagerDuty, o PagerDuty estará configurado para enviar notificações de alerta para o serviço especificado. 
 * Se você tiver configurado a integração de ferramenta Slack, o Slack estará configurado para enviar notificações de alerta sobre status de implementação para o canal especificado. 
 * Se você tiver configurado a integração de ferramenta
GitHub, o repo GitHub de amostra é clonado na conta do GitHub. 

# Links relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}

* [Crie e use sua primeira cadeia de ferramentas (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Crie uma cadeia de ferramentas customizada (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Crie um aplicativo com três microsserviços (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}

## Links relacionados
{: #general}

* [Cadeia de ferramentas de microsserviços (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Cadeia de ferramentas simples (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (O link é aberto em uma nova janela)](https://www.ibm.com/devops/method){:new_window}
