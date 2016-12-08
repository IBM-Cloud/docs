---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introdução a cadeias de ferramentas
{: #toolchains-setup}

Última atualização: 28 de abril de 2016
{: .last-updated}  

É possível criar uma cadeia de ferramentas de duas maneiras: usar um modelo para
criar uma cadeia de ferramentas ou incluir uma cadeia de ferramentas em um
app. Dependendo do modelo ou cadeia de
ferramentas que usar, a cadeia de ferramentas poderá incluir um
repositório
(repo) GitHub que é preenchido com o código de início do app e um pipeline de entrega pré-configurado. Ao
enviar por push as mudanças no repo GitHub da cadeia de
ferramentas, o pipeline de entrega automaticamente constrói e implementa o app no {{site.data.keyword.Bluemix}}. 
{: shortdesc}  

**Importante**: este recurso é experimental. As cadeias de ferramentas podem não ser estáveis e podem mudar de
formas que não sejam compatíveis com versões anteriores. Elas não são recomendadas para uso em ambientes de produção. Para usar cadeias de ferramentas,
deve-se fazer uma
[solicitação
para acesso](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window} única. As cadeias de ferramentas estão disponíveis
somente na região de Dallas.

##Criando uma cadeia de ferramentas com base em um modelo   
{: #creating_a_toolchain_from_a_template}

Após sua solicitação de acesso a cadeias de ferramentas ser aprovada, será possível usar um modelo como um ponto de início para criar uma
cadeia de ferramentas que inclua um conjunto específico de integrações de ferramenta.

1. No painel DevOps, na guia **Cadeias de ferramentas**, clique em **Criar uma cadeia de ferramentas** para
criar sua primeira cadeia de ferramentas. Se você já tiver uma cadeia de ferramentas, clique no botão (+) para criar outra cadeia de ferramentas.
1. Clique em um modelo da cadeia de ferramentas. Por exemplo, para usar uma
amostra de armazenamento on-line para criar a cadeia de ferramentas, clique em
**Cadeia de ferramentas nativas da nuvem para microsserviços**. 
1. Na página de criação da cadeia de ferramentas, revise o diagrama da cadeia de ferramentas que estiver prestes a criar. O diagrama
mostrará cada integração de ferramenta em sua fase de ciclo de vida na cadeia de ferramentas. O diagrama na imagem a seguir é um exemplo. Ao criar
uma cadeia de ferramentas, o diagrama mostrará cada integração de ferramenta que é parte da cadeia de ferramentas.
![Diagrama da cadeia de ferramentas](images/toolchain_diagram.png)

1. Revise as informações padrão para as configurações da cadeia de ferramentas. O nome da cadeia de ferramentas as identifica em
{{site.data.keyword.Bluemix}}. Se você já tiver uma cadeia de ferramentas com esse nome ou se desejar usar um nome diferente, mude o nome
da cadeia de ferramentas.  
1. Se você desejar criar a cadeia de ferramentas antes de configurar as
integrações de ferramentas, clique em **CRIAR** e confirme que deseja
criar a cadeia sem as integrações. Continue na seção
[Criando uma cadeia de ferramentas](#creating_a_toolchain) que descreve
as etapas executadas automaticamente para configurar sua cadeia de ferramentas.  
1. Se você desejar configurar integrações de ferramentas antes de criar a cadeia
de ferramentas, na seção Integrações configuráveis, selecione cada integração de
ferramenta que deseja configurar. Para
obter informações sobre configurar integrações de ferramentas, consulte [Configurando integrações de ferramenta](../toolchains/toolchains_integrations.html){: new_window}. 

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
obter informações sobre configurar integrações de ferramentas, consulte [Configurando integrações de ferramenta](../toolchains/toolchains_integrations.html){: new_window}.

## Configurando uma cadeia de ferramentas
{: #setting_up_a_toolchain}

Se você não tiver criado ainda a cadeia de ferramentas, clique em **CRIAR**. Várias etapas são executadas automaticamente para configurar sua cadeia de ferramentas:

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
 
##Visualizando uma cadeia de ferramentas
{: #viewing_a_toolchain}

Após a configuração da cadeia de ferramentas e de todas as integrações de
ferramentas, a página Integrações de ferramentas é aberta.

1. Revise a página para ver uma representação visual da cadeia de ferramentas para seu app.
1. Para acessar uma integração de ferramenta que esteja em sua cadeia de ferramentas, clique no ladrilho da ferramenta. 
 
 **Dica**: se você tiver mais de um
repo
GitHub, poderá ter diversos ladrilhos para a mesma integração de ferramenta
porque cada repo precisa de seu próprio pipeline.
