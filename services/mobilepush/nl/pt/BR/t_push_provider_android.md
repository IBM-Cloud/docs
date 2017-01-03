---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurando credenciais para o FCM
{: #create-push-enable-gcm}
Última atualização: 06 de dezembro de 2016
{: .last-updated}

O Firebase Cloud Messaging (FCM) é o gateway usado para entregar notificações push para dispositivos Android e navegadores da web Google Chrome e Mozilla. O FCM
substituiu o Google Cloud Messaging (GCM). É necessário obter as suas credenciais do FCM e, em seguida, configurar o serviço
{{site.data.keyword.mobilepushshort}} no painel. Assegure-se de usar configurações do FCM para novos apps. Apps existentes continuarão a funcionar com configurações do GCM.

##Obtendo seu ID de emissor e chave de API
{: #android-senderid-apikey}

A chave API é armazenada com segurança e usada pelo serviço {{site.data.keyword.mobilepushshort}} para se conectar ao servidor FCM e o ID do emissor
(número do projeto) é usado pelo SDK do Android e o SDK do JS para Google Chrome e Mozilla Firefox no lado do cliente. 

Para configurar o FCM, gerar a chave API e o ID do emissor, conclua as etapas:

1. Visite o [Console do Firebase](https://console.firebase.google.com/?pli=1).
2. Selecione **Criar novo projeto**. 
3. Na janela Criar um projeto, forneça um nome do projeto, escolha um país/região e clique em **Criar projeto**.
3. Na área de janela de navegação, clique no ícone Configurações e selecione **Configurações do projeto**.
4. Escolha a guia Cloud Messaging para gerar uma Chave API Server e um ID do emissor.

##Configurando o serviço {{site.data.keyword.mobilepushshort}} para Android e Apps Chrome e Extensões
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
5. Próximas etapas. [Ativando notificações para Android](c_enable_push.html) ou [Ativando notificações para
Apps Google Chrome e Extensões](c_enable_push.html).

###Configurando para push da web do Google Chrome e do Mozilla Firefox (usando FCM/GCM)
{: #config-gcm-mozilla}

1. Na área de janela de navegação Painel Push, selecione
**Configurar**.
2. Selecione a guia Web.
	![Configuração de WebPush](images/webpush_configure.jpg)
3. Configure a chave API do FCM/GCM e a URL de seu website que estará registrada para receber notificações push.
4. Clique em **Salvar**.
5. Próximas etapas. [Ativando notificações para navegadores Google Chrome e Mozilla Firefox](c_enable_push.html).
