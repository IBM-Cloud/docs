---

copyright:
  years: 2016, 2017
lastupdated: "2016-06-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visualizando dados do dispositivo
{: #visualizingdata_data}

Esta amostra ajuda a visualizar dados em tempo real e históricos de dispositivos registrados em sua organização do {{site.data.keyword.iot_full}}.
{:shortdesc}

## Antes de iniciar
{: #byb}

Antes que seja possível visualizar seus dados, deve-se executar as ações a seguir:

- Registre seus dispositivos em sua organização do {{site.data.keyword.iot_short_notm}}.
- Assegure que seus dispositivos estejam enviando eventos ao {{site.data.keyword.iot_short_notm}}.
- [Faça download da amostra de visualização](https://github.com/ibm-messaging/iot-visualization/archive/v0.2.0.zip) a partir do repositório github e extraia o arquivo .zip.
- [Instale a ferramenta de linha de comandos cf](../../starters/install_cli.html) a partir do {{site.data.keyword.Bluemix_notm}}.

## Executando a amostra no {{site.data.keyword.Bluemix_notm}}
{: #running_sample}

1. Crie um aplicativo no {{site.data.keyword.Bluemix_notm}} usando o SDK (kit de desenvolvimento de software) do Node.js. Tome nota do nome do aplicativo e do nome do host do aplicativo, essas informações são necessárias para fazer upload do aplicativo para o {{site.data.keyword.Bluemix_notm}}.
2. Ligue o aplicativo node.JS à sua instância do {{site.data.keyword.iot_short_notm}} no painel do {{site.data.keyword.Bluemix_notm}} concluindo as etapas a seguir:

  a. No painel {{site.data.keyword.Bluemix_notm}}, clique no aplicativo Node.JS que você criou.

  b. Clique em **Ligar um serviço ou uma API (interface de programação de aplicativos)** e, em seguida, selecione o serviço do {{site.data.keyword.iot_short_notm}} e clique em **Incluir**.
3. Usando a ferramenta de linha de comandos cf, mude seu diretório para o pacote de amostra de visualização extraído e execute o comando a seguir para se conectar ao {{site.data.keyword.Bluemix_notm}}.
```
cf api https://api.ng.bluemix.net
```
4. Em seguida, efetue login no {{site.data.keyword.Bluemix_notm}} usando:
```
cf login -u <your_bluemix_login_id>
```
Se você não estiver usando a organização e o espaço padrão, será possível usar:
```
cf target-o <your_bluemix_org> -s dev
```

5. Edite o arquivo `manifest.yml` e atualiza os nomes do host e do aplicativo usando o formato a seguir:
```
applications:
 - disc quota: 1024M
   host: <your_bluemix_hostname>
   name: <your_bluemix_appname>
   command: node ap.js
   path:
   domain: mybluemix.net
   instances: 1
   memory: 128M
```
6. Implemente sua amostra de visualização usando o comando a seguir:
```
cf push <your_application_name>
```
7. No navegador, insira a seguinte URL:
```
http://<your_application_name>.mybluemix.net
```

Todos os dispositivos em sua organização estão listados no menu suspenso do dispositivo. Quando selecionado, será necessário ver a visualização em tempo real dos dados que o dispositivo está enviando para seu serviço do {{site.data.keyword.iot_short_notm}}. Para ver os dados históricos, clique no botão **Dados históricos**.

## Customizando a amostra
{: #customize_sample}

Esse aplicativo de amostra é um aplicativo da web independente, escrito na estrutura node.js. A amostra visualiza eventos que são enviados por dispositivos registrados em seu {{site.data.keyword.iot_short_notm}}. A amostra usa as ferramentas a seguir:

- Express: estrutura de aplicativo da web Node.js
- JQuery: Chamadas da interface com o usuário e Ajax
- Rickshaw: Ferramenta de visualização gráfica
- Paho: Cliente MQTT

O aplicativo de amostra é estruturado com os diretórios a seguir:

- Publico
- CSS: folhas de estilo
- Imagens
- JS: principais arquivos de lógica JavaScript
- Historian: código para visualização do historiador
- Realtime: código para visualização em tempo real
- Uicontroller.js: código para controlar a interface com o usuário
- Routes: lógica de roteamento e o aplicativo da web
- Utils: funções de utilitário usadas para fazer chamadas HTTP (Protocolo de Transporte de Hipertexto)
- Views: arquivos da interface com o usuário escritos em Jade
- A biblioteca de gráficos do Rickshaw é usada para criar o gráfico para dados em tempo real e históricos.

## Customizando a exibição de dados em tempo real
{: #customize_real_time_display}

O diretório que contém o código de visualização gráfica para dados em tempo real é `public/ja/realtime`. A lógica dos gráficos pode ser customizada editando-se `public/js/historian/realtimeGraph.js`.

O arquivo que faz referência à biblioteca MQTT Paho para assinar tópicos do dispositivo e receber eventos de dispositivo do {{site.data.keyword.iot_short_notm}} pode ser localizado em `public/js/historian/realtime.js`.

Eventos de dispositivo são passados para o arquivo `realtimeGraph.js` para criar o gráfico.

## Customizando a exibição de dados históricos
{: #customize_historical_display}

O diretório que contém o código de visualização gráfica para dados do dispositivo históricos é `public/js/historian`. A lógica dos gráficos pode ser customizada editando-se `public/js/historian/historianGraph.js`.

O arquivo que controla as chamadas API (interface de programação de aplicativos) REST para coletar dados do dispositivo históricos é `public/js/historian/historian.js`.

Dados históricos são passados para o arquivo `historianGraph.js` para criar o gráfico.

Um guia do desenvolvedor mais detalhado está disponível na wiki de visualização
do Github iot.
