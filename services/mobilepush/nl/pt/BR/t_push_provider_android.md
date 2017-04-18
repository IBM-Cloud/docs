---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurando credenciais para o FCM
{: #create-push-enable-gcm}
Última atualização: 16 de janeiro de 2017
{: .last-updated}

Firebase Cloud Messaging (FCM) é o gateway usado para entregar notificações push para dispositivos Android e para o Google Chrome. FCM é a nova versão do Google Cloud Messaging (GCM). Para configurar o serviço {{site.data.keyword.mobilepushshort}} no painel, é necessário obter suas credenciais do FCM. Assegure-se de usar configurações do FCM para novos apps. Apps existentes continuarão a funcionar com configurações do GCM.

## Obtendo seu ID de emissor e chave de API
{: #android-senderid-apikey}

A chave API é armazenada com segurança e usada pelo serviço {{site.data.keyword.mobilepushshort}} para se conectar ao servidor FCM e o ID do emissor
(número do projeto) é usado pelo SDK do Android e o SDK do JS para Google Chrome e Mozilla Firefox no lado do cliente. 

Para configurar o FCM, gerar a chave API e o ID do emissor, conclua as etapas:

1. Visite o [console do Firebase ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://console.firebase.google.com/?pli=1){: new_window}.
2. Selecione **Criar novo projeto**. 
3. Na janela Criar um projeto, forneça um nome do projeto, escolha um país/região e clique em **Criar projeto**.
3. Na área de janela de navegação, clique no ícone Configurações e selecione **Configurações do projeto**.
4. Escolha a guia Cloud Messaging para gerar uma Chave API Server e um ID do emissor.

## Configurando o serviço {{site.data.keyword.mobilepushshort}} para Android e Apps Chrome e Extensões
{: #setup-push-android}

**Nota:** você precisará da sua Chave API e do ID do emissor do FCM/GCM (número do projeto).

1. Abra o painel Bluemix e, em seguida, clique na instância de serviço
{{site.data.keyword.mobilepushfull}} que você criou para abrir o painel. O painel Push é exibido. Para configurar um serviço {{site.data.keyword.mobilepushshort}} desvinculado
para Android, selecione o ícone do serviço {{site.data.keyword.mobilepushshort}}
desvinculado para abrir o painel do serviço {{site.data.keyword.mobilepushshort}}. 

![painel Push](images/push_unbound.jpg)

2. Clique no botão **Configurar push**, para configurar as credenciais do FCM/GCM para aplicativos Android e Apps Google Chrome e Extensões.
3. Na página **Configuração**, para Android, acesse a guia **Móvel** e configure o ID do emissor (número do projeto do
GCM) e a Chave API. Para Apps Google Chrome e Extensões, acesse a guia **Web** e configure o ID do emissor (número do projeto do FCM/GCM) e
a Chave API apropriadamente.
4. Clique em **Salvar**.
5. Próximas etapas. [Ativando notificações para Android](c_enable_push.html) ou [Ativando notificações para Apps Google Chrome e Extensões](c_enable_push.html).


