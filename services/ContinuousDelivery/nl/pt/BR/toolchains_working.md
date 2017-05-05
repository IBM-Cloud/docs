---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-7"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Criando cadeias de ferramentas
{: #toolchains_getting_started}

Uma *cadeia de ferramentas* é um conjunto de integrações de ferramentas que suporta tarefas de desenvolvimento, de implementação e de operações. O
poder coletivo de uma cadeia de ferramentas é maior que a soma de suas integrações de ferramentas individuais.
{: shortdesc}

As cadeias de ferramentas abertas estão disponíveis nos ambientes Public e Dedicated no {{site.data.keyword.Bluemix}}. É possível criar uma cadeia de ferramentas de duas formas: usar um modelo para criar uma cadeia de ferramentas ou criar uma cadeia de
ferramentas a partir de um app. No {{site.data.keyword.Bluemix_notm}} Public, cadeias de ferramentas estão disponíveis somente na região sul dos EUA.

Cada cadeia de ferramentas é associada a uma organização específica (org) e qualquer usuário que seja membro dessa organização poderá ser incluído na lista de controle de acesso de qualquer uma de suas cadeias de ferramentas associadas. Para obter mais informações sobre o controle de acesso de cadeias de ferramentas, veja [Gerenciando o acesso](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}. Antes de
você criar uma cadeia de ferramentas, certifique-se de estar trabalhando na organização na qual deseja criar a cadeia de ferramentas. A organização na qual você está trabalhando é exibida na barra de menus. Para alternar para outra organização, clique na organização na barra de menus e selecione a organização para a qual você deseja alternar.


##Criando uma cadeia de ferramentas com base em um modelo   
{: #creating_a_toolchain_from_a_template}

É possível usar um modelo como um ponto de início para [criar uma cadeia de ferramentas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/devops/create){: new_window} que inclua um conjunto específico de integrações de ferramentas. Saiba mais sobre como usar os modelos no [IBM Cloud Garage Method ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/category/tools){:new_window}.

1. Se você usar o {{site.data.keyword.Bluemix_notm}} Public, efetue login no [{{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://console.ng.bluemix.net){:new_window}.
1. Se você usar o {{site.data.keyword.Bluemix_notm}} Dedicated, efetue login no ambiente Dedicated no {{site.data.keyword.Bluemix_notm}}.
1. No menu de hambúrguer, clique em **Serviços** e, em seguida, clique em **DevOps**.
1. No painel DevOps, na página **Cadeias de ferramentas**, clique em **Criar uma cadeia de ferramentas**.
1. Na página **Criar uma cadeia de ferramentas**, clique em um
modelo de cadeia de ferramentas.
1. Revise o diagrama da cadeia de ferramentas que você está prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas.

 **Dica**: alguns dos modelos de cadeia de ferramentas têm múltiplas instâncias de uma integração de ferramenta. Por exemplo, o modelo de cadeia de ferramentas de Microsserviços no {{site.data.keyword.Bluemix_notm}} Public contém três instâncias do GitHub e três instâncias do Delivery Pipeline, uma para cada um dos três microsserviços.

 O diagrama na imagem a seguir é um exemplo. Ao criar
uma cadeia de ferramentas, o diagrama mostrará cada integração de ferramenta que é parte da cadeia de ferramentas.
![Diagrama da cadeia de ferramentas](images/toolchain_diagram.png)

1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em
{{site.data.keyword.Bluemix_notm}}. Se você desejar usar um nome diferente, mude
o nome da cadeia de ferramentas.  
1. Na seção Integrações de ferramentas, selecione cada integração de ferramenta que deseja configurar para sua cadeia de ferramentas. Algumas integrações de ferramentas não requerem configuração. Para obter informações sobre como configurar as integrações de ferramentas, consulte
[Configurando
integrações de ferramentas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Clique em **Criar**. Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas. As integrações de ferramentas configuradas são diferentes, dependendo de qual modelo de cadeia de ferramentas você selecionou e se está usando o {{site.data.keyword.Bluemix_notm}} Public ou o {{site.data.keyword.Bluemix_notm}} Dedicated. Por exemplo, quando você cria uma cadeia de ferramentas de Microsserviços no {{site.data.keyword.Bluemix_notm}} Public, estas etapas são executadas:

 * A cadeia de ferramentas é criada.
 * Se você tiver configurado o Delivery Pipeline, os pipelines serão criados e acionados.
 * Se você tiver configurado o Sauce Labs, a cadeia de ferramentas será configurada para incluir tarefas de teste do Sauce Labs nos pipelines.
 * Se tiver configurado o PagerDuty, a cadeia de ferramentas será configurada para enviar notificações de alerta para o serviço PagerDuty especificado.
 * Se tiver configurado o Slack, a cadeia de ferramentas será configurada para enviar notificações sobre o status de implementação para o canal Slack especificado.
 * Se tiver configurado a integração de ferramenta do código-fonte, como o GitHub, o repositório GitHub de amostra será clonado na conta do GitHub.


##Criando uma cadeia de ferramentas com base em um aplicativo
{: #creating_a_toolchain_from_an_app}

É possível criar uma cadeia de ferramentas a partir de seu aplicativo. A cadeia de
ferramentas pode suportar desenvolvimento, implementação e monitoramento contínuos e mais, e é associada ao seu app. Cada app pode ser
associado a uma cadeia de ferramentas. Quando você envia por push as mudanças para o GitHub ou o repositório {{site.data.keyword.ghe_short}} da cadeia de ferramentas, o pipeline constrói e implementa automaticamente o app.  

1. Na página Visão geral de seu app, no cartão do Continuous Delivery, clique em **Ativar**. Se você usar o {{site.data.keyword.Bluemix_notm}} Public, seu app será configurado para entrega contínua por meio de um novo repositório GitHub que é preenchido com o código de início do app. Se você usar o {{site.data.keyword.Bluemix_notm}} Dedicated, seu app será configurado para entrega contínua por meio de um novo GitHub ou repositório {{site.data.keyword.ghe_short}} que é preenchido com o código de início do app.
1. Na página de criação da cadeia de ferramentas, revise o diagrama da cadeia de ferramentas que estiver prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas.
1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em
{{site.data.keyword.Bluemix_notm}}. Se você desejar usar um nome diferente, mude
o nome da cadeia de ferramentas.
1. Na seção Integrações de ferramentas, selecione cada integração de ferramenta que deseja configurar para sua cadeia de ferramentas. Algumas integrações de ferramentas não requerem configuração. Para obter informações sobre como configurar as integrações de ferramentas, consulte
[Configurando
integrações de ferramentas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Clique em **Criar**.  Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas. As integrações de ferramentas configuradas são diferentes, dependendo de se você está usando cadeias de ferramentas no {{site.data.keyword.Bluemix_notm}} Public ou no {{site.data.keyword.Bluemix_notm}} Dedicated. Por exemplo, quando você cria uma cadeia de ferramentas de um app no {{site.data.keyword.Bluemix_notm}} Public, estas etapas são executadas:

 * A cadeia de ferramentas é criada.
 * Se você tiver configurado o Delivery Pipeline, os pipelines serão criados e acionados.
 * Se você tiver configurado o GitHub, o repositório GitHub de amostra será clonado na conta do GitHub.


##Visualizando uma cadeia de ferramentas
{: #viewing_a_toolchain}

Após configurar a cadeia de ferramentas e as suas integrações de ferramenta, é possível visualizar uma representação visual da cadeia de ferramentas.

1. No painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique em **Visão geral**.
2. Para acessar uma integração de ferramenta que esteja em sua cadeia de ferramentas, clique na ferramenta.

 **Dica**: se você tiver mais de um GitHub, {{site.data.keyword.ghe_short}} ou repositório Git, poderá ter múltiplos cartões para a mesma integração de ferramenta porque cada repositório é representado por seu próprio cartão. Se você tiver mais de um pipeline, poderá ter múltiplos cartões para a mesma integração de ferramenta porque cada pipeline será representado por seu próprio cartão. Por exemplo, quando você cria uma cadeia de ferramentas de Microsserviços, cada um dos três microsserviços tem seu próprio GitHub, {{site.data.keyword.ghe_short}} ou repositório Git e seu próprio pipeline.
