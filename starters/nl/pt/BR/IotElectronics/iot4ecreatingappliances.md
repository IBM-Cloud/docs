---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}

{:shortdesc: .shortdesc}


# Usando o aplicativo iniciador
*Última atualização: 15 de setembro de 2016*
{: .last-updated}

Crie dispositivos simulados no aplicativo iniciador {{site.data.keyword.iotelectronics_full}}. Experimente como um fabricante corporativo pode monitorar dispositivos que estão conectados ao
{{site.data.keyword.iot_short_notm}}. Interaja manualmente com o dispositivo simulado para acionar alertas, notificações e ações.
{:shortdesc}


## Abrindo o aplicativo iniciador
{: #iot4e_openAppMain}

Como o método de abrir o aplicativo iniciador varia um pouco dependendo de qual versão do console do {{site.data.keyword.Bluemix_notm}} é usada, você deverá ler as instruções para a versão
apropriada.

É possível determinar qual versão está sendo usada procurando as opções a seguir:
  - [Novo {{site.data.keyword.Bluemix_notm}}](#iot4e_openApp). Se você estiver usando a experiência do {{site.data.keyword.Bluemix_notm}} Novo, **Tente
o Novo Bluemix** *não* será exibido na seção do cabeçalho.
  - [{{site.data.keyword.Bluemix_notm}}](#iot4e_openApp_c) Clássico. Se você estiver usando a experiência do {{site.data.keyword.Bluemix_notm}} Clássico,
**Tente o Novo Bluemix** aparecerá na seção de título.  

**Dica:** para alternar para a experiência do {{site.data.keyword.Bluemix_notm}} Clássico, clique em seu nome do usuário na seção do cabeçalho e, em seguida, role para baixo e
clique em **Alternar para Clássico**. Para alternar para a experiência do {{site.data.keyword.Bluemix_notm}} Novo, clique em **Tente o Novo Bluemix** na seção do
cabeçalho.

### Abrindo o aplicativo iniciador na experiência do {{site.data.keyword.Bluemix_notm}} Novo.
{: #iot4e_openApp}
1. Em seu painel do {{site.data.keyword.Bluemix_notm}}, inicie o seu aplicativo iniciador {{site.data.keyword.iotelectronics}} clicando no tile do aplicativo iniciador.

    ![{{site.data.keyword.iotelectronics}} no painel, Nova
experiência.](images/IoT4E_bm_dashboard.png "{{site.data.keyword.iotelectronics}} in the dashboard, New Experience")

2. Espere a mensagem de status *Seu aplicativo está em execução* no cabeçalho e, em seguida, clique em **Visualizar aplicativo** para exibir o aplicativo iniciador.  

    ![{{site.data.keyword.iotelectronics}} no painel, Nova
experiência.](images/IoT4E_view_app.png "{{site.data.keyword.iotelectronics}} in the dashboard, New Experience")

### Abrindo o aplicativo iniciador na experiência do {{site.data.keyword.Bluemix_notm}} Clássico.
{: #iot4e_openApp_c}

1. Em seu painel do {{site.data.keyword.Bluemix_notm}}, inicie o seu aplicativo iniciador {{site.data.keyword.iotelectronics}} clicando no tile do aplicativo iniciador.

    ![{{site.data.keyword.iotelectronics}} no painel, Clássico.](images/IoT4E_bm_dashboard_c.png "{{site.data.keyword.iotelectronics}} in the dashboard, Classic")

2. Espere a mensagem de status *Seu aplicativo está em execução* na seção Funcionamento do aplicativo e, em seguida, na janela principal, pelo nome do aplicativo, clique na URL
**Rotas** para exibir o aplicativo iniciador.  

    ![{{site.data.keyword.iotelectronics}} no painel, Clássico.](images/IoT4E_view_app_c.png "{{site.data.keyword.iotelectronics}} in the dashboard")

## Criando dispositivos simulados
{: #iot4eCreateAppliances}

No aplicativo iniciador, é possível criar e controlar dispositivos simulados como o fabricante do dispositivo ou como um consumidor. Status e dados do evento para esses dispositivos simulados são
armazenados e podem ser visualizados no {{site.data.keyword.iot_full}}.

1. Selecione
uma das seguintes opções:
    - **Conectar e gerenciar dispositivos simulados** para criar dispositivos simulados como o fabricante do dispositivo
    - **Controlar remotamente os seus dispositivos conectados** para criar dispositivos simulados e se conectar com o [aplicativo móvel
de amostra](iotelectronics_config_mobile.html) como o proprietário de dispositivo.

    ![ experiência do iniciador do {{site.data.keyword.iotelectronics}}](images/IoT4E_remotely_option.png "{{site.data.keyword.iotelectronics}} starter experience")

2. Role até a seção rotulada **Em seguida, escolha ou inclua a nova arruela simulada** e clique no ícone +. Uma nova lavadora é criada.

    ![Incluindo uma arruela.](images/IoT4E_add_washer.png "Adding a washer")

3. Para visualizar os detalhes de sua arruela, comandos de emissão e falhas de causa, clique em uma arruela.

  ![Detalhes de status da arruela.](images/IoT4E_washer_control.png "Washer status details")


# Links Relacionados
{: #rellinks}

## documentação da API
{: #api}
* [API do {{site.data.keyword.iotelectronics}}](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [API do {{site.data.keyword.iot_short}}](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## afetados
{: #general}

* [Documentação do {{site.data.keyword.iotelectronics}}](iotelectronics_overview.html)
* [Documentação do {{site.data.keyword.iot_full}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
*  [Documentação do {{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [Documentação do {{site.data.keyword.sdk4nodefull}}](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## Amostras
{: #samples}
* [Aplicativo móvel de
amostra](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
