---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Usando o aplicativo iniciador
Crie dispositivos simulados no aplicativo iniciador {{site.data.keyword.iotelectronics_full}}. Experimente como um fabricante corporativo pode monitorar dispositivos que estão conectados ao
{{site.data.keyword.iot_short_notm}}. Interaja manualmente com o dispositivo simulado para acionar alertas, notificações e ações.
{:shortdesc}


## Abrindo o aplicativo iniciador
{: #iot4e_openApp}

1. Em seu painel do {{site.data.keyword.Bluemix_notm}}, inicie o seu aplicativo iniciador {{site.data.keyword.iotelectronics}} clicando no tile do aplicativo iniciador.

    ![{{site.data.keyword.iotelectronics}} no painel.](images/IoT4E_bm_dashboard.svg "{{site.data.keyword.iotelectronics}} no painel")

2. Espere a mensagem de status *Seu aplicativo está em execução* no cabeçalho e, em seguida, clique em **Visualizar aplicativo** para exibir o aplicativo iniciador.

    ![App de visualização do {{site.data.keyword.iotelectronics}}.](images/IoT4E_view_app.svg "App de visualização do {{site.data.keyword.iotelectronics}}")

## Criando dispositivos simulados
{: #create_sim}

No aplicativo iniciador, é possível criar e controlar dispositivos simulados como o fabricante do dispositivo ou como um consumidor. Status e dados do evento para esses dispositivos simulados são
armazenados e podem ser visualizados no {{site.data.keyword.iot_full}}.

1. Selecione uma das seguintes opções:
    - **Conectar e gerenciar dispositivos simulados** para criar dispositivos simulados como o fabricante do dispositivo
    - **Controlar remotamente os seus dispositivos conectados** para criar dispositivos simulados e se conectar com o [aplicativo móvel
de amostra](iotelectronics_config_mobile.html) como o proprietário de dispositivo.

    ![Experiência do
iniciador do {{site.data.keyword.iotelectronics}}](images/IoT4E_remotely_option.svg "Experiência do iniciador do {{site.data.keyword.iotelectronics}}")

2. Role até a seção rotulada **Em seguida, escolha ou inclua a nova arruela simulada** e clique no ícone +. Uma nova lavadora é criada.

    ![Incluindo uma arruela.](images/IoT4E_add_washer.svg "Adding a washer")

3. Para visualizar os detalhes da arruela, clique em uma. No painel de comando e controle, inicie a arruela ou clique nos diferentes tipos
de falhas para visualizar mudanças de status. Também é possível visualizar as mudanças de status e controlar a arruela por meio do seu app móvel.

  ![Detalhes de status da arruela.](images/IoT4E_washer_control.svg "Washer status details")
