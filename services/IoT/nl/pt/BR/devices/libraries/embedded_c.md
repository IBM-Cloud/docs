---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-08-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Embedded C para desenvolvedores de dispositivos
{: #embedded_c}

É possível usar o Embedded C para construir e customizar dispositivos que interagem com sua organização no {{site.data.keyword.iot_full}}. Use as informações e os exemplos fornecidos para iniciar o desenvolvimento de seus dispositivos usando o Embedded C.
{:shortdesc}

## Fazendo download de cliente e recursos de Embedded C
{: #embeddedc_client_download}

Para acessar as bibliotecas do cliente Embedded C e as amostras para o {{site.data.keyword.iot_short_notm}}, acesse o repositório [iotf-embeddedc](https://github.com/ibm-messaging/iotf-embeddedc) no GitHub e conclua as instruções de instalação.


## Dependências
{: #dependencies}

|Dependência |Descrição|
|:---|:---|
|[Biblioteca Eclipse Paho Embedded C](http://git.eclipse.org/c/paho/org.eclipse.paho.mqtt.embedded-c.git) |Fornece uma biblioteca de MQTT do cliente C. Para obter mais informações, consulte [Pacote do cliente MQTT - C para dispositivos integrados](http://www.eclipse.org/paho/clients/c/embedded/).|


## Instalação
{: #installation}

Para instalar a biblioteca do cliente do {{site.data.keyword.iot_short_notm}} para Embedded C, conclua as instruções a seguir:

1. Para instalar a versão mais recente da biblioteca, insira o código a seguir na linha de comandos:
```
  [root@localhost ~]# git clone https://github.com/ibm-messaging/iotf-embeddedc.git
```
2. Copie o arquivo .tar da biblioteca Paho para o diretório *lib*.
```
    cd iotf-embeddedc
    cp ~/org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz lib/
```
3. Extraia o arquivo de biblioteca
```  cd lib
    tar xvzf org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz
```
O cliente transferido por download tem a estrutura do arquivo a seguir:

```
 |-lib - contains all the dependent files
 |-samples - contains the helloWorld and sampleDevice samples
   |-sampleDevice.c - sample device implementation
   |-helloworld.c - quickstart application
   |-README.md
   |-Makefile
   |-build.sh
 |-iotfclient.c - Main client file
 |-iotfclient.h - Header file for the client
```

## Inicializando a biblioteca do cliente
{: #initialize_client_library}

Após a biblioteca do cliente ser transferida por download, ela deve ser inicializada e conectada ao {{site.data.keyword.iot_short_notm}}. É possível inicializar a biblioteca do cliente do {{site.data.keyword.iot_short_notm}} para Embedded C passando parâmetros ou usando um arquivo de configuração.

### Transmitindo Parâmetros

A função `initialize` usa os parâmetros a seguir para se conectar ao serviço do {{site.data.keyword.iot_short_notm}}:

|Definição |Descrição |
|:---|:---|
|`client`|Um ponteiro para o *iotfclient*.|
|`org`|O ID de sua organização.|
|`type` |O tipo de seu dispositivo.|
|`id` |O ID do dispositivo.|
|`auth-method` |O método de autenticação a ser usado. O único valor atualmente suportado é `token`.|
|`auth-token`|Um token de autenticação para conectar seu dispositivo de forma segura ao Watson IoT Platform.|


```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	//quickstart
	rc = initialize(&client,"quickstart","iotsample","001122334455",NULL,NULL);
	//registered
	rc = initialize(&client,"org","type","id","auth-method","auth-token");
	....
```

### Usando um arquivo de configuração

É possível também usar um arquivo de configuração para inicializar a Biblioteca do cliente C integrada. A função `initialize_configfile` aceita o caminho do arquivo de configuração como um parâmetro.

```
	#include "iotfclient.h"
	....
	....
	char *filePath = "./device.cfg";
	Iotfclient client;
	rc = initialize_configfile(&client, filePath);
	....
```

O arquivo de configuração deve usar o formato a seguir:

```
	org=$orgId
	type=$myDeviceType
	id=$myDeviceId
	auth-method=token
	auth-token=$token
```

## Conectando ao serviço
{: #connecting_service}

Após inicializar a biblioteca do cliente Embedded C do {{site.data.keyword.iot_short_notm}}, é possível se conectar ao {{site.data.keyword.iot_short_notm}} chamando a função `connectiotf`.

```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	char *configFilePath = "./device.cfg";

	rc = initialize_configfile(&client, configFilePath);

	if(rc != SUCCESS){
		printf("initialize failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}

	rc = connectiotf(&client);

	if(rc != SUCCESS){
		printf("Connection failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}
	....
```

## Manipulando comandos
{: #handling_commands}

Quando o cliente do dispositivo conecta, ele automaticamente assina qualquer comando para esse dispositivo. Para processar comandos específicos, você precisa registrar uma função de retorno de chamada de comando chamando a função `setCommandHandler`. A função de retorno de chamada tem as propriedades a seguir:

|Propriedade |Descrição|
|:---|:---|
|`commandName`  |O nome do comando que foi chamado. |  
|`format`  |O formato do evento. O formato pode ser qualquer sequência, por exemplo, JSON.|
|`payload`  |Os dados para a carga útil do comando. O comprimento máximo é 131072 bytes. |


```
	#include "iotfclient.h"

	void myCallback (char* commandName, char* format, void* payload)
	{
	printf("The command received :: %s\n", commandName);
	printf("format : %s\n", format);
	printf("Payload is : %s\n", (char *)payload);
	}
	...
	...
	char *filePath = "./device.cfg";
	rc = connectiotfConfig(filePath);
	setCommandHandler(myCallback);

	yield(1000);
	....

```
**Nota:** a função `yield()` permite que o dispositivo receba comandos do Watson IoT Platform e mantém a conexão ativa. Se a função `yield()` não for chamada dentro do prazo especificado pelo intervalo keepAlive, quaisquer comandos que forem enviados da plataforma não serão recebidos pelo dispositivo. O valor designado à função `yield()` especifica a duração (em milissegundos) para leitura de dados do soquete antes que o controle seja retornado ao aplicativo.

## Publicando eventos
{: #publishing_events}

Eventos podem ser publicados com as propriedades a seguir:

|Propriedade |Descrição|
|:---|:---|
|eventType  |O tipo de evento publicado, por exemplo, status ou gps. |  
|eventFormat  |O formato pode ser qualquer sequência, por exemplo, `json`. |
|dados  |Os dados para a carga útil. O comprimento máximo é 131072 bytes. |
|QoS  |O nível de qualidade de serviço para o evento de publicação. Valores suportados são `0`, `1`, `2`.|


```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", "{\"d\" : {\"temp\" : 34 }}", QOS0);
	....
```

## Desconectando o cliente
{: #disconnect_client}

Para desconectar o cliente e liberar as conexões, execute o fragmento de código a seguir:

```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", payload , QOS0);
	...
	rc = disconnect();
	....
```

## Amostras
{: #samples}

Dispositivo e código do aplicativo de amostra são fornecidos no [GitHub](https://github.com/ibm-messaging/iotf-embeddedc/tree/master/samples).
