
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Configurando credenciais para o Google Cloud Messaging (GCM)
{: #create-push-enable-gcm}
Última atualização: 16 de agosto de 2016
{: .last-updated}

Obtenha suas credenciais do Google Cloud Messaging (GCM) e, em seguida, configure o serviço {{site.data.keyword.mobilepushshort}} no painel Push.

##Obtendo seu ID de emissor e chave de API

A chave API é armazenada com segurança e usada pelo serviço {{site.data.keyword.mobilepushshort}} para se conectar ao servidor GCM e o ID do emissor (número do projeto) é usado pelo Android SDK no lado do cliente. Para obter mais informações sobre o ID do emissor, consulte em [Mensagem do Google Cloud](https://developers.google.com/cloud-messaging/gcm#arch).

1. Obtenha uma conta do Google Development em [Console do Google Dev](https://console.developers.google.com/start){: new_window}. Para obter mais informações sobre o Google Cloud Messaging
(GCM), consulte [Criando
um projeto de API do Google](https://developers.google.com/console/help/new/){: new_window}.

2. No Google Developers Console, crie um novo projeto. Por
exemplo, "hello
                        world".

![Criar Projeto](images/gcm_createproject.jpg)

3. Em **Nome do projeto**, insira o nome de
seu projeto e clique no botão **Criar**.
4. Clique em **Início** para visualizar o número
do projeto. Documente seu número de projeto.

![número do projeto GCM](images/gcm_projectnumber.jpg)

	**Nota**: Ao criar seu projeto, um número de projeto (ID
do emissor) é criado. Use esse número para configurar o Push
Notification Service na tela do painel Push.

5. Clique em **APIs & Auth** e na seção **APIs
móveis**, clique em **Cloud Messaging for Android**.

![APIs ](images/gcm_mobileapi.jpg)

6. Clique em **APIs** e depois no botão
**Ativar API** para criar a chave de API para
seu projeto.

![Ativar API ](images/gcm_enable_api.jpg)

7. Vá para a tela **APIs & Autorizações ->
Credenciais**. Clique em **Incluir credenciais** e depois em **Chave de API**.

![Credenciais de API](images/api_credentials.jpg)

8. Clique na opção **Chave do servidor**
para gerar a chave de API GCM que você usará no painel Push do Bluemix.
9. No campo **Nome**, informe o nome da chave de API do servidor.

![chave do servidor GCM](images/gcm_serverkey.jpg)

10. Clique no botão **Criar**. 
A chave de API
é exibida.

![chave de API GCM](images/gcm_apikey.jpg)

11. Copie a chave de API GCM e depois clique no botão **OK**. Você
precisará do número de projeto (ID do emissor) e da chave de API para configurar
suas credenciais na tela Configuração do painel Notificação push do Bluemix. 


##Configurando o serviço {{site.data.keyword.mobilepushshort}} para Android

###Antes de iniciar
{: before-you-begin}

Obtenha uma chave de API GCM e ID de emissor
(número de projeto). 

1. Abra o aplicativo backend no painel do Bluemix e, em seguida, clique no serviço IBM {{site.data.keyword.mobilepushshort}} para abrir o painel.
 
![painel Push](images/bluemixdashboard_push.jpg)

O painel Push é exibido.
	
![Configuração de Push](images/setup_push_main.jpg)
Para configurar um serviço {{site.data.keyword.mobilepushshort}} desvinculado para Android, selecione o ícone Desvincular o serviço {{site.data.keyword.mobilepushshort}} para abrir o painel do serviço {{site.data.keyword.mobilepushshort}}.
 
	![painel Push](images/push_unbound.jpg)

2. Clique no botão **Configurar push** para
configurar as credenciais de GCM.
1. Na guia **Configuração**, acesse a seção **Google
Cloud Messaging** e configure o ID do emissor (número do projeto GCM) e a chave
de API.

4. Clique no botão **Salvar**. 
5. Próximas etapas. [Ativando notificações para Android](c_enable_push.html).


##Criando um serviço {{site.data.keyword.mobilepushshort}} desvinculado para Android

###Antes de iniciar
{: before-you-begin}

Crie uma instância de serviço do {{site.data.keyword.mobilepushshort}}. É possível usar a instância de serviço do {{site.data.keyword.mobilepushshort}} sem ligar a nenhum aplicativo backend.

1. Ligue a instância de serviço do {{site.data.keyword.mobilepushshort}} a um aplicativo Bluemix. Ao ligar, você será capaz de ver que todos os detalhes relacionados ao serviço são armazenados no formato JSON na variável de ambiente VCAP_SERVICES. 

![Ligando um serviço Push Notification](images/unbound_1.jpg)
 
2. Clique em **Ligar** e escolha a instância de serviço do {{site.data.keyword.mobilepushshort}} a ser ligada. Quando o aplicativo é ligado ao serviço {{site.data.keyword.mobilepushshort}}, as informações sobre o serviço são armazenadas no formato JSON na variável de ambiente VCAP_SERVICES do app. Por exemplo: 

```
{
   "imfpush_Dev": [
   {
         "name": "neekrish_20JulUnbound",
         "label": "imfpush_Dev",
         "plan": "Basic",
         "credentials": null
      }
   ]
}
```
